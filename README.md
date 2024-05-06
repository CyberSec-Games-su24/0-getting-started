# Welcome! #
Welcome! Over the course of this experience, you will be introduced to key concepts about 
information security and network security in a live environment. This will leave you 

---
---

# Getting Started #
Before we can begin down this rabbit hole, we first need a testing environment. While cyber-security 
is relevant to every digital system, this process will go best if we can establish some toolboxes to 
work with.

---
---

# Table of Contents #
- [Welcome!](#welcome)
- [Getting Started](#getting-started)
- [Table of Contents](#table-of-contents)
- [Installing Linux (optional)](#installing-linux-optional)
  - [Choosing a Distro](#choosing-a-distro)
  - [Downloading And Verifying](#downloading-and-verifying)
  - [Mounting The OS](#mounting-the-os)
  - [Final Steps](#final-steps)
- [Setting Up a VM](#setting-up-a-vm)
  - [Downloading A Virtual Host](#downloading-a-virtual-host)
    - [For Linux Users](#for-linux-users)
    - [For Windows Users](#for-windows-users)
  - [Installing A Machine](#installing-a-machine)
- [Checking Install Dependencies](#checking-install-dependencies)
  - [git](#git)
    - [Git On Linux](#git-on-linux)
    - [Git On Windows](#git-on-windows)
  - [ssh](#ssh)
  - [OpenSSL](#openssl)
  - [John The Ripper](#john-the-ripper)
- [Hello, World!](#hello-world)
  - [In Python](#in-python)
  - [In A Different Language](#in-a-different-language)

---
---

# Installing Linux (optional) #
While this isn't necessary, if you intend on having a machine specifically for programming 
and/or cyber-security related activities, it is highly recommended you mount a Linux-based 
Operating system. Linux is often the intended operating system for the tools we're going to 
be using, and the terminal-centric emphasis will more quickly reinforce practices that will 
be necessary. All of the documentation I provide will include references for Windows systems, 
but I will not always be able to test them so you'll need to reference the online resources 
when applying a new concept.

## Choosing a Distro ##
There are an endless number of Linux operating systems that can accomplish any number of things. 
For the purposes of this, any general-use Linux distribution like Mint, Ubuntu, or MX will 
accomplish what you need.

If you're a masochist or an adventurer, you're welcome to choose an operating system that will 
provide an extra challenge. Kali Linux, which we will host virtually, can be mounted as an integrated 
operating system as well. It is definitely not intended for this, and you will find some weird issues, 
but it can be done (I have used Kali as my main OS since high school, and I definitely don't recomment it). 
Along with that, some operating systems have no GUI, so if you want to force yourself to become one with the 
terminal, something like Alpine could be the choice for you.

No matter what you choose, learn what you like and don't like about it. These systems are often heavily modifiable, 
so if you don't like something, try to change it. Worst case scenario you have to re-mount a fresh system.

## Downloading And Verifying ##
If you've never downloaded a fresh Linux OS before, make sure that you find one with clear installation 
instructions and a section about verifying your install. We are intending on rewriting the central interface 
to the system, so the more information available the better. Usually installation will be as straightforward as 
clicking on a file. Verification, in tandem, needs to be taken to confirm that the file you install is authentic.

To verify an installation, follow the instructions in the installation guide. Its goal is to check the hash value of 
the file (we will do more of this later!) and compare it to an expected value to make sure they are the same. IF THEY 
ARE NOT IDENTICAL, DO NOT CONTINUE UNTIL YOU HAVE A DOWNLOAD THAT CAN BE VERIFIED!

Here are the landing pages to some suggested operating systems:<br>
<a href="https://www.linuxmint.com/edition.php?id=311">Linux Mint - Cinnamon</a><br>
<a href="https://ubuntu.com/download/desktop">Ubuntu</a><br>
<a href="https://mxlinux.org/download-links/">MX Linux</a><br>


## Mounting The OS ##
Just to be absolutely clear, this will wipe the current filesystem partitions. Save any data you care about somewhere else, 
because it will be gone. Flashing a fresh OS is most easily done with two devices (one for instructions/google and the one you're flashing), 
so if you need to find a public library, borrow a family member's iPad, etc, do so now.

At this point, you should have a verified .iso file for your chosen operating system downloaded. Now you will need to 
create a mountable USB flashed with this .iso to write to your device. To create this drive, you will need a sufficiently sized 
thumb drive (8gb should be ok, but >16gb will absoultely be fine) that you don't mind losing everything on and your .iso file. 
If you've never flashed a thumb drive, I recommend using <a href="https://etcher.balena.io/#download-etcher">Balena Etcher</a> to flaash. 
It's relatively easy to do, so just follow the instructions and you'll be ok.

Now that you have a bootable USB drive, you're ready to flash the computer. To do so, first look up "enter BIOS \<your computer model>" and 
have that process ready to go. From there, shut your computer completely down. Upon rebooting, do the following:
1. Enter your BIOS menu (this is manufactrurer specific)
2. Navigate to the boot procedure, probably under BOOT
3. Move the USB to the top of the list
4. Save and Exit
5. If needed, click a button upon boot to boot from USB

Your computer should start up with the new operating system!

## Final Steps ##
You are now in a new Linux operating system, but it's not officially mounted to your filesystem. Take some time to familiarize yourself with 
the landscape; if you don't like it, nothing is permanent yet. You can just start over by turning off the computer, unplugging the USB, and rebooting. 
If you are happy with the choice you made, you're ready to permanently mount it. This should be as easy as clicking a desktop icon 
titled something like "mount system".

Play around with it for a bit, the world is your oyster!

---
---

# Setting Up a VM #
Handling static information will be fine in a mounted operating system, but some of the attacks we're going to run are not ethical to 
do in a public environment. To isolate these systems, we can install virtual machines (VMs) to be hosted within the computer. 
This will turn our physical device into a network host, with the VMs emulating an ethernet connection to this false network. This 
virtualized network will allow us to run network-based expiriments without risking penetrating a real network.

## Downloading A Virtual Host ##
I recommend <a href="https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1751&productId=1377&rPId=117008">VMWare Workstation Player</a> 
for working with virtual networks. If you have a preferred VM service, go ahead and use it, but you're on you're own cowboy.

- [For Linux Users](#for-linux-users)
- [For Windows Users](#for-windows-users)

### For Linux Users ###
On Linux, you will need to download the first listed option. This will install a .bundle file to your device, now open your terminal. 
We have an archive downloaded, but we need to unpack it and build the app. Luckily, this is only a two-step process in this circumstance. 

---

Firstly, we need to give executable permissions to the read-only archive. In linux, this command is
```
chmod a+x ./path/to/bundle
```
where "./path/to/bundle" is the relative path to your VMWare download.

*Command Breakdown* <br>
chmod is instrumantal for controlling file permissions in Linux, so let's break down what's actually happening here.

**a** <br>
The first character in our seemingly random string following the chmod command designates which groups we are updating permissions for. 
In Linux, there are four groups u (the single user), g (the users in the file's group), o (others), and a (all users). In this case, we are just updating the 
permissions this file has for all the users because this system isn't complex enough for it to particularly matter _in this case!_

**+** <br>
With chmod, we can grant and remove permissions at any given point, so which one we are doing is represented by a + (granting) or a - (removing).

**x** <br>
Now that we've defined who we're talking about and what action we're taking, we need to define which permissions are being affected. Because we want to 
create an executable we are using x, but there are many more including w (write) and r (read). Some of these permissions have lengthy definitions, so I recommend 
<a href="https://www.computerhope.com/unix/uchmod.htm">reading this</a> for a more in-depth look.

**In Other Words...** <br>
Now that we've defined each portion of this command, we can write this command in English with the sentence
```
Using chmod, we are going to be granting execute permissions for all users to the file at this location.
```
---

Now that we have an executable file, we simply need to execute it from the terminal by passing the path (relative or absolute) into the command line as follows 
```
./path/to/bundle
or
/absolute/path/to/bundle
```
And that's it! With the file having executable permissions, the terminal knows when it reads the path that you're trying to execute it.

---

\<TODO> Signing kernels and MOK Enrollment


### For Windows Users ###
On windows, you simply need to download the executable listed second on the above download page. From there, click on it and follow the 
setup wizard.

## Installing A Machine ##
To create a virtual machine in your chosen virtual host, you simply need to download the system file to your local files 
and upload it through your newly-installed software. For Linux-based virtual machines, you can use any of the downloads listed in 
[Downloading And Verifying](#downloading-and-verifying). For Windows machines, refer to these sources for 
<a href="https://www.microsoft.com/en-us/software-download/windows10ISO">Windows 10</a> and 
<a href="https://www.microsoft.com/software-download/windows11">Windows 11</a> .iso file downloads.

Alternatively, there are .ova files available that will download a full environment that extends beyond that of a base operating system 
(extra apps/dependencies, custom scripts, etc). The use of these will not be covered in the content of this exploration, but they are an 
interesting thing to explore if you feel compelled.

---
---

# Checking Install Dependencies #
These labs are aimed at developing a tool kit of security skills, 
so there are some dependencies we will use throughout that need checked/installed.

## git ##
To check whether or not git is installed on the system you will be using, run the command below.
```
git -v
```
If this returns something like "git version x.xx.x", the dependency is installed. If this command returns an error, 
continue below.

### Git On Linux ###
To install git on a Linux machine, run the command 
```
sudo apt install git
```
and enter your password if requested.

### Git On Windows ###

## ssh ##

## OpenSSL ##

## John The Ripper ##

---
---

# Hello, World! #
Hello

## In Python ##

## In A Different Language ##