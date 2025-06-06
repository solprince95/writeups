
✅ README.md Template: Mr. Robot CTF (Recon Phase)

# 🤖 Mr. Robot CTF – Phase 1: Recon & Enumeration

## 🧠 Overview

This writeup documents the first stage of the Mr. Robot CTF from TryHackMe, focused on discovering services, inspecting the web server, and attempting to locate hidden files and flags.

---

## 📍 Target

- *IP:* 10.10.147.120
- *Platform:* TryHackMe attack machine (browser-based Kali)

---

## 🛠 Tools Used

- nmap for port scanning
- gobuster for directory brute-forcing
- Firefox (from attack box) for browsing & source inspection
- Apache server-status & index.html analysis

---

## 🔍 Step 1: Port Scan (Nmap)

```bash
nmap -sV -sC -oN nmap.txt 10.10.147.120

✅ Result (summary):

22 → SSH (OpenSSH 8.2)

53 → DNS (dnsmasq)

80 → WebSockify Python server (returns 405)

81 → Apache 2.4.41 (default Ubuntu page)

111, 389, 3389, 5901, 6001 → Other services (RPC, LDAP, RDP, VNC)


🧠 Focus was shifted to port 81, where a real web page was visible.


---

🌐 Step 2: Web Recon on Port 81

Visited:

http://10.10.147.120:81/

Shows Apache Ubuntu default index page

No custom CTF content at root

/robots.txt, /key-1-of-3.txt, and /fsocity.dic return 404



---

🔗 Step 3: Directory Brute Force (Gobuster)

gobuster dir -u http://10.10.147.120:81 -w /usr/share/wordlists/dirb/common.txt -t 40

gobuster dir -u http://10.10.147.120:81 -x txt,dic -w /usr/share/wordlists/dirb/common.txt -t 40

🔎 Results:

/index.html – Apache default page

/server-status – mod_status exposed (Apache load info)

/.htaccess, /.htpasswd – 403 Forbidden


🧠 No sign of flag 1 or fsocity.dic yet — likely hidden in a subdirectory


---

🔬 Step 4: Source Code Analysis

Viewed /index.html source:

No embedded flag hints or usernames

Just standard Apache server guidance and file layout



---

🚧 Current Status

✔️ Recon completed
🚫 Flag 1 not yet found
⏳ Room timed out (TryHackMe free user limit reached)


---

📌 Next Steps (Tomorrow):

Resume Gobuster with a larger wordlist: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

Search for /blog, /wp, /admin, or /key-1-of-3.txt

Locate fsocity.dic and key-1-of-3.txt to move to exploitation phase



---

🧠 Lessons Learned

How to enumerate services using nmap

How to detect default Apache deployments

How to brute-force directories with gobuster

Importance of checking server-status and HTML source



---

📁 Files Included

nmap.txt – Full Nmap scan output



---

> 📅 Writeup by Prince | CTF Phase 1 | GitHub Portfolio Project
