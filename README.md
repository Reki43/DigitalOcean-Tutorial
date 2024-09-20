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
![Picture of instruction](Pictures/Click%20manage%20on%20the%20left-hand%20side%20of%20the%20menu%20.jpg)

2. Select **Backups and Snapshots** from the **Manage** menu
![Picture of instruction](Pictures/Select%20Backups%20and%20Snapshots%20from%20the%20Manage%20menu.jpg)

3. Select **Custom Images**
![Picture of instruction](Pictures/Select%20Custom%20Images.jpg)

4. Select **Upload Image**
![Picture of instruction](Pictures/Select%20Upload%20Image.png)

5. Select **Arch Linux Image** and click **Open**
![Picture of instruction](Pictures/Select%20Arch%20Linux%20Image%20and%20click%20Open%20.jpg)

6. Click on **Distribution** and from the drop-down list, select **Arch Linux**
![Picture of instruction](Pictures/Click%20on%20Distribution%20and%20from%20the%20drop-down%20list%20select%20Arch%20Linux.jpg)

7. Select your closes region and Click **Upload Image**
![Picture of instruction](Pictures/Select%20your%20closes%20region%20and%20Click%20Upload%20Image.jpg)

## Creating an SSH Key Pair
