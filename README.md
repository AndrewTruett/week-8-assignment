# Project 8 - Pentesting Live Targets

Time spent: **5** hours spent in total

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

Vulnerability #1: SQLI
For this attack, login and navigate to a salespersons information. In the URL, replace the id as your SQL injection. In this case, I added `' OR SLEEP(10) = 0 -- '`. This will make the webpage load for 10 seconds when refreshed. In this case, I timed how long the webpage loaded after refreshing, and it took approximately 10 seconds, which indicates the attack was successful.
<img src="https://media.giphy.com/media/2AKMsJjfRDpEq1D7C4/giphy.gif" />

Vulnerability #2: Session Hijacking/Fixation
Using a tool provided by the site `public/hacktools/change_session_id.php` I was able to obtain and change the session ID for a given session. In Chrome, I logged in, and then copied that session ID. Then I opened an entirely new browser, and used the tool to change my session ID to the same one I got in Chrome. Once the session ID was changed, I was able to click login, and I was immediately logged in without the need for a username or password.
<img src="https://media.giphy.com/media/QJsUDwH1uZTfTOqElo/giphy.gif" />


## Green

Vulnerability #1: __________________

Vulnerability #2: __________________


## Red

Vulnerability #1: __________________

Vulnerability #2: __________________


## Notes

Describe any challenges encountered while doing the work
