
# TryHackMe - Retro Writeup

## Room Overview
**Room Name:** Retro  
**Difficulty:** Hard  
**Category:** CTF, Windows, Web Exploitation, Privilege Escalation  
**Target OS:** Windows  
**Date Completed:** September 27, 2026  
**Tools Used:** Nmap, Gobuster, Burp Suite, xfreerdp, Metasploit (CVE-2017-0213)

---

## 1. Reconnaissance

The first step was to identify open ports and services running on the target machine.

### Command Used:
```bash
nmap -sV -sC -p- -T4 <MACHINE_IP>
 
Findings:
• Port 80/tcp – HTTP (Microsoft IIS httpd 10.0)
• Port 3389/tcp – RDP (Microsoft Terminal Services) 
Analysis:
The presence of IIS on port 80 suggested a web application. Port 3389 (RDP) indicated a Windows machine that could be accessed remotely if credentials were found. 
 
2. Enumeration
 
2.1 Web Directory Enumeration
 
Using Gobuster, I searched for hidden directories on the web server.
 
Command Used:
gobuster dir -u http://<MACHINE_IP> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 
Findings:
• /retro – A hidden directory containing the website. 
2.2 Exploring the Website
 
Navigating to http://<MACHINE_IP>/retro revealed a WordPress blog titled "Retro Fanatics".
 
Key Observations:
• The blog had a post titled "Ready for Retro?" with a comment hinting at a password.
• A comment on the post contained the password: parzival.
• The author's username was displayed as wade. 
2.3 WordPress Enumeration
 
Using wpscan (or manual enumeration), I confirmed the WordPress version and found:
• Username: wade
• Password: parzival (found in the blog comments) 
 
3. Initial Access (Foothold)
 
3.1 Logging into WordPress
 
Using the credentials found, I logged into the WordPress admin panel at:
http://<MACHINE_IP>/retro/wp-login.php
 
Credentials:
• Username: wade
• Password: parzival 
3.2 Gaining RDP Access
 
Since this was a Windows machine with RDP enabled, I attempted to connect using the same credentials.
 
Command Used:
xfreerdp /u:wade /p:parzival /v:<MACHINE_IP> /cert:ignore
 
Result: Successfully gained RDP access to the Windows machine as the user wade. 
 
4. User Flag
 
Once logged in via RDP, I navigated to the desktop and found the user flag.
 
Location: C:\Users\wade\Desktop\user.txt
 
User Flag:
3b99fbdc6d430bfb51c72c651a261927
 
 
5. Privilege Escalation
 
5.1 Enumeration
 
I checked the Windows version and installed patches.
 
Command Used:
systeminfo
 
Findings:
• The system was missing the patch for CVE-2017-0213 (Windows COM Aggregate Marshaler privilege escalation). 
5.2 Exploiting CVE-2017-0213
 
I uploaded the exploit to the target machine and executed it.
 
Exploit Details:
• CVE: CVE-2017-0213
• Type: Windows COM Aggregate Marshaler Elevation of Privilege
• Impact: Allows a local user to escalate to SYSTEM. 
After running the exploit, I gained a SYSTEM shell.
 
5.3 Alternative Path (CVE-2019-1388)
 
Another path involved exploiting CVE-2019-1388 (Windows Certificate Dialog EoP), which could also be used to gain administrator privileges. 
 
6. Root Flag
 
With SYSTEM privileges, I navigated to the Administrator's desktop.
 
Location: C:\Users\Administrator\Desktop\root.txt
 
Root Flag:
7958b569565d7bd88d10c6f22d1c4063
 
 
7. Mistakes & Challenges Faced
 
During this room, I encountered several challenges:
1. Confusion about hidden directories:
At first, I didn't know how to find the /retro directory. I learned that tools like Gobuster and ffuf are essential for this task.
2. Incorrect flag format:
I initially entered the flags without the correct format, which caused errors. I learned to always double-check the answer format required by TryHackMe.
3. Internet connectivity issues:
My weak internet connection caused delays and timeouts. I learned to be patient and retry commands when needed.
4. Understanding the privilege escalation path:
I was initially confused about which exploit to use. I learned to always check systeminfo and compare it with known CVE databases. 
 
8. What I Learned
• Web Enumeration: Using Gobuster to find hidden directories.
• WordPress Enumeration: Finding credentials in comments and source code.
• RDP Access: Connecting to Windows machines remotely using xfreerdp.
• Windows Privilege Escalation: Exploiting CVE-2017-0213 to gain SYSTEM access.
• Persistence & Patience: Overcoming technical issues and learning from mistakes. 
 
9. Recommendations for Defense
• Remove sensitive information from public posts: Never store passwords in blog comments or source code.
• Patch Windows systems regularly: Apply security updates to prevent CVE exploitation.
• Restrict RDP access: Use VPNs and strong authentication for remote desktop services.
• Use strong passwords: Avoid weak or easily guessable passwords. 
 
10. References
• CVE-2017-0213 Details
• TryHackMe Retro Room

---
**Written by:** Salah Eddin Essbihi  
**LinkedIn:** [salah-eddin-essbihi](https://www.linkedin.com/in/salah-eddin-essbihi-911b0443a)  
**TryHackMe:** [cyber.salah.sec](https://tryhackme.com/p/cyber.salah.sec)  
**GitHub:** [salahreds06-selawy](https://github.com/salahreds06-selawy)
