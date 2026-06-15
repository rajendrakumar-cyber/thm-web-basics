# CTF Log Analysis Findings

## 🛡️ WAF Logs (Web Attacks)
- **Question:** Single source IP responsible for blocked web attacks?
- **Answer:** `198.51.100.12`
- **Command:** `grep "BLOCK" waf_logs.txt | awk -F'src_ip=' '{print $2}' | awk '{print $1}' | sort | uniq`

## 🔥 Firewall Logs (Network Traffic)
- **Question:** External IP that performed most reconnaissance? 
  - **Answer:** `203.0.113.45`
- **Question:** Internal host targeted by scans?
  - **Answer:** `10.0.0.100`
- **Question:** Port used for lateral SMB attempts?
  - **Answer:** `445`

## 🔐 VPN Logs (Authentication)
- **Question:** Username targeted in VPN logs?
  - **Answer:** `awilliams` (Verify if failed attempts use this username)
- **Question:** Internal IP assigned after successful VPN login?
  - **Answer:** `10.8.0.62`
- **Command:** `grep "success" vpn_auth.log | grep "198.51.100.92"`

## 🚨 IDS Logs (Alerts & C2)
- **Question:** Host that beaconed to C2?
  - **Answer:** `10.0.0.60`
- **Question:** IP observed to be associated with C2?
  - **Answer:** `198.51.100.77`
- **Question:** Host that showed exfiltration attempts?
  - **Answer:** `10.0.0.51`

---
*Notes generated on June 15, 2026*
