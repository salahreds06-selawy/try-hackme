# TryHackMe - Packed Light Writeup

## Room Overview
**Room Name:** Packed Light  
**Difficulty:** Easy  
**Category:** Forensics, Network Analysis, Covert Channels  
**Target:** A PCAP file  
**Date Completed:** September 27, 2026  
**Tools Used:** Wireshark, CyberChef, Linux Terminal

---

## 1. Introduction

Packed Light is a forensics challenge that focuses on analyzing network traffic captured from a hotel's guest network. The goal is to identify a covert communication channel used to exfiltrate data.

The room description states:  
*"Tiny packets. Odd hours. Suspiciously regular. Someone's smuggling out the data equivalent of a hotel towel every night, folded neatly inside traffic that looks ordinary until you decode it."*

---

## 2. Initial Analysis

I downloaded the provided PCAP file and opened it in **Wiresharkl**.

### Initial Observations:
- The traffic appeared ordinary at first glance.
- The room hint mentioned:
  - Regular traffic to a specific port.
  - Suspicious request headers.
  - Something related to encryption.

---

## 3. Identifying the Covert Channel

I applied the following Wireshark filter to isolate the suspicious traffic:
 
tcp.port == 8080

This revealed a series of packets communicating on port **8080**, which stood out from the rest of the traffic.

### Analysis of the Packets:
- The traffic was **periodic** and consistent (matching the "clockwork" hint from the room).
- Each request carried a custom HTTP header that looked out of place.

---

## 4. Extracting the Hidden Data

I right-clicked on one of the packets and selected **Follow → HTTP Stream** to view the full conversation.

**Findings:**
- The requests contained a custom header with what appeared to be **Base64-encoded data**.
- The header values were being sent in fragments across multiple requests.

### Example Header:
 
X-Data: VEhNe3RoM19jMHYzcnRfY2g0bm4zMX0=

---

## 5. Decoding the Data

I copied the Base64 string and decoded it using **CyberChef** (or the command line):

```bash
echo "VEhNe3RoM19jMHYzcnRfY2g0bm4zMX0=" | base64 -d
 
Result:
THM{th3_c0v3rt_ch4nn3}
 
 
6. Flag
 
Flag:
THM{th3_c0v3rt_ch4nn3l}
 
 
7. Mistakes & Challenges Faced
1. Filtering the traffic:
At first, I didn't know which port to filter. I learned to look for repeated patterns and unusual ports.
2. Identifying the covert channel:
I initially overlooked the custom HTTP header. After following the TCP stream, the hidden data became visible.
3. Base64 decoding:
I accidentally copied extra characters. I learned to copy the exact string carefully.
4. Internet connectivity:
Slow connection caused delays in downloading the PCAP file. 
 
8. What I Learned
• Network Forensics: Analyzing PCAP files with Wireshark.
• Covert Channels: How attackers hide data in HTTP headers.
• Base64 Decoding: Using CyberChef and command-line tools.
• Filtering Traffic: Using Wireshark filters to isolate suspicious packets. 
 
9. Recommendations for Defense
• Inspect HTTP headers: Look for unusual or custom headers in network traffic.
• Monitor periodic traffic: Covert channels often use regular timing patterns.
• Use DLP solutions: Data Loss Prevention tools can detect exfiltration attempts.
• Encrypt and authenticate: Use HTTPS with strong TLS to prevent header inspection. 
 
10. References
• TryHackMe Packed Light Room
• Wireshark Documentation
• CyberChef 
 
Written by: Salah Eddin Essbihi
LinkedIn: salah-eddin-essbihi
TryHackMe: cyber.salah.sec
GitHub: salahreds06-selawy
