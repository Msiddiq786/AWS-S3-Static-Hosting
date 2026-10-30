# ☁️ AWS Static Website Hosting | S3, EC2, VPC & Nginx

<p align="center">
  <b>Cloud Infrastructure | AWS | Linux | Web Server Deployment</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws" />
  <img src="https://img.shields.io/badge/EC2-Compute-orange?logo=amazonec2" />
  <img src="https://img.shields.io/badge/S3-Storage-green?logo=amazons3" />
  <img src="https://img.shields.io/badge/Linux-Amazon%20Linux%202023-black?logo=linux" />
  <img src="https://img.shields.io/badge/Nginx-Web%20Server-009639?logo=nginx" />
</p>

## 📌 Project Overview

This project demonstrates the deployment of a static portfolio website using **Amazon Web Services (AWS)**.

An Amazon EC2 instance running Amazon Linux 2023 was launched and configured with Nginx to host a static HTML/CSS portfolio website. The project also covers Amazon S3 bucket creation and object uploads, VPC configuration, Security Groups, Linux administration, and remote server connectivity.

The primary objective was to understand how cloud infrastructure works and how web applications can be deployed and accessed through AWS.

## 🎯 Project Objectives

- Understand AWS cloud infrastructure and compute services.
- Create and configure an Amazon S3 bucket.
- Launch and configure an EC2 instance.
- Understand VPC and network configuration.
- Configure Security Groups for HTTP and SSH access.
- Connect to a Linux server using EC2 Instance Connect and SSH.
- Install, configure and manage the Nginx web server.
- Deploy a static portfolio website.
- Practise essential Linux commands using Ubuntu WSL2.

## 🏗️ Architecture

```text
                 USER / WEB BROWSER
                         |
                         |
                      Internet
                         |
                         |
                  AWS Infrastructure
                         |
                    Amazon VPC
                         |
                      Subnet
                         |
                    Security Group
                     /         \
                SSH : 22      HTTP : 80
                    |             |
                    |             |
                  EC2 Instance (Amazon Linux 2023)
                         |
                    Nginx Web Server
                         |
                   Website Files
                  /      |       \
             index.html style.css about.html
                         |
                    Portfolio Website
```

**Amazon S3 Storage:**

A separate S3 bucket was created to practise cloud object storage and file management. Objects were uploaded under the `incoming/` prefix.

## 🛠️ AWS Services & Technologies

| Service / Technology | Purpose |
|---|---|
| Amazon S3 | Cloud object storage and file uploads |
| Amazon EC2 | Virtual server for website hosting |
| Amazon VPC | Network isolation and configuration |
| Security Groups | Control inbound and outbound traffic |
| Amazon Linux 2023 | Operating system for EC2 |
| Nginx | Web server for serving static files |
| EC2 Instance Connect | Browser-based Linux connectivity |
| SSH | Secure remote server connectivity |
| Ubuntu WSL2 | Local Linux command practice |
| HTML5 | Website structure |
| CSS3 | Website styling |

## ⚙️ Implementation Steps

### 1. Amazon S3 Configuration

- Created an S3 bucket named `college-admission-docs`.
- Configured general bucket settings and object ownership.
- Created and used the `incoming/` prefix.
- Uploaded sample application files:
  - `APP-1003.json`
  - `Cloud Admission System.txt`
  - `sample-application.json`
- Verified uploaded objects in the S3 console.

### 2. Amazon EC2 Instance Creation

Created an EC2 instance with the following configuration:

| Configuration | Value |
|---|---|
| Instance Name | MY WEB SERVER |
| AMI | Amazon Linux 2023 |
| Instance Type | t3.micro |
| Key Pair | MYKEYPAIR |
| Key Pair Type | RSA |
| Private Key Format | .pem |
| Username | ec2-user |

### 3. VPC Configuration

Created a VPC with the following configuration:

| Configuration | Value |
|---|---|
| VPC Name | my-vpc-01 |
| IPv4 CIDR | 10.0.0.0/24 |
| IPv6 | No IPv6 CIDR block |
| Tenancy | Default |

### 4. Security Group Configuration

Configured the EC2 Security Group to allow website access and remote server connectivity.

| Type | Protocol | Port | Source |
|---|---|---|---|
| SSH | TCP | 22 | 0.0.0.0/0 |
| HTTP | TCP | 80 | 0.0.0.0/0 |
| Outbound | All | All | 0.0.0.0/0 |

**Security Note:** The SSH rule shown above is for demonstration purposes. In production, restrict SSH access to your own IP address or use a managed connection method.

### 5. Linux Server Connectivity

Connected to the EC2 instance using:

- EC2 Instance Connect.
- SSH Client with the generated `.pem` key pair.

SSH connection example:

```bash
chmod 400 MYKEYPAIR.pem

ssh -i "MYKEYPAIR.pem" ec2-user@<EC2-PUBLIC-DNS>
```

Verified the server connection using:

```bash
whoami
nginx -v
sudo systemctl status nginx --no-pager
```

### 6. Nginx Web Server Configuration

Used Nginx to serve the static portfolio website.

Install Nginx on Amazon Linux 2023:

```bash
sudo dnf install nginx -y
```

Enable and start the service:

```bash
sudo systemctl enable --now nginx
```

Verify installation:

```bash
nginx -v
sudo nginx -t
sudo systemctl status nginx --no-pager
```

Default Nginx web root:

```bash
/usr/share/nginx/html
```

To deploy website files, copy the HTML and CSS files into the Nginx web root.

### 7. Website Deployment

The portfolio website contains the following files:

```text
portfolio/
│
├── index.html
├── style.css
└── about.html
```

The website includes:

- Home
- About
- Education
- Technical Skills
- Experience
- Projects
- Achievements
- Contact

The website was accessed through the EC2 public IPv4 address using HTTP.

## 🐧 Linux Command Practice

Practised Linux commands using Ubuntu WSL2 and the Amazon Linux EC2 terminal.

| Command | Description |
|---|---|
| `pwd` | Display current directory |
| `whoami` | Display logged-in user |
| `date` | Display system date and time |
| `uname -a` | Display system information |
| `ls` | List files and directories |
| `ls -lah` | List files with detailed information |
| `cd` | Change directory |
| `cd ..` | Move to parent directory |
| `cd ~` | Navigate to home directory |
| `mkdir` | Create directory |
| `touch` | Create files |
| `nano` | Edit files |
| `cat` | Display file contents |
| `echo` | Write text into files |
| `df -h` | Display disk usage |
| `chmod` | Change file permissions |
| `systemctl` | Manage Linux services |

## 🧪 Testing & Verification

The following checks were performed:

- EC2 instance successfully launched.
- EC2 status checks passed (3/3).
- Linux server connection established.
- Nginx service verified as active and running.
- Website successfully accessed through the EC2 public IP.
- Portfolio pages loaded successfully.
- Website navigation links and page sections tested.
- Local Python HTTP server tested using Ubuntu WSL2.

**Result:** The static portfolio website was successfully deployed and accessed through an Amazon EC2 instance running Nginx.

## 📸 Project Screenshots

The repository contains screenshots documenting:

1. Amazon S3 bucket creation.
2. Uploaded S3 objects.
3. EC2 instance launch and AMI selection.
4. EC2 instance type and key pair creation.
5. VPC configuration.
6. EC2 Instance Connect.
7. SSH client configuration.
8. Security Group inbound and outbound rules.
9. Linux terminal and Nginx status.
10. Ubuntu WSL2 command execution.
11. Website project file creation.
12. Final portfolio website deployment.
13. Technical Skills section.
14. Achievements and Contact sections.

## 📚 Key Learnings

Through this project, I gained practical experience in:

- AWS cloud infrastructure fundamentals.
- Amazon S3 object storage.
- EC2 instance provisioning and management.
- VPC and network configuration.
- Security Group and port management.
- Linux server administration.
- SSH-based remote connectivity.
- Nginx installation and service management.
- Static website deployment on AWS.
- Basic Linux filesystem and permission management.

## 🔄 S3 vs EC2 + Nginx

| Feature | Amazon S3 Static Hosting | EC2 + Nginx |
|---|---|---|
| Infrastructure | Managed object storage | Virtual server |
| Server Management | Not required | Required |
| Operating System | Not required | Required |
| Web Server | S3 website endpoint | Nginx |
| Maintenance | Minimal | Server maintenance |
| Use Case | Static websites | Websites and server-hosted applications |

*Note: This project documents S3 bucket creation and object uploads separately from the EC2 + Nginx website deployment.*

## 👨‍💻 Author

**Mohammad Siddiq Shaik**

Cloud Data Engineer Trainee | B.Tech Computer Science Engineering

**Reference ID:** HCLTFP2261308



<p align="center">
  <b>Learning Cloud | Building Infrastructure | Deploying Solutions ☁️</b>
</p>
