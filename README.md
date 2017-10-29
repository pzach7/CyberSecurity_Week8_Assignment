# CyberSecurity_Week8_Assignment

# Project 8 - Pentesting Live Targets

Time spent: **12** hours spent in total

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

Vulnerability #2: Session Hijacking/Fixation

  - [x] Summary: The blue machine is vulnerable to session highjacking/fixation using the given PHP change session tool, allowing admin access. The first GIF shows session fixation, the second shows session hijacking. In both scenarios the Chrome browser is the attacker, and the Firefox browser is the victim
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/1FpJZAy.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/Chq9oxx.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Follow the instructions listed on the Assignment week 8 page "Use two different web browsers (e.g., Firefox and Chrome). Let one browser be the attacker and the other the target. Choose if you want to attempt a session hijacking or session fixation. For hijacking, log the target in first, then give the logged-in session ID to the attacker. For fixation, get a session ID for the attacker, give it to the target, then the target will log in. In both cases, the attacker should now have access to the staff area."

## Green

Vulnerability #1: Cross-Site Scripting (XSS)
  - [x] Summary: The feedback field is vulnerable to Stored XSS attacks
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/CQbR5hz.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Enter a simple script command in the feedback field such as <script>alert('Zach Puderbach found the XSS!');</script> and submit. Then when an admin/user goes to view the feedback forms, the script is executed and a popup appears

Vulnerability #2: Username Enumeration 

  - [x] Summary: The login error message shows "Log in was unsuccessful." (Not bolded) when the user does not exist, and "**Log in was unsuccessful.**" (Bolded) if the user exists
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/MbEQpvw.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Go to the login page on the Green machine, and enter existing usernames (as a baseline), and note the error message is bolded. To test if a username exists or not, just enter in a username and anything in the password field, and if the error message is bold, the username exists, otherwise if it is not bolded, it doesn't exist

## Red

Vulnerability #1: Insecure Direct Object Reference (IDOR)

  - [x] Summary: The ID field on the salesperson page is directly accessible, allowing anyone to change it and view all salespeople
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/YCN6bga.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Go the the "Find a Salesperson" Page and click on any salesperson. Directly change the ID number to 10 or 11 to see salespeople that aren't supposed to be public.

Vulnerability #2: Cross-Site Request Forgery (CSRF)

  - [x] Summary: The CSRF token isn't checked properly when submitting post requests, allowing anyone knowing the URL and Session ID of a logged in admin to make admin changes
  - [x] GIF Walkthrough: <img src='https://i.imgur.com/PYqhVPL.gif' title='GIF Walkthrough' width='' alt='GIF Walkthrough' />
  - [x] Steps to recreate: Obtain the Session ID of a logged in admin, create a post request to edit a state (In my case Alaska), you can put anything in the csrf token field since it isn't properly checked. Then just submit the POST request. The change will only notice once the page that was changed is reloaded.

## Notes

Most of the challenges I faced while performing this assignment were due to my assumptions, the vulnerabilities were not in the places I initially expected them to be. For example, I expected the SQL injection vulnerability to be in a user input field, not directly in a URL.
