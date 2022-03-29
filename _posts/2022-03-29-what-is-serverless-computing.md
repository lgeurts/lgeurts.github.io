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
 
The “serverless” solution does not mean it is literally running out of thin air with absolutely no physical server at all. You still need a CPU, a RAM, a network interface card, and other physical server devices to process data. Serverless simply means that a particular service requires less server management – meaning, a cloud service provider like AWS handles all of the manual server management tasks for you. This allows you to focus on implementing your core business logic instead of just wasting your time doing time-consuming server deployment and maintenance tasks that don’t add much value to your business

Cloud Computing ushered a new era of on-demand virtual machines that you can use to launch your online solutions in a matter of minutes, instead of days or weeks. The bare-metal server runs the host operating system and the virtualization layer which produces tens or hundreds of virtual machines. This pool of virtual machines is sharing the CPU cores, RAM, network bandwidth, and local storage of a single physical server. So if a rack server running in your on-premises network has 40 CPU cores, then you can roughly launch 40 virtual machines with 1 CPU core each or so. Each of these virtual machines is running a guest operating system that you also have to patch regularly.

Since a VM has its own OS, it also has its own kernel which provides a secure boundary over the other VMs running in the host computer. There is a considerable amount of time necessary to launch these instances due to the different components that its hypervisor must virtualize and allocate. Moreover, you will have to pay the cost of running your VMs, including its idle time where your resource isn’t used at all.
 
There is also a smaller virtualized entity than virtual machines called containers. A container shares the physical server’s OS system kernel but does not launch its own guest OS, unlike a VM. It virtualizes the libraries and dependencies of your applications, instead of the whole Operating System. Therefore, a container doesn’t have its own kernel unlike a VM, so it is not fully isolated to other containers running in the physical host. It’s important to note that a container is primarily used for running applications only, which can also be moved to another host or server if necessary. This is the reason why it is faster to launch a Docker container or a Kubernetes pod compared with an Amazon EC2 instance. Again, it is smaller than a virtual machine and doesn’t run its own guest operating system. A container also works continuously so you will be billed for the total time that this container is running.

Although a container provides a significantly reduced startup time over VM, it still has an operating cost that you have to cover. The burden of paying both its active and idle time remains, even if no one is using your containerized application at all. This is especially true if you have workloads that only need to run once a month or infrequently.

This is where serverless computing comes in. Serverless is essentially a combination of a VM and a container. It is powered by a micro virtual machine, or a microVM, which has its own kernel. Just like a container, it deploys faster than a Virtual Machine and it can be used to run your applications.

In contrast with VMs and containers, a serverless service doesn’t run continuously at all. A serverless solution will only run once you invoked it and then release its computing capacity afterward. This is the reason why a serverless architecture is cost-effective since you won’t have to pay for its idle time.
