#pen200 #active-information-gathering

----

host -- to find ip address of the website

Each domain can use different types of DNS records. Some of the most common types of DNS records include:
	•NS - Nameserver records contain the name of the authoritative servers hosting the DNS
	records for a domain.
	•A - Also known as a host record, the “a record” contains the IP address of a hostname (such as www.megacorpone.com).
	•MX - Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records.
	•PTR - Pointer Records are used in reverse lookup zones and are used to find the record associated with an IP address.
	•CNAME - Canonical Name Records are used to create aliases for other host records.
	•TXT - Text records can contain any arbitrary data and can be used for various purposes,
	such as domain ownership verification.

> host -t mx findme.com
> host findme.com



-----

[[Dns Enumeration]]
[[00-Pen200]]
[[02-Active information gathering]]