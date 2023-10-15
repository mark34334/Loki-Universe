#pen200 #active-information-gathering #smb-enumeration 

---

Nmap contains many useful NSE scripts that can be used to discover and enumerate SMB services. These scripts can be found in the ***/usr/share/nmap/scripts*** directory

`ls -1 /usr/share/nmap/scripts/smb*`

Let’s try the smb-os-discovery module:

`nmap -v -p 139, 445 --script=smb-os-discovery 10.11.1.227`

To check for known SMB protocol vulnerabilities, we can invoke one of the smb-vuln NSE scripts.
We will take a look at smb-vuln-ms08-067, which uses the --script-args option to pass
arguments to the NSE script.

`nmap -v -p 139,445 --script=smb-vuln-ms08-067 --script-args=unsafe=1 10.11.1.5`




---
links:
[[00-Pen200]]
[[02-Active information gathering]]
[[SMB enumaration]]
