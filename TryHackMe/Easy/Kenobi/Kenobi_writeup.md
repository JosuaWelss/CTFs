# Kenobi

[Kenobi](https://tryhackme.com/room/kenobi) 

### Description:
Walkthrough on exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.

## Task 1 Deploy the vulnerable machine

#### Question 1: Scan the machine with nmap, how many ports are open?

A simple scan like 'nmap -sV -sC 10.10.165.110' gives the answer: **7**

## Task 2 Enumerating Samba for shares

#### Question 1: Using the nmap command above, how many shares have been found?

Nmap scripting-engine does the job: 

nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.165.110

The answer is **3**

#### Question 2: Once you're connected, list the files on the share. What is the file you can see?

 1) Connection to the share: Connect smbclient //<10.10.165.110>/anonymous
 2) ls
 3) log.txt

#### Question 3:
 
 


