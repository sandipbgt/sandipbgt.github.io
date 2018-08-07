---
layout:     post
post_id : 10
title:      "How To Control Your Monitor Brightness From Command Line In Ubuntu?"
date:       2015-10-1 8:45:00
author:     "Sandip Bhagat"
thumbnail: ""
---

I use a Ubuntu desktop with a LCD display. As a developer, working late night in front of a computer is very common for me. But working late night has got one problem.
The brightness of my monitor is usually very high which affects the eyes in the long run. Though, I could adjust the brightness from monitor settings with its hardware
buttons but after adjusting, the display of my monitor doesn't looks that good. If it was a laptop, the task is very easy as there are some dedicated keys to control
the brightness which makes it easy to adjust the brightness on demand.

After searching in Google, I found some applications and tried those but for some reason they didn't work for me. Then I got to know about `xrandr` command. I can use
this to control the brightness of my screen and the best thing is, I don't need to install this as it comes with Ubuntu already.

Here is the process to adjust the brightness of your screen.

* First open a terminal with `Ctrl` + `Alt` + `T`
* Type `xrandr | grep " connected" | cut -f1 -d " "` to find your monitor's name
* Now type `xrandr --output your-monitor-name --brightness brightness-level`

For example

{% highlight bash %}
$ xrandr | grep " connected" | cut -f1 -d " "
VGA1
$ xrandr --output VGA1 --brightness 0.7
{% endhighlight %}

In my case, the name of my monitor was `VGA1` so, I used `VGA1` as the monitor name and changed my brightness to `0.7`.

**Note**: The brightness level must be between `0 to 1` with 0 being the dimmest and 1 being the brightest.

{% if site.url != 'http://localhost:4000' %}
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2234798818029685"
     data-ad-slot="1035049530"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
{% endif %}

I have created a script to adjust the screen brightness.
<script src="https://gist.github.com/sandipbgt/330de5b709db86b4e74c.js"></script>

## Adding script to startup
If you have restarted your computer then you might have realized that the changes are lost. Whenever you change brightness using `xrandr` command, the change
is temporary and is lost when you reboot your computer. Everytime, you reboot your computer, you need to type these commands again to adjust the brightness.

In order to avoid typing the command everytime, we can create a script that will run everytime the computer boots.

* Create `dimmer-startup.sh` file at `~/dimmer-startup.sh`
* Copy the below code to `dimmer-startup.sh` file.

{% highlight bash %}
#!/bin/bash
# Bash script to control the monitor brightness
brightness_level=0.7
screenname=$(xrandr | grep " connected" | cut -f1 -d" ")
xrandr --output $screenname --brightness $brightness_level;
{% endhighlight %}

* Give execute permission to `dimmer-startup.sh` file by typing `sudo chmod +x ~/dimmer-startup.sh`
* You can change the value of `brightness_level` variable to your taste. It must be between `0 to 1`.
* Create `Dimmer.desktop` file at `~/.config/autostart/Dimmer.desktop`
* Copy the below code to `Dimmer.desktop` file.

{% highlight bash %}
[Desktop Entry]
Type=Application
Exec="/home/user-name/dimmer-startup.sh"
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name=Dimmer Script
GenericName=Dimmer Script
Categories=Utility;
StartupNotify=false
Comment=Dimmer App to control screen brightness
{% endhighlight %}

* Replace `user-name` with your account username

Now, whenever your computer boots, the scripts runs automatically and your screen brightness is adjusted.