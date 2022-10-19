---
layout: post
title: An Open Source tool for keeping on top of the activity in your AWS account
read_time: true
comments: true
category: Open Source
tags: [ Cloud Computing, GitHub Projects ]
---

Today we are going to talk a bit about this open source tool called [Activity Aware IDS for AWS](https://github.com/Giftbit/activity-aware-ids-aws) which helps system admins be more aware of activities in their AWS account, including those that might include potential account compromises. My post will focus on some more common use cases for Activity Aware IDS, and how to start using it today. But before we get to that, it’s important to understand the 3 security threats you face as an AWS customer, your responsibility in protecting against them, and get an overview of the least privilege principle as best practice in thinking about security and access control.

## **The principle of least privilege**

Any systems, any identities (users, programs, systems, etc.) granted privileges to access resources or information, should be granted only the minimum privileges necessary to perform their tasks. In the Activity Aware IDS default configuration, it will inform your or your team team when users and roles are attempting to use actions or access resources beyond their privileges. It is also possible to configure Activity Aware IDS to notify you of AWS API actions, even when these actions are permitted, but this is more complex and something I did not have time for.

## **The AWS Shared Responsibility Model**

The cornerstone of security in the AWS Cloud is the Shared Responsibility Model. At a high level, this is a delineation between what AWS takes responsibility to secure, and what you as an AWS Customer are responsible for securing. Most simply, AWS takes care of security OF the cloud, and you are responsible for security IN the cloud.

For the AWS side, they take responsibility for securing the building blocks used to compose your systems. These include the Compute (EC2 hosts), Storage (S3 infrastructure), Databases (RDS Hosts), Networking infrastructure, and so on. That’s not to say that you can just throw all of your customers’ credit card data into an S3 bucket and think your security responsibility is according the rules. You have to lock that bucket!

## **Security Threats in the Cloud**

There are 3 major types of security incidents in AWS: nfrastructure Impact, Host Compromise, and Account Compromise.

Infrastructure Impact includes external attacks on the underlying infrastructure of your application. This type of attack largely consists of Distributed Denial of Service (DDoS) attacks, where an attacker sends a large volume of traffic at your site. AWS Shield is a service you can use that kind of attacks.

Host Compromise involves techniques like command injection to gain access to your resources, such as your EC2 instances. These days mostly to use tem for BitCoin Mining or gaining access to its data or approach other instances that likely have valuable data. Host-based intrusion detection and intrusion prevention are the most common methods of alleviating this type of threat. 

Account Compromise involves an attacker gaining access to users or roles on an instance, and then using them for the data it has access to, or the resources it can create.
There are not many solutions that fill this gap. Activity Aware IDS for AWS does. 
When an attacker is attempting toscout the permissions of a compromised identity user/role), they will probably be denied access to a number of the actions and resources they attempt to use while probing. Activity Aware IDS notifies you of these denials where your team will notice them most, like ffor example Slack.

## **Use Cases**

Activity Aware IDS uses CloudTrial and the least privilege principle.

Lets imagine a user named Mr. X had his credentials compromised by a attacker Mr. Z.
Mr. Z wants to see what Groups and Roles they have access to through Mr. X's account. FMr. Z doesn’t have access to view the Groups he is associated with, or  doesn’t have access to view the policies attached to those groups. If Mr. Z attempts to view the policies of those groups, the system will raise a access denied which, logically as it's an account action, gets logged to CloudTrail. 

At this point Activity Aware IDS receives the denial log, converts it into a friendly format, and then sends it to your Slack Channel. Once the message arrives, you will see that there are strange “Access Denied” messages associated with Mr. X.. A good administrator will call the culprit causing that message and finds he is not performing the actions. Time to replace his credentials.

In the above Mr. Z was blocked from performing actions due to the least privilege principle. Although this is a common recommendation regarding security, it can be difficult in finding the exact set of permissions that a User or Role should have. Activity Aware IDS can also assist with this.

You are deploying a new service, and you want to give it permissions following the least privilege. The easiest place to start is to create a role with no permissions. Let's assume the system needs to send logs to CloudWatch Logs (this is a requirement for AWS Lambda). When the system attempts to create a new Log Group, it will get denied, because the role has no permissions. This denial will get logged to CloudTrail. Activity Aware IDS for AWS will send the denial to your Slack, where you can see the action being attempted, the Role attempting to perform the action, and the arn of the specific resource it’s trying to perform the action on. 

At this point, you can add a statement to the policy for the role allowing it access to “CreateLogGroup” and even provide a fairly restrictive resource description.

## **What to do next**

Feel like getting your hands dirty? Checkout the [Giftbit Guide](https://github.com/Giftbit/activity-aware-ids-aws#getting-started).
