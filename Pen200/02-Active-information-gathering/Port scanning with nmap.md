#pen200 #active-information-gathering #nmap

---

What is iptables?

Iptables is a command-line tool that is used to configure the Linux firewall. It allows you to control which network traffic is allowed to enter and exit your system. Iptables is a powerful tool that can be used to protect your system from attack, but it can also be complex to use.

**commands**

	`sudo iptables -I INPUT 1 -s 10.11.1.220 -j ACCEPT`

	`sudo iptables -I OUTPUT 1 -d 10.11.1.220 -j ACCEPT`

	`sudo iptables -Z`


Now let’s generate some traffic using nmap:

	nmap 10.11.1.220

Stealth / SYN Scanning;

	`sudo nmap -sS 10.11.1.220`

TCP Connect Scanning:

	`nmap -sT 10.11.1.220`

UDP Scanning:

	`sudo nmap -sU 10.11.1.115`

	`sudo nmap -sS -sU 10.11.1.115`

Network Sweeping:

	`nmap -sn 10.11.1.1-254`

Searching for live machines using the grep command on a standard nmap output can be cumbersome. Instead, let’s use Nmap’s “greppable” output parameter, -oG, to save these results into a format that is easier to manage:

	`nmap -v -sn 10.11.1.1-254 -oG ping-sweep.txt`

	`grep Up ping-sweep.txt | cut -d " " -f 2`

	`nmap -p 80 10.11.1.1-254 -oG web-sweep.txt`

	`grep open web-sweep.txt | cut -d" " -f2`

	`nmap -sT -A --top-ports=20 10.11.1.1-254 -oG top-port-sweep.txt`

	`cat /usr/share/nmap/nmap-services`

**OS Fingerprinting**

	`sudo nmap -O 10.11.1.220`

**Banner Grabbing/Service Enumeration**

	`nmap -sV -sT -A `10.11.1.220`

**Nmap Scripting Engine (NSE)**

	`nmap 10.11.1.220 --script=smb-os-discovery`

	`nmap --script=dns-zone-transfer -p 53 ns2.megacorpone.com`











---
links:
[[00-Pen200]]
[[02-Active information gathering]]
[[Port scanning]]
