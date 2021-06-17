# Kenobi

[Kenobi](https://tryhackme.com/room/kenobi) 

### Description:
Walkthrough on exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.

## Task 1 Deploy the vulnerable machine

#### Question 1: Scan the machine with nmap, how many ports are open?

 1) nmap -sV -sC 10.10.165.110  
 2) **7**

## Task 2 Enumerating Samba for shares

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

## Task 3 Gain initial access with ProFtpd
 
##### Question 1: What is the version?

 1) **1.3.5** (as seen in the nmap output from the beginning)

#### Question 2: How many exploits are there for the ProFTPd running?


