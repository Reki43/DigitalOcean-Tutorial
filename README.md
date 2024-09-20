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
<img src="Pictures/Select Backups and Snapshots from the Manage menu.jpg" alt="Description of instruction" style="width: 50%; height: 50%;" />

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

## Creating a SSH Key Pair
Creating a SSH key pair allows you to securely connect to a remote server. It's more secure than using a password because the keys are much harder to get a hold of. The public key is stored on the server, and the private key stays on your computer, ensuring only you can access the server.

1. Open **Terminal**
2. Type **cd ~**
3. Type **mkdir .ssh**
4. Type **ls** to see if **.ssh directory** exists
<img src='Pictures/Type ls to see if .ssh directory exists.jpg' alt='Picture of instruction' style='width: 50%;'>

5. Type the following command below to create a new **SSH key pair**
<img src='Pictures/Type the following command below to create a new SSH key pair.jpg' alt='Picture of instruction' style='width: 50%;'>

**Note:** Change **your-user-name** to your displayed terminal name beside Users, and change and type **“youremail@email.com”** to your desired email address  


## Adding the Public Key to your DigitalOcean Account

1. Copy and paste the following code below into the terminal to copy SSH key 
<img src='Pictures/Copy and paste the following code below into the terminal to copy SSH key.jpg' alt='Picture of instruction' style='width: 50%;'>

**IMPORTANT:** Change the **“your-user-name"** part of the code to the username of the current user in the terminal.

2. Select **Settings** on the left-hand side of the menu in DigitalOcean
<img src='Pictures/Select Settings on the left-hand side of the menu in DigitalOcean.jpg' alt='Picture of instruction' style='width: 50%;'>

3. Select **Security** and click on **Add SSH Key**
<img src='Pictures/Select Security and click on Add SSH Key.jpg' alt='Picture of instruction' style='width: 50%;'>

4. Press **Ctrl + V** into the **Public Key** box and type a **Key Name**
<img src='Pictures/Press Ctrl + V into the Public Key box and type a Key Name.jpg' style='width: 50%;'>


## Creating a Droplet 
