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



### So we need to take a look in each service, let's start with HTTP!
### When we visited the website of the machine we noted a critical note: there a data breach of the employees' credentials at the twitter account 

![](assets/Twitter%20find1.png)


### Then we gone to this twitter account to find this creds and we got this twitt 
![](assets/twitt.png)


### which is redirected us into the breached creds which password's hash for each user..
![](assets/hashes.png)


### So we need to crack this hashes, you can this website to crack simple hashes ```https://crackstation.net/``` or use hashcat.

![](assets/crackedhashes.png)



