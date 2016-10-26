---
layout:     post
post_id : 9
title:      "How To Create Bootable USB From ISO File In Ubuntu"
date:       2015-09-29 07:00:00
author:     "Sandip Bhagat"
thumbnail: ""
---

Today I downloaded ISO file of Ubuntu MATE 15.04 from [https://ubuntu-mate.org/vivid](https://ubuntu-mate.org/vivid). Instead of installing the OS on my disk, I thought to first try it live from USB. So, to try it live, I need to make my USB bootable. In Windows, making a bootable USB is very easy. [Univeral USB Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3) is my best tool to do the job. But in Ubuntu, I have never created a bootable USB. So I googled for the instructions and came to know that **Startup Disk Creator** and **[unetbootin](http://unetbootin.github.io/linux_download.html)** are some recommended tools in Ubuntu for creating bootable USB. I tried them but unfortunately, it didn't work for me. So, I searched for `dd` command since I had used this tool to write Raspbian OS img file on my Raspberry Pi 2 B and came to know that we can use `dd` command to make USB bootable.
So, first I formated my USB to NTFS file system and then typed the following command in terminal.
{% highlight bash %}
sudo dd if=input.iso of=/dev/sdb
{% endhighlight %}
where `input.iso` is ISO file of your downloaded OS and `/dev/sdb` is your USB device. It took around 8 minutes to complete and I was able to make my USB bootable.

