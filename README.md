# DigitalOcean Arch Linux Droplet Setup Guide

# Introduction
DigitalOcean is a cloud computing service. It offers you access to remote servers that act like physical computers. For example, a Droplet is a virtual machine that can be quickly deployed. These Droplets are accessed over the internet for hosting and managing websites and applications.

## Overview
This instruction manual is designed for term 2 CIT students, who want to set up a cloud-based server to host and manage websites or applications. The following steps will teach you how to create a Droplet using DigitalOcean's `doctl` command-line tool, configuring it with cloud-init, and connecting to it using SSH keys:
    
1. Uploading a Custom Image onto DigitalOcean
2. Creating an SSH Key Pair
3. Adding the Public Key to Your DigitalOcean Account
4. Installing and Configuring `doctl`
5. Creating a Droplet with Cloud-init
6. Connecting to the Droplet Using SSH
7. Installing Essential Software on the New Server

# Instructions

## Uploading a Custom Image onto DigitalOcean

You will need a custom image like Arch Linux to upload to DigitalOcean. This allows you to create a Droplet with your preferred pre-installed operating system and configurations.

1. Click **manage** on the left-hand side of the menu 
<img src='Pictures/Click manage on the left-hand side of the menu .jpg' alt='Picture of instruction' style='width: 50%;'>

2. Select **Backups and Snapshots** from the **Manage** menu
<img src='Pictures/Select Backups and Snapshots from the Manage menu.jpg' alt='Picture of instruction' style='width: 50%;'>

3. Select **Custom Images**
<img src='Pictures/Select Custom Images.jpg' alt='Picture of instruction' style='width: 50%;'>

4. Select **Upload Image**
<img src='Pictures/Select Upload Image.png' alt='Picture of instruction' style='width: 50%;'>

5. Select **Arch Linux Image** and click **Open**
<img src='Pictures/Select Arch Linux Image and click Open .jpg' alt='Picture of instruction' style='width: 50%;'>

6. Click on **Distribution** and from the drop-down list, select **Arch Linux**
<img src='Pictures/Click on Distribution and from the drop-down list select Arch Linux.jpg' alt='Picture of instruction' style='width: 50%;'>

7. Select your closes region and Click **Upload Image**
<img src='Pictures/Select your closes region and Click Upload Image.jpg' alt='Picture of instruction' style='width: 50%;'>

## Creating an SSH Key Pair
