# Kenobi

[Kenobi](https://tryhackme.com/room/kenobi) 

### Description:
Walkthrough on exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.

## Task 1 Deploy the vulnerable machine

### Question 1: Scan the machine with nmap, how many ports are open?

A simple scan like 'nmap -sV -sC 10.10.165.110' gives the answer: **7**

## Task 2 Enumerating Samba for shares

### Question 1: Using the nmap command above, how many shares have been found?

