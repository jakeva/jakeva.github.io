---
layout: post
title: "How I post to this blog using iOS Shortcuts and Pythonista"
description: "In which I automate posting to my blog"
category: Blog
tags: []
---
I've had this blog for many years, and basically never posted anything. I wanted to become better about that, so I've been writing more haikus and trying to write up some of my home projects. My blog uses [Jekyll](https://jekyllrb.com) and is hosted on [Github Pages](https://pages.github.com) which already makes it pretty easy to write content but I wanted to see if I could make it even easier. I started with a "create new haiku" shortcut. This way anytime I have an idea for a haiku it doesn't matter where I am, as long as I have an internet connection on my phone I can post a new one easily.

So, I began playing with iOS Shortcuts. I wanted a button on my phone that would let me write and post to my blog without needing anything else. The solution I came up with uses a bit of Python in [Pythonista](http://omz-software.com/pythonista/) for some formatting, as well as [Working Copy](https://workingcopyapp.com) for the git actions.

Unfornately, the only way to share an iOS shortcut is to share it directly. I wanted to export and paste a JSON payload here or something so others could edit and import easily, but it looks like the only way is to share a public link to it. So, here's my [shortcut](https://www.icloud.com/shortcuts/7d86a57504eb47098bc7d1290e3239d6) for writing and posting a haiku. With a little editing it should be easy enough to change if you wanted to rework it to post to your own blog. It assumes you have the Working Copy app I linked above, as well as a Pythonista script.

Here are the actions it performs:
* Pull the latest changes from your blog repo
* Ask for the name of the Haiku
* Executes a search in [Giphy](https://giphy.com) for the given title and lets you choose your favorite gif
* Stages the chosen gif in `/assets` in your repo
* Asks for the content of the Haiku. Adding an empty line between each line of content renders the content on new lines. I haven't figured this part out yet, but if you don't do this the whole haiku ends up on one line.
* It then sends the input to the Pythonista script to format it as Jekyll front matter
* It takes the resulting formatted content and stages it as a new file in your repo
* It commits the changes to your repo and pushes to remote
* It then texts my girlfriend to let her know there's a new haiku (I haven't tested this with other people, but I expect that unless you have her number it won't work for you)

So now the only piece missing is the Pythonista script. Here it is:

```
from webbrowser import open
from datetime import date
from urllib.parse import quote, unquote
import sys
import x_callback_url

title=sys.argv[1]
body=sys.argv[2]
gif=quote(sys.argv[3])

haiku='''---
layout: haiku
category: Haikus
title: ''' + title + '''
---
{% include JB/setup %}

''' + body + '''

![--''' + title + '''--](\{\{ site.url \}\}/assets/''' + gif + '''.gif)'''

x_success = sys.argv[-1] # shortcuts-production://x-callback-url/ic-success/<UUID>
x_cancel = x_success.replace('ic-success', 'ic-cancel')
x_error = x_success.replace('ic-success', 'ic-error')

x_success += '?x-source=Pythonista3'
x_success += '&result=' + quote(haiku)
x_success += '&datetime=' + quote(str(date.today().strftime('%Y-%m-%d')))

open(x_success)
```

I've been having fun with this, I've also made a version that will make a full blog post like this one but haven't used it much since writing long form on an iOS device is not that convenient for me. Anyway, if you're reading this feel free to play with my shortcut and python script! I'd love to hear about any projects you use them for!

{% include JB/setup %}
