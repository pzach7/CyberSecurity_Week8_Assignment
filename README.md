# CyberSecurity_Week8_Assignment

# Project 8 - Pentesting Live Targets

Time spent: **X** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQL Injection (SQLi)

  - [x] GIF Walkthrough: <img src='https://i.imgur.com/TYNn5av.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Heads up, the GIF is a long one. The short version is, I was looking through GET URL fields, and found the salesperson one. I first tested to see if it was vulnerable with a simple "id=3' or '1'='1" until I got the webpage to "break" when I used "id=3 or '1'='1". This revealed "Database Query Failed" showing the database field was vulnerable. I then ran the full URL through sqlmap for confirmation and database information
  - [x] sqlmap results: Database type = MySql, Databases found: [*] globitek_blue, globitek_green, globitek_red, information_schema, mysql, performance_schema, sys

Vulnerability #2: __________________


## Green

Vulnerability #1: Cross-Site Scripting (XSS)
  - [x] Summary: The feedback field is vulnerable to Stored XSS attacks
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/CQbR5hz.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Enter a simple script command in the feedback field such as <script>alert('Zach Puderbach found the XSS!');</script> and submit. Then when an admin/user goes to view the feedback forms, the script is executed and a popup appears

Vulnerability #2: __________________


## Red

Vulnerability #1: __________________

RED ALLOWS FOR REUSE OF TOKENS IN CONTACT PHP

Vulnerability #2: __________________

##Other

Vulnerability #1: Cross-Site Scripting (XSS)

- [x] Summary: All three sites are vulnerable to Reflected attacks under the territory field

## Notes

Most of the challenges I faced while performing this assignment were due to my assumptions, the vulnerabilities were not in the places I initially expected them to be. For example, I expected the SQL injection vulnerability to be in a user input field, not directly in a URL.
