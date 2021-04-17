## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:

- Answer: Karl Fitzgerald
Chairman & Chief Executive Officer
Altoro Mutual

- How can this information be helpful to an attacker:
-Answer: attacker can use this info for social engineering compaign


#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located: 
  - Answer: Sunnyvale, CA, USA

  2. What is the NetRange IP address:
  - Answer: 65.61.137.64 - 65.61.137.127

  3. What is the company they use to store their infrastructure:
   -Answer: Rackspace Backbone Engineering

  4. What is the IP address of the DNS server:
  - Answer: 65.61.137.117

#### Step 3: Shodan

- What open ports and running services did Shodan find:
- Answer: 80, 443, 8080 and running services: tcp, http

#### Step 4: Recon-ng

- Install the Recon module `xssed`. 
- Set the source to `demo.testfire.net`. 
- Run the module. 

Is Altoro Mutual vulnerable to XSS: 
- Answer : Yes
(images/xxsed.png)

### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine:
-Answer: nmap -T4 -F --script ftp-vsftpd-backdoor 192.168.0.10
 
- Bonus command to output results into a new text file named `zenmapscan.txt`:

- Zenmap vulnerability script command: 

(images/zenmap.png)

- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:

- Answer: sftpd 2.3.4 downloaded between 20110630 and 20110703 contains a backdoor which opens a shell on port 6200/tcp.
  2. Why is it dangerous:
  - Answer : he attack can be initiated remotely. No form of authentication is required for a successful exploitation

  3. What mitigation strategies can you recommendations for the client to protect their server:

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

