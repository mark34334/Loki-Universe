#pen200 #active-information-gathering 

---
Brute force is a trial-and-error technique that seeks to find valid information, including directories on a webserver, username and password combinations, or in this case, valid DNS records. By using a wordlist that contains common hostnames, we can attempt to guess DNS records and check the response for valid hostnames.

**For example**
kali@kali:~$ cat list.txt
www
ftp
mail
owa
proxy
router

kali@kali:~$ **for ip in $(cat list.txt); do host $ip.megacorpone.com; done**
www.megacorpone.com has address 38.100.193.76
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 38.100.193.84
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 38.100.193.71


----
[[00-Pen200]]
[[02-Active information gathering]]
[[Dns Enumeration]]

