# 🚀 Deploying NGINX on AWS EC2: A Comprehensive Setup Guide

This guide will walk you through the process of deploying an NGINX web server on an AWS EC2 instance. We’ll cover everything from setting up your networking configurations to ensuring your NGINX server is up and running. By the end of this tutorial, you'll have a fully functional NGINX server accessible via the internet.

## 📋 Table of Contents

- [Introduction](#-introduction)
- [Prerequisites](#-prerequisites)
- [Step 1: Create an EC2 Instance, VPC, and Subnet](#-step-1-create-an-ec2-instance-vpc-and-subnet)
  - [Networking Configuration](#-networking-configuration)
- [Step 2: Create a Key Pair](#-step-2-create-a-key-pair)
- [Step 3: Connect to Your EC2 Instance](#-step-3-connect-to-your-ec2-instance)
  - [Troubleshooting Permissions](#-troubleshooting-permissions)
- [Step 4: Update and Install NGINX](#-step-4-update-and-install-nginx)
- [Step 5: Verify NGINX Installation](#-step-5-verify-nginx-installation)
  - [Handling Inactive NGINX](#-handling-inactive-nginx)
- [Step 6: Configure Security Groups](#-step-6-configure-security-groups)
  - [Adding HTTP Inbound Rule](#-adding-http-inbound-rule)
- [🎉 Conclusion](#-conclusion)
- [🖼 Screenshots](#-screenshots)
- [📂 Directory Structure](#-directory-structure)

## 🌟 Introduction

This project demonstrates how to deploy an NGINX server on an AWS EC2 instance. We'll cover key concepts like networking, SSH, and server management, making this guide a valuable resource for both beginners and experienced developers.

## ✅ Prerequisites

Before you begin, ensure you have the following:

- An AWS account
- SSH client installed
- Basic knowledge of Linux commands

## 🖥 Step 1: Create an EC2 Instance, VPC, and Subnet

First, you'll need to set up an EC2 instance, Virtual Private Cloud (VPC), and a subnet. This is crucial for managing your server's network and security settings.

### 🌐 Networking Configuration

When setting up your VPC and subnet, ensure they are correctly configured to allow traffic to your instance. Here's an example screenshot of my networking settings:

![Networking Configuration](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/4c5055489072fb9b7ab1317385f954f11fd79074/screenshots/Screenshot%202024-08-26%20225224.png)

## 🔐 Step 2: Create a Key Pair

Creating a key pair is essential for securely connecting to your EC2 instance. Make sure to select the correct key pair type (`.pem`), which is required for SSH access.

![Key Pair Configuration](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/keypair%20setup%20.png)

> **Note:** The `.pem` file is crucial. Store it securely as you'll need it to SSH into your instance.

## 💻 Step 3: Connect to Your EC2 Instance

Open your terminal and use the following command to SSH into your EC2 instance:

```bash
ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
```

### 🚧 Troubleshooting Permissions

While running `yum update`, you might encounter a permission error. A common workaround (though not best practice) is to use `sudo su` to become the root user:

```bash
sudo su
```

This grants you the necessary permissions to perform administrative tasks. Here's an example screenshot showing this:

![Root User Access](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/not%20being%20superuser%20command%20.png)

## 🛠 Step 4: Update and Install NGINX

Now that you have root access, update your system and install NGINX:

```bash
yum update -y
yum install nginx -y
```

![NGINX Installation](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/yum%20update%2Cnginx%20install%20.png)

## 🔍 Step 5: Verify NGINX Installation

To verify the installation, run the following command:

```bash
nginx -v
```

This checks the installed version of NGINX and confirms the installation. If NGINX is disabled, enable it using:

```bash
sudo systemctl enable nginx
```

![NGINX Enabled](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/nginx%20enabled%2Cbut%20still%20inactive.png)

### ⚙️ Handling Inactive NGINX

If you find that NGINX is inactive, start it with:

```bash
sudo systemctl start nginx
```

![NGINX Active](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/nginx%20needed%20to%20start%20therefore%20now%20running%20active%20and%20enabled.png)

## 🔐 Step 6: Configure Security Groups

Check your EC2 instance's security group settings. If you're unable to access the NGINX welcome page, it might be because HTTP (port 80) is not allowed.

### ➕ Adding HTTP Inbound Rule

To fix this, add an HTTP inbound rule to your security group:

![HTTP Inbound Rule](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/add%20http%20rule%20.png)

After adding the rule, type the public IP of your EC2 instance in a web browser. You should see the NGINX welcome page:

![NGINX Welcome Page](https://github.com/qais20/Deploying-NGINX-on-AWS-EC2-A-Comprehensive-Setup-Guide/blob/main/screenshots/success%20nginx%20been%20publsihed.png)

## 🎉 Conclusion

Congratulations! You’ve successfully deployed an NGINX web server on AWS EC2. This guide covered essential steps, including setting up networking, configuring security, and installing software on a remote server.

## 🖼 Screenshots

All screenshots referenced in this guide are located in the `/screenshots` directory. Below are some key screenshots:

- [Networking Configuration](screenshots/networking%20ec2%20setting%20config.png)
- [Key Pair Configuration](screenshots/keypair%20setup%20.png)
- [Root User Access](screenshots/not%20being%20superuser%20command%20.png)
- [NGINX Installation](screenshots/yum%20update%2Cnginx%20install%20.png)
- [NGINX Enabled](screenshots/nginx%20enabled%2Cbut%20still%20inactive.png)
- [NGINX Active](screenshots/nginx%20needed%20to%20start%20therefore%20now%20running%20active%20and%20enabled.png)
- [HTTP Inbound Rule](screenshots/add%20http%20rule%20.png)
- [NGINX Welcome Page](screenshots/success%20nginx%20been%20publsihed.png)

## 📂 Directory Structure

Here's the structure of the project repository:

```plaintext
Deploying-NGINX-on-AWS-EC2/
│
├── README.md
├── docs/
│   └── detailed-setup.md
├── screenshots/
│   ├── networking-ec2-setting-config.png
│   ├── keypair-setup.png
│   ├── root-user-access.png
│   ├── nginx-installation.png
│   ├── nginx-enabled.png
│   ├── nginx-active.png
│   ├── add-http-rule.png
│   └── nginx-welcome-page.png
└── scripts/
    └── setup-nginx.sh
```
```

### Key Updates:

1. **Correct Links**: All image links now point to the correct location in the repository.
2. **Table of Contents**: The links in the Table of Contents are fully functional, allowing readers to navigate directly to the sections of interest.
3. **Consistent Naming**: Screenshot filenames and paths are consistent with the directory structure provided.
