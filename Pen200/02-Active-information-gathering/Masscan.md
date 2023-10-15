#pen200 #active-information-gathering #port-scanning 

---

Masscan is arguably the fastest port scanner; it can scan the entire Internet in about 6 minutes, transmitting an astounding 10 million packets per second! While it was originally designed to scan the entire Internet, it can easily handle a class A or B subnet, which is a more suitable target range during a penetration test.

Consider this demonstration that locates all machines on a large internal network with TCP port 80 open (using the -p80 option). Since masscan implements a custom TCP/IP stack, it will require access to raw sockets and therefore requires sudo.

`sudo masscan -p80 10.0.0.0/8`

To try masscan on a class C subnet in the PWK internal lab network, we can use the following example. We will add a few additional masscan options, including --rate to specify the desired rate of packet transmission, -e to specify the raw network interface to use, and --router-ip to specify the IP address for the appropriate gateway:

`sudo masscan -p80 10.11.1.0/24 --rate=1000 -e tap0 --router-ip 10.11.0.1`







---
links:
[[00-Pen200]]
[[02-Active information gathering]]
[[Port scanning]]
