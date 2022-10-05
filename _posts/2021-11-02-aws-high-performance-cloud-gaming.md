---

layout: post
title: A dive into Cloud Gaming using AWS Cloud and Parsec’s Remote Access Tech solution
read_time: true
comments: true
category: Entertainment
tags: [ Cloud Computing, Gaming ]

---

In this guide I explain how to build a Cloud Gaming environment using Amazon Web Services and [Parsec](https://parsec.app/). Its basics are similar to other services like for example Amazon Prime Video or Disney+; your games are streamed at a very low latency from a high-end EC2 host in AWS to your home device that would flip-out when even thinking running games demanding so much juice. Sounds cool, right?

## **Dude, why cloud gaming when I already have a gaming machine?**

Not everybody can afford a monster the likes of a [**Falcon Northwest**](https://www.falcon-nw.com/desktops) Talon. Even so, how long will you be able to keep that glorious toy up to date? Think PRICEY video cards, new processors, faster and bigger drives, watercooling, all that cash you'll have to shell out for playing the latest and greatest? 

Building yourself? Sure, but the same principle for all components applies. And that's the reason I opted for an AWS instance. It's always on the latest standard, no need to worry about compatibility, hardware upgrades, updating drivers, OS patches. And with cloud gaming, you can stream content to notebooks, phones, thus making a high-fidelity gaming experience cheap and mobile.

## **OK, I'm convinced. What do I need?**

### List of requirements that you’ll need to get this working properly:

1.     [AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) - Some knowhow in AWS would be nice, but no worries, just follow my steps in this post and you will be ok.
2.     [Parsec account](https://parsec.app/) - Sounds like a logical decision.
3.     A stabile internet connection, at least 30/40mbps FTTH (for low latency). The most difficult part is streaming latency. Running the game, encoding and decoding the game video and converting the player input are done in real time.
4.     A job to pay the bill - AWS isn’t free, but it’s cheap.
5.     A game - Anything you want with the exception of VR.
6.     A local machine running any of the following:
   - Windows 7+
   - Linux – Ubuntu 18.04+
   - Firefox, Google Chrome or Microsoft Edge
   - MacOS 10.11
   - Raspberry PI 3
   - Android – With Google Play

Hint: Find your [nearest region at the lowest price](https://openupthecloud.com/find-aws-region-closest/). Want the fastest connection possible? Use Eugene Kalinin's [AWS ping](https://github.com/ekalinin/awsping).

## Action-list

**Configuring the Parsec account:**

- Go to the Parsec site, new account:

  <img src="/assets/aws-parsec-setup/parsec-new-account.png" width="654">

- Sign up with a username, email-address and password. You'll get a confirmation (check your spam folder) with a link to click on. Press the mouse button.

- [Download](https://parsec.app/downloads/) the client for your platform, install it on your device and login.

**Setting up AWS:**

- By now you created and activated your AWS account. Continue with adding a VPC (Virtual Private Network) by logging in to your account and checking the VPC  console. Click on the *Launch VPC Wizard*, and the next screen opens:

  <img src="/assets/aws-parsec-setup/vpc-dashboard.png" width="654">

- Select VPC with a Single Public Network:

  <img src="/assets/aws-parsec-setup/step1-select-vpc-configuration.png" width="654">

- We don’t need IPv6 for this so you don’t have to give that but give a Name tag so that we can understand what it’s for:

  <img src="/assets/aws-parsec-setup/step2-vpc-with-a-single-public-subnet.png" width="654">

- This is what it looks like when you clicked on *Create VPC*:

  <img src="/assets/aws-parsec-setup/vpc-successfully-created.png" width="654">

- The default VPC is automatically configured to allow Internet access. My VPC has an ID of vpc-01fe1843d2da4b0e4. If I click on the Internet Gateways tab there's an Internet gateway attached to my default VPC. I did not create this Internet gateway. AWS created the gateway automatically at the time that I set up my subscription.

  <img src="/assets/aws-parsec-setup/vpc-internet-gateway.png" width="654">

- Hence the same for the subnet. Note that though it is best practice to create a second availability zone for HA, I'm gonna skip it. Remember this is for gaming, not for company production. Should you feel an irresistible urge, a how-to can be found [here](https://tomgregory.com/when-to-create-different-subnets-in-aws-vpcs/).

  <img src="/assets/aws-parsec-setup/vpc-subnet.png" width="654">

- And the route table:

  <img src="/assets/aws-parsec-setup/vpc-route-table.png" width="654">

- Go to the Security / Security Groups tab and check that rules are conform below values:

  <img src="/assets/aws-parsec-setup/ec2-security-group.png" width="654">
  
  This is not at all secure but it's convenient and only for this post. You can check [here](https://support.parsecgaming.com/hc/en-us/articles/360043419312) and [here](https://support.parsecgaming.com/hc/en-us/articles/360045297592) to get the exact port requirements.
  
  - Inbound: `All traffic | All | All | Anywhere | “0.0.0.0/0” / “::/0”`
  
  
  - Outbound:`All traffic | All | All | Anywhere | “0.0.0.0/0” / “::/0”`
  

**Configuring the gaming server:**

- Login to your AWS account and subscribe to the [NVIDIA Gaming PC – Windows Server 2019](https://aws.amazon.com/marketplace/pp/prodview-xrrke4dwueqv6?ref_=beagle) g4dn.xlarge AMI (which features the NVIDIA T4 GPU) from the AWS Marketplace (click on the different regions to compare hourly prices).
- Once done, you can launch your instance with the following settings:
- 
