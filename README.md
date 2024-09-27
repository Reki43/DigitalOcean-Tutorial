# DigitalOcean Arch Linux Droplet Setup Guide

# Introduction
DigitalOcean is a cloud computing service. It offers you access to remote servers that act like physical computers. For example, a Droplet is a virtual machine that can be quickly deployed. These Droplets are accessed over the internet for hosting and managing websites and applications.

## Overview
This instruction manual is designed for term 2 CIT students, who want to set up a cloud-based server to host and manage websites or applications. The following steps will teach you how to create a Droplet using DigitalOcean's `doctl` command-line tool, configuring it with cloud-init, and connecting to it using SSH keys:
    
1. [Uploading a Custom Image onto DigitalOcean](#uploading-a-custom-image-onto-digitalocean)
2. [Creating a SSH Key Pair](#creating-a-ssh-key-pair)
3. [Adding the Public Key to Your DigitalOcean Account](#adding-the-public-key-to-your-digitalocean-account)
4. [Installing `doctl`](#installing-doctl)
5. [Creating an API Token](#creating-an-api-token)
6. [Granting Access to `doctl` using API Token](#granting-access-to-doctl-using-api-token)
7. [Configuring the Cloud-init File](#configuring-the-cloud-init-file)
8. [Deploying the Droplet with Cloud-init](#deploying-the-droplet-with-cloud-init)
9. [Installing and Configuring `doctl` in an Existing Droplet](#installing-and-configuring-doctl-in-an-existing-droplet)


# Instructions

## Uploading a Custom Image onto DigitalOcean

You will need a custom image like Arch Linux to upload to DigitalOcean. This allows you to create a Droplet with your preferred pre-installed operating system and configurations.

1. Click **manage** on the left-hand side of the menu
<br><br>
![click manage](./Pictures/Click%20manage%20on%20the%20left-hand%20side%20of%20the%20menu%20.jpg)

2. Select **Backups and Snapshots** from the **Manage** menu
![select backups and snapshots](./Pictures/Select%20Backups%20and%20Snapshots%20from%20the%20Manage%20menu.jpg)

3. Select **Custom Images**
![select custom images](./Pictures/Select%20Custom%20Images.jpg)

4. Select **Upload Image**
![Select upload image](./Pictures/Select%20Upload%20Image.png)

5. Select **Arch Linux Image** and click **Open**
![Select arch linux image](./Pictures/Select%20Arch%20Linux%20Image%20and%20click%20Open%20.jpg)

6. Click on **Distribution** and from the drop-down list, select **Arch Linux**
![Select arch linux from drop-down](./Pictures/Click%20on%20Distribution%20and%20from%20the%20drop-down%20list%20select%20Arch%20Linux.jpg)


7. Select your closes region and Click **Upload Image**
![Upload Image](./Pictures/Select%20your%20closes%20region%20and%20Click%20Upload%20Image.jpg)


## Creating a SSH Key Pair
Creating a SSH key pair allows you to securely connect to a remote server. It's more secure than using a password because the keys are much harder to get a hold of. The public key is stored on the server, and the private key stays on your computer, ensuring only you can access the server.

1. Open **Terminal**
2. Type **cd~**
```
cd ~
```
3. Type **mkdir .ssh**
```
mkdir .ssh
```
4. Type **ls** to see if **.ssh directory** exists
```
ls
```
![Check if .ssh exist](./Pictures/Type%20ls%20to%20see%20if%20.ssh%20directory%20exists.jpg)


5. Type the following command below to create a new **SSH key pair**
```
ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"
```
![Command to create ssh key](./Pictures/Type%20the%20following%20command%20below%20to%20create%20a%20new%20SSH%20key%20pair.jpg)


**Note:** Change **your-user-name** to your displayed terminal name beside Users, and change and type **“youremail@email.com”** to your desired email address  


## Adding the Public Key to your DigitalOcean Account

1. Copy and paste the following code below into the terminal to copy SSH key 
```
Get-Content C:\Users\your-user-name\.ssh\do-key.pub | Set-Clipboard
```
![paste code into terminal to copy SSH key](./Pictures/Copy%20and%20paste%20the%20following%20code%20below%20into%20the%20terminal%20to%20copy%20SSH%20key.jpg)


**IMPORTANT:** Change the **“your-user-name"** part of the code to the username of the current user in the terminal.

2. Select **Settings** on the left-hand side of the menu in DigitalOcean
![Click settings](./Pictures/Select%20Settings%20on%20the%20left-hand%20side%20of%20the%20menu%20in%20DigitalOcean.jpg)


3. Select **Security** and click on **Add SSH Key**
![Add SSH Key](./Pictures/Select%20Security%20and%20click%20on%20Add%20SSH%20Key.jpg)


4. Press **Ctrl + V** into the **Public Key** box and type a **Key Name**
![Paste public key](./Pictures/Press%20Ctrl%20+%20V%20into%20the%20Public%20Key%20box%20and%20type%20a%20Key%20Name.jpg)




## Installing `doctl` 
1. Open your **Terminal** in **Administrator Mode**

2. Type the following into the **Terminal** to download **`doctl`**

```bash
Invoke-WebRequest https://github.com/digitalocean/doctl/releases/download/v1.110.0/doctl-1.110.0-windows-amd64.zip -OutFile ~\doctl-1.110.0-windows-amd64.zip
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

![API on menu](./Pictures/Click%20API%20on%20the%20left-hand%20side%20of%20the%20menu%20.jpg)


2. Click **Generate New Token**
3. Type a **Token Name**, give it **Full Access**, then click **Generate Token**
![Generate Token](./Pictures/Type%20a%20Token%20Name%20and%20give%20it%20Full%20Access.jpg)

4. Copy, paste, and save the generated token somewhere safe.

**IMPORTANT:** Token is only shown once! 

## Granting Access to `doctl` using API Token

1. Open **Terminal**
2. Type the following command to grant `doctl` access to your DigitalOcean account:
```bash
doctl auth init --context personal
```
**Note:** You can change the name to anything after **--context**. I just named it **"personal"**

3. Copy and Paste your token access key into the terminal 
![token key into terminal](./Pictures/Copy%20and%20Paste%20your%20token%20access%20key%20into%20the%20terminal.jpg)

**Note:** Make sure there's a blue checkmark beside **Validating token** to confirm it worked 

4. Type the following command to confirm you have successfully authorized `doctl`
```bash
doctl account get
```

![Authorize doctl](./Pictures/Type%20the%20following%20command%20to%20confirm%20you%20have%20succesffully%20authorized%20doctl.jpg)


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
    ssh_authorized_keys:
      - <your public SSH Key>
disable_root: true
packages:
  - nginx
runcmd:
  - 'export PUBLIC_IPV4=$(curl -s http://169.254.169.254/metadata/v1/interfaces/public/0/ipv4/address)'
  - 'echo Droplet: $(hostname), IP Address: $PUBLIC_IPV4 > /var/www/html/index.html'
```
**Note:** The file creates a new user, installs nginx, which is a web server and reverse proxy, adds a public ssh key, and disables root access




3. Change **name** to your actual name
4. Change `<your public SSH Key>` line with your public SSH key

**Note:** Refer back to [**Adding the Public Key to your DigitalOcean Account**](#adding-the-public-key-to-your-digitalocean-account), step 1 to get public SSH key.


5. Click on **file** in the top left corner, then select **Save As**
6. Click on the *Save as type** drop down and select **All files**
7. Change *File name** to **"cloud-config.yaml"**, then click **Save** to your desired location


## Deploying the Droplet with Cloud-init
1. Open **Terminal**
2. Type the following command, then locate your key **ID** on the left side:
```bash
doctl compute ssh-key list
```
**Note:** Remember or note your **ID** somewhere for the next step

3. Copy and paste the following into the **Terminal**:
```
doctl compute droplet create --image 165064169 --size s-1vcpu-1gb --region sfo3 --ssh-keys < git-user > --user-data-file < path-to-your-cloud-init-file > --wait first-droplet 
```

**Note:** Adding another name beside **--wait first-droplet** will create a "second-droplet"


4. Replace **< git-user >** with your **ID** number from step 2

5. Replace **< path-to-your-cloud-init-file >** to the path location of your **cloud-config.yaml** file

![yaml path command](./Pictures/Copy%20and%20paste%20the%20following%20into%20the%20Terminal.jpg)

6. Press **enter**
![End part of yaml file](./Pictures/end%20part.jpg)

**Note:** May take a minute. If the output looks like the picture above, you have succesfully deployed your Droplets


7. Type the following command to verify it worked:
```
ssh -i < /path/to/private-key > username@your-droplet-ip
```
8. Change **< /path/to/private-key >** to where your private key is and **username** as your user

9. Change **"your-droplet-ip"** to the IP address of the droplet you want to connect. 

**Note:** Can find your IP by typing the following command:
```
doctl compute droplet list
```

10. Press **enter** 
![Succesful login of droplet](./Pictures/Succesful%20login%20of%20droplet.jpg)

**Note:** You have succesfully connected to your droplet if your terminal prompts `[user@first-droplet:~]$`

## Installing and Configuring `doctl` in an Existing Droplet

1. Connect to your existing droplet from the previous step
```
ssh -i < /path/to/private-key > username@your-droplet-ip
```

2. Type the following command to update your package database:
```
sudo pacman -Syu
```

3. Install `doctl` with the following command:
```
sudo pacman -S doctl
```

4. Authenticate with DigitalOcean
```
doctl auth init
```
**Note:** There will be a prompt asking for your access token. Please remember where you saved it

5. Verify `doctl` installation 
```
doctl account get
```
**IMPORTANT:** Make sure **status** is **active**

6. Create a new droplet using `doctl` by typing the following command:
```
doctl compute droplet create <droplet-name> --size s-1vcpu-1gb --image <image-id> --region <region> --ssh-keys <your-ssh-key-id>
```

![New droplet photo](./Pictures/creating%20droplet%20using%20doctl.jpg)


**Note:** Ensure you replace `<your-existing-droplet-ip>`, `<droplet-name>`, `<image-id>`, `<region>`, and `<your-ssh-key-id>` with the values we did in the previous steps for your setup.

7. Connect to your new droplet
```
ssh -i < /path/to/private-key > username@your-droplet-ip
```
**Note:** Remember you can type the following command to find your **Public IPv4** address:
```
doctl compute droplet list
```

Congratulations! You just learned how to install and configure `doctl` in an existing droplet. Then used it to create a new droplet.


# References

*How to automate droplet setup with cloud-init*.    DigitalOcean . (n.d.). 
  https://docs.digitalocean.com/products/droplets/how-to/automate-setup-with-cloud-init/ 

*How to create a personal access token*. DigitalOcean . (n.d.). 
  https://docs.digitalocean.com/reference/api/create-personal-access-token/ 

*How to install and configure doctl*. DigitalOcean . (n.d.). 
  https://docs.digitalocean.com/reference/doctl/how-to/install/ 

McNinch, N. (2024). *Week 2 ACIT 2420: Create an SSH key pair to authenticate and connect to a DigitalOcean droplet*. 
  [Lecture Notes]. BCIT. https://gitlab.com/cit2420/2420-notes-f24/-/blob/main/2420-notes/week-two.md



