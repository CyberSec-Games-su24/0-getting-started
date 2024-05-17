# Welcome! #
These instructions are intended to walk you through setting up your environment for this summer in the way that I think 
will be the most successful by default. That being said, I understand that we can't all just flash a fresh operating system 
to our device and start from scratch. Along with that, if you have an already-established environment that you enjoy, 
please use it! The best systems are the ones you enjoy the most. While my instructions will be most rigorously tested on 
the prescribed materials, I will strive to include comments and resources for users of all systems.

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
  - [Choosing a Distribution](#choosing-a-distribution)
  - [Downloading And Verifying](#downloading-and-verifying)
  - [Mounting The OS](#mounting-the-os)
  - [Final Steps](#final-steps)
- [Setting Up a VM](#setting-up-a-vm)
  - [Downloading A Virtual Host](#downloading-a-virtual-host)
  - [Update!!](#update)
  - [Old Install Instructions (ignore unless you're VERY stubborn)](#old-install-instructions-ignore-unless-youre-very-stubborn)
    - [For Linux Users](#for-linux-users)
    - [For Windows Users](#for-windows-users)
  - [Installing A Machine](#installing-a-machine)
    - [General-Use OS as a VM](#general-use-os-as-a-vm)
    - [Kali Linux as a VM](#kali-linux-as-a-vm)
- [Checking Install Dependencies](#checking-install-dependencies)
  - [git](#git)
    - [Git On Linux](#git-on-linux)
    - [Git On Windows](#git-on-windows)
  - [ssh](#ssh)
    - [On Linux](#on-linux)
    - [On Windows](#on-windows)
  - [OpenSSL](#openssl)
  - [John The Ripper](#john-the-ripper)
    - [Flush The System](#flush-the-system)
    - [Install Dependencies](#install-dependencies)
    - [Clone and Make John The Ripper](#clone-and-make-john-the-ripper)
    - [Alias Custom Commands](#alias-custom-commands)
    - [Test It Out](#test-it-out)

---
---

# Installing Linux (optional) #
While this isn't necessary, if you intend on having a machine specifically for programming 
and/or cyber-security related activities, it is highly recommended you mount a Linux-based 
Operating system. Linux is often the intended operating system for the tools we're going to 
be using, and the terminal-centric emphasis will more quickly reinforce practices that will 
be necessary. All of the documentation I provide will include references for Windows systems, 
but since I will not always be able to test them, you'll need to reference the online resources 
when applying a new concept.

## Choosing a Distribution ##
There are an endless number of Linux operating systems that can accomplish a number of things. 
For the projects presented over the course of this summer, any general-use Linux distribution like Mint, Ubuntu, or MX will 
accomplish what you need.

If you're a masochist or an adventurer, you're welcome to choose an operating system that will 
provide an extra challenge. Kali Linux, which we will host virtually, can be mounted as an integrated 
operating system as well. (It is definitely not intended for this, and you will find some weird issues, 
but it can be done). On the other hand, there are also some Linux distros that are extremely lightweight, 
allowing for the maximization of available resources within a computer.

No matter what you choose, learn what you like and don't like about it. These systems are often heavily modifiable, 
so if you don't like something, try to change it. Worst case scenario, you have to re-mount a fresh system.

## Downloading And Verifying ##
If you've never downloaded a fresh Linux OS before, make sure that you find one with clear installation 
instructions and a section about verifying your install. We intend to rewrite the central interface 
to the system, so the more information available the better. Usually installation will be as straightforward as 
clicking on a file, but with a procedure as invasive as this we also need to verify the authenticity of our file.

To verify an installation, follow the instructions in the installation guide. Its goal is to check the hash value of 
the file (we will do more of this later!) and compare it to an expected value to make sure they are the same. IF THEY 
ARE NOT IDENTICAL, DO NOT CONTINUE UNTIL YOU HAVE A DOWNLOAD THAT CAN BE VERIFIED!

Here are the landing pages to some suggested operating systems:<br>
<a href="https://www.linuxmint.com/edition.php?id=311">Linux Mint - Cinnamon</a><br>
<a href="https://ubuntu.com/download/desktop">Ubuntu</a><br>
<a href="https://mxlinux.org/download-links/">MX Linux</a><br>

## Mounting The OS ##
Just to be absolutely clear, mounting a new operating system will wipe the current filesystem partitions. 
Save any data you care about somewhere else, because it will be gone. Flashing a fresh OS is most easily done 
with two devices (one for instructions/google and the one you're flashing), so if you need to find a public library, 
borrow a family member's iPad, etc, do so now.

At this point, you should have a verified .iso file for your chosen operating system downloaded. Now you will need to 
create a mountable USB flashed with the file to write to your device. To create this drive, you will need a sufficiently sized 
thumb drive (16gb or larger is strongly recommended, but if you NEED to do it with 8gb contact me) that you don't mind losing everything on and your .iso file. 
If you've never flashed a thumb drive, I recommend using <a href="https://etcher.balena.io/#download-etcher">Balena Etcher</a> to flash. 
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
virtualized network will allow us to run network-based expiriments without the risk of affecting a real network.

## Downloading A Virtual Host ##

## Update!! ##
Since I wrote this documentation, VMWare has gortten bought out by a commercial distributor. It is still accessible, so I'll leave the original instructions below, but it is a huge pain to get to. Instead, <a href="https://www.virtualbox.org/wiki/Downloads">Oracle's VirtualBox</a> is available for free. I haven't had a chance to rigorously confirm that this service won't cause hiccups later, but it'll suffice for now.

## Old Install Instructions (ignore unless you're VERY stubborn) ##

I recommend <a href="https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1751&productId=1377&rPId=117008">VMware Workstation Player</a> 
for working with virtual networks. If you have a preferred VM service, go ahead and use it, but you're on you're own cowboy.

- [For Linux Users](#for-linux-users)
- [For Windows Users](#for-windows-users)

### For Linux Users ###
On Linux, you will need to download the first listed option. This will install a .bundle file to your device, now open your terminal. 
We have an archive downloaded, but we need to unpack it and build the app. Luckily, this is only a two-step. 

---

We need to give executable permissions to the read-only archive. In Linux, this command is
```
chmod a+x ./path/to/bundle
```
where "./path/to/bundle" is the relative path to your VMware download.

*Command Breakdown* <br>
chmod is instrumantal for controlling file permissions in Linux, so let's break down what's actually happening here.

**a** <br>
The first character in our seemingly random string, following the chmod command, designates which groups we are updating permissions for. 
In Linux, there are four groups: u (the single user), g (the users in the file's group), o (others), and a (all users). In this case, we are just updating the 
permissions this file has for all the users because this system isn't complex enough for it to particularly matter

**+** <br>
With chmod, we can grant and remove permissions at any given point, so which one we are doing is represented by a + (granting) or a - (removing).

**x** <br>
Now that we've defined who we're talking about and what action we're taking, we need to define which permissions are being affected. Because we want to 
create an executable, we are using x, but there are many more including w (write) and r (read). Some of these permissions have lengthy definitions, so I recommend 
<a href="https://www.computerhope.com/unix/uchmod.htm">reading this</a> for a more in-depth look.

**In Other Words...** <br>
Now that we've defined each portion of this command, we can write this command in English with the sentence:
```
Using chmod, we are going to be granting execute permissions for all users to the file at this location.
```
---

Now that we have an executable file, we simply need to execute it from the terminal by passing the path (relative or absolute) into the command line as follows:
```
sudo ./path/to/bundle
or
sudo /absolute/path/to/bundle
```
And that's it! With the file having executable permissions, the terminal knows when it reads the path that you're trying to execute it. 
This app can be found wherever your chosen operating system shows its installed apps. From there, you can pin it to taskbars and/or add desktop icons 
as you wish.

---

### For Windows Users ###
On Windows, you simply need to download the executable listed second on the above download page. From there, click on it and follow the 
setup wizard.

## Installing A Machine ##
To create a virtual machine in your chosen virtual host, you simply need to download the system file to your local files 
and upload it through your newly-installed software. We will want to have a variety of virtual machines established so that we can simulate 
network environments later on. Please have at least one general-use operating system machine and one Kali machine ready to go.

### General-Use OS as a VM ###

For Linux-based virtual machines, you can use any of the downloads listed in 
[Downloading And Verifying](#downloading-and-verifying). For Windows machines, refer to these sources for 
<a href="https://www.microsoft.com/en-us/software-download/windows10ISO">Windows 10</a> and 
<a href="https://www.microsoft.com/software-download/windows11">Windows 11</a> .iso file downloads.

Alternatively, there are .ova files available that will download a full environment that extends beyond that of a base operating system 
(extra apps/dependencies, custom scripts, etc). The use of these will not be covered in the content of this exploration, but they are an 
interesting thing to explore if you feel compelled.

### Kali Linux as a VM ###
Along with the non-Kali virtual machine(s), you will need an attacker machine. This operating system is tailored to fill this role, so 
we're going to take advantage of the tools it provides. 

**Install the .iso image** <br>
To install the necessary .iso file, click the box labeled "Installer" <a href="https://www.kali.org/get-kali/#kali-installer-images">here</a>. Once 
the ~4 GB download is done, you need to verify the download by comparing the file's hash sum with that listed on the download page (view this by 
clicking the corner of the "Installer" box that says "sum").

To check the sum of the file in a Windows system, open up command prompt by searching "cmd" and navigate to wherever the downloaded .iso 
is located. From there, run the following command:

On Windows:<br>
```
certutil -hashfile C:\path\to\file.iso SHA256
```

On Linux:<br>
```
sha256sum ./path/to/file.iso
```
This command will return a string of letters and numbers. Compare that with what is found on Kali's website to verify that they are identical.

**Loading the .iso into VM software**<br>
If you're using VMware Workstation Player, there will be an option in the home menu labeled "create a New Virtial Machine". 
From there, select the "Use ISO Image" option and select the Kali .iso file. Upon clicking next, you'll be brought to a screen to select the Guest 
Operating System. Click "2. Linux", and then select the most recent version of Debian 64-bit (as of now, it is Debian 12.x 64-bit). Click next again, 
and name the machine however you'd like. Select your virtual drive size on the next page. 20 GB should be enough, but I tend to allocate 25 just in case. 
Click next once more, finish, and then close. The machine will build and then power up.

If you're on Linux, it is likely that you are seeing an error pop up saying, "Could not open /dev/vmmon: ...". This is because our kernel modules have not been signed by default. 
To do so, we will need to run a series of commands before rebooting the device. 

**Generate a new key pair to sign with:**<br>
```
openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -nodes -days 36500 -subj "/CN=VMware/"
```

Replace MOK in this command with what you would like the key's files to be named.

**Sign the modules with the newly-generated key**<br>
Because of the discrepencies between different Linux ecosystems, we first need to probe and see where your kernel modules are stored. 
To do so, run the command 
```
ls /usr/src/kernels
```

If you don't get an error, meaning the system lists a bunch of files, run the commands below. 
```
sudo /usr/src/kernels/$(uname -r)/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vmmon)
sudo /usr/src/kernels/$(uname -r)/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vmnet)
```

If you _do_ get an error stating the file or directory was not found, run these commands instead:
```
sudo /usr/src/linux-headers-`uname -r`/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vmmon)
sudo /usr/src/linux-headers-`uname -r`/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vmnet)
```

Finally, execute the command 
```
sudo mokutil --import MOK.der
```
and confirm it with a password.

Now, reboot your machine. There should be a pop-up on restart  with an option to Enroll MOK. Select that, select continue until you are 
prompted to enter a password, enter the password you entered for the previous command, and then continue until you're prompted to reboot. 
There are quite a few other options during this process, but we won't need any of them beyond the "Enroll MOK" button.

**Fire it up!**<br>
Upon reboot, try to open the virtual machine again. It should fire right up. If not, contact me directly.

---
---

# Checking Install Dependencies #
These labs are aimed at developing a tool kit of security skills, 
so there are some dependencies we will use throughout that need checked/installed.

## git ##
To check whether or not git is installed on the system you will be using, run the command below.
```
git
```
If this command doesn't return an error, the dependency is installed. Otherwise, continue below.

### Git On Linux ###
To install git on a Linux machine, run the command:
```
sudo apt install git
```
and enter your password if requested.

### Git On Windows ###
\<TODO> Git on Windows

## ssh ##
Similar to checking if git is installed, run the command
```
ssh
```
If this command returns an error, run the install command below:

### On Linux ###
```
apt install ssh
```

### On Windows ###
\<TODO> Ssh on Windows


## OpenSSL ##
You might start to notice a pattern... Check to see if openssl exists with the command:
```
openssl
```

if its not installed, run the following command to install it.
```
sudo apt install openssl
```

## John The Ripper ##
Check John The Ripper similar to previous dependencies with this command:
```
john
```
NOTE: the terminal may gove you the suggestion to `sudo apt install john`. Do not do this.

If it is installed, check that zip2john (an important subsidiary of john) is also installed using:
```
zip2john
```

If either of these commands are not recognized, continue below.

### Flush The System ###
If `john` was recognized as a command but zip2john was not, we need to flush john's current aliasing out to replace with our own. 
To do so, run the following two commands:
```
sudo apt remove john
sudo apt-get remove john
```

### Install Dependencies ###
```
sudo apt install libc6-dev
sudo apt install libssl-dev
```

### Clone and Make John The Ripper ###

With a john-free system, we will need to manually get the package from its git repo and compile it. 

```
cd /
sudo git clone https://github.com/openwall/john
cd john/src
sudo ./configure
sudo make -s clean && sudo make -sj4
```

The above code block will navigate to the root directory, clone the repo, and install it into your system.

### Alias Custom Commands ###

Now that we have this repo built, john and zip2john are both functioning. The commands, though, are currently bound to executable 
files, which leads to clunky commands. To alleviate this, we can alias a command to a file within our system's path variables. To do so, 
we will have to declare a few custom commands. The commands: 
```
alias john='/john/run/john'
alias zip2john='/john/run/zip2john'
```
will create the custom commands we want, but simply running these in our terminal means they will only work as long as that terminal 
is opened. To remedy this, we will need to add these aliases to our terminal's config file (if you're in Linux and you don't know which 
terminal you're using, it's probably bash). To edit this file in bash, for example, we simply need to run the command:
```
nano .bashrc
```

Now that we have opened this file in our terminal shell and can edit it, navigate to the very bottom of the file and add the 
two alias commands, each on their own lines. This will configure this alias every time you open up a new instance.

To close the file, enter Command (denoted as ^) + x and then hit y and enter.

---

### Test It Out ###

That should be it! Now that you have the commands aliased, close and reopen your terminal and type **john** and **zip2john**. These 
should both return some basic introductions on the functionality of these packages.

---
---
