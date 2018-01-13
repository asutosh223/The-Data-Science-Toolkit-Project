# The-Data-Science-Toolkit-Project
## Pre-requisite
1.	AWS account
2.	Git Bash 
3.	Github to submit the Project
## System Architecture
![image 1](https://user-images.githubusercontent.com/33742913/34903727-9b3a8a04-f7ec-11e7-94cf-2ab3b6cfe59d.png)
## Solution
#### 1.	Go to Bash & Generate your SSH key
In comand line use below command
```ssh-keygen```

<Image 2>

This will create two files id_rsa & id_rsa.pub
 
 <image 3>
 
Get the content of id_rsa.pub (this will be required while we set up AWS key pair)
To get content of id_rsa.pub use below command
```
less ~/.ssh/id_rsa.pub 
or 
cat ~/.ssh/id_rsa.pub
```
#### 2.	Go to AWS account & create your EC2 instance (AWS OS)
Set your region in AWS (I set it up as Oregan) Select the closet location.
Before creating a EC2 instance, we need to create Key pairs & Security Groups. Follow below steps

**Key Pairs**

Create Key Pairs, provide a key pair name. 
Import Key pair (copy paste the content of id_rsa.pub)
 
 <Image 4>
 
**Security Groups**

Create new Security Group & not use default security group. Add rule
Add SSH to connect our system
Add HTTP to connect to internet. Source is selected as anywhere

<Image 5>
 
**Starting a server on AWS**—called an **EC2 instance**. The first step is to launch EC2.

6 steps to setup the environment on AWS:
- Choose AMI
- Choose Instance Type
-	Configure Instance
-	Add storage
-	Add Tag
-	Configure Security Group

**Choosing an AMI for our project**

When launching an EC2 instance, you must choose an Amazon Machine Image (AMI), which contains all information required to start an instance. For example, an AMI defines which operating system is installed on your EC2 instance and which software is included.

For our project we selected Ubuntu Server 16.04 LTS (HVM), SSD Volume Type, Ubuntu is an open source operating system (Linux Based)

**Choosing Instance Type**

We selected the default & cost-effective option of T2micro with 1 GiB memory. In AWS you aren’t locked into the instance type that you originally choose. You can change your instance type later based on need.

**Configuring Instance**

Select the default option (change based on your need). In our case 1 instance was selected.

**Add Storage**

30GB free storage space is available for the AMI selected with an IOPS of 100/3000 (low but will do our job)

**Add Tags**

No tags selected. (Default)

A tag consists of a case-sensitive key-value pair. For example, you could define a tag with key = Name and value = Webserver. A copy of a tag can be applied to volumes, instances or both.
Tags will be applied to all instances and volumes

**Configure Security Group**

In the EC2 launch wizard, you define a security group, which acts as a virtual firewall that controls the traffic for one or more instances. Use the already created security Group by selecting “Select an existing security group” from Assign a security group option.

Once done review the selected option & launch your instance. Instance status should be running & status checks 2/2.

#### 3.	Dockers Installation

Take the public IP address IPv4 from the instance created in AWS. Go to bash shell & type below command.

```ssh ubuntu@54.214.205.229```
 
Use the below command curl to download docker by piping it to shell

```curl -sSL https://get.docker.com | sh```

Once download is complete use sudo command mentioned below
 
Logout to make docker in effect. Log back in & type ```docker -v``` to check the version of doctor installed
 
Docker installation is complete.

#### 4.	Launch Juypter notebook

Connect to ubuntu server ```ssh ubuntu@54.201.102.48```

Now Pull jupyter image in docker using below command

```docker pull jupyter/datascience-notebook```

To verify jupyter image is available type docker images 
 
 
Run the Jupyter container using below command

```docker run -v /home/ubuntu:/home/jovyan -p 8888:8888 -d jupyter/datascience-notebook```
 
```docker exec 9c5c jupyter notebook list```

Go to internet browser & provide the IPv4 public IP & get token from bash using above command 
 

Juypter is ready for use & we can start R programming. Happy Programming :smile: !!:thumbsup:

## Cost Analysis

- Amazon EC2 – Cost Involved
- Docker – Free
- Juypter Notebook - Free

Amazon FREE USAGE TIER: New Customers get free usage tier for first 12 months

Amazon EC2 Pricing for On-Demand Instance for Ubuntu 


(http://calculator.s3.amazonaws.com/index.html)
 
 
Cost for 3 Instances, 30GB Storage, 1GiB per Month as per AWS for Free Tier user


**Cost for 3 Month = 16.80*3 = $50.4**

**Note**: Elastic IP, Data Transfer & Elastic Load Balancing is not taken into account. Price may vary for existing non FREE USAGE TIER customer


