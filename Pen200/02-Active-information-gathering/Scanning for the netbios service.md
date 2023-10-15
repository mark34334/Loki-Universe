#pen200 #active-information-gathering #smb-enumeration 

---

The NetBIOS210 service listens on TCP port 139 as well as several UDP ports. It should be noted that SMB (TCP port 445) and NetBIOS are two separate protocols. NetBIOS is an independent session layer protocol and service that allows computers on a local network to communicate with each other. While modern implementations of SMB can work without NetBIOS, NetBIOS over TCP (NBT)211 is required for backward compatibility and is often enabled together. For this reason, the enumeration of these two services often goes hand-in-hand. These can be scanned with tools like nmap, using syntax similar to the following:

`nmap -v -p 139,445 -oG smb.txt 10.11.1.1-254`

There are other, more specialized tools for specifically identifying NetBIOS information, such as nbtscan, which is used in the following example. The -r option is used to specify the originating UDP port as 137, which is used to query the NetBIOS name service for valid NetBIOS names:

`sudo nbtscan -r 10.11.1.0/24`



---
links
[[00-Pen200]]
[[02-Active information gathering]]
[[SMB enumaration]]
