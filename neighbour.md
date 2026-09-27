# TryHackMe - Neighbour Writeup

## Room Overview
**Room Name:** Neighbour  
**Difficulty:** Easy  
**Category:** Web, IDOR (Insecure Direct Object Reference)  
**Target OS:** Linux  
**Date Completed:** September 27, 2026  
**Tools Used:** Web Browser, Burp Suite (optional), Linux Terminal

---

## 1. Introduction

Neighbour is a beginner-friendly room that focuses on **IDOR (Insecure Direct Object Reference)**. The goal is to find a flag hidden in another user's profile by manipulating a URL parameter.

The room description hints:  
*"You definitely wouldn't be able to find any secrets that other people have in their profile, right?"*

---

## 2. Initial Access

I started the Lab Machine and navigated to the web application:
 
http://<MACHINE_IP>

The page presented a login form. Since no credentials were provided, I registered a new account.

**Registration Details:**
- Username: `testuser`
- Password: `password123`

After registering, I was redirected to my profile page.

---

## 3. Enumeration

While exploring the application, I noticed that the profile URL contained a parameter:
 
http://<MACHINE_IP>/profile.php?user=testuser

I suspected that changing the `user` parameter might allow me to view other users' profiles.

---

## 4. Exploitation – IDOR

I changed the parameter from `testuser` to `admin`:
 
http://<MACHINE_IP>/profile.php?user=admin

**Result:** The page loaded the admin's profile, which contained the flag.

---

## 5. Flag

**Flag:**
 
flag{66be95c478473d91a5358f2440c7af1f}

---

## 6. Mistakes & Challenges Faced

1. **Understanding IDOR:**  
   At first, I didn't realize that the `user` parameter was vulnerable. I tried other parameters like `id` and `user_id` before settling on `user`.

2. **Incorrect flag format:**  
   I initially entered the flag with extra spaces or missing characters. I learned to copy it exactly as shown.

3. **Weak internet connection:**  
   The application loaded slowly at times. I had to be patient and retry.

---

## 7. What I Learned

- **IDOR:** How to exploit insecure direct object references by manipulating URL parameters.
- **Access Control:** The importance of server-side authorization checks.
- **Enumeration:** Always inspect URL parameters for potential vulnerabilities.

---

## 8. Recommendations for Defense

- **Implement proper access controls:** Ensure users can only access their own data.
- **Use indirect references:** Instead of exposing usernames or IDs, use random tokens.
- **Server-side validation:** Never rely on client-side checks for authorization.

---

## 9. References

- [TryHackMe Neighbour Room](https://tryhackme.com/room/neighbour)

---
**Written by:** Salah Eddin Essbihi  
**LinkedIn:** [salah-eddin-essbihi](https://www.linkedin.com/in/salah-eddin-essbihi-911b0443a)  
**TryHackMe:** [cyber.salah.sec](https://tryhackme.com/p/cyber.salah.sec)  
**GitHub:** [salahreds06-selawy](https://github.com/salahreds06-selawy)
 
