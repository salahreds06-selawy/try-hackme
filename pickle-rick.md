# TryHackMe - Pickle Rick

**Difficulty:** Easy
**Tools Used:** Nmap, Gobuster, Burp Suite, Linux Terminal

## Steps
1. Scanned the target with Nmap and found Port 22 (SSH) and Port 80 (HTTP) open.
2. Ran Gobuster and checked `/robots.txt`, found the password `WubbaLubbaDubDub`.
3. Checked the page source code and found the username `R1ckRul3s`.
4. Logged into the portal and accessed the Command Panel.
5. Found the first ingredient in `Sup3rS3cretPickl3Ingred.txt`.
6. Bypassed the disabled `cat` command by using `less`.
7. Escalated privileges with `sudo -l` (found NOPASSWD: ALL).
8. Read the second ingredient in `/home/rick/2nd.txt`.
9. Read the final ingredient in `/root/3rd.txt`.

## What I Learned
- How to bypass command filters (using `less` instead of `cat`).
- How to escalate privileges using misconfigured `sudo` permissions.
- Basic web enumeration (robots.txt, source code).
