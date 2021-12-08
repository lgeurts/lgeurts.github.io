---

layout: post
title: A dive into Cloud Gaming using AWS and Parsec’s Remote Access Tech solution on Windows
read_time: true
comments: true
category: Entertainment
tags: [ Cloud Computing, Gaming ]

---

In this guide I explain how I built a Cloud Gaming environment using Amazon Web Services and Parsec. The principle is similar to any other services like Amazon Prime Video or Disney+; your games are streamed at a **very low latency** from a high-end host instance in AWS to your home device that would crash when even thinking running a game that demands that extra bit of juice. Sounds pretty cool, right?

## **Dude, why should I use cloud gaming when I already have a high-end gaming machine?**

Not everybody can afford having a monster like for example the [Falcon Northwest Talon](falcon-nw.com)](https://www.falcon-nw.com/desktops) at home. But even so, how long will you be able to keep the machine up to date? Think PRICEY video cards, processors outdated, in general the cash you'll have to shell out for playing the latest and greatest? Building yourself? Sure but the same principle for all hardware components applies, and that's why I use an AWS instance. Not up to date? I just create a new one. And with cloud gaming, you can stream games to a notebook, even a phone, making a high-fidelity gaming experience cheap and mobile.

## **OK, I'm convinced. What do I need?**

### There are a few requirements that you’ll need to get this working properly:

1. [AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) - Some basics in AWS would be nice, but no worries, follow my steps in this post and you will be ok.
   **Note:** If you want to save on the last penny, and need to [find your nearest region at the lowest price](https://openupthecloud.com/find-aws-region-closest/), while also having the fastest connection possible, you can use tools like [AWS ping](https://github.com/ekalinin/awsping) by Eugene Kalinin on GitHub.
2. [Parsec account](https://parsec.app/) - Sounds like a logical decision.
3. A good internet connection – 30/40mbps - FTTH (for low latency). The most difficult part is streaming latency. All steps - such as running the game, encoding and decoding the game video and converting the player input are done in real time.
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

**Configuring the Parsec account:**

<img src="/assets/aws-parsec-setup/parsec-new-account.png" width="654">

1. Sign up with a username, email-address and password. You'll get a confirmation (check your spam folder) with a link to click on. Press the mouse button.
2. [Download](https://parsec.app/downloads/) the client for your platform, install it on your device and login.

**Setting up AWS:**

1. By now you created and activated your AWS account. Continue with adding a VPC (Virtual Private Network) by logging in to your account and checking the VPC  console. Click on the *Launch VPC Wizard*, and the next screen opens:

<img src="/assets/aws-parsec-setup/vpc-dashboard.png" width="654">

2. Select VPC with a Single Public Network:

<img src="/assets/aws-parsec-setup/step1-select-vpc-configuration.png" width="654">

3. We don’t need IPv6 for this so you don’t have to give that but give a Name tag so that we can understand what it’s for:

<img src="/assets/aws-parsec-setup/step2-vpc-with-a-single-public-subnet.png" width="654">

4. This is what it looks like when you clicked on *Create VPC*:

<img src="/assets/aws-parsec-setup/vpc-successfully-created.png" width="654">

5. The default VPC is automatically configured to allow Internet access. My VPC has an ID of vpc-01fe1843d2da4b0e4. If I click on the Internet Gateways tab there's an Internet gateway attached to my default VPC. I did not create this Internet gateway. AWS created the gateway automatically at the time that I set up my subscription.

<img src="/assets/aws-parsec-setup/vpc-internet-gateway.png" width="654">

6. Hence the same for the subnet. Note that though it is best practice to create a second availability zone for HA, I'm gonna skip it. Remember this is for gaming, not for company production. Should you feel an irresistible urge, a how-to can be found [here](https://tomgregory.com/when-to-create-different-subnets-in-aws-vpcs/).

<img src="/assets/aws-parsec-setup/vpc-subnet.png" width="654">

7. And the route table:

<img src="/assets/aws-parsec-setup/vpc-route-table.png" width="654">

8. Moving to EC2. We first have to verify our security group, then subscribe to the required AMI from the [AWS Marketplace](https://aws.amazon.com/marketplace/), and then we have to launch the instance.

9. Go to the Security / Security Groups tab and check that rules are conform below values:

<img src="/assets/aws-parsec-setup/ec2-security-group.png" width="654">

This is not at all secure but it's convenient and only for this post. You can check [here](https://support.parsecgaming.com/hc/en-us/articles/360043419312) and [here](https://support.parsecgaming.com/hc/en-us/articles/360045297592) to get the exact port requirements.

   Inbound:
   `All traffic | All | All | Anywhere | “0.0.0.0/0” / “::/0”`

<img src="/assets/aws-parsec-setup/ec2-security-group-inbound.png" width="654">

   Outbound:
   `All traffic | All | All | Anywhere | “0.0.0.0/0” / “::/0”`

<img src="/assets/aws-parsec-setup/ec2-security-group-outbound.png" width="654">

10. Subscribe to the [NVIDIA Gaming PC – Windows Server 2019](https://aws.amazon.com/marketplace/pp/B07STLTHM8?ref_=beagle) from the AWS Marketplace.




