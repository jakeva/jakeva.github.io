---
layout: post
title: "Raspberry Pi BTC Node"
description: "In which I set up a Raspberry Pi to run a full BTC node"
category: Blog
tags: [BTC, Raspberry Pi]
---
{% include JB/setup %}

## Time to put one of my spare Raspberry Pis to work
I woke up this morning and thought, 'Hey why not get a full BTC node running on one of those Pis you got laying around?' So that's what I'm doing today.

## Basics
This assumes something like [Raspbian Lite](https://www.raspberrypi.org/downloads/raspbian/) is already installed and SSH access configured. For Wifi, I use these [Edimax USB chips](https://www.amazon.com/gp/product/B003MTTJOY). Configuring them is not too difficult. It boils down a simple config in `/etc/network/interfaces/`

```
auto lo

iface lo inet loopback
iface eth0 inet dhcp

auto wlan0
allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-ssid "**YOUR_WIFI**"
wpa-psk "**YOUR_PASSWORD**"
```

I'm going to install to the 32 GB SD mini card I used for the OS, which means I'm not planning on storing all the blocks. And since flash is less resilient than a HDD, I'm going to disable SWAP.

`sudo swapoff --all`

## Installing the Bitcoin client
Go to [https://github.com/bitcoin/bitcoin/releases](https://github.com/bitcoin/bitcoin/releases) and make not of the newest stable release. For me it's currently 0.19.0.1. So, with that:
```
cd ~
git clone -b v0.19.0.1 https://github/com/bitcoin/bitcoin.git
cd bitcoin
```

I'm going to install it without a wallet, since I only want a node.
```
./autogen.sh
./configure CXXFLAGS="--param ggc-min-expand=1 --param ggc-min-heapsize=32768" --enable-cxx --without-gui --disable-shared --with-pic --disable-tests --disable-bench --enable-upnp-default --disable-wallet
make # This will take a long time, best run in tmux or screen, and grab a beer
sudo make install
```

## Configure
For this, I want a bitcoin user.
`sudo adduser bitcoin`

Now switch to the new user
`sudo su - bitcoin`

And create the app data directory
`mkdir ~/.bitcoin`

Add the following to `~/.bitcoin/bitcoin.conf`
```
# makes client run in background
daemon=1
# is required by Fail2Ban described below
logips=1
# magic RBP optimisations
maxconnections=40
maxuploadtarget=5000

# Run without SWAP
dbcache=100
maxorphantx=10
maxmempool=50

upnp=1

prune=550 # Only keep the last two days of blocks if like me you are running off a small SD card
```

Return to the `pi` user
`exit`

Now create the systemd service to launch the bitcoin client daemon
`sudo vim /etc/systemd/system/bitcoind.service`
and give it the following
```
[Unit]
Description=Bitcoin daemon
After=network.target
[Service]
ExecStart=/usr/local/bin/bitcoind -conf=/home/bitcoin/.bitcoin/bitcoin.conf -pid=/home/bitcoin/.bitcoin/bitcoind.pid
# Creates /run/bitcoind owned by bitcoin
RuntimeDirectory=bitcoind
User=bitcoin
Type=forking
PIDFile=/home/bitcoin/.bitcoin/bitcoind.pid
Restart=on-failure
# Hardening measures
####################
# Provide a private /tmp and /var/tmp.
PrivateTmp=true
# Mount /usr, /boot/ and /etc read-only for the process.
ProtectSystem=full
# Disallow the process and all of its children to gain
# new privileges through execve().
NoNewPrivileges=true
# Use a new /dev namespace only populated with API pseudo devices
# such as /dev/null, /dev/zero and /dev/random.
PrivateDevices=true
# Deny the creation of writable and executable memory mappings.
MemoryDenyWriteExecute=true
[Install]
WantedBy=multi-user.target
```

Make sure the new service starts on boot
`sudo systemctl enable bitcoind`

## Security
Uncomplicated firewall
`sudo apt install ufw`

Allow limited ssh
`sudo ufw limit ssh`

Allow for main net bitcoin traffic
`sudo ufw allow 8333 comment "Bitcoin mainnet"`

Enable the firewall
`sudo ufw enable`

Preview the enforced rules
`sudo ufw status verbose`

Install Fail2ban
`sudo apt install fail2ban`

See the active jails - for now it will only be sshd
`sudo fail2ban-client status`

Start the bitcoin client
`sudo systemctl start bitcoind`

It will take a few minutes to start, but if you want to monitor its progress switch back to the bitcoin user and enter
`tail -n 100 -f ~/.bitcoin/debug.log`

You will need to figure out how to forward port 8333 to your new btc node depending on your router.

Check it's accessible from the outside world with
`curl -sL https://bitnodes.earn.com/api/v1/nodes/me-8333/ | jq`
