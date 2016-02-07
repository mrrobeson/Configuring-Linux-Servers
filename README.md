# Configuring-Linux-Servers

To add a new user to the system

Effectively adding users to a Linux instance involves two basic operations: adding the user to the system, and providing that user with a way to log in remotely.

To add a new user to the system, use the adduser command followed by any relevant options and the name of the user you wish to create.

Important
If you are adding a user to an Ubuntu system, you should add the --disabled-password option to avoid adding a password to the account.
[ec2-user ~]$ sudo adduser newuser
This command adds the newuser account to the system (with an entry in the /etc/passwd file), creates a newuser group, and creates a home directory for the account in /home/newuser.

To provide remote access to this account, you must create a .ssh directory in the newuser home directory and create a file within it named "authorized_keys" that contains a public key.

Switch to the new account so that newly created files have the proper ownership.

[ec2-user ~]$ sudo su - newuser
[newuser ~]$
Note that the prompt now says newuser instead of ec2-user; you have switched the shell session to the new account.

Create a .ssh directory for the authorized_keys file.

[newuser ~]$ mkdir .ssh
Change the file permissions of the .ssh directory to 700 (this means only the file owner can read, write, or open the directory).

Important
This step is very important; without these exact file permissions, you will not be able to log into this account using SSH.
[newuser ~]$ chmod 700 .ssh
Create a file named "authorized_keys" in the .ssh directory.

[newuser ~]$ touch .ssh/authorized_keys
Change the file permissions of the authorized_keys file to 600 (this means only the file owner can read or write to the file).

Important
This step is very important; without these exact file permissions, you will not be able to log into this account using SSH.
[newuser ~]$ chmod 600 .ssh/authorized_keys
