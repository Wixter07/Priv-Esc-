# Wonderland

`Target IP - 10.10.105.226`

## nmap
```console
┌──(wixter07㉿krakenbone)-[~/Downloads]
└─$ nmap -sV -sC 10.10.70.234
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-06 14:55 EST
Nmap scan report for 10.10.70.234
Host is up (0.18s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8e:ee:fb:96:ce:ad:70:dd:05:a9:3b:0d:b0:71:b8:63 (RSA)
|   256 7a:92:79:44:16:4f:20:43:50:a9:a8:47:e2:c2:be:84 (ECDSA)
|_  256 00:0b:80:44:e6:3d:4b:69:47:92:2c:55:14:7e:2a:c9 (ED25519)
80/tcp open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Follow the white rabbit.
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.40 seconds
```

So we need to ssh into port 22.

## Analysis

Launched the IP on browser

![Screenshot from 2024-11-06 14-59-01](https://github.com/user-attachments/assets/18c08742-226e-4b70-ae61-cf3d53c7d082)

Aight time to goubster with common.txt

```console
┌──(wixter07㉿krakenbone)-[~/Downloads]
└─$ gobuster dir -u "http://10.10.70.234/" -w common.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.70.234/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/img                  (Status: 301) [Size: 0] [--> img/]
/index.html           (Status: 301) [Size: 0] [--> ./]
/r                    (Status: 301) [Size: 0] [--> r/]
/render/https://www.google.com (Status: 301) [Size: 0] [--> /render/https:/www.google.com]
Progress: 4734 / 4735 (99.98%)
===============================================================
Finished
===============================================================
```


/r had 
![Screenshot from 2024-11-06 15-07-24](https://github.com/user-attachments/assets/b6a2811e-9a6e-4f39-8c2e-7ab218156252)

Nothing quite intereseting

/img had the juice. Three image files alice_door.jpg, alice_door.png, white_rabbit_1.jpg

White rabbit
![image](https://github.com/user-attachments/assets/d677f86c-d63c-4b2c-9282-b4768ac5d21d)

Wasn't able to access the other two images directly so wget it.

Hmm hmm hmm. Nothing in the image tbh. I'll run gobuster with big.txt lmao.



