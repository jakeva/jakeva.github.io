---
layout: post
title: "GPG & YubiKey & You"
description: "In which I do interesting things with my YubiKey"
category: Blog
tags: [yubikey]
---

I've recently taken on the task of setting up my YubiKeys for usage beyond 2 factor auth. Something I learned was that OpenPGP smartcards (which include YubiKeys) have slots for three separate keys: Signature, Encryption, and Authentication.

My first goal is to sign git commits with it. Because I am a man of negligible importance, this is in fact NOT an excercise in security. I'm taking more of a hobbyist approach. If security was of a more significant concern in my life, I would probably generate my keys in a live booted and air gapped [Tails](https://tails.boum.org) environment.

When I started going down this route I had only in the first place acquired my YubiKey to simplify 2 factor authorization, a flow that I have found myself increasingly spending time due to work and the fact I turn it on everywhere that supports it. I think I was vaguely aware they could be used for more. Regardless, I started by playing around with signing. One of the first things I became aware of was that these things have PIN codes. Never needed them for 2FA, but for managing GPG keys you do. The default user PIN (which is used for signing, among other things) is `123456` and the default admin PIN (used for modifying certain card attributes) is `12345678`.

If you're following along, I'm assuming you have a YubiKey and a recent version of GnuPG.

## Configure your YubiKey
To change the PIN (and configure things like your name, language, etc) run `gpg --card-edit` with your key plugged in. You should see information about your key. Type `admin` and `help` to enable and list the available commands. Use `passwd` to change the user PIN code.

## A little about GPG keys
GPG keys have capabilities: Sign, Certify, and Encrypt. When you generate a GPG public / private keypair, by default you get a primary pub/priv key and a sub pub/priv key. The primary key can Sign and Certify. The subkey can Encrypt. The reason for this default is that Certify is all powerful. It really is your identity. Delegating powers to other keys signed by it is a good way to reduce your security footprint. If someone steals your encrypt key, all you have to do is revoke it, create a new one, and Certify it with your unstolen primary key. If someone steals your primary private key, well they've just stolen the ability to revoke your other keys or make new keys as you. So keep it extra safe.

## Create a GPG key
It's time to generate your GPG key. `gpg --expert --full-gen-key`
* Select `RSA and RSA(default)`
* Key size: depending on the version of your key
  * YubiKey NEO - 2048
  * YubiKey 4 / 5 - 4096
* Do it again for the subkey
* Pick an expiration date
* Enter your name (must be more than 5 characters)
* Enter your email
* Enter an optional comment

Note the ID of the key generated. For fun, let's look at what we've got so far. Run `gpg --edit-key <KEY ID>`. You should see something like
```
Secret key is available.

gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u
gpg: next trustdb check due at 2021-03-12
sec  rsa4096/98973C978ECA988D
     created: 2020-03-14  expires: never       usage: SC
     trust: ultimate      validity: ultimate
ssb  rsa4096/015D68EE1E7AC274
     created: 2020-03-14  expires: never       usage: E
[ultimate] (1). Jake Van Alstyne (testing) <email@address.org>
```

The usage of the first key is marked as `SC`. The second is `E`. That means the primary key can sign and certify, while the subkey can encrypt.

While we're here, let's add separate authentication and signing keys to prepare to fill the slots on the YubiKey.

### Authentication Key
If you're still at the gpg prompt `gpg>` from the last command, exit out with Ctrl-C or `quit` and enter `gpg --expert --edit-key <KEY ID>`. Notice the extra flag for expert. Now enter the command `addkey`.
* Pick RSA.
* Toggle capabilities until only authentication is enabled. You should need to enter each option once: `S, E, A`
* Enter `Q` to finish
* Pick the key size
* Pick the expiration (good idea to keep it the same as your master key)
* Follow the rest of the prompts

### Signing Key
The steps are the same as for the authentication key, only you should only have to deselect Encrypt when picking the key capabilities since by default Signing and Encryption are selected.
If you `quit` out of here now, make sure to save or you'll lose the keys you just made.

## Import key to YubiKey
Make sure the YubiKey is plugged into your computer. Edit the key again, if you aren't already `gpg --edit-key <KEY ID>`. Enter the command `toggle` followed by `keytocard`.
* Enter `y` to move the primary key
* Select `1`. This moves the signature subkey to the signature slot of the YubiKey.

Enter `key 1` (which now shouljd select the encryption key) followed by `keytocard`. Select `2`. This moves the encryption key to the encryption slot.

Enter `key 1` again and then `key 2`. `keytocard` and `3`. This does the same but for the authentication key.

Now `quit` and `y` for save.

Now your secret keys are on your YubiKey and can be used for their intended purpose when it's connected.

## Configure Git for commit signing
Configure git for GPG signing:
* `git config --global commit.gpgsign true`
* `git config --global user.signingkey <KEY ID>`

And let's restart the GPG agent: `gpg-connect-agent reloadagent`. Now when you make a commit, git will require the key to be present. If it's not, the commit will fail. If you want to make a signed commit and see what it looks like in the log, the command for that is `git log --show-signature`.


{% include JB/setup %}
