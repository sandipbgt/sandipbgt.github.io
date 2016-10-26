---
layout:     post
post_id : 19
title:      How To Display Network Speed On Unity Panel In Ubuntu?
date:       2016-08-08 08:39 +0545
author:     "Sandip Bhagat"
thumbnail: "https://farm9.staticflickr.com/8747/28734167682_0e40b15fe1_o_d.png"
---

The `Indicator Netspeed` displays the total current network traffic on the Unity Panel. It also shows current download and upload speed
as individual values.

![https://farm9.staticflickr.com/8747/28734167682_0e40b15fe1_o_d.png](https://farm9.staticflickr.com/8747/28734167682_0e40b15fe1_o_d.png)

## Installing Indicator Netspeed
The `Indicator Netspeed` can be installed by adding the PPA from webupd8.

{% highlight bash %}
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt-get update
sudo apt-get install indicator-netspeed
{% endhighlight %}

You can also download the deb package from [here](http://ppa.launchpad.net/nilarimogard/webupd8/ubuntu/pool/main/i/indicator-netspeed/) and 
install it manually.

After the installation completes, you have to log out and log in again in other for `Indicator Netspeed` to work.

After `Indicator Netspeed` starts for first time, you have to specify the network interace from indicator menu because it does not detect
currently used network interface and by default it selects wlan0.