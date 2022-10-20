---
layout: post
title: An Open Source tool for keeping on top of the activity in your AWS account
read_time: true
comments: true
category: Open Source
tags: [ Cloud Computing, GitHub Projects ]
---

Today we are going to talk a bit about this open source tool called [Activity Aware IDS for AWS](https://github.com/Giftbit/activity-aware-ids-aws) which helps system admins be more aware of activities in their AWS account, including those that might include potential account compromises. Our post will focus on some more common use cases for Activity Aware IDS, and how to start using it today. But before we get to that, it’s important to understand the 3 security threats you face as an AWS customer, your responsibility in protecting against them, and refresh what you learned about the least privilege principle as best practice in thinking about security and access control.

## **The principle of least privilege**

Any systems, any identities (users, programs, systems, etc.) granted privileges to access resources or information, should be granted only the minimum privileges necessary to perform their tasks. In the Activity Aware IDS default configuration, it will inform you or your team when users or roles are attempting to use actions or access resources beyond their privileges. 

You can also configure Activity Aware IDS to notify you of AWS API actions, even when these actions are permitted, but this turns out to be more complex and was something we simply did not have the time for (so that task is up to you).

## **The AWS Shared Responsibility Model**

A cornerstone of security in the AWS Cloud is the Shared Responsibility Model. At its highest level, this is a **delineation** between what **AWS** takes responsibility for to secure, and what you as an **AWS customer** are responsible for securing.
<br>AWS takes care of security OF the cloud, YOU take care for security IN the cloud.

From the AWS side, they take responsibility for securing the building blocks used to compose your systems. These typically include **Compute** (EC2) hosts, **Storage** (S3) infrastructure, **Databases** (RDS), **Networking** infrastructure, and so on. That’s not to say you should throw all of your customers' credit card data into an S3 bucket and think your security responsibility is according AWS agreement.
<br>You still have to lock that bucket!

## **Security Threats in the Cloud**

The 3 major types of security incidents in AWS: 
- Infrastructure Impact, 
- Host Compromise, 
- Account Compromise.

Infrastructure Impact includes external attacks on the underlying infrastructure of your application. This type of attacks largely consists of Distributed Denial of Service (DDoS) attacks, where an attacker sends a large volume of traffic at your site. AWS Shield is a service you can use to prevent that kind of attacks.

Host Compromise involves techniques like command injection to gain access to your resources, such as those EC2 instances. A free source for BitCoin mining or gaining access to their data & approach other instances that likely hold valuable data. Host-based intrusion detection and intrusion prevention are the two most common methods of alleviating this type of threat. 

Account Compromise involves an attacker gaining access to users or roles on an instance, and then using them for the data they have access to, or the resources they can create.
<br>There are not many solutions that fill the gap. Activity Aware IDS for AWS does. 
When the attacker attempts to scout for permissions of compromised identities (users, roles), he/she will definitely get access denied to a number of the actions and resources they attempt to use while testing. Activity Aware IDS notifies you of these denials in for example a Slack channel.

## **Use Cases**

Activity Aware IDS uses CloudTrial and the least privilege principle.

Lets imagine a user named Mr. X had his credentials compromised by a attacker Mr. Z.
Mr. Z wants to see what groups and roles they have access to through Mr. X's account. Mr. Z doesn’t have access rights to view groups Mr. X is associated with, and doesn’t have access to view policies attached to those groups. 
If Mr. Z tries to view the policies, the system raises a access denied which gets logged to CloudTrail. 

At this point Activity Aware IDS receives a denial log, converts it into a friendly format, and then sends it to your Slack Channel. Once the message arrives, you will see that there are strange “Access Denied” messages associated with Mr. X. 
<br>Good administrators will call the user causing that message and find he wasn't performing the actions. Time to replace his credentials.

Mr. Z was blocked from performing actions due to the least privilege principle. Although this is a standard recommendation in security land, it can be difficult in finding the exact set of permissions that a User or Role should have. Activity Aware IDS can also assist with this.

You are deploying a new service, and you want to give it permissions following the least privilege. The easy way to start is creating a role with no permissions. Let's assume your system needs to send logs to CloudWatch Logs (requirement for AWS Lambda). When the system attempts to create a new Log Group, it will get denied, because the role has no permissions. In turn an event logs to CloudTrail where Activity Aware IDS for AWS will pick it ip and send as message to your Slack, where you can see the action being attempted, the Role attempting to perform the action, and the arn of the specific resource it’s trying to perform the action on. 

At this point, you can add a statement to the policy for the role allowing it access to “CreateLogGroup” and even provide a fairly restrictive resource description.

## **What to do next**

Feel like getting your hands dirty? Checkout the [Giftbit Guide](https://github.com/Giftbit/activity-aware-ids-aws#getting-started).

*Ref: Web: Some content was copied from the Giftbit repo.*
