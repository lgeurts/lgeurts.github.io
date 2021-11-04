---

layout: post
title: A dive into gaming on Windows 11 using AWS and Parsec’s Remote Access Tech solution
read_time: true
comments: true
category: Entertainment
tags: [ Cloud Computing, Gaming ]

---

In this guide I explain how I built a Cloud Gaming environment using Amazon Web Services and Parsec. The principle is similar to any other services like Amazon Prime Video or Disney+; your games are streamed at a **very low latency** from a high-end host instance in AWS to your home device that would crash when even thinking running a game that demands that extra bit of juice. Sounds pretty cool, right?

## **Dude, why should I use cloud gaming when I already have a high-end gaming machine?**

Not everybody can afford having a monster like for example the [Falcon Northwest Talon](falcon-nw.com)](https://www.falcon-nw.com/desktops) at home. But even so, how long will you be able to keep the machine up to date? Think PRICEY video cards, processors outdated, in general the cash you'll have to shell out for playing the latest and greatest? Building yourself? Sure but the same principle for all hardware components applies, and that's why I use an AWS instance. Not up to date? I just create a new one.

## **OK, I'm convinced. What do I need?**

### There are a few requirements that you’ll need to get this working properly:

1. [AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) - Some basics in AWS would be nice, but no worries, follow my steps in this post and you will be ok.

   **Note:** If you really want to save on the last penny, and need to [find your nearest region at the lowest price](https://openupthecloud.com/find-aws-region-closest/), you can use [AWS ping](https://github.com/ekalinin/awsping) by Eugene Kalinin on GitHub.

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

## Action-list

- [ ] **Configuring the Parsec account:**

<img src="/assets/aws-parsec-setup/parsec-new-account.png" width="654">

1. Sign up with a username, email-address and password. You'll get a confirmation (check your spam folder) with a link to click on. Press the mouse button. 

2. [Download](https://parsec.app/downloads/) the client for your platform, install it on your device and login.

- [ ] **Setting up AWS:**

1. By now you created and activated your AWS account. Continue with adding a VPC (Virtual Private Network) by logging in to your account and checking the VPC  console. Click on the *Launch VPC Wizard*, and the next screen opens:

<img src="/assets/aws-parsec-setup/vpc-dashboard.png" width="654">

2. Select VPC with a Single Public Network:

<img src="/assets/aws-parsec-setup/step1-select-vpc-configuration.png" width="654">

3. We don’t need IPv6 for this so you don’t have to give that but give a Name tag so that we can understand what it’s for:

<img src="/assets/aws-parsec-setup/step2-vpc-with-a-single-public-subnet.png" width="654">

4. This is what it looks like when you clicked on *Create VPC*:

<img src="/assets/aws-parsec-setup/vpc-successfully-created.png" width="654">

5. The default VPC is automatically configured to allow Internet access. You can see that my VPC has an ID of vpc-01fe1843d2da4b0e4. If I click on the Internet Gateways tab, you can see that there's an Internet gateway attached to my default VPC. I did not create this Internet gateway. AWS created the gateway automatically at the time that I set up my subscription.

<img src="/assets/aws-parsec-setup/vpc-internet gateway.png" width="654">



