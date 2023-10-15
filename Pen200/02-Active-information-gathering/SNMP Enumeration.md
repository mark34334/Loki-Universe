#pen200 #active-information-gathering #snmp-enumeration 

---

we have often found that the Simple Network Management Protocol (SNMP) is
not well-understood by many network administrators. This often results in SNMP
misconfigurations, which can result in significant information leakage.

SNMP is based on UDP, a simple, stateless protocol, and is therefore susceptible to IP spoofing
and replay attacks. In addition, the commonly used SNMP protocols 1, 2, and 2c offer no traffic
encryption, meaning that SNMP information and credentials can be easily intercepted over a local
network. Traditional SNMP protocols also have weak authentication schemes and are commonly
left configured with default public and private community strings.

---
Links:
[[00-Pen200]]
[[02-Active information gathering]]
[[SNMP Enumeration]]
