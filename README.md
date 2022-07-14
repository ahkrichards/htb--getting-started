# HackTheBox - Getting Started Guide

## Environment

### GUI (Recommended)

The easiest path forward is to leverage VirtualBox and run a virtualized Kali on it. You can download premade VMs or baremetal ISOs from the [Kali site](https://www.kali.org/get-kali/). I recommend setting up a baremetal install on VirtualBox for complete customization. 

The biggest parts of setting up a successful virtualized environment are:

* Assigned CPU Processors
* Assigned RAM
* Assigned Graphical Memory
* Host<->VM Clipboard Access
* Host Mounted Storage

### VirtualBox VM

#### Assigned CPU Processors

Ensure that you assign at least 2 processors. I have noticed that going beyond 4 processors without dedicating all processors to virtualization can lead to the "turtle" status of the VM running slowly (I have 16 logical processors on my HTB lab environment).

P.S. What is the "turle" status, you ask? It is an icon in the status tray of the VirtualBox application. It is an indicator to show that a VM is running suboptimally and a good sign that you should spend some time triaging configuration. 

#### Assigned RAM

I recommend assigning at least 4 GB RAM, however 8 GB is what I tend to use.

#### Assigned Graphical Memory

I have had a ton of issues when not assigning the maximum 128 MB the graphical memory. This is because it looks like using apps like Burp end up using lots of graphical memory.

#### Host<->VM Clipboard Access

I personally don't like researching in my VM, but rather use my host system. This means I need to transfer data between the host and VM a lot, and I do not want to have to create a file on my mounted storage. This means using copy-paste functionality or drag-n-drop file support from host<->VM. Do do this you must install the VBox Guest Addtions on your VM.

The VBox Guest Additions ISO comes with the VirtualBox install, so configure your drive device on the VM to mount the VBox Guest Additions image, then mount the disk and run the installation.

I highly recommend doing this as a first step in your VM setup and creating a snaphost "Vanilla" iamge.

#### Host Mounted Storage

Things happen, VMs die. Let's make our environment more ephermeral by putting our absolutely needed data on host mounted storage. That way if you ever need to rebuild or reset your VM, your data will be safely stored on your host machine instead. While snapshot storage is nice, it does take a lot of storage and requires active forethought to backup your data.

This requires that the VBox Guest Additions be installed on your VM.

## Utilities

A big part of offensive security is maintaining your tooling suite that isn't necessarily a part of base Kali installs. I personally like to install my additional scripts and programs in the `/opt` directory. Consider building a repo that you can quickly clone to pull in your additional resources as your offesnive security skils mature. See an example repo of mine here where I leverage git submodules to avoid decoupling version management from the opensource projects: https://github.com/ahkrichards/HackTheBox

## VPN

HackTheBox requires VPNs to connect to their assets usually. This means you will have to download the VPN configuration profile from your account or send you. This will need to be accessible on your VM as I do not recommend putting your host on offesnive VPN profiles or when only the VM will be accessing those resources.

Once the VPN profile is accessible to the VM, I recommend opening a terminal session, and running `sudo openvpn <path-to-the-profile>`. We have to run with elevated privileges to configure network devices. 

I like to open a new tab and rename the tab running OpenVPN to "VPN". I do this instead of sending the application to the background for ease of access and monitoring of OpenVPN logs for troubleshooting connectivity issues.