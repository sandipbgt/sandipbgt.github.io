---
layout:     post
post_id : 12
title:      "How To Copy Any Text To Clipboard From Terminal In Ubuntu?"
date:       2015-10-22 4:15:00
author:     "Sandip Bhagat"
thumbnail: ""
---

`xclip` is a commandline interface to the X selections (clipboard). This tool helps you to copy the output of any command directly into the clipboard and saves you
from manually copying and pasting from the terminal. If you have tried copying from the terminal output, you have already realized how tedious the task is. Imagine,
if the output is very long, it will be difficult to copy the output manually. This is where `xclip` tool can benefit you. You can copy the output of any command using
this tool. It also allows you to copy the contents of a file directly into the clipboard as well as print the contents of a selection to the standard out.

## Installing xclip
`xclip` is available as a package for Ubuntu so, it can be installed as below. Open a terminal `Ctrl` + `Alt` + `T` and run:

{% highlight bash %}
sudo apt-get install xclip
{% endhighlight %}

## Using xclip
To copy the output of a command into the clipboard, pipe the command into `xclip` as below:

#### Long version
{% highlight bash %}
ls -la | xclip -selection clipboard
{% endhighlight %}

#### Short version
{% highlight bash %}
ls -la | xclip -sel clip
{% endhighlight %}

This puts the output of `ls -la` command into the clipboard, and you can now paste the output into any other program (eg. a text editor) with `Ctrl` + `V`
outside terminal and `Ctrl` + `Shift` + `V` inside terminal.

To copy the contents of a file (eg. /etc/apt/sources.list) into the clipboard:

#### Long version
{% highlight bash %}
xclip -selection clipboard -in /etc/apt/sources.list
{% endhighlight %}

#### Short version
{% highlight bash %}
xclip -sel clip -i /etc/apt/sources.list
{% endhighlight %}

To print the contents of the clipboard:

#### Long version
{% highlight bash %}
xclip -selection clipboard -out
{% endhighlight %}

#### Short version
{% highlight bash %}
xclip -sel clip -o
{% endhighlight %}

To save the contents of the clipboard to a file (eg. ~/myfile.txt):

#### Long version
{% highlight bash %}
xclip -selection clipboard -out > ~/myfile.txt
{% endhighlight %}

#### Short version
{% highlight bash %}
xclip -sel clip -o > ~/myfile.txt
{% endhighlight %}