## commands to check compromised server

w
###### currently logged users

cat /etc/passwd | grep /bin/bash
###### Each line in this file represents login information for one user who can use the shell

last
###### The last command lists the sessions of users who recently logged in to the system

lastb (fail)
###### failed login

cat /var/log/messages

sudo cat /var/log/auth.log | grep ssh | grep Accept
###### ssh connections attempts 

history
###### show bash history

ls -lart
###### check the files, their owner and time of modification

netstat -na 
###### displays the current listening sockets on the machine

netstat -natp 
###### Looks for any suspicious connections that are running on odd ports

ps -wauxef
###### track down any errant processes that are listening and shows other odd processes 

lsof |grep <pid> 
###### to find more information about open files that a process is using

cat /proc/<pid>/cmdline 
######might also tell you where the file that controls a process exists.


top
###### check cpu intensive processes

lsattr in /bin /sbin /usr/bin /usr/sbin
###### check immutability ex: -------i----- /bin/ps

ls -la –author
###### who is the author of the file

find
###### find files modified in the past 5 days : find / -mtime 5

## check rootkit
apt install rkhunter
rkhunter --check
/var/log/rkhunter.log
## trivy for vuln check or iac misconfiguration
trivy repo : https://github.com/knqyf263/trivy-ci-test
apt-get install trivy

#### vulnerability
trivy rootfs --severity HIGH,CRITICAL /
trivy fs --severity HIGH,CRITICAL path

#### Iac misconfiguration 
trivy config --severity HIGH,CRITICAL path
trivy image --severity HIGH,CRITICAL --security-checks config IMAGE_NAME #docker image
trivy fs --severity HIGH,CRITICAL --security-checks config /path/to/dir #path