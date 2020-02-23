# Git-Hostgator

Access Hostgator server via SSH

$ ssh -p 2222 user-name@your-domain.com

$ Enter your password: **********


Get your public key into Hostgator. Your public key is located at ~/.ssh/id_rsa.pub (on your workstation). If you dont have 
~/.ssh/id_rsa.pub on your workstation, run ssh-keygen in your console and hit enter all the way through. At the end of that, you will 
have the ~/.ssh/id_rsa.pub file on your computer. If you do skip to the second line below to copy the key to hostgator.


$ ssh-keygen -t rsa

$ scp -p 2222 ~ /.ssh/id_rsa.pub user-name@your-domain.com:~/.ssh/authorized_keys   (ps. delete space after ~)

$ ssh -p 2222 user-name@your-domain.com 'chmod 600 ~/.ssh/authorized_keys'

If ~/.ssh/authorized_keys does not exist on hostgator, then create it by running the command below.

$ touch ~/.ssh/authorized_keys

TO CLONE FROM HOSTGATOR TO PC
-----------

$ git clone ssh://user-name@your-domain.com:2222/~/public_html/path..


SET UP HOSTGATOR SERVER TO ACCEPT PUSHES
----------

$ mkdir REPOSITORY_NAME

$ cd REPOSITORY_NAME

$ git init

Next you need to set a config option in your hostgator repo to accept pushes into this working directory. In this same directory run:

$ git config receive.denyCurrentBranch ignore



SEARCH FOR post-receive file into .git/hooks/

IF IT DOESN'T EXIST, CREATE IT BY RUNNING 'nano post-receive' AS FOLLOWING:

$ cd .git/hooks/

$ nano post-receive

Then add the following two code lines to the post_receive file, save and exit.
```
#!/bin/sh
GIT_WORK_TREE=../ git checkout -f
```

Now you want to make it executable. Run the following command

$ chmod +x ~/public_html/REPOSITORY_NAME/.git/hooks/post-receive



