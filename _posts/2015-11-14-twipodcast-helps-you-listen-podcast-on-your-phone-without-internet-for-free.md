---
layout:     post
title:      TwiPodcast, A Web App that Helps You Listen Podcast On Your Phone Without Internet
date:       2015-11-14 11:00 +0545
author:     "Sandip Bhagat"
---

I am happy to release my new open source project **TwiPodcast**. Actually, I built this project for one of my best friend who lives in India.

We usually have a regular chat on Facebook and wishing her **Good Morning** and **Good Night** everyday had become my daily routine. One day, I thought, why not wish her everyday in my own voice via phone call. So, to wish her, I can use Facebook Messenger, WhatsApp or Viber as there are so many VOIP alternatives. But all these options require active internet connection both to sender side and receiver side. If it was one day task, I could call from my phone or use those free VOIP apps but I need to wish her everyday and it is going to cost me a lot if I continue with existing call options.

As a developer, I thought why not build something myself that can be used to call phones for free. This is how the idea for the project comes in my mind. Initially this project was made specifically for my friend but then I realized, there might be many people like me, who wants to wish their beloved ones in their own voice for so, I generalized the project for normal people.

Though, the initial idea was to wish my friend but after working on the project for some days, the idea changed from wishing to listening podcast and so named TwiPodcast as there are many people who love listening podcast.

## What is TwiPodcast

Twipodcast is a web app that allows you to listen podcast or any mp3 media file on your phone for free without internet.

Yes, you heard it right. You don’t need internet to listen podcast.

## How it works?

The web app uses the url of the mp3 file and calls the given phone number to stream the mp3 file directly to the phone number via phone call without requiring internet to the receiver side. You can supply a valid url of any media file that is of mp3 format to stream the media file to your phone without internet.

## Use cases

### Listening podcast

Suppose, you want to listen any podcast on your mobile phone. To listen it, you must have internet connection and you know, it is going to eat your data package if you are on mobile network. In such a situation, you can use TwiPodcast to stream the podcast directly to your phone for free without internet.

### Dedicating songs

Suppose, you liked any song and want to dedicate it to your beloved ones. In order to do so, you must have url of that song and you can also use TwiPodcast to dedicate song to your beloved ones.

### Convert text to speech

Suppose, you want to convert the text into speech so that you friend can listen what you typed. In such a situation, you can use TwiPodcast to perform the task. You need to type the message and TwiPodcast will convert the text into speech once the call is made. The result is, your friend listens the message you typed in the textbox.

## How to use TwiPodcast?

* Create an account at [http://twilio.com](http://twilio.com)
* Verify your email.
* Get a Twilio number.
* Verify the number whom you want to call.
* Copy your **account sid** and **auth token** from Twilio dashboard page.
* Visit [http://sandipbgt.github.io/twipodcast/#/sendPodcast](http://sandipbgt.github.io/twipodcast/#/sendPodcast)
* Enter all the details.
* In **Voice text** input field, type the message you want to convert to speech.
* In **Podcast Url** input field, type the url of the podcast you want to listen. Some of the podcasts url can be found by clicking **Browse Podcasts** menu. You can also use url of any valid mp3 file.
* Click on **SEND** button and a phone call will be made to the number that you entered in **To phone** input field.

If you are a developer, you might be interested in reading the source code at [https://github.com/sandipbgt/twipodcast](https://github.com/sandipbgt/twipodcast) or the documentation at [http://sandipbgt.github.io/twipodcast/docs](http://sandipbgt.github.io/twipodcast/docs)

**Note:** Most of  the countries are supported for Twilio phone calls. However, Nepal is not in the list currently.