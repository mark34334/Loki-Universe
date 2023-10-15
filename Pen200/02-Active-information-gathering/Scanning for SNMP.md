#pen200 #active-information-gathering #snmp-enumeration 

---

To scan for open SNMP ports, we can run nmap as shown in the example that follows. The -sU
option is used to perform UDP scanning and the --open option is used to limit the output to only
display open ports:

`sudo nmap -sU --open -p 161 10.11.1.1-254 -oG open-snmp.txt`

```
kali@kali:~$ sudo nmap -sU --open -p 161 10.11.1.1-254 -oG open-snmp.txt
Starting Nmap 7.70 ( https://nmap.org ) at 2019-05-01 06:26 MDT
Nmap scan report for 10.11.1.7
Host is up (0.080s latency).
PORT
STATE
SERVICE
161/udp open|filtered snmp
MAC Address: 00:50:56:89:1A:CD (VMware)
Nmap scan report for 10.11.1.10
Host is up (0.080s latency).
PORT STATE SERVICE
161/udp open|filtered snmp
MAC Address: 00:50:56:93:4E:DC (VMware)
```

Alternatively, we can use a tool such as **onesixtyone**

Which will attempt a brute force attack against a list of IP addresses. First we must build text files containing community strings and the IP addresses we wish to scan:

```
kali@kali:~$ echo public > community
kali@kali:~$ echo private >> community
kali@kali:~$ echo manager >> community
kali@kali:~$ for ip in $(seq 1 254); do echo 10.11.1.$ip; done > ips
kali@kali:~$ onesixtyone -c community -i ips
```

---
links:
[[00-Pen200]]
[[02-Active information gathering]]
[[SNMP Enumeration]]
