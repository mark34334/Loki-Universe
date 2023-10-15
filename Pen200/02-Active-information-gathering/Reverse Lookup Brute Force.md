#pen200 #active-information-gathering 

---

Our DNS forward brute force enumeration revealed a set of scattered IP addresses in the same approximate range (38.100.193.X). If the DNS administrator of megacorpone.com configured PTR191 records for the domain, we could scan the approximate range with reverse lookups to request the hostname for each IP.

Let’s use a loop to scan IP addresses 38.100.193.50 through 38.100.193.100. We will filter out
invalid results by showing only entries that do not contain “not found” (with grep -v):

  
For example:
```
kali@kali:~$ for ip in $(seq 50 100); do host 38.100.193.$ip; done | grep -v "not
found"
69.193.100.38.in-addr.arpa domain name pointer beta.megacorpone.com.
70.193.100.38.in-addr.arpa domain name pointer ns1.megacorpone.com.
72.193.100.38.in-addr.arpa domain name pointer admin.megacorpone.com.
73.193.100.38.in-addr.arpa domain name pointer mail2.megacorpone.com.
76.193.100.38.in-addr.arpa domain name pointer www.megacorpone.com.
77.193.100.38.in-addr.arpa domain name pointer vpn.megacorpone.com.
......
```
``

We have successfully managed to resolve a number of IP addresses to valid hosts using reverse DNS lookups. If we were performing an assessment, we could further extrapolate these results, and might scan for “mail1”, “mail3”, etc and reverse lookup positive results. 

The point is that these types of scans are often cyclical; we expand our search based on any information we receive at every round.

---
[[00-Pen200]]
[[02-Active information gathering]]
[[Dns Enumeration]]
