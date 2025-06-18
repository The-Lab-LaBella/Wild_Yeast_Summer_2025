# Outline

[Introduction](#introduction)

[VPN Instructions](#before-you-get-started)

[Account Setup](#account-setup)

[Logging in](#logging-in)

[Short Activity](#short-activity)

&nbsp;
&nbsp;

# Introduction

If this is your first time connecting to a high-performance computing (HPC) cluster or your first time connecting to our HPC, this guide will help you connect and get ready to assemble our genomes. 

If you are completely new to the command line, here are some websites to review before you begin 

- Basic Command Line Commands: https://www.geeksforgeeks.org/basic-linux-commands/
- Navigating in the command line https://www.youtube.com/watch?v=dzHscTzpAME 
- POSIX game to get you started: https://gitlab.com/slackermedia/bashcrawl
- What is SLURM!? https://blog.ronin.cloud/slurm-intro/

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

### Mac Step 2 - Log into the cluster

Once the terminal is open, you will log into the cluster using the command below. Your username is your UNC Charlotte username aka your email address without the @charlotte.edu portion 

Type the following command and hit enter/return.

`ssh username@hpc.charlotte.edu`

### Mac Step 3 - Enter your password

You will be prompted to enter your password. **You will not see anything as you type!!** 

Once your password is typed in hit enter/return.

### Mac Step 4 - Complete two factor authentication

Then you will be prompted to complete the DUO authentication. Enter 1, 2, or 3 for your preferred way of authenticating, and then press Enter/Return.

&nbsp;

## Using a Windows Computer

### Windows Step 1 - Open or install Windows PowerShell

The PowerShell comes installed on most new Windows machines. If you do not have it installed search "PowerShell" in the Windows Store and install the App

![image](https://github.com/user-attachments/assets/5e99d02c-0db8-438f-97f4-3163846438cd)

### Windows Step 2 - Log into the cluster

Once the terminal is open, you will log into the cluster using the command below. Your username is your UNC Charlotte username aka your email address without the @charlotte.edu portion 

Type the following command and hit enter/return.

`ssh -m hmac-sha2-512 username@hpc.charlotte.edu`

### Windows Step 3 - Enter your password

You will be prompted to enter your password. **You will not see anything as you type!!** 

Once your password is typed in hit enter/return.

### Windows Step 4 - Complete two factor authentication

Then you will be prompted to complete the DUO authentication. Enter 1, 2, or 3 for your preferred way of authenticating, and then press enter/return.

&nbsp;

# Short Activity

If you are new to the command line and the research cluster, below is a short activity that will help you practice essential skills for working in the command line

## Step 1 - Navigating the Cluster

You are currently in your home directory. You can return to this directory at any time by using the command ```cd```

To see where you are in the cluster at any time use the command ```pwd``` which stands for Print Working Directory

The cluster has folders and files just like your local computer. 

```bash
#change directory
cd
#present working directory
pwd
```
&nbsp;

### Step 1a - Make a Folder

To make a folder or directory you use the command ```mkdir```

Create a folder called ```candida_activity``` using the command below

```bash
mkdir candida_activity

```

**_TIP_** _**DO NOT** use spaces or other special characters in your folder or file names. Use only letters and numbers. If you want to differentiate words you can use_ ```_``` _or_ ```.```

&nbsp;
### Step 1b - List folders and directories

To list the files or folders/directories in your current location use the ```ls``` command

You can also use the command ```tree``` to view all the files and directories below where you are. 

```bash
#to list the files in the current directory
ls
#to see a tree of the files
tree
```

&nbsp;

### Step 1c - Enter your new directory 

To change directories you use the ```cd``` or change directory command. 

We want to enter the directory we just made. To do that execute the command below

```bash
cd candida_activity
```

Check to make sure you are where you think you are using ```pwd```. 

_**TIP**_ _You can autocomplete any file or directory currently accessible by using tab. For example, if you are in your home directory and want to enter the lab_1 directory, you can type_ ```cd la[tab]``` _and it will complete to_ ```cd lab_1```
_If there is more than one option it will list all of the options, and you will have to type more to complete the process._

&nbsp;

&nbsp;

## Step 2 - Upload the genome file 

We now need to get the file from your computer to the research cluster. You will first need to download the file from GitHub to your computer. 

To transfer a file **from** your computer, you need a terminal that is connected to your local computer and _not_ to the HPC.

### Step 2a - Open a new terminal and navigate to the folder

Open a second terminal window and navigate to wherever your file is saved. 

You can use ``cd`` to navigate to where your file is located. 

Another option is to find the exact path of your file and nagivate there. To do that, you can open the finder/folder view and right-click/control-click on the file. You will see an option to ``Copy [item] as Pathname`` or ``Copy as path``

You will then get a pathname like this: ``C:\Users\alabell3\Desktop\candida_albicans.fas.tar.gz`` the folder where the file is located is ``C:\Users\alabell3\Desktop\``

Navigate to that folder using a command such as

```
cd C:\Users\alabell3\Desktop\
```

Use ``ls`` to make sure the file is in your current directory. 

&nbsp;

### Step 2b - Upload file

The command for transferring a file from one computer to another is ``scp`` or "Secure CoPy". 

The general format for ```scp``` or secure copying a file from your local computer to the cluster is:
```bash
scp LOCAL_FILE username@hpc.charlotte.edu:DIRECTORY/IN/DESTINATION
```

In Windows you will have to add an extra option.

```bash
scp -o MACs=hmac-sha2-512 LOCAL_FILE username@hpc.charlotte.edu:/DIRECTORY/IN/DESTINATION
```

Now, when you go back to your terminal that is logged into the cluster and type ``ls`` you should see your file! 

&nbsp;

### Step 3 - Uncompress the file 

Sequence files can become quite large. There are numerous ways to compress a file using methods like tar, gzip, and zip. The file we are working with has been compressed using the tar command. 

If you were to use the command ```cat``` or ```head``` to look at our file right now it would go crazy! (you can try it). If you ever need to exit a command that is running you can use ```[Cntrl]+[c]``` in windows or ```[command]+[.]``` on a mac. 


To uncompress our file use the command
```bash
tar -xvf candida_albicans.fas.tar.gz
```

The ```-xvf``` tells the tar program what to do with the file listed

```-x``` = extract 

```-v``` = verbose (list all the files as they are being extracted)

```-f``` = next item is the file

You should now see a file called ```candida_albicans.fas```

**_HINT_** You can see the options for any command by typing the command and following that with ```--help``` or sometimes ```-h```. For example ```tar --help``` will provide you with a detailed set of options for the command

&nbsp;

### Step 4 - Visualize the file

This is a LARGE file. It is the whole genome of the yeast species _Saccharomyces candida_albicans_. It is in what is called FASTA format. Our file contains **nucleotide** data but FASTA files can contain amino acid or nucleotide data. The general format for FASTA format is:
```
>sequence identifier 1
sequence data
>sequence identifier 2
sequence data
```

Let's take a look at our file using the ```less``` command.

```bash
less candida_albicans.fas
```

This will display the file in your terminal. You can press enter to see more of the file. To quit this view hit the ```q``` key


Now let's take a look at our file using the ```head``` command. This command will print into your terminal the first set of lines in the file. You can also specify how many lines you would like it to display. Let's look at the first 5 lines. 

```bash
head -5 candida_albicans.fas
```

### Knowledge Check 1
What is the sequence identifier of the first sequence in the candida_albicans.fas file 

<details>
 <summary>Answer</summary>
 Ca22chr1A_C_albicans_SC5314 (3188363 nucleotides)
</details>

&nbsp;

### Step 5 - Count the number of sequences

There are a wide variety of tools to analyze sequence data. The built-in tools in our terminal can also be very powerful. One of the most powerful tools is ```grep```. 

The ```grep``` command can search for a pattern in a large file. 

If we want to count how many sequences there are in our file, we can simply count the number of times the ```>``` character appears in our file. 

Try out grep using this command:
```bash
grep ">" candida_albicans.fas
```

One of the options in ```grep``` is to count the number of instances instead of returning them. This is the ```-c``` option. 
```bash
grep -c ">" candida_albicans.fas
```

To see more options in ```grep``` try ```grep --help```

### Knowledge Check 2
How many sequences are in our file. 

<details>
 <summary>Answer</summary>
9
</details>

&nbsp;
# Step 6 - Analyze the base composition of our genome

While there are many useful programs already included in the terminal, there are programs that have been installed on the cluster as **modules**

To access these modules we will need to load them.

The program module we will be using in this section is called EMBOSS. Let's see if EMBOSS is installed in the cluster using the command ```module search```

```bash
module search EMBOSS
##this will return 
------------------------------------------------------------------ /apps/usr/modules/apps -------------------------------------------------------------------
        emboss/6.6.0: EMBOSS (European Molecular Biology Open Software Suite) is a software analysis package specially developed for the needs of the molecular biology (e.g. EMBnet) user community. The software automatically copes with data in a variety of formats and even allows transparent retrieval of sequence data from the web.
````

We can see that EMBOSS version 6.6.0 is installed on the cluster

**_TIP_** _Case (upper vs lower) matters when loading modules. You will need to type it exactly as written before the : in the description._

**_TIP_** _Placing a_ ```#``` _before any line of code means it's a comment and not a command. I will often put notes in the code using # that will be ignored._

To load emboss we can now type

```bash
module load emboss
```

Within emboss we want to run the ```geecee```. As you can see from the name, it is a program for calculating the fraction of G (gee) or C (cee) in a sequence file. To learn more about the program use ```geecee --help```


To run geecee on our sequences use the command below where we provide an informative output file name for the results to be saved

```bash
geecee -sequence candida_albicans.fas -outfile candida_albicans.geecee.out
```


### Knowledge Check 2
What is the maximum GC content observed in our yeast genome sequences?

<details>
 <summary>Answer</summary>
0.34
</details>



