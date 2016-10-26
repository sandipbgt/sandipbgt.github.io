---
layout:     post
post_id : 13
title:      "How To Install Arc Theme In Ubuntu?"
date:       2015-10-25 14:11 +0545
author:     "Sandip Bhagat"
thumbnail: "https://farm1.staticflickr.com/641/22497045831_a5b6488eaf_z_d.jpg"
---

Ubuntu’s default theme is nice enough, but it is hasn’t changed much
in several years. If you want a stylish looking Ubuntu desktop, try an
alternative theme. Mine favourite is `Arc` theme.

Note: You must be running **Ubuntu 15.04 or later** to use this theme.

![Arc Theme Preview](https://farm1.staticflickr.com/641/22497045831_a5b6488eaf_z_d.jpg)

## Installation

Open your terminal and run the below commands

{% highlight bash %}
sudo apt-get install unity-tweak-tool
wget http://download.opensuse.org/repositories/home:Horst3180/xUbuntu_15.04/Release.key
sudo apt-key add - < Release.key
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/home:/Horst3180/xUbuntu_15.04/ /' >> /etc/apt/sources.list.d/arc-theme.list"
sudo apt-get update
sudo apt-get install arc-theme
{% endhighlight %}

## Configuration

* Launch `Unity Tweak Tool` from the `Dash`.
* Click on `Theme` under `Appearance` section.
* Select `Arc` theme from `Available themes` list.
* Click `Icons` tab.
* Select `Elementary-xfce-dark` from `Available themes` list.

Enjoy the new look of your Ubuntu desktop.