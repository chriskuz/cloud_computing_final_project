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

It's important on the top right of the hub that you see in <font color="gree">IMAGE 01</font> that you specify the desired region for your server. We zoom in to show this on the absolute top right of <font color="gree">IMAGE 02</font> to which we changed the region to "N. Virginia", whereas previously on <font color="gree">**IMAGE 01**</font> it was initially set to Ohio in the top right.

<font color="gree">**IMAGE 02**</font>
![i02](pics/i02_aws_region.png)

After specifying the region, we will then want to access the AWS service that gives us the power to create virtual machiness. This service is called "EC2". To find EC2, use the search bar present at the top of your hub to look for it and select the most generic menu option for EC2. For reference, observe the top of <font color="gree">**IMAGE 01**</font> for the location of your search bar.

## EC2

EC2 (Elastic Compute Cloud), is Amazon's "rent-a-computer-remotely" service offered through their AWS platform. It allows anyone with an eligible account to quickly spin up servers with easy scalability non-locally. 

When entering the EC2 hub, you should notice your menu looking similar to <font color="gree">IMAGE 03. </font>

<font color="gree">**IMAGE 03**</font>
![i03](pics/i03_ec2_menu.png)

This EC2 control center offers a flexible amount of options for configuring VM instances and can provide some basic KPIs on any existing instances or previous configurations. Today, we will only go through a basic setup and running of a small instnace with some small mentions on key pairing and security specifications. To open a menu that allows us to set up and spin a server, we chose to select "Instances" and then select "Launch Instance" as seen in <font color="gree">**IMAGE 04**</font>. However, the same process could be executed similarly by first selecting "Instances (running)" and then selecting the golden "Launch Instance" in that following menu. Or to bypass all of this and go directly into the menu we want, you can just select "Launch Instance" from the EC2 hub. 

From the EC2 hub shown in <font color="gree">**IMAGE 03**</font>, choosing "Instances" or "Instances (running)" would tease us with a menu that showcases your historically made and ready-to-run instances that we would later see referenced similarly in <font color="gree">**IMAGE 06**</font>. The "(running)" option is just an auto-filter that takes you to that same menu, but automatically applied a filter to the menu to showcase which VMs are currently running. If you ever create an instance in EC2 and observe this menu, but don't see your instance, be sure to double check what filters you have applied as it may hide some results you are looking for. 

<font color="gree">**IMAGE 04**</font>
![i04](pics/i04_instances_menu.png)

Now we observe the below gif, <font color="gree">**GIF 00**</font>...

<font color="gree">**GIF 00**</font>
![g00](pics/g00_gui_instance_creation.gif)

<font color="gree">**GIF 00**</font> takes us through some of the initial settings of EC2's instance creation. Here we deicde to populate the "Name and Tags" field with a custom name for our instance. In this case, we name our instance `00_gui_launched_instance`. 

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

Observe through <font color="gold">**OUTPUT 00**</font> the items found within the `.ssh` folder. These objects found in the output folder are objects from previous ssh connections via Google Cloud and other known hosts. 

<font color="gree">**IMAGE 05**</font>
![i05](pics/i05_firewall.png)

<font color="gree">**IMAGE 05**</font> is another important component needing to be considered when spinning up an instance through this platform and is found beyond the key pairing menu upon scrolling down. For our purpose it's important to make a customer security group for the firewall. Here you should select the box to allow SSH traffic and adjust the option to "My IP" which will call upon your public IPv4 address. This selection ensures that you and only you can be the one to access your server directly. At the same time, for testing out a todolist application (which we hope to achieve before submission), you will also want to allow HTTP traffic from the internet so that appropriate protocol messaging can occur. 

To double check your IPv4 public address, in your MacOS terminal you can enter the below commands and verify the output...

<font color="skyblue">**INPUT 01**</font>
```
(base) chriskuzemka@Mac ~ % curl ipv4.icanhazip.com
```


<font color="gold">**OUTPUT 01**</font>
```
74.73.86.110
```

Scrolling down further, you will see a button that will generate your instance. It may take a few moments to generate, but you should jump into the menu seen in <font color="gree">**IMAGE 06**</font> where all of your instances are shown. If you don't recall this menu, return to comments above regarding the EC2 hub seen in <font color="gree">**IMAGE 03**</font> and how to navigate from there to a page showcasing all of your generated instances. 

<font color="gree">**IMAGE 06**</font>
![i06](pics/i06_instance_menu_IP.png)

In <font color="gree">**IMAGE 06**</font>, we zoom in to the running instance and select it with a check mark to pull up information regarding its existence. In the Details tab shown on the bottom of this image, you notice a "Public IPv4 address." This address will be important for accessing your server from your local machine, assuming that the instructions above were followed correctly and verified. 

## Accessing your Instance

You will want to click the copy icon to copy this external server IP to be used in the next commands. These next commands we showcase will involve how to access your server...

Please take note of the changing colors of the <font color="skyblue">**INPUT**</font> comannds from <font color="skyblue">skyblue</font> to <font color="violet">violet</font>. The <font color="violet">violet **INPUT**</font> commands will indicate what commands are put into the terminal that correspond to work being done on the cloud. 

<font color="skyblue">**INPUT 02**</font>
```
(base) chriskuzemka@Chriss-MacBook-Pro-9 .ssh % ssh -i ~/.ssh/00_gui_launched_instance_KEY.pem ubuntu@204.236.206.229    

The authenticity of host '204.236.206.229 (204.236.206.229)' can't be established.
ED25519 key fingerprint is SHA256:JbAq1ufvvUtTtiyqohEBFwiWrIwbU42gIohQAd/h6hQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```
<font color="GOLD">**OUTPUT 02**</font>
```
Warning: Permanently added '204.236.206.229' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1029-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Tue Aug  5 02:01:55 UTC 2025

  System load:  0.08              Processes:             102
  Usage of /:   22.1% of 7.57GB   Users logged in:       0
  Memory usage: 24%               IPv4 address for ens5: 172.31.43.49
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@ip-172-31-43-49:~$
```

In <font color="skyblue">**INPUT 02**</font>, we use the command: `ssh -i ~/.ssh/00_gui_launched_instance_KEY.pem ubuntu@204.236.206.229`. This command leverages the correctly setup `ssh` protocol to access our server from a local terminal. Through this protocol we invoke on the downloaded and stored `.pem` file, which is our specific AWS private RSA key that accesses our server, to tie in as an access key for the target public IPv4 address of the server. Since we installed Ubuntu and unless otherwise specified, we use `ubuntu` as our direct username `@` the IP address of our server. 

# On Cloud

## Setup 

On this instance, we showcase some simple commands that help update our system to run Python programs. The first thing that can be done is to switch to the `root` user, by running the below command. 

<font color="violet">**INPUT 03**</font>
```
ubuntu@ip-172-31-43-49:~$ sudo su
root@ip-172-31-43-49:/home/ubuntu#
```

After doing such, you can run commands and respond `y`/`yes` accordingly to various installations. We particularly update the `apt` toolkit, install `pip3`, install `flask`, and install `vim` (just in case we need a native editor). <font color="violet">**INPUT 04**</font> will showcase various inputs conducted at different instances post different corresponding installations. We truncate our interaction with the terminal to avoid overpopulating text here. Therefore, it is expected to see outputs in your terminal reflective of installations and intended to not see the disclosed output here. 

<font color="violet">**INPUT 04**</font>
```
root@ip-172-31-43-49:/home/ubuntu# apt-get update

root@ip-172-31-43-49:/home/ubuntu# apt install python3-pip

root@ip-172-31-43-49:/home/ubuntu# pip install flask

root@ip-172-31-43-49:/home/ubuntu# apt install vim
```

Above we showcase how to access our terminal locally and we have updated some packages. Let's `exit` the cloud momentarily and begin moving over a project onto the cloud instead. 

<font color="skyblue">**INPUT 05**</font>
```
root@ip-172-31-43-49:/home/ubuntu# exit
exit

ubuntu@ip-172-31-43-49:~$ exit
logout
Connection to 34.204.94.1 closed.
```

Note how the IP address is different here than previous commands. This callout specifically is meant to highlight how we actually spun up our instance after shutting it down a different day (the report took more than one day to write). The external IP address will typically change whenever the instance is spun up and down due to many variables, but mainly due to avialbaility of a machine.  

Continuing, you now should either navigate to the folder where this project resides or call upon the full file PATH of the project to pull in corresponding files for upload (more recommended you move first to the root of the repository where the files exist to warrant less typing). 

<font color="skyblue">**INPUT 06**</font>
```
(base) chriskuzemka@Mac cloud_computing_final_project % scp -i ~/.ssh/00_gui_launched_instance_KEY.pem -r todolist.py todolist.db templates ubuntu@34.204.94.1:~
```

Now jump back into your cloud the same way you did before. We are going to adjust the file and set the port to 80 to run. Pay attention to these next commands. We are going to use `vim` which should be installed per previous directions. This will allow us to edit our `todolist.py` file. Within vim we will want to change the last line of this Python file to specify an output port of 80. This should be an open port on your server, if you allowed HTTP traffic upon instance setup. 

Aside: use this time to also check if Python3 is installed.

<font color="violet">**INPUT 07**</font>
```
root@ip-172-31-43-49:/home/ubuntu# ls
templates  todolist.db  todolist.py

root@ip-172-31-43-49:/home/ubuntu# cat todolist.py
```

<font color="gold">**OUTPUT 07**</font>
```
# This is a simple example web app that is meant to illustrate the basics.
from flask import Flask, render_template, redirect, g, request, url_for
import sqlite3

DATABASE = 'todolist.db'

app = Flask(__name__)
app.config.from_object(__name__)


@app.route("/")
def show_list():
    db = get_db()
    cur = db.execute('SELECT what_to_do, due_date, status FROM entries')
    entries = cur.fetchall()
    tdlist = [dict(what_to_do=row[0], due_date=row[1], status=row[2])
              for row in entries]
    return render_template('index.html', todolist=tdlist)


@app.route("/add", methods=['POST'])
def add_entry():
    db = get_db()
    db.execute('insert into entries (what_to_do, due_date) values (?, ?)',
               [request.form['what_to_do'], request.form['due_date']])
    db.commit()
    return redirect(url_for('show_list'))


@app.route("/delete/<item>")
def delete_entry(item):
    db = get_db()
    db.execute("DELETE FROM entries WHERE what_to_do='"+item+"'")
    db.commit()
    return redirect(url_for('show_list'))


@app.route("/mark/<item>")
def mark_as_done(item):
    db = get_db()
    db.execute("UPDATE entries SET status='done' WHERE what_to_do='"+item+"'")
    db.commit()
    return redirect(url_for('show_list'))


def get_db():
    """Opens a new database connection if there is none yet for the
    current application context.
    """
    if not hasattr(g, 'sqlite_db'):
        g.sqlite_db = sqlite3.connect(app.config['DATABASE'])
    return g.sqlite_db


@app.teardown_appcontext
def close_db(error):
    """Closes the database again at the end of the request."""
    if hasattr(g, 'sqlite_db'):
        g.sqlite_db.close()


if __name__ == "__main__":
    app.run("0.0.0.0")
```

<font color="violet">**INPUT 08**</font>
```
root@ip-172-31-43-49:/home/ubuntu# vim todolist.py
```
Follow these keystrokes exactly to appropriately navigate `vim`:
- press `SHIFT+G` to get to the last line
- press `i` to go to "insert" mode
- use the cursor to navigate along the last line to change the line `app.run("0.0.0.0")` to `app.run("0.0.0.0", port=80)`
- press the escape key to exit insert mode
- press `:wq` to write and quit vim (saves and exits)

Now enter the next command and the sample web application should deploy. 

<font color="violet">**INPUT 09**</font>
```
root@ip-172-31-43-49:/home/ubuntu# sudo python3 todolist.py
```

<font color="gold">**OUTPUT 09**</font>
```
 * Serving Flask app 'todolist'
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:80
 * Running on http://172.31.43.49:80
Press CTRL+C to quit
```

The above output signifies a successful runtime instance of your web application. However, this doesn't always mean it is accessible as firewall rules could prevent accesss. For our case, there was no trouble-shooting involved as we allowed HTTP traffic, certified our IP as a user, and decided to run on port 80. To access the web application for testing, copy the running external IP address you've been usinig this whole time that allowed access into the server to begin with into a web browser. It is NOT the IPs shown above which are internal IPs for the server itself (yours may look different). Again, use the external IP that is tagged near the username of your terminal within cloud. 

And finally observing <font color="gree">**IMAGE 07**</font>, we see our web application reflecting the most recent external IP address we've been operating in within the last few commands. 

<font color="gree">**IMAGE 07**</font>
![i06](pics/i07_web_application.png)


## Remarks

This walkthrough has demonstrated how to spin up an instance on AWS and also how to deploy a small web applicaiton on AWS. This application works with the reliance on a development of tight coupling which is not scalable practice. It removes the need for multi-instance deployment to seperate backend and frontend development, where backend may call to a database. However, as a proof of concept we show that this method of operation works from the perspective of experimentation.

# BONUS Installing the AWS CLI

This section discusses the installation of the AWS CLI interface which can be used optimally for shell scripts. [The official guide for installation could be found from this link.](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

There are several unique commands that can be used to download a form of the AWS CLI. For this case, we leverage the commands and steps to install the CLI on MacOS for "All Users". Observe the next few commands. Take note of the colors of out <font color="skyblue">**INPUTS**</font>. It's best recommended to do this in a new terminal. 

<font color="skyblue">**INPUT 10**</font>

```
(base) chriskuzemka@Mac ~ % curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

<font color="gold">**OUTPUT 10**</font>

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 37.8M  100 37.8M    0     0  19.3M      0  0:00:01  0:00:01 --:--:-- 19.3M
Password:
installer: Package name is AWS Command Line Interface
installer: Installing at base path /
installer: The install was successful.
```

<font color="skyblue">**INPUT 11**</font>

```
(base) chriskuzemka@Mac ~ % which aws
aws --version
```

<font color="gold">**OUTPUT 11**</font>

```
/usr/local/bin/aws
aws-cli/2.28.2 Python/3.13.4 Darwin/24.5.0 exe/x86_64
```

Now that we verified the installation of AWS CLI, we want to authenticate our access to our account. If following along the AWS CLI installation, you will notice that it shall recommend you use an IAM to access your instances from terminal with the CLI. However, this isn't necessary and for our case, we won't be doing such. It is possible for us to make this access key as a root user. 

<font color="gree">**IMAGE 08**</font>
![i06](pics/i08_redacted_account_details.png)

Based off <font color="gree">**IMAGE 08**</font>, you will want to open your AWS portal and navigate to the top right to find "Security credentials". This will bring you to a new menu where you can generate various forms of keys and assign different roles. Scroll down...

<font color="gree">**IMAGE 09**</font>
![i06](pics/i09_create_access_key_menu.png)

<font color="gree">**IMAGE 10**</font>
![i06](pics/i10_root_user_access_key_creation.png)

The above <font color="gree">**IMAGE 08**</font> displays a sub-menu in your scroll that has the option to create the access key and when clicking on the transparent "Create access key" on the top right, you'll open a new menu that looks like the above <font color="gree">**IMAGE 10**</font>. Note that AWS is warning against the use of a root access key. This is not an issue for us to resolve today, but it is important to learn how to set up an IAM to allow flexible access among multiple developers onto a single server. 

Check the box and proceed with clicking the golden colored "Create access key" button on the bottom right of your screen as shown in <font color="gree">**IMAGE 10**</font>

<font color="gree">**IMAGE 11**</font>
![i06](pics/i11_root_user_access_keys.png)

Now you shoud find yourself at a new page that displays your access keys. **THIS IS VERY SENSITIVE INFORMATION.** For the sake of this documentation, the access keys were redacted from <font color="gree">**IMAGE 11**</font>. Keep this page open for now and do not close it until you enter them as credentials into your terminal. 

The next local <font color="skyblue">**INPUTS**</font> and <font color="gold">**OUTPUTS**</font> will showcase where you must enter these credentials. Observe below. 


<font color="skyblue">**INPUT 12**</font>
```
(base) chriskuzemka@Mac ~ % aws configure  
```

<font color="gold">**OUTPUTS 12**</font>
```
AWS Access Key ID [None]:     <your access key ID>
AWS Secret Access Key [None]: <your secret key>
Default region name [None]:   us-east-1
Default output format [None]: json
```

Above, we have opened our own local configuration file that is set with the AWS CLI. Corresponding to the incremental outputs of <font color="gold">**OUTPUTS 07**</font> (which are truncated samples of what you would see), enter the credentials where appropriate. 

AWS states best practices for how to manage these keys, inclusive of the option to download a `.csv` file for them. If you try to change this page, select "Done", or close your browser then AWS will provide you a warning if you chose not to download their `.csv` file. The "Secret acces key" in particular will not be stored anywhere within your portal and effectively will be lost remotely. However, should you completely lose this key and not have you configuration file not properly set, this is not the biggest issue. So long as you are signed into your account as a root user, you have the power through the portal to deactivate and delete keys within the same page "Security" page and sub-menu shown per <font color="gree">**IMAGE 09**</font>. 

Regarding setting the location, note that earlier we specified the region much earlier in this documentation. Also note in <font color="gree">**IMAGE 11**</font>, within our instances page that the location of our VM is set to `us-east-1a`. In our testing (which may be different for you), we initially applied the full server location of `us-east-1a` for this credential. This yielded a broken URL endpoint. What fixes this issue is to remove the suffix character `a`. This properly set the region of our instance. You may experience a similar issue and this correct way of setting a sup-region corresponding to the sub-region of your server may fix any potential issues. 

Finally, you can specify the output format which is nothing more than how information around your instances is displayed in terminal. It will not affect any web application you wish to deploy unless you are using a script that directly must wrangle the information output from the AWS CLI. In this case, we left this as default which was `json` output. 

<font color="gree">**IMAGE 12**</font>
![i06](pics/i12_instance_location.png)

If this was all set properly, you can now see your instance(s) by running the next input..

<font color="skyblue">**INPUT 13**</font>
```
(base) chriskuzemka@Mac ~ % aws ec2 describe-instances
```

This command should yield a very large JSON formatted output describing qualities of your instance. 

## Remarks

AWS CLI is different from Google Cloud's CLI (`gcloud`) in that it is more "atomized." `gcloud` has a nice structure that allows one to cleanly input commands to kick start applications simplistically through the use of streamlined `gcloud` commands. With web application deployment on a VM instance, as shown above, we manually moved over our code without the use of the CLI. AWS encourages users to be very "surgical" with their usage of their products - which may be one reason why it is a major industry standard among companies today. Though there is still belief that with more time and research, AWS CLI could be used similarly to the way `gcloud` was used for the course to kick off web applications through more streamlined commands.  