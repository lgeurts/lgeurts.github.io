---

layout: post
title: Serverless computing for CIOs & CFOs
read_time: true
comments: true
category: Cloud Computing
tags: [ Cloud Computing ]

---
 
Back in the days, a company had to buy expensive physical servers, set those up somewhere in rooms that were outfitted with peripheral subsystems for cooling, ventilation, fire suppression, etc., and then configure each server in order to run their applications. They also had to hire engineers to maintain these bare-metal servers and troubleshoot any issues that could occur along the way.
 
This entire process of deploying servers -(or any other devices), could take days to complete, and requires properly estimating and allocating capacity since you can't dynamically add or remove CPUs, RAM, disks, etc. The server-based model is basically quite inconvenient, labor-intensive, and entails exorbitant costs.
 
The serverless solution does not mean it is literally running out of thin air with absolutely no physical server at all. You still need CPU, RAM, network interface card, and other physical server devices to process data. Serverless simply means that a particular service requires less server management, meaning an CSP (like for example AWS) handles all of the manual server management tasks for you. This allows organizations to focus solely on their core business logic instead of just wasting time doing time-consuming server deployments and maintenance tasks that don’t add much value to the business.

Cloud Computing ushered a new era of on-demand virtual machines (VMs) that you can use to launch online solutions in a matter of minutes instead of days or weeks. Ae bare-metal server runs the host OS and the virtualization layer which produces tens or hundreds of virtual machines. This pool of virtual machines is sharing the CPU cores, RAM, network bandwidth, and local storage of the server. So if a machine running in your local infrastructure has XX CPU cores, then you can roughly launch XX virtual machines with 1 CPU core.

Since a VM has its own OS, it also has its own kernel which provides for a secure boundary over other VMs running in our host computer. It takes time to launch all of these instances due to the different components that the hypervisor must virtualize and allocate. Moreover, you will have to pay the costs of running your VMs, including idling time when a resource isn’t used at all. And let's not forget that virtual machines are running a guest operating system that needs updates.
 
There is also a smaller virtualized entity called containers (Docker). A container shares the physical server’s OS system kernel but does not launch its own guest OS, unlike a VM. It virtualizes application libraries and dependencies instead of the whole Operating System. Therefore, a container doesn’t have its own kernel unlike a VM, so it is not fully isolated to other containers running in the host. A container is primarily used for running applications and that's why it's faster to launch compared with an Amazon EC2 instance (VM).

Although a container provides a significantly reduced startup time over a VM, it still has operating costs that you have to cover. The burden of paying active and idle time remains, even if no one is using your containerized application at all.

This is where serverless kicks in. Serverless is in essence a combo of a VM and a container. It is powered by a microVM with its own kernel, and like containers it deploys faster than a virtual machine while at the same time it can be used to run your applications.

In contrast with VMs and containers, serverless services don't run continuously at all. A serverless solution will only run once invoked and then release its computing capacity. This is the reason why a serverless architecture is the most cost-effective since you won’t have to pay for its idle time.
