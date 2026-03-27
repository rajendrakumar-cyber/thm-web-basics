# Nmap Live Host Discovery

## Overview

This project demonstrates how to discover live hosts using Nmap.

## Tools Used

* Nmap
* Kali Linux
* TryHackMe Lab

## Techniques Covered

* ARP Scan
* ICMP Scan
* TCP SYN & ACK Ping
* UDP Ping

## Key Commands

```
sudo nmap -PR -sn <target>/24
sudo nmap -PE -sn <target>/24
sudo nmap -PS22,80,443 -sn <target>/30
```

## Learning Outcome

* Understood host discovery techniques
* Learned CIDR basics
* Practiced real-world scanning

## Screenshots

(See /screenshots folder)
