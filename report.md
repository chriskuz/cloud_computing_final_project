# How to Run a Web Application Through AWS EC2

**Author: Christopher Kuzemka**

# Introduction

In this course, we learned how to leverage Google Cloud to deploy simplistic programs as web applications. This was accomplished through the use of a simple todo-list application provided by our professor.

# AWS 

# Account Creation

The first step is to make an AWS account as a root user. [This can be done here](https://aws.amazon.com/free/?trk=6dc34671-f363-4ae3-86d4-30712bec6512&sc_channel=ps&ef_id=Cj0KCQjwtMHEBhC-ARIsABua5iRGLGBu0myy-bC9GIDRqzQeXVEkxdvmonNlRSxMzxzHYhVFNqk1lIIaAjwPEALw_wcB:G:s&s_kwcid=AL!4422!3!651751059789!p!!g!!amazon%20web%20services!19852662200!145019195937&gad_campaignid=19852662200&gbraid=0AAAAADjHtp-yAApZMf7dG8Z0g8DH4Ot0R&gclid=Cj0KCQjwtMHEBhC-ARIsABua5iRGLGBu0myy-bC9GIDRqzQeXVEkxdvmonNlRSxMzxzHYhVFNqk1lIIaAjwPEALw_wcB). There is the possibility to sign-in as an IAM (Identity and Access Management) user, however for the scope of this report and for the scope of our goals, this is not necessary. IAM comes more into play when multiple users are accessing and manipulating the same server(s) directly. This is important when it comes to server configurations and automatic budget thresholds set through AWS' platform. 

AWS offers the free-tier services lasting up to a year. A user on a free-trial service is able to freely spin up small compute instances among a select list of operating systems and hardware specs. Additionally, a free-tier option (like the one we are using now) should allow up to 750 hours of compute usage among instances. 

# Spinning an Instance (via Platform GUI)

Here, we will create an instance directly through the platform of AWS housed within a browser. Optimistically, we also will discuss how AWS CLI could be used to accomplish the same thing. 

![i00](pics/i00_aws_home.png)

![i01](pics/i01_aws_region.png)

![i02](pics/i02_ec2_menu.png)

![i03](pics/i03_instances_menu.png)

![g00](pics/g00_gui_instance_creation.gif)

![i04](pics/i04_firewall.png)

![i05](pics/i05_instance_menu_IP.png)
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