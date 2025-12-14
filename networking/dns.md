# DNS Record Types — Complete Overview

DNS (Domain Name System) records map domain names to IP addresses, services, and metadata that control how traffic is routed and handled on the internet.

---

## **A (Address)**
* → **Maps a domain to an IPv4 address.**
* Example: `example.com → 93.184.216.34`
* Commonly used for websites and servers.

---

## **AAAA (IPv6 Address)**
* → **Maps a domain to an IPv6 address.**
* Example: `example.com → 2606:2800:220:1:248:1893:25c8:1946`
* IPv6 equivalent of an A record.

---

## **CNAME (Canonical Name)**
* → **Aliases one domain name to another.**
* Example: `www.example.com → example.com`
* Cannot coexist with other records on the same name.

---

## **MX (Mail Exchange)**
* → **Routes email to mail servers.**
* Includes priority values (lower number = higher priority).
* Example: `example.com → mail.example.com (priority 10)`

---

## **NS (Name Server)**
* → **Delegates a domain to authoritative DNS servers.**
* Defines who controls DNS records for the domain.

---

## **SOA (Start of Authority)**
* → **Defines DNS zone metadata.**
* Includes primary name server, admin email, serial number, refresh/retry timers.
* Mandatory for every DNS zone.

---

## **TXT (Text)**
* → **Stores arbitrary text data.**
* Common uses:
  * SPF (email validation)
  * DKIM / DMARC
  * Domain verification (Google, AWS, etc.)

---

## **PTR (Pointer)**
* → **Maps an IP address to a domain name (reverse DNS).**
* Used mainly for email server validation.
* Example: `34.216.184.93 → example.com`

---

## **SRV (Service)**
* → **Defines the location of services.**
* Includes priority, weight, port, and target host.
* Used by VoIP, SIP, Microsoft services, etc.

---

## **CAA (Certification Authority Authorization)**
* → **Specifies which Certificate Authorities can issue SSL/TLS certificates.**
* Improves security by preventing unauthorized certificate issuance.

---

## **SPF (Sender Policy Framework)**
* → **Defines which mail servers are allowed to send email.**
* Implemented as a TXT record.
* Helps prevent email spoofing.

---

## **DKIM (DomainKeys Identified Mail)**
* → **Adds cryptographic signatures to emails.**
* Implemented as a TXT record.
* Ensures message integrity and authenticity.

---

## **DMARC (Domain-based Message Authentication)**
* → **Defines email authentication policy and reporting.**
* Implemented as a TXT record.
* Works with SPF and DKIM.

---

## **NAPTR (Naming Authority Pointer)**
* → **Rewrites DNS queries into new domains or services.**
* Used in advanced telecommunication and SIP systems.

---

## **LOC (Location)**
* → **Specifies geographic location of a domain.**
* Rarely used; mostly informational.

---

## **HINFO (Host Information)**
* → **Provides host hardware and OS information.**
* Rarely used due to security concerns.

---

## **SSHFP (SSH Fingerprint)**
* → **Stores SSH public key fingerprints.**
* Allows SSH clients to verify host keys via DNSSEC.

---

## **TLSA (DANE)**
* → **Associates TLS certificates with domain names.**
* Used with DNSSEC for certificate validation.

---

## **DS (Delegation Signer)**
* → **Links parent and child DNS zones in DNSSEC.**
* Establishes a chain of trust.

---

## **DNSKEY**
* → **Contains public keys for DNSSEC.**
* Used to verify DNS record signatures.

---

## **RRSIG**
* → **Cryptographic signature for DNS records.**
* Ensures integrity and authenticity via DNSSEC.

---

## **NSEC / NSEC3**
* → **Proves non-existence of DNS records.**
* Prevents DNS spoofing under DNSSEC.

---

## **OPT (EDNS)**
* → **Extends DNS protocol capabilities.**
* Supports larger payloads and DNS extensions.

---

## **Common DNS Record Groups (Quick Reference)**

* **Web Traffic:** A, AAAA, CNAME
* **Email:** MX, SPF, DKIM, DMARC, PTR
* **Security:** CAA, DNSKEY, DS, RRSIG, TLSA, SSHFP
* **Service Discovery:** SRV, NAPTR
* **Infrastructure:** NS, SOA
* **Metadata:** TXT, LOC, HINFO

---

## **Key Takeaway**
DNS is more than name-to-IP mapping — it is a **critical control plane** for traffic routing, security, email authentication, and service discovery across the internet.
