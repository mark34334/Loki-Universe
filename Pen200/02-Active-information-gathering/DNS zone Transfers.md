#pen200 #active-information-gathering 

----

A zone transfer is basically a database replication between related DNS servers in which the zone file is copied from a master DNS server to a slave server. The zone file contains a list of all the DNS names configured for that zone. Zone transfers should only be allowed to authorised slave DNS servers but many administrators misconfigure their DNS servers, and in these cases, anyone asking for a copy of the DNS server zone will usually receive one.

`host -l <domain name> <dns server address>`

`host -l megacorpone.com ns2.megacorpone.com`

`host -t ns megacorpone.com | cut -d " " -f 4`

```
#!/bin/bash

# Simple Zone Transfer Bash Script
# $1 is the first argument given after the bash script
# Check if argument was given, if not, print usage
if [ -z "$1" ]; then
	echo "[*] Simple Zone transfer script"
	echo "[*] Usage
	: $0 <domain name> "
	exit 0
fi
# if argument was given, identify the DNS servers for the domain
for server in $(host -t ns $1 | cut -d " " -f4); do
	# For each of these servers, attempt a zone transfer
	host -l $1 $server |grep "has address"
done
```

`./dns-axfr.sh megacorpone.com`

---
links:
[[00-Pen200]]
[[02-Active information gathering]]
[[Dns Enumeration]]
