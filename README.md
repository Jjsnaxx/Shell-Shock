

<h2>Shell-Shock</h2>


<h3>Overview:</h3>

OWASP Top 10 is an awareness document that outlines the most critical security risks to web applications. Pentesting is performed according to the OWASP TOP 10 standard to reduce or mitigate security risks.
In this lab, we will focus on OWASP A9 Using Components with Known Vulnerabilities flaws, and we will perform an attack against a web server that is vulnerable to CVE-2014-6071.

<h3>Lab Environment:</h3>
In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at demo.ine.local.

<h3>Objective:</h3>
Exploit the vulnerability and execute arbitrary commands on the target machine.

<h3>Tools:</h3>

[Nmap](https://nmap.org/) <br />
[BurpSuite](https://portswigger.net/burp/documentation/desktop/getting-started/download-and-install) <br />
[NetCat](https://nmap.org/ncat/)

<br />

<p align="center">
  
<h2>Actions:</h2>

- First lets boot up the lab instance.
<img src="https://i.imgur.com/ArGcLEH.jpeg"/>


<br />
<br />

- Next we ping the IP provided to check if it is reachable
<img src="https://i.imgur.com/Bvd4dhX_d.webp?maxwidth=760&fidelity=grand"/>


<br />
<br />

- Nmap SV scan to check what port is being used and what services are online.
<img src="https://i.imgur.com/fiN4EAH_d.webp?maxwidth=760&fidelity=grand"/>


<br />
<br />

- Cool we see that on port 80 there is an Apache web server.
- Lets see what the website looks like. We navigate to demo.ine.local using Firefox.
<img src="https://i.imgur.com/7T7eZVC_d.webp?maxwidth=760&fidelity=grand"/>


<br />
<br />

- On the landing page we see there is a dynamic countdown timer being used. We can assume the web server is using a script to do this.
- Lets check the Web page source.
<img src="https://i.imgur.com/FSIIy4o_d.webp?maxwidth=760&fidelity=grand"/>


<br />
<br />

- We can see that the webpage is using a CGI script called gettime.cgi
- Next I want to check if this CGI script is vulnerable to the shellshock exploit.
- We can do this using a Nmap script called 'http-shellshock' and providing the correct arguments.
<img src="https://i.imgur.com/Imwc761.jpeg"/>


<br />
<br />

- From the Nmap scan we can see that it is vulnerable to the shellshock exploit.
- Lets use BurpSuite to exploit this. First we switch on FoxyProxy.
<img src="https://i.imgur.com/17acyhU.jpeg"/>


<br />
<br />

- Next lets bootup Burpsuite using default configurations.
<img src="https://i.imgur.com/opQIGM4.jpeg"/>


<br />
<br />

- Navigate to the 'Proxy' tab and ensure 'Intercept is on' is selected.
- Forward the request. Send the request to the repeater.
<img src="https://i.imgur.com/rJs20aR_d.webp?maxwidth=760&fidelity=grand"/>
<img src="https://i.imgur.com/uD9A7j6.jpeg"/>


<br />
<br />

- First we try to enumerate the passwd file.
<img src="https://i.imgur.com/w0qFNEv.jpeg"/>


<br />
<br />

- Perfect it works. Let's modify the payload to enumerate the User ID.
<img src="https://i.imgur.com/GttOyvB.jpeg"/>


<br />
<br />

- Lastly let's see what kind of processes are running on this system.
<img src="https://i.imgur.com/nPzH8OJ.jpeg"/>


<br />
<br />

<h3>Conclusion:</h3>
In this lab, we learned about the exploitation of the "Shellshock" vulnerability (CVE-2014-6071) and performed an attack against a web server.


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
