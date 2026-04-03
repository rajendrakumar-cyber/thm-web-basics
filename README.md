# Nmap and OpenVPN - TryHackMe

## Overview

This project demonstrates connecting to TryHackMe using OpenVPN and performing network scanning using Nmap.

## Tools Used

* OpenVPN
* Nmap
* Kali Linux
* TryHackMe

## OpenVPN Setup

```bash
sudo openvpn username.ovpn
```

## Verification

```bash
ip a
ping 10.10.x.x
```

## Nmap Scan

```bash
nmap -sC -sV <target-ip>
```

## Results

* Connected successfully to VPN
* Discovered open ports:

  * 21 (FTP)
  * 22 (SSH)
  * 80 (HTTP)

## Learning Outcome

* Understood VPN usage in labs
* Learned network scanning basics
* Identified attack surfaces

## Screenshots

(See /screenshots folder)
