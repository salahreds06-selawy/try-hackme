# TryHackMe - OhSINT Writeup

## Room Overview
**Room Name:** OhSINT  
**Difficulty:** Easy  
**Category:** OSINT, Open-Source Intelligence  
**Target:** A single image file  
**Date Completed:** September 27, 2026  
**Tools Used:** ExifTool, Web Browser, Social Media, Google

---

## 1. Introduction

OhSINT is an OSINT (Open-Source Intelligence) challenge. The goal is to extract as much information as possible from a single image file and use it to answer a series of questions.

---

## 2. Initial Analysis

I downloaded the provided image file (`WindowsXP_1551719014755.jpg`). The first step was to extract metadata using **ExifTool**.

### Command Used:
```bash
exiftool WindowsXP_1551719014755.jpg
 
Findings:
• Copyright: Woodflint
• GPS Coordinates: 54°17'41.27"N, 2°15'1.33"W (a location in the UK) 
 
3. OSINT Investigation
 
3.1 Searching for the Username
 
I searched for the username "Woodflint" on Google and social media platforms.
 
Findings:
• A Twitter account: @Woodflint
• A GitHub account: Woodflint
• A personal blog or website 
3.2 Exploring the Twitter Account
 
The Twitter account contained a tweet with a GitHub link.
 
3.3 Exploring the GitHub Account
 
The GitHub profile had a repository with a README that contained an email address: OWoodflint@gmail.com.
 
3.4 Finding the City
 
Using the GPS coordinates from the image metadata, I identified the city as London.
 
3.5 Finding the SSID
 
The GitHub README also mentioned a Wi-Fi network: UnileverWiFi.
 
3.6 Finding the Holiday Destination
 
The Twitter account had a tweet mentioning a holiday in New York.
 
3.7 Finding the Password
 
The GitHub repository contained a file with a password: pennYDr0pper.!. 
 
4. Answers
• User's avatar: cat
• City: London
• SSID of the WAP: UnileverWiFi
• Personal email: OWoodflint@gmail.com
• Site where email was found: GitHub
• Holiday destination: New York
• Password: pennYDr0pper.! 
 
5. Mistakes & Challenges Faced
1. Understanding EXIF Data:
I initially didn't know how to extract metadata. I learned to use exiftool.
2. Searching efficiently:
I had to try multiple search queries to find the correct social media accounts.
3. Weak internet connection:
Slow internet made some searches time-consuming. I learned to be patient. 
 
6. What I Learned
• How to extract metadata from images using ExifTool.
• How to use OSINT techniques to find information about a person.
• The importance of checking social media and code repositories for leaked data.
• How to correlate multiple pieces of information to answer specific questions. 
 
7. Recommendations for Defense
• Strip metadata from images before uploading them online.
• Avoid posting sensitive information on social media or public repositories.
• Use strong, unique passwords and never store them in plaintext.
• Be mindful of what you share online, as it can be used against you. 
 
8. References
• TryHackMe OhSINT Room
• ExifTool Documentation 
 
Written by: Salah Eddin Essbihi
LinkedIn: salah-eddin-essbihi
TryHackMe: cyber.salah.sec
GitHub: salahreds06-selawy
