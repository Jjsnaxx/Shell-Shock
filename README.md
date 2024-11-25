

<h2>Shell-Shock</h2>


<h3>Overview:</h3>

OWASP Top 10 is an awareness document that outlines the most critical security risks to web applications. Pentesting is performed according to the OWASP TOP 10 standard to reduce or mitigate security risks.
In this lab, we will focus on OWASP A9 Using Components with Known Vulnerabilities flaws, and we will perform an attack against a web server that is vulnerable to CVE-2014-6071.

<h3>Lab Environment:</h3>
In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at demo.ine.local.

Objective: Exploit the vulnerability and execute arbitrary commands on the target machine.

<h3>Tools:</h3>
- Nmap
- BurpSuite

<br />

<p align="center">
  
<h2>Questions:</h2>
   
Q1. As an analyst, you need to submit details to the CTI team. What is the signature left by the threat actor that compromised the website? (2 points)

- We investigate the 'after.jpg' file. At the bottom right hand side we can see the answer.
<img src="https://i.imgur.com/2HxuPKQ.png" height="80%" width="80%" alt="after.jpg"/>

Answer: Team ApashKirikiri2.0

<br />
<br />

Q2. The attacker deleted some files. What are they? (Alphabetical order based on filename) (2 points)

- We investigate the 'Fim2.jpg' file and we can see two files were deleted with rule id 553.


<img src="https://i.imgur.com/nypU4P0.png" height="80%" width="80%" alt="deleted files"/>

Answer: Access_log, Error_log

<br />
<br />

Q3. What is the scanner used by the attacker to identify the vulnerability? (3 points)

- Start by going through our available fields. It is pretty limited in what we can search for.
<img src="https://i.imgur.com/6GgHyDd.png" height="10%" width="20%" alt="fields"/>


- So I start filtering with 'verb' aka HTTP commands. Removing GET and POST and making sure a verb 'exists'. I start looking at each individual command for suspicious logs. Dropped the log count to 26.
<img src="https://i.imgur.com/HHd9Mnl.png" height="80%" width="80%" alt="deleted files"/>


- From the remaining logs there are 2 suspicious events. 
<img src="https://i.imgur.com/JDWXUJo.png" height="80%" width="80%" alt="suspicious log"/>
<img src="https://i.imgur.com/EndWCuh.png" height="80%" width="80%" alt="suspicious log"/>

- A quick search through google helps us find what NIKTO is. 
<img src="https://i.imgur.com/gFSOcmt.png" height="80%" width="80%" alt="nikto"/>


Answer: Nikto

<br />
<br />

Q4. Which PHP page is vulnerable to Remote File Inclusion (RFI)? (2 points)

- Personally had no idea what RFI was and how it worked. So I did a quick google search.
- According to google: "RFI is a type of vulnerability that allows an attacker to include a remote file, usually through a script on the web server. This can occur due to improper handling of user inputs in the PHP code, particularly in functions or statements that include files."
Cool. So I'm going to try look for a file that was downloaded from a suspicious site.
- So the verb I filter for is 'GET' looking for any suspicious PHP file. Pretty much immediately I find a suspicious sounding file called 'backdoor.jpg.php'. 
<img src="https://i.imgur.com/sL728vf.png" height="100%" width="100%" alt="RFI"/>

- Filtering for backdoor.jpg.php we find out it was downloaded through mediafire with a parameter called getimageonly.php.
<img src="https://i.imgur.com/SH7w7dr.png" height="80%" width="80%" alt="fields"/>

Answer: getimagesonly.php

<br />
<br />

Q5. What is the IP address of the remote attacker? (3 points)

- I just looked at the IP that was trying to download the suspicious file from the previous question.
<img src="https://i.imgur.com/5plWK7E.png" height="80%" width="80%" alt="attacker IP"/>

Answer: 91.192.103.35

<br />
<br />

Q6. What is the name of the PHP shell? (2 points)

- I had no clue what a PHP shell was either so I had to do some research on that.
- According to google: "HP Shell or Shell PHP is a program or script written in PHP (Php Hypertext Preprocessor) which provides Linux Terminal (Shell is a much broader concept) in Browser. PHP Shell lets you to execute most of the shell commands in browser, but not all due to its limitations"
- Cool so I knew to look for a PHP file, lucky for me I had a good idea where to look. 'backdoor.jpg.php'. Clearly a suspicious sounding PHP file pretending to be a JPG file.

Answer: backdoor.jpg.php

<br />
<br />

Q7. The attacker downloaded the PHP shell from a file-hosting website. What is the name of the website? (2 points)

- This ones pretty self explanatory, we saw from question 4 where the file was downloaded from.

Answer: mediafire.com

<br />
<br />

Q8. What time was the first command executed through the PHP shell? (3 points)

-We search through the logs with the PHP shell file. Looking at the time from when it was downloaded onwards. I can see the command 'whoami'

<img src="https://i.imgur.com/VVy2iDI.png" height="80%" width="80%" alt="first command"/>

Answer: 18/02/2021 11:42:44

<br />
<br />

Q9. Which config file does the attacker attempt to read using the command 'cat'? (2 points)

-The keywords I was looking for was cat and config file.  I filtered for "backdoor.jpg.php" and "cat"
<img src="https://i.imgur.com/2pnmg2v.png" height="80%" width="80%" alt="first command"/>

Answer: lampp/htdocs/MikePharmaSystem/config.php

<br />
<br />

Q10. At what time was the database dumped by the attacker? (2 points)

-A quick google search tells me a database dump file extension would be db or dump. So I try filtering for those two. I find a log with the message saying 'db_export.php'.
<img src="https://i.imgur.com/uVFcwlb.png" height="80%" width="80%" alt="first command"/>

Answer: 18/02/2021 11:44:59

<br />
<br />

Q11. The attacker exfiltrated the database records. What is the database name? (Just the name, without any extension) (2 points)

-I look at the details of the request to export the database. I can see the name of the database.
<img src="https://i.imgur.com/TEGkniV.png" height="80%" width="80%" alt="first command"/>

Answer: Mike_Pharmaceuticals











<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
