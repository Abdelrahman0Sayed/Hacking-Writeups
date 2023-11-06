# FowSniff CTF
Easy Tryhackme Free Machine

## Recon 
### First: Run a nmap scan to get the open-ports and services with ```nmap -A -sV -F -T4 10.10.114.172 ```

```
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 90:35:66:f4:c6:d2:95:12:1b:e8:cd:de:aa:4e:03:23 (RSA)
|   256 53:9d:23:67:34:cf:0a:d5:5a:9a:11:74:bd:fd:de:71 (ECDSA)
|_  256 a2:8f:db:ae:9e:3d:c9:e6:a9:ca:03:b1:d7:1b:66:83 (ED25519)
80/tcp  open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Fowsniff Corp - Delivering Solutions
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Apache/2.4.18 (Ubuntu)
110/tcp open  pop3    Dovecot pop3d
|_pop3-capabilities: PIPELINING USER RESP-CODES AUTH-RESP-CODE SASL(PLAIN) TOP UIDL CAPA
143/tcp open  imap    Dovecot imapd
|_imap-capabilities: OK LOGIN-REFERRALS capabilities more post-login have listed IMAP4rev1 ID Pre-login AUTH=PLAINA0001 IDLE ENABLE SASL-IR LITERAL+
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).

```


### So we need to take a look at each service, let's start with HTTP!
### When we visited the website of the machine we noted a critical note: there was a data breach of the employees' credentials on the twitter account 

![](assets/Twitter%20find1.png)


### Then we went to this Twitter account to find these creds and we got this tweet. 
![](assets/twitt.png)


### which redirected us to the breached creds which passwords hash for each user.
![](assets/hashes.png)


### So we need to crack this hashes, you can this website to crack simple hashes ```https://crackstation.net/``` or use hashcat.

![](assets/crackedhashes.png)




### Now, it's your turn pop3!
## Challenge 1: you can use metasploit module to bruteforce pop3 login to know which user use pop3 service.

### Now we need to check emails of this user.

![](assets/pop3.png)

## Challenge 2: use retr command to return the message and the user and pass to make ssh login.
![](assets/meta-scan.png)


## Gaining Access
### We've got username and password to login.

![](assets/ssh-shell.png)


### We noted that the username is a member in a group called <users> so we need to know what this group can do with root perm, just write ``` find / f -group 'users' 2>/dev/null``` 

![](assets/group-permissions.png)

### There's a script called cube.sh we need to take a look 
### IDEA: As long as we can edit this file, we can add a python reverse shell but make sure the system has a python with: ``` which python``` or ``` which python3```


![](assets/Gain-shell.png)  
#This photo from ```https://www.hackingarticles.in/fowsniff-1-vulnhub-walkthrough/``` because i've forgot to take a screenshot to this section :D


### Did you notice something?
### This pattern is the same pattern that appeared when we logged in with ssh, so I think this script running when you log in. 

### So I setup a Netcat listener and logged-in again 
![](assets/Pwned.png)  


### We've got the root privileges.





