---
author: "Alon Shrestha"
title: "How to Restore Ubuntu with Systemback"
pageheading: "How to Install Systemback and Restore Ubuntu Linux"
date: 2019-07-21
description: "Guide to install systemback on Ubuntu and restore it creating backup image without losing data."
topics: [Linux, Backup & Restore]
tags: [Ubuntu]
draft: false
# cover:
#   image: /images/posts/install-systemback-restore-previous-state-ubuntu-linux/10.webp
#   alt: "Hello"
#   caption: "Image from my previous website, sTechalon.com"
ShowToc: true
TocOpen: false
---
Upgrading an open-source operating system like Linux can be intimidating, as it often involves the risk of data loss. 	

But worry not, I was able to utilized Systemback to create a backup image of my Ubuntu and restore it.

This page will guide you through the process of installing Systemback and restoring your Ubuntu system. 

## Advantages of Using Systemback
- Backup and restore system with users configuration files.
- System copying, system installation and Live system creation.
- Convert backup image into bootable ISO file.
- Upgrading system and software.
- Easy installation and fast recovery.

## Install Systemback on Ubuntu 16.04
To install Systemback on Ubuntu 16.04 or older, simply run the following commands in your terminal:
```shell
sudo add-apt-repository ppa:nemh/systemback

sudo apt-get update

sudo apt-get install systemback
```

*There haven't been any updates to Systemback since 2016, so these commands only work for Ubuntu 16.04 and earlier versions.* 

While Systemback might function on later Ubuntu versions using the 16.04 PPA, this method is not officially supported and could lead to compatibility issues.

## Install Systemback on Ubuntu 18.04 - 20.04
First remove the PPA.
```shell
sudo add-apt-repository --remove ppa:nemh/systemback
```

Now, run the following command to import the PGP signing key of this PPA. This verifies the signature from the package manager. You can get the signing key from {{< newtabref  href="https://launchpad.net/~nemh/+archive/ubuntu/systemback" title="here" rel="nofollow">}}.

```shell 
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 382003C2C8B7B4AB813E915B14E4942973C62A1B 
```

You might get some error regarding *“gpg: keyserver”*

You can fix such errors using different keyservers. Instead of using **keyserver.ubuntu.com**, use **pgp.mit.edu**.

```shell
sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 382003C2C8B7B4AB813E915B14E4942973C62A1B
```

Add the PPA running below command.

```shell
sudo add-apt-repository "deb http://ppa.launchpad.net/nemh/systemback/ubuntu xenial main"
```

Finally, updated the list and install systemback on Ubuntu 20.04, 19.10, 18.04
```shell
sudo apt update

sudo apt install systemback
```

## How to Use Systemback?

After installation, open the application. 

Enter your user password and press `OK`. 

![SystemBack On Ubuntu | sTechalon.com](/images/posts/install-systemback-restore-previous-state-ubuntu-linux/3.PNG)

Here, you can see many options in the function menu. Click on `>>Live system create`.

![ Restore Linux To Previous State With System Back| sTechalon.com](/images/posts/install-systemback-restore-previous-state-ubuntu-linux/4.PNG)

## Create Image of Your Current System

To use a different working directory path, you can replace the current path "/home" with the desired path. This is the location where your backup image and ISO files will be stored.

Give name to your new live system replacing the name *“auto”*.

If you want to create an image that includes your personal settings and configurations, make sure to select the option `Include user data files` while creating the backup.

After these, click on `Create new` to continue.

![Create Image with System Back | sTechalon.com](/images/posts/install-systemback-restore-previous-state-ubuntu-linux/5.PNG)

***Note**: The time to create a backup depends on the size of your system.*

Once the process is completed, your backup image will be created and saved as a .sblive file as shown below.

![Backup Image And Convert .sblive to ISO File System Back | sTechalon.com](/images/posts/install-systemback-restore-previous-state-ubuntu-linux/7.PNG)

After creating a .sblive file, Systemback provides the option to write the file directly to your USB flash drive.

## Convert .sblive File to Bootable ISO File 
Now it's time to write an image in your usb flash drive.

For that, insert your usb drive and click on the `Green Refresh` button. 

The `Write target` box should display your pendrive. In my case it’s `SanDisk Cruzer Blade`. 
 
![Backup Image And Convert .sblive to ISO File System Back | sTechalon.com](/images/posts/install-systemback-restore-previous-state-ubuntu-linux/8.PNG)

Select  the created image displayed on the `Created Live Images` box. There will be different *“Live operations”* available that you can apply to this image.

Click on `Write to target`. You will see the configuration dialog box, click on Start. This operation writes the new image to your flash drive and a  progress bar is displayed.

Click on `Convert to ISO` if you want to create a bootable iso file from the created .sblive image.

You can also delte the .sblive image and re-create the new image using `Create New` option.
 
**Note*: Your image cannot be converted into iso if the .sblive file is greater than 4 GB.*

## Conclusion

In conclusion, Systemback is a useful tool for Ubuntu/Debian users who want to create backup and restore points of their entire system. 

With Systemback, you can easily revert your Ubuntu system to a previous state without losing any data. Although there haven't been any updates to Systemback {{< newtabref  href="https://answers.launchpad.net/systemback" title="since 2016" rel="nofollow">}}, it is still compatible with later versions of Ubuntu and can be installed using the  {{< newtabref  href="https://launchpad.net/~sonicwalker" title="Ubuntu 16.04 PPA" rel="nofollow">}}. 

Overall, Systemback provides an easy and fast way to backup and restore your Ubuntu system, giving users peace of mind when upgrading or making changes to their operating system.