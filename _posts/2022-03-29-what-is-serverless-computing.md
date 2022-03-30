---

layout: post
title: Serverless computing for CIOs & CFOs
read_time: true
comments: true
category: Cloud Computing
tags: [ Cloud Computing ]

---
 
Back in the days, a company had to buy expensive physical servers, set those up somewhere in rooms that were outfitted with peripheral subsystems for cooling, ventilation, fire suppression, etc., and then configure each server in order to run their applications. They also had to hire engineers to maintain these bare-metal servers and troubleshoot any issues that could occur along the way.
 
This entire process of deploying servers, or any other devices, could take days to complete, and required properly allocating capacity since you can't dynamically add and remove CPUs, RAM, disks, etc. For those living on the bleeding edge the server-based model often proved to be quite inconvenient, very labor-intensive, and entailing high costs (CAPEX vs OPEX).
 
Starting 2017, cloud computing ushered the era of [on-demand virtual machines](https://aws.amazon.com/ec2/) that you can use to launch online solutions in a matter of minutes instead days or weeks. A bare-metal server runs the host OS and a virtualization layer which produces tens or hundreds of virtual machines. This pool of virtual machines is sharing the CPU cores, RAM, network bandwidth, and disks that are attached to the host computer. 

Since a VM has its own OS, it also has its own kernel which provides for a secure boundary over other VMs running in our host computer. It takes time to launch all of these instances due to the different components that the hypervisor must virtualize and allocate. Moreover, you will have to pay the costs of running your VMs, including idling time when a resource isn’t used at all. And let's not forget that virtual machines are running a guest operating system that needs updates.
 
Next step was a smaller virtualized entity called container ([Docker](https://aws.amazon.com/docker/), [Kubernetes pods](https://aws.amazon.com/kubernetes/)). Containers share the physical server’s OS system kernel but do not run a guest OS with its own kernel, unlike a VM. They are primarily used to virtualize and run application libraries and dependencies.

Although a container provides a significantly reduced startup time over a VM, it still has operating costs that you have to cover. The burden of paying active and idle time remains, even if no one is using your containerized application at all.

This is where [serverless](https://aws.amazon.com/serverless/) kicks in. Serverless is in essence a combo of a VM and a container, but in contrast to containerization, serverless uses a small optimized kernel virtualized on top of a kernel-based virtual machine (MicroVM).

Serverless let's you run code, manage data, and integrate business applications without managing any servers because the CSP will handle these tasks for you. 

Speaking about cost efficiency, in contrast with VMs and containers, serverless services don't run continuously. A serverless setup will only run when it's invoked and will afterwards release all computing capacity. This is the reason why a serverless architecture is the most cost-effective way since you won’t have to pay for idle time.
