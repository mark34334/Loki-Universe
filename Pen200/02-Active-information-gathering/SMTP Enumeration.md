#pen200 #active-information-gathering #smtp-enumeration

---

We can also gather information about a host or network from vulnerable mail servers. The Simple
Mail Transport Protocol (SMTP)216 supports several interesting commands, such as VRFY and
EXPN. A VRFY request asks the server to verify an email address, while EXPN asks the server for
the membership of a mailing list. These can often be abused to verify existing users on a mail
server.

```
kali@kali:~$ nc -nv 10.11.1.217 25
(UNKNOWN) [10.11.1.217] 25 (smtp) open
220 hotline.localdomain ESMTP Postfix
VRFY root
252 2.0.0 root
VRFY idontexist
550 5.1.1 <idontexist>: Recipient address rejected: User unknown in local recipient
table
```

In an automated fashion:
	Consider the following Python script that opens a TCP socket, connects to the SMTP server, and issues a VRFY command for a given username

```
#!/usr/bin/python
import socket
import sys
if len(sys.argv) != 2:
	print "Usage: vrfy.py <username>"
	sys.exit(0)
# Create a Socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# Connect to the Server
connect = s.connect(('10.11.1.217',25))
# Receive the banner
banner = s.recv(1024)
print banner
# VRFY a user
s.send('VRFY ' + sys.argv[1] + '\r\n')
result = s.recv(1024)
print result
# Close the socket
s.close()
```


---
links:
[[00-Pen200]]
[[02-Active information gathering]]
[[SMTP Enumeration]]
