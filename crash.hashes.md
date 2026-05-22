# THM - Crack the Hash (Clean Notes)

## Cracked Hashes

MD5
48bb6e862e54f2a795ffc4e541caed4d
Password: easy

SHA1
CBFDAC6008F9CAB4083784CBD1874F76618D2A97
Password: password123

SHA256
1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032
Password: letmein

bcrypt
$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom
Password: bleh

MD4
279412f945939ba78ce0758d3fd83daa
Password: Eternity22

---

## Identify Hash Type

hashid hash.txt

or

nth --text HASH

---

## Unzip rockyou wordlist

sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

---

## Hashcat Commands

MD5:

hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt

SHA1:

hashcat -m 100 hash.txt /usr/share/wordlists/rockyou.txt

SHA256:

hashcat -m 1400 hash.txt /usr/share/wordlists/rockyou.txt

NTLM:

hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt

bcrypt:

hashcat -m 3200 hash.txt /usr/share/wordlists/rockyou.txt

MD4:

hashcat -m 900 hash.txt /usr/share/wordlists/rockyou.txt

HMAC-SHA1:

hashcat -m 160 hash.txt /usr/share/wordlists/rockyou.txt

---

## Show Cracked Results

hashcat --show hash.txt

---

## Rule-Based Attack

hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule

---

## John the Ripper

john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Show results:

john --show hash.txt

---

## Useful Reminder

32 chars → MD5 / MD4 / NTLM
40 chars → SHA1
64 chars → SHA256
$2y$ → bcrypt
$6$ → SHA512
$1$ → MD5 Unix
