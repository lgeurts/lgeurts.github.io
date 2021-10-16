---
layout: post
title: Cloud Gaming on AWS (using Parsec)
read_time: true
comments: true
category: Gaming
tags: [ Cloud Computing ]
---

TLDR: Instructions for building a high performance Windows 10 Cloud Gaming environment using the Azure Cloud and Parsec @ 0,9€ per gaming hour.
Let´s start:

In this guide I will explain how to build your own Cloud Gaming environment using Microsoft Azure and Parsec. The principle is similar to Netflix or other streaming services. Your games are streamed from the host (in this case our Azure machine) to your device.

The video and audio output is sent directly to your device, but the actual work is done by the cloud instance. Because you can use pretty powerful machines in Azure, you can build yourself a real hell machine for little money. Pretty cool, right?
Why should I make use of Cloud Gaming?

It’s simple: you only have to take care of the hardware maintenance to a limited extent. With cloud gaming, you can stream games to a Notebook or even a phone, making high-fidelity gaming experience cheap and mobile.
How does Cloud Gaming work?

To stream a game between your machine in the cloud and your client (local device), the following things are required:

- A codec for compressing video/audio on the server side and decompressing on the client-side.

- A channel for the server to receive player input from the client.

- A high-performance Internet connection, at least 20–30 Mbps .

The most difficult part is the stream latency. All steps — such as running the game, encoding and decoding the game video and converting the player input are done in real time.

The Turing test for cloud gaming is that it should be indistinguishable from a game played on a powerful console or PC.

Thanks to advances in video codecs, cloud computing and the Internet, cloud gaming has evolved from a cool idea to a convenient alternative to playing on local devices. Today you can play the latest games titles in the cloud at 1080P and sometimes even 4K with extremely high frame rates and low input and display latency.
What can we do with Azure?

GPU optimized VMs are specialized virtual machines available with single or multiple NVIDIA GPUs. GPU optimized machines are optimized and designed for remote visualization, streaming, gaming, encoding, and VDI scenarios using frameworks such as OpenGL and DirectX. These VMs are backed by the NVIDIA Tesla M60 GPU which is perfect for gaming. We will use the machine type NV6 with a Windows 10 Image instead of a Server.
Azure Datacenters are all around the world
1) Let´s create your Azure VM

The prerequisite for all this is, of course, that you have a basic understanding of what Azure is and how it works. I will not go into how you create an account there. But you can register and have 12 months to test it.

When creating the VM you have to be careful about a few points. These are the following:

    Give your VM a name (which can be any name you like).
    Then choose a good region. If you want to make it perfect, choose a region that is near the data center of the actual game server, so that you are closest to it.
    As image choose “Windows 10 Pro, Version 1809” — so we don’t get a classic server but a Windows 10 instance which is of course better than a server.
    Before you continue, set the hard disk type to “HDD”. (on the nearest side). Then the size of the VM can be set to NV6 (on the first page of the setup. Now enter a login, with which you can register on the VM.

For the rest you can play around and test a little bit first. It’s best for everyone to do their own fine tuning at this point. I would suggest to enable auto-shutdown — it will save you a ton of money if you forget to shutdown your VM after a session. In the summary we see the costs for the VM. These are, if it runs the whole month of course extremely high, but if you only play 1–2 hours a week very manageable.

    Cost per month for the VM: 0.9217 EUR/hr

2) Let´s configure your VM/GPU

Now, after we have created the basic VM, it’s up to the actual configuration of the whole thing. First of all, dial up to the machine via RDP. When this is done, do the following:

    Install all Windows updates (if required; restart may be required)
    Install latest NVIDIA driver for your Tesla GPU: Download link
    Install TeamViewer and Parsec (on both the VM and your local PC)

Then go to the VM via TeamViewer and close the RDP session. From there we now have to reconfigure the graphics card (source):

    Connecting to the VM with TeamViewer, open a prompt as admin (Start Menu -> search for “cmd” -> right click on command prompt and select Run as Administrator).
    Go to the C:\Program Files\NVIDIA Corporation\NVSMI folder, and run nvidia-smi. This will get you a table that gives you both what mode your Tesla is set to (which will be TCC by default, check under the heading TCC/WDDM), and the GPU_ID, which is the thing under the Bus-Id heading.
    Run nvidia-smi -g {GPU_ID} -dm {0|1} with your Bus-Id and 0 to set it to WDDM, like so (the GPU_ID may differ):

    nvidia-smi -g X019:00:00.5 -dm 0

    You might need to restart at this point, but when it’s set and you reconnect, the resolution will go super high, and everything will be tiny. But if you go to the device manager, your second monitor connected to the Tesla GPU is there! Now disable the original display driver in the device manager so that the Tesla GPU is the only one enabled, and voila! We are good to go.

2) Let´s setup Parsec

Access the VM with TeamViewer. RDP will not work because it has no active monitor. So just download TeamViewer, setup Parsec and then close the TeamViewer session.

    Create a free Parsec account here
    Setup Parsec (with TeamViewer, RDP will not work) so it starts with Windows
    Disable V-Sync on both your local machine and your VM
    Connect from your local machine to the Host via Parsec

3) Install whatever you want

Everything is done at this point. You could now install Steam for example and then download your games. Because the VM is in the MS datacenter it has a perfect internet connection with a 3Gbit download and 2Gbit upload performance.

    Cloud
    Azure
    Gaming
    Microsoft
