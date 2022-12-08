# ACIT 2420 FINAL EXAM
## Author
* Phuong Vi Dang A01292902

## Part 1: update most of software
* use 2 commands: **sudo apt update** and **sudo apt upgrade**
$ sudo apt update will check if the current softwares in Ubuntu are up-to-date
$ sudo apt upgrade is the command to actually update softwares

## Part 2: Vim
**Normal Mode**
* to move the cursor: 
   * k to move up
   * j to move down
   * h to move left
   * j to move right

* to replace letter:
    rx to replace the letter with x

> in this part:
> use **rC** to replace character V to C
> use **r0** to replace 1 to 0

![image replace 1 to 0](/images/vim-replace-0.png)

![image replace V to C](/images/vim-replace-C.png)

The final edited image is

![image of edited file](/images/vim-file-edited.png)


## Part 3: journalctl

## Part 4: 

### Step 1: create new user
* to create new user with bash shell use: 
$ useradd -ms /bin/bash username

* to add the new user to sudo group use:
$ usermod -aG sudo username

### Step 2: create script to find users in /etc/passwd

* create script:
$ touch findUsers

* add execution permission:
$ chmod + x findUsers

* The script file path must MATCH with file path in **ExecStart** in service file

* write script

![image of script](/images/script.png)

* the output looks like
![img of output](/images/output.png)

## Part 5: write a service file

**Note**: the service file must have same name with the script
$ touch findUsers.service

Service file should look like image below

![image of service file](/images/service-file.png)

* the type must be **oneshot** because it works with timer file

* the ExecStart must have the location of the script. In this case, it is in /opt/findUsers directory

## Part 6: write a timer file

**Note**: the timer file must have same name with the script
$ touch findUsers.timer

Timer file should look like image below

![image of timer file](/images/timer-file.png)

* since the timer starts 1 minute after booting, we have:
$ OnBootSec=1min

* timer file runs everyday if active, we have:
$ OnUnitActiveSec=1d


**NOTE**
* Both timer and service file must be in /etc/systemd/system directory
* After creating the files, you must run:

> sudo systemctl daemon-reload
> sudo systemctl start findUsers.service
> sudo systemctl start findUsers.timer

* To make sure that the timer run when booting, you must enable the timer file:

$ sudo systemctl enable findUsers.timer

* To check if files are run properly, use **systemctl status**

> systemctl status findUsers.service
> systemctl status findUsers.timer

The desired status should be

![image of service file status](/images/service-file-status.png)

![image of timer file status](/images/timer-file-status.png)

