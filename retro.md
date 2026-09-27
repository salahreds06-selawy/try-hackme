# TryHackMe - Retro

**Difficulty:** Hard
**Tools Used:** Nmap, Gobuster, RDP

## Steps
1. Ran Nmap scan and found Port 80 and 3389.
2. Found hidden directory /retro using Gobuster.
3. Logged in with credentials wade:parzival.
4. Found user flag.
5. Used CVE-2017-0213 for privilege escalation.
6. Found root flag.

## What I Learned
- Web enumeration with Gobuster.
- Windows privilege escalation.
