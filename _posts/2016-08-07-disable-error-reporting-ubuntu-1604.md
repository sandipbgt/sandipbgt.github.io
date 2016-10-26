---
layout:     post
post_id : 18
title:      How To Disable Error Reporting In Ubuntu 16.04?
date:       2016-08-07 21:06 +0545
author:     "Sandip Bhagat"
thumbnail: "https://farm9.staticflickr.com/8563/28542913480_0db5227b0b_z_d.jpg"
---

Sometimes while using Ubuntu, you may get some error popups that asks you to report problems. These errors are really very annoying.
In other to disable these error reporting, you can do either of the two things.

### Stopping the error reporting temporarily
* Open terminal by typing `Ctrl` + `Alt` + `T` and run the following command.

{% highlight bash %}
sudo service apport stop
{% endhighlight %}

![https://farm9.staticflickr.com/8563/28542913480_0db5227b0b_z_d.jpg](https://farm9.staticflickr.com/8563/28542913480_0db5227b0b_z_d.jpg)

### Stopping the error reporting permanently
* Open terminal by typing `Ctrl` + `Alt` + `T` and run the following command.

{% highlight bash %}
sudo gedit /etc/default/apport
{% endhighlight %}

![https://farm9.staticflickr.com/8746/28542915700_8b8b739e79_o_d.png](https://farm9.staticflickr.com/8746/28542915700_8b8b739e79_o_d.png)

* After the file opens, change the value of `enabled=1` to `enabled=0` and save it.

![https://farm9.staticflickr.com/8059/28827061535_d6604ab8db_o_d.png](https://farm9.staticflickr.com/8059/28827061535_d6604ab8db_o_d.png)

That's it. From now on, you won't get those annoying error reporting popups.