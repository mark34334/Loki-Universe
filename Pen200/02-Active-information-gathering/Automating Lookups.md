#pen200 #active-information-gathering 

---

Now that we have some initial data from the megacorpone.com domain, we can continue to use additional DNS queries to discover more hostnames and IP addresses belonging to the same domain. For example, we know that the domain has a web server, with the hostname
“www.megacorpone.com”

kali@kali:~$ host idontexist.megacorpone.com
Host idontexist.megacorpone.com not found: 3(NXDOMAIN)

In Listing 212, we queried a valid hostname and received an IP resolution response. By contrast, Listing 213 returned an error (NXDOMAIN189) that indicated that a public DNS record does not exist for that hostname. Now that we understand how to search for valid hostnames, we can automate our efforts.

---
[[Dns Enumeration]]
[[00-Pen200]]
[[02-Active information gathering]]