#pen200 #active-information-gathering 

---

**DNSRecon**

DNSRecon is an advanced, modern DNS enumeration script written in Python. Running dnsrecon against megacorpone.com using the -d option to specify a domain name, and -t to specify the type of enumeration to perform (in this case a zone transfer)

`dnsrecon -d megacorpone.com -t axfr`

To begin the brute force attempt, we will use the -d option to specify a domain name, -D to
specify a file name containing potential subdomain strings, and -t to specify the type of
enumeration to perform (in this case brt for brute force)

`dnsrecon -d megacorpone.com -D ~/list.txt -t brt`


**DNSEnum**:

DNSEnum is another popular DNS enumeration tool. To show a different output, let’s run dnsenum against the zonetransfer.me domain (which is owned by DigiNinja194 and specifically allows zone transfers)

`dnsenum zonetransfer.me`

---
links
[[00-Pen200]]
[[02-Active information gathering]]
[[Dns Enumeration]]
