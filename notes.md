
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

- installing cli [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
    - follow the all users installation for the command line


# CLI Installer

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