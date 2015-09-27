---
layout:     post
title:      "How To Remove Facebook Page's Post In Bulk Using Python"
date:       2015-09-28 06:30:00
author:     "Sandip Bhagat"
---
Few days back I was going through the timeline posts of my personal Facebook page which I hadn't updated since very long. After going through some posts, I found that many of these posts were pointing to a external link, which was dead. So, I thought to remove all those posts in order to have a clean timeline :) . First I tried to delete posts manually by clicking and clicking like a school kid... But after removing around 5 posts manually, I thought to check how many posts are there actually with such dead links and I found that the posts were since 2013. You can imagine the number of posts now. If I do the task manually, it is going to take a lot of time. In order to save my time and perform it quickly, I thought to write a Python script to delete the posts, thus automating my task.

In order to perform my task, I need to interact with Facebook Graph API. First I went to [https://developers.facebook.com/tools/explorer](https://developers.facebook.com/tools/explorer) and obtained my Facebook page access token. To obtain access token, click on **Get Token** button and then click on **Get Page Token**. By default Facebook does not give permission to read your posts via API so, you need to get permissions to read your page's posts. To obtain permission, click on **Get Token** button again and tick **user_posts** permission under **User Data Permissions** tab and click on **Get Access Token** button. The popup window appears to authorize the application. Give permission to the app by authorizing it.

Now, copy the access token you just obtained since we need it to make API calls to Facebook and download the script from my GitHub [repo](https://github.com/sandipbgt/fb-post-bulk-delete) .

Open **app.py** and paste you access token in **access_token** key's value. You also need to specifiy time period in order to delete the facebook posts of certain range. Facebook requires dates in Unix timestamps format. So, to obtain the date in that format, go to [http://www.unixtimestamp.com](http://www.unixtimestamp.com) and enter the date in human readable format to obtain the date in Unix timestamps format and replace the value of **until** and **since** with your date.

Now perform the following steps from your current directory where the script resides:
Note: You must have *Python 3*, *pip* and *virtualenv* installed.
{% highlight bash %}
$ virtualenv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
$ python app.py
{% endhighlight %}
After the script runs, it will display the number of posts to delete and will delte them automatically.