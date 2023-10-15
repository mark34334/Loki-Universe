#pen200 #active-information-gathering #snmp-enumeration 

---

***snmpwalk*** provided we at least know the SNMP read-only community string, which in most cases is “public”.


Enumerating the Entire MIB Tree:

Windows SNMP port exposed with the community string “public”. This command enumerates the entire MIB tree using the -c option to specify the community string, and -v to specify the SNMP version number as well as the -t 10 to increase the timeout period to 10 seconds:

`snmpwalk -c public -v1 -t 10 10.11.1.14`

Enumerating Windows Users;

`snmpwalk -c public -v1 10.11.1.14 1.3.6.1.4.1.77.1.2.25`

Enumerating Running Windows Processes:

`snmpwalk -c public -v1 10.11.1.73 1.3.6.1.2.1.25.4.2.1.2`

Enumerating Open TCP Ports:

`snmpwalk -c public -v1 10.11.1.14 1.3.6.1.2.1.6.13.1.3`

Enumerating Installed Software;

`snmpwalk -c public -v1 10.11.1.50 1.3.6.1.2.1.25.6.3.1.2`

---
link:
[[00-Pen200]]
[[02-Active information gathering]]
[[SNMP Enumeration]]
