
# General Notes
- make account
- sign in as a root user (for this case, do not use an IAM)..;.be a root user
- there may be an eligible option online that promotes a free-tier subscription. some are available for 1 year
- we want to find a menu such as this one (i00)
- ensure you set a sensible region for yourself (i01)
- use the search bar on the top to search for an ec2
- observe this menu....we will want to make an instance (i02)
- launch instance button (i03)
- showcase menu (g00)..
    - g00 slowly go through the amazon instance showcasing the keypair set and the 
- make an ssh key pairing (g00)
    - double check whether operating on mac or windows whcih may dictate the kind of key pairing you want
    - provide a link on how to make an ssh directory if not available
    - go through the commands of moving the ssh key pairing into the ssh folder 
- commands for moving the key and activating it

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

<font color="skyblue">**INPUT 01**</font>
```
(base) chriskuzemka@Chriss-MacBook-Pro-9 .ssh % chmod 400 ~/.ssh/00_gui_launched_instance_KEY.pem
```

- when creating a firewall rule, do not use the default
    - you won't be able to ssh or test a web server from your local machine then
- here we want to allow ssh traffic from My IP (where this is the IP address from your home router/network)
    - the i,mage shows IPv4, so run the command: `(base) chriskuzemka@Mac ~ % curl ipv4.icanhazip.com`
    - `74.73.86.110`
- http traffic can also be checked (i04)


- go back to the instances main menu and locate the IP address you need
- next few lines show how to sign in. 


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

# CLI Installer

- installing cli [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
    - follow the all users installation for the command line

**LEGEND**
- <font color="skyblue">Skyblue INPUT headers designate user-guided input sections in local terminal. Note, some trivial outputs are included in these INPUT sections.</font>
- <font color="violet">Violet INPUT headers designate user-guided input sections on cloud. Note, some trivial outputs are included in these INPUT sections.</font>
- <font color="gold">Gold OUTPUT headers designate terminal/shell outputs the user would see. Note, there may exist some differences between these ntoes and the user's actual screen.</font>
- <font color="gree">Green notes are comments made by the author on local INPUTS, OUTPUT, and processes.</font>
- <font color="red">Red notes are comments on error/inefficiency in process </font>

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