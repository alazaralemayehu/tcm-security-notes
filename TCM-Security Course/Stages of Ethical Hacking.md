**There are Fives Stages of Ethical hacking**

1.  Reconnaissance
    - **Active**: Interacting with the system and gathering information
    - **Passive**: Not interacting with the website, Google search, LinkedIn,
2.  Scanning and Enumeration
    - Using Tools to see the existence of Vulnerabilities and issues with the systems
    - Enumeration: Enumeration the vulnerability against the service running systems
3.  Gaining Access (Exploitation)
    - Trying to get an access
4.  Maintain Access
    - Creating a username, having connection to the system
    - Having access even if the system is restarted
5.  Covering tracks
    - Deleting information that directs the investigation to us
    - Penetration Testing

**Information Gathering**

- In information gathering we have two types of reconnaissance: Active and Passive \***\*passive reconnaissance stage\*\***

We focus on finding information from publicly available resources.

- It can be Physical information like Location information (Satellite images, Drone recon, Building layout {badge readers, break areas, smoking areas, security and fencing}).
- It can be Social information Job Information (Employee names, job title, phone number, pictures badge photos, desk photos, computer photos, social media posts).

\***\*Active reconnaissance stage\*\***

We interact with the system actively to know about the services and information about our target. Looking for open ports, subdomains, fingerprinting, trying to connect, pinging...

**Target Validation** (WHOIS, nslookup, dnsrecon), **finding subdomains** (Google Fu, dig, Nmap, Bluto, Sublist3r, crt.sh), **Fingerprinting** (Nmap, Wappalyzer, WhatWeb, BuiltWith, Netcat) and **Finding Data Breaches** (HaveIBeenPwned, Breach-Parse, WeLeakInfo)

**Discovering Email addresses:** useful for marketing and phishing.
\- Finding the pattern of the email (hunter.io)
\- Finding exact email address (phonebook.cz)
\- Check the existence of the email
\- check forget password feature to check connected emails.

```
Tools
```

- https://www.voilanorbert.com/
- https://phonebook.cz/
- https://hunter.io/
- https://clearbit.com/
- https://tools.emailhippo.com/ (To verify email)
- https://email-checker.net/ (To verify email)

```
password and breach database
```

- dehashed.com
- hash.com
  Sub-domain Hunting tools
- sublist3r
- crt.sh
- OWASP Amass
  Check technologies used in website
- builtwith
- wapplyzer
- whatweb
- Burpsuite (Web Proxy => Helps us to intercept request)

Social media information gathering

- Look for photos from LinkedIn and Twitter
- Find people who work in the company from LinkedIn

To discover machines on the network we can use:
apr-scan -interface=InterfaceName -l
netdiscover tool
