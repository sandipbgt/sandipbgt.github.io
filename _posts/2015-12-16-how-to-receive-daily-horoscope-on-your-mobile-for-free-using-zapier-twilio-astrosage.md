---
layout:     post
title:      How To Receive Daily Horoscope On Your Mobile For Free Using Zapier, Twilio and Astrosage
date:       2015-12-16 14:23 +0545
author:     "Sandip Bhagat"
---

Have you ever wondered of receiving daily horoscope on your mobile for free? If yes, then follow this simple guide to setup your mobile to receive daily horoscope.

We will be using [Zapier](https://zapier.com) to automate the task, [Twilio](http://twilio.com) to send free SMS and [Astrosage API](https://astrosage-api.herokuapp.com/) for horsocope api.

So, let's get started.

## Setting up Twilio

* First, signup for a Twilio trial account at [https://www.twilio.com/try-twilio](https://www.twilio.com/try-twilio)
* Visit [https://www.twilio.com/user/account/phone-numbers/getting-started](https://www.twilio.com/user/account/phone-numbers/getting-started) and click on `Get your first Twilio phone number` button to get a phone number from Twilio.

![Step 1](https://farm1.staticflickr.com/584/23675858242_43681a849c_b_d.jpg)

* After the modal window appears, click on `Choose this Number` and copy this phone number as we will need this later.

![Step 2](https://farm1.staticflickr.com/717/23702017431_fec8e98739_b_d.jpg)

* While you are on this page, click `Show API Credentials` and copy your `ACCOUNT SID` and `AUTH TOKEN`.
* Visit [https://www.twilio.com/user/account/phone-numbers/verified](https://www.twilio.com/user/account/phone-numbers/verified) and click on `Verify a number` button to verify the phone number to which you want to receive horoscope.

![Step 3](https://farm6.staticflickr.com/5826/23156172814_e7892a313b_b_d.jpg)

* Visit [https://www.twilio.com/user/account/settings/international/sms](https://www.twilio.com/user/account/settings/international/sms) and tick the country to which your phone number belongs to enable `Geographic Permissions`.

## Setting up Zapier

* Signup for a `Zapier` account at [https://zapier.com/sign-up/](https://zapier.com/sign-up/)
* Click on `Make a New Zap` button

![Step 4](https://farm6.staticflickr.com/5707/23784336105_45a1bac42c_b_d.jpg)

* Click on `Choose a Trigger app` and select `Schedule by Zapier` from the list.
* Click on `Choose a Trigger` and select `Every Day` from the list.
* Click on `Choose an Action app` and select `Webhooks by Zapier` from the list.
* Click on `Choose a Action` and select `POST` from the list.

![Step 5](https://farm6.staticflickr.com/5719/23157524843_aca9bccd28_b_d.jpg)

* Click on `Continue` button until you reach `Step 4 Filter Schedule By trigger` sreen.
* In `Time of Day` select the time you want to receive daily horoscope and click on `Continue` button.
* In `Match up  Schedule by Zapier Day to  Webhooks by Zapier POST` screen, enter `https://astrosage-api.herokuapp.com/api/horoscope/{your-horoscope}/daily` in `URL` field replacing `your-horoscope` with your own horoscope.
* Select `json` in `Payload Type`.
* In `Data` screen, click on plus button three times to add three more text boxes.
* Enter the details as shown in the screenshot below replacing `auth_token` with your Twilio Auth Token, `account_sid` with your Twilio Account SID, `to_phone` with phone number to which you want to receive horoscope and `from_phone` with the phone number you got from Twilio.

![Step 6](https://farm6.staticflickr.com/5661/23758223596_5f49609c47_b_d.jpg)

* Click on `Continue` button to go `Test this ZAP` screen.
* Click on `Test Schedule by Zapier trigger` to check the trigger and click on `Continue` button.
* in `Name and turn this Zap on` screen, enter the name for your zap and click on `Turn Zap on` button to turn on your zap.

Congratulation, you have successfully setup your phone numer to receive daily horoscope for free everyday.

If you find it complex to setup, you can order my [Fiverr Gig](https://www.fiverr.com/sandipbgt/send-you-horoscope-on-your-phone-as-sms) and I would set it up for you or you can also contact me via email.
