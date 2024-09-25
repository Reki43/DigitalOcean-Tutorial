# DigitalOcean Arch Linux Droplet Setup Guide

# Introduction
DigitalOcean is a cloud computing service. It offers you access to remote servers that act like physical computers. For example, a Droplet is a virtual machine that can be quickly deployed. These Droplets are accessed over the internet for hosting and managing websites and applications.

## Overview
This instruction manual is designed for term 2 CIT students, who want to set up a cloud-based server to host and manage websites or applications. The following steps will teach you how to create a Droplet using DigitalOcean's `doctl` command-line tool, configuring it with cloud-init, and connecting to it using SSH keys:
    
1. Uploading a Custom Image onto DigitalOcean
2. Creating a SSH Key Pair
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


## Installing `doctl` 
1. Open your **Terminal** in **Administrator Mode**

2. Type the following into the **Terminal** to download **`doctl`**

```bash
Invoke-WebRequest https://github.com/digitalocean/doctl/releases/download/v1.110.0/doctl-1.110.0-windows-amd64.zip -OutFile ~\doctl-1.110.0-windows-amd64.zip
Expand-Archive -Path ~\doctl-1.110.0-windows-amd64.zip
```

3. Type the following to extract the binary:

```bash
Expand-Archive -Path ~\doctl-1.110.0-windows-amd64.zip
```


4. Create a new directory for `doctl` by typing the following:
```bash
New-Item -ItemType Directory $env:ProgramFiles\doctl\
```

5. Move the `doctl` binary to the new directory by typing the following:
```bash
Move-Item -Path ~\doctl-1.110.0-windows-amd64\doctl.exe -Destination $env:ProgramFiles\doctl\
```

6. Add `doctl` to the System's PATH by typing the following:
```bash
[Environment]::SetEnvironmentVariable(
    "Path",
    [Environment]::GetEnvironmentVariable("Path",
    [EnvironmentVariableTarget]::Machine) + ";$env:ProgramFiles\doctl\",
    [EnvironmentVariableTarget]::Machine)
```
**Note:** This part is necessary to ensure that you can run `doctl` from any terminal session, regardless of your current directory.

7. Reload PATH for current session by typing the following:
```bash
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
```

## Creating an API token

1. Click **API** on the left-hand side of the menu on DigitalOcean homepage
<img src='Pictures/Click API on the left-hand side of the menu .jpg' style='width: 50%;'>

2. Click **Generate New Token**
3. Type a **Token Name**, give it **Full Access**, then click **Generate Token**
<img src='Pictures/Type a Token Name and give it Full Access.jpg' style='width: 50%;'>

4. Copy and paste the generated token somewhere safe.

**IMPORTANT:** Token is only shown once! 

## Granting Access to `doctl` using API Token

1. Open **Terminal**
2. Type the following command to grant `doctl` access to your DigitalOcean account:
```bash
doctl auth init --context personal
```
**Note:** You can change the name to anything after **--context**. I just named it **"personal"**

3. Copy and Paste your token access key into the terminal 
<img src='Pictures/Copy and Paste your token access key into the terminal.jpg' style='width: 50%;'>

**Note:** Make sure there's a blue checkmark beside **Validating token** to confirm it worked 

4. Type the following command to confirm you have successfully authorized `doctl`
```bash
doctl account get
```
<img src='Pictures/Type the following command to confirm you have succesffully authorized doctl.jpg' style='width: 65%;'>


## Configuring the Cloud-init File
Cloud-init helps set up a Droplet automatically by using a YAML file. This file tells the server what name to use, what software to install, and what tasks to run, making setup faster and easier without needing to do everything manually. 

1. Open **Notepad**
2. Copy and paste the following into the blank page:

```
#cloud-config
users:
  - name: example-user
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh_import_id:
      - gh:<your-GitHub-username>
disable_root: true
packages:
  - nginx
runcmd:
  - 'export PUBLIC_IPV4=$(curl -s http://169.254.169.254/metadata/v1/interfaces/public/0/ipv4/address)'
  - 'echo Droplet: $(hostname), IP Address: $PUBLIC_IPV4 > /var/www/html/index.html'
```

3. Change **name** to your actual name
4. Change `gh:<your-GitHub-username>` line with your actual GutHub username
5. Click on **file** in the top left corner, then select **Save As**
6. Click on the *Save as type** drop down and select **All files**
7. Change *File name** to **"cloud-config.yaml"**, then click **Save** to your desired location


## Deploying the Droplet with Cloud-init
1. Open **Terminal**
2. Type the following command, then locate your **ID** on the left side:
```bash
doctl compute ssh-key list
```
**Note:** Remember or note your ID somewhere for the next step

3. Copy and paste the following into the **Terminal**:
```
doctl compute droplet create --image 165064169 --size s-1vcpu-1gb --region sfo3 --ssh-keys git-user --user-data-file <path-to-your-cloud-init-file> --wait first-droplet second-droplet
```

4. Replace **git-user** with your **ID** number from step 2

5. Replace **"path-to-your-cloud-init-file"** to the path location of your **cloud-config.yaml** file
<img src='Pictures/Copy and paste the following into the Terminal.jpg' style='width: 65%;'>

6. Press **enter**
<img src='Pictures/end part.jpg' style='width: 65%;'>

**Note:** May take a minute. If the output looks like the picture above, you have succesfully deployed your Droplets

7. Type the following command to verify it worked:
```bash
ssh example-user@your-droplet-ip-address
```
**Note:** Change **"your-droplet-ip-address"** to the IP address of the droplet you want to connect. Can find your IP by typing the following command:
```
doctl compute droplet list
```

**Note:** It is succesful if your terminal prompts `example-user@first-droplet:~$`


# References

*How to automate droplet setup with cloud-init*. DigitalOcean . (n.d.). 
  https://docs.digitalocean.com/products/droplets/how-to/automate-setup-with-cloud-init/ 

*How to create a personal access token*. DigitalOcean . (n.d.). 
  https://docs.digitalocean.com/reference/api/create-personal-access-token/ 

*How to install and configure doctl*. DigitalOcean . (n.d.). 
  https://docs.digitalocean.com/reference/doctl/how-to/install/ 

McNinch, N. (2024). *Week 2 ACIT 2420: Create an SSH key pair to authenticate and connect to a DigitalOcean droplet*. 
  [Lecture Notes]. BCIT. https://gitlab.com/cit2420/2420-notes-f24/-/blob/main/2420-notes/week-two.md



