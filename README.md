# 🌐 Web Fundamentals Notes (DNS, HTTP, Websites)

> Personal learning notes from TryHackMe — focused on real-world understanding for ethical hacking.

---

## 📌 1. DNS (Domain Name System)

### What is DNS?
DNS is like the internet’s phonebook. It converts human-readable domain names into IP addresses.



---

### How DNS Works

1. User enters URL
2. Browser checks cache
3. OS checks DNS cache
4. Query sent to Resolver
5. Resolver contacts:
   - Root Server
   - TLD Server (.com, .org)
   - Authoritative Server
6. IP returned to browser
7. Browser connects to server

---

### Common DNS Records

| Record | Purpose |
|--------|--------|
| A | Domain → IPv4 |
| AAAA | Domain → IPv6 |
| CNAME | Alias |
| MX | Mail server |
| TXT | Metadata / verification |

---

### Tools (Recon)

```bash
nslookup example.com
dig example.com
amass enum -d example.com

HTTP Request Example
GET /index.html HTTP/1.1
Host: example.com
HTTP Response Example
HTTP/1.1 200 OK
Content-Type: text/html

| Method | Purpose       |
| ------ | ------------- |
| GET    | Retrieve data |
| POST   | Send data     |
| PUT    | Update data   |
| DELETE | Remove data   |

| Code | Meaning               |
| ---- | --------------------- |
| 200  | OK                    |
| 201  | Created               |
| 301  | Redirect              |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |
| 503  | Service Unavailable   |

