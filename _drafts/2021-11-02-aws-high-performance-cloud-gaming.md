---

layout: post
title: A dive into gaming on Windows 11 using AWS and Parsec’s Remote Access Tech solution
read_time: true
comments: true
category: Entertainment
tags: [ Cloud Computing, Gaming ]

---

In this guide I explain how I built a Cloud Gaming environment using Amazon Web Services and Parsec. The principle is similar to any other services like Amazon Prime Video, Hulu or Disney+, your games are streamed at a very low latency from a high-end host instance in AWS to your low-end device that probably would crash at even thinking to run games from 5 years ago. Sounds pretty cool, right?

## **Dude, why should I use cloud gaming when I already have a high-end gaming machine?**

Consider yourself a lucky person. Not everybody can afford having a monster like for example the [Falcon Northwest Talon](falcon-nw.com)](https://www.falcon-nw.com/desktops) at home. But even so, how long will you be able to keep the machine up to date? Think PRICEY video cards, processors that get outdated, in general the amount of cash you will have to shell out for playing the latest and greatest? Building yourself? Sure but the same principle for all hardware components applies. 

## **OK, I'm convinced. What do I need?**

### There are a few requirements that you’ll need to get this working properly:

1. AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) - Some basic knowledge in AWS would be great but no worries, just follow the steps in this post and you will be ok.

2. [Parsec account](https://parsec.app/) - Sounds like a logical decision.
3. A good internet connection – 30/40mbps - FTTH (for low latency).
4. A job/business to pay the bill – AWS isn’t free, but it’s cheap.
5. A game – Anything you want with the exception of VR (I'm actually gonna test that one).
6. A local machine running any of the following:
   - Windows 7+
   - Linux – Ubuntu 18.04+
   - Google Chrome or Microsoft Edge
   - MacOS 10.11
   - Raspberry PI 3
   - Android – With Google Play

- [ ] #### **Setting up the Parsec account**

<img src="/assets/aws-parsec-setup/parsec-new-account.png" width="654">

1. Sign up with a username, email-address and password. You'll get a confirmation (check your spam folder) with a link to click on. Do that. 

2. [Download](https://parsec.app/downloads/) the client for your platform, install it on your device and login.



