#pen200 #active-information-gathering #port-scanning

---

Port scanning is the process of inspecting TCP or UDP ports on a remote machine with the intention of detecting what services are running on the target and what potential attack vectors may exist.

![[Pasted image 20231008103612.png]]


`nc -nv -u -z -w 1 10.11.1.115 160-162`

Most UDP scanners tend to use the standard “ICMP port unreachable” message to infer the status of a target port. However, this method can be completely unreliable when the target port is filtered by a firewall. In fact, in these cases the scanner will report the target port as open because of the absence of the ICMP message.





---
link:
[[00-Pen200]]
[[02-Active information gathering]]
[[Port scanning]]
