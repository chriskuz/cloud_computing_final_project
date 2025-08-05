# How to Run a Web Application Through AWS EC2

**Author: Christopher Kuzemka**

# Introduction

In this course, we learned how to leverage Google Cloud to deploy simplistic programs as web applications. This was accomplished through the use of a simple todo-list application provided by our professor.


**LEGEND**
- <font color="skyblue">Skyblue INPUT headers designate user-guided input sections in local terminal. Note, some trivial outputs are included in these INPUT sections.</font>
- <font color="violet">Violet INPUT headers designate user-guided input sections on cloud. Note, some trivial outputs are included in these INPUT sections.</font>
- <font color="gold">Gold OUTPUT headers designate terminal/shell outputs the user would see. Note, there may exist some differences between these ntoes and the user's actual screen.</font>
- <font color="gree">Green titles reference images and relevant embedded media.</font>
- <font color="red">Red notes are comments on error/inefficiency in process </font>

# AWS 

# Account Creation

The first step is to make an AWS account as a root user. [This can be done here](https://aws.amazon.com/free/?trk=6dc34671-f363-4ae3-86d4-30712bec6512&sc_channel=ps&ef_id=Cj0KCQjwtMHEBhC-ARIsABua5iRGLGBu0myy-bC9GIDRqzQeXVEkxdvmonNlRSxMzxzHYhVFNqk1lIIaAjwPEALw_wcB:G:s&s_kwcid=AL!4422!3!651751059789!p!!g!!amazon%20web%20services!19852662200!145019195937&gad_campaignid=19852662200&gbraid=0AAAAADjHtp-yAApZMf7dG8Z0g8DH4Ot0R&gclid=Cj0KCQjwtMHEBhC-ARIsABua5iRGLGBu0myy-bC9GIDRqzQeXVEkxdvmonNlRSxMzxzHYhVFNqk1lIIaAjwPEALw_wcB). AWS offers the free-tier services lasting up to a year. A user on a free-trial service is able to freely spin up small compute instances among a select list of operating systems and hardware specs. Additionally, a free-tier option (like the one we are using now) should allow up to 750 hours of compute usage among instances. 

There is the possibility to sign-in as an IAM (Identity and Access Management) user, however for the scope of this report and for the scope of our goals, this is not necessary. IAM comes more into play when multiple users are accessing and manipulating the same server(s) directly. This is important when it comes to server configurations and automatic budget thresholds set through AWS' platform. Observe below what the selection may look like.

<font color="gree">**IMAGE 00**</font>
![i00](pics/i00_aws_root_user_sign_in.png)


Directions are provided to create an account and once created, return to this page and sign in as a root user as instructed previously. You may be asked to provide extra verification via codes sent to your email. It may also ask you to set up a 2-factor authentication. The configurations are up to you. 

# Spinning an Instance (via Platform GUI)

Here, we will create an instance directly through the platform of AWS housed within a browser. Optimistically, we also will discuss how AWS CLI could be used to accomplish the same thing. 

## Main Hub
<font color="gree">**IMAGE 01**</font>
![i01](pics/i01_aws_home.png)

Upon signing into your AWS account, you should see a menu similar to the one shown in <font color="gree">IMAGE 01</font>. This is a main hub that has several different services you can access and navigate to. Some of these services are limited if you are using the free-tier subscription. 

It's important on the top right of the hub that you see in <font color="gree">IMAGE 01</font> that you specify the desired region for your server. We zoom in to show this on the absolute top right of <font color="gree">IMAGE 02</font> to which we changed the region to "N. Virginia", whereas previously on <font color="gree">IMAGE 01</font> it was initially set to Ohio in the top right.

<font color="gree">**IMAGE 02**</font>
![i02](pics/i02_aws_region.png)

After specifying the region, we will then want to access the AWS service that gives us the power to create virtual machiness. This service is called "EC2". To find EC2, use the search bar present at the top of your hub to look for it and select the most generic menu option for EC2. For reference, observe the top of <font color="gree">IMAGE 01</font> for the location of your search bar.

## EC2

EC2 (Elastic Compute Cloud), is Amazon's "rent-a-computer-remotely" service offered through their AWS platform. It allows anyone with an eligible account to quickly spin up servers with easy scalability non-locally. 

When entering the EC2 hub, you should notice your menu looking similar to <font color="gree">IMAGE 03. </font>

<font color="gree">**IMAGE 03**</font>
![i03](pics/i03_ec2_menu.png)

This EC2 control center offers a flexible amount of options for configuring VM instances and can provide some basic KPIs on any existing instances or previous configurations. Today, we will only go through a basic setup and running of a small instnace with some small mentions on key pairing and security specifications. To open a menu that allows us to set up and spin a server, we chose to select "Instances" and then select "Launch Instance" as seen in <font color="gree">IMAGE 04</font>. However, the same process could be executed similarly by first selecting "Instances (running)" and then selecting the golden "Launch Instance" in that following menu. Or to bypass all of this and go directly into the menu we want, you can just select "Launch Instance" from the EC2 hub. 

From the EC2 hub shown in <font color="gree">IMAGE 03</font>, choosing "Instances" or "Instances (running)" would tease us with a menu that showcases your historically made and ready-to-run instances that we would later see referenced similarly in <font color="gree">IMAGE 06</font>. The "(running)" option is just an auto-filter that takes you to that same menu, but automatically applied a filter to the menu to showcase which VMs are currently running. If you ever create an instance in EC2 and observe this menu, but don't see your instance, be sure to double check what filters you have applied as it may hide some results you are looking for. 

<font color="gree">**IMAGE 04**</font>
![i04](pics/i04_instances_menu.png)

Now we observe the below gif, <font color="gree">GIF 00</font>...

<font color="gree">**GIF 00**</font>
![g00](pics/g00_gui_instance_creation.gif)

<font color="gree">GIF 00</font> takes us through some of the initial settings of EC2's instance creation. Here we deicde to populate the "Name and Tags" field with a custom name for our instance. In this case, we name our instance `00_gui_launched_instance`. 

As you scroll a little lower, you will find that you can select various different OS options and today we decide to select an Ubuntu image (AMI) and change our verion to "Ubuntu 22.04 LTS". This version of Ubuntu is not the most updated version and scaled a few versions back, however this is done to ensure we are not going to encounter any "new-version" bugs that may be present with the latest version of software. This is considered more legacy, but otherwise thought of to be "tried-and-true." It's important to notice here that Amazon will also dictate which options we have on a free-tier eligibility, which limits our options, but does not prevent us from accomplishing out goals. 

Next, you can can choose between instance type options which can dictate how your VM usage can be billed. It will also set limits on the kind of hardware you allocate for your VM. Even though these options are pre-set there are still ways one can customize fully what specs they desire out of their hardware. 

As we scroll further, we end our GIF at a very critical step which will allow us to directly access the instnace from our local machine. A VM here requires an SSH key-pairing to be securely accessed from trusted devices. This protocol strengthens the security of our account, preventing malicious users or bots from manipulating with our server, unless they have an accessible key. Depending on your OS, you may instead choose to download an ED-based encryption key. In this case, we download an RSA key to be paired up with our server and set a custom name for this key.

DO NOT SHOW THIS KEY TO ANYONE AS IT IS PRIVATE. Losing this key will prevent you from gaining any access to your created instance forever; making the instance practically useless. 

Once this key is downloaded, you will want to organize it into your working `.ssh` directory that is local to your machine. If you do not have an `.ssh` folder set, [please reference this documentation for UNIX based OS' that walks through how to set up an `.ssh` folder properly.](https://medium.com/@SergioPietri/how-to-setup-and-use-ssh-for-remote-connections-e86556d804dd)

The below lines of <font color="skyblue">**INPUT**</font> and <font color="gold">**OUTPUT**</font> showcase how our key was moved over to the correct folder post download and how we wanted to organize it...

<font color="skyblue">**INPUT 00**</font>
```
(base) chriskuzemka@Chriss-MacBook-Pro-9 .ssh % mv ~/Downloads/00_gui_launched_instance_KEY.pem ~/.ssh/00_gui_launched_instance_KEY.pem

(base) chriskuzemka@Chriss-MacBook-Pro-9 .ssh % ls
```

<font color="gold">**OUTPUT 00**</font>
```
(base) chriskuzemka@Chriss-MacBook-Pro-9 .ssh % ls
00_gui_launched_instance_KEY.pem	google_compute_known_hosts		known_hosts
google_compute_engine			id_rsa					known_hosts.old
google_compute_engine.pub		id_rsa.pub
```

<font color="gree">**IMAGE 05**</font>
![i05](pics/i05_firewall.png)

<font color="gree">**IMAGE 06**</font>
![i06](pics/i06_instance_menu_IP.png)


![i01]()

# Installing the AWS CLI

- installing cli [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
    - follow the all users installation for the command line

<font color="skyblue">**INPUT 00**</font>

```
(base) chriskuzemka@Mac ~ % curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

<font color="gold">**OUTPUT 00**</font>

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 37.8M  100 37.8M    0     0  19.3M      0  0:00:01  0:00:01 --:--:-- 19.3M
Password:
installer: Package name is AWS Command Line Interface
installer: Installing at base path /
installer: The install was successful.
```

<font color="skyblue">**INPUT 01**</font>

```
(base) chriskuzemka@Mac ~ % which aws
aws --version
```

<font color="gold">**OUTPUT 01**</font>

```
/usr/local/bin/aws
aws-cli/2.28.2 Python/3.13.4 Darwin/24.5.0 exe/x86_64
```