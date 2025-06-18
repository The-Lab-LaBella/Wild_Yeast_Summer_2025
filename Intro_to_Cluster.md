# Outline

[Introduction](#introduction)

[VPN Instructions](#before-you-get-started)

[Account Setup](#account-setup)

[Logging in](#logging-in)

&nbsp;
&nbsp;

# Introduction

If this is your first time connecting to a high-performance computing (HPC) cluster or your first time connecting to our HPC, this guide will help you connect and get ready to assemble our genomes. 

If you are completely new to the command line, here are some websites to review before you begin 

- Basic Command Line Commands: https://www.geeksforgeeks.org/basic-linux-commands/
- Navigating in the command line https://www.youtube.com/watch?v=dzHscTzpAME 
- POSIX game to get you started: https://gitlab.com/slackermedia/bashcrawl

&nbsp;

# Before you get started
You will need your DUO authentication method and if you want to log in off-campus you will need to connect to the University via the VPN

YOU MUST HAVE THE VPN CONNECTED TO LOG IN OFF CAMPUS!!! Or anytime you are not on the UNC Charlotte wifi.

To set up the VPN see here: https://services.help.charlotte.edu/TDClient/33/Portal/KB/ArticleDet?ID=677

&nbsp;

# Account Setup

High Performance Computing Cluster
You will need access to the HPC here at UNC Charlotte. If you had access in a class this will not be sufficient for our work. You will need to request a research account by going to this link https://services.help.charlotte.edu/TDClient/33/Portal/Requests/ServiceDet?ID=140

Make sure you also ask for access to /projects/labella_lab

The HPC has some help pages, but I've put together a quick-start HPC guide here: https://github.com/The-Lab-LaBella/Welcome_to_the_Lab/blob/51e711fc28308f657b9648db7fc7e7ff8d9fc557/HPC_getting_started.md#submitting-jobs-to-the-cluster
 
&nbsp;

# Logging in

To access the remote computer servers, you will use the command line. There are numerous software/apps that will help you log in. This includes PuTTY and MobaXterm. Belowe are the instructions for the Windows PowerShell and standard mac command line. 

&nbsp;

## Using a Mac Computer

### Mac Step 1 - Open SSH Client

Navigate to the Utilities folder within applications and double-click on the Terminal application.

![image](https://github.com/user-attachments/assets/6b6ee9f0-b7dd-4fb7-98b2-79e5614892c4)

### Mac Step 2 - Log into cluster

Once the terminal is open, you will log into the cluster using the command below. Your username is your UNC Charlotte username aka your email address without the @charlotte.edu portion 

Type the following command and hit enter/return.

`ssh username@hpc.charlotte.edu`

### Mac Step 3 - Enter your password

You will be prompted to enter your password. **You will not see anything as you type!!** 

Once your password is typed in hit enter/return.

### Mac Step 4 - Complete two factor authentication

Then you will be prompted to complete the DUO authentication. Enter 1, 2, or 3 for your preferred way of authenticating, and then press enter/return.

&nbsp;

## Using a Windows Computer

### 



