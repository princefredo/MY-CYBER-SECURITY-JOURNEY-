this folder will contain my notes on cybersecurity tools like;
- Nmap .md
- Burpsuite .md
- Goburster .md
# NMAP
## WHAT IS NMAP
Nmap is a network scanning tool used to discover devices and services.
## COMMANDS I USED 
- Nmap -sn ==> 10.0.2.0/24
- nmap -sv ==> 10.0.2.2
- ## WHAT EACH COMMAND DOES
- -sn ==> finds active devices
- -sv ==> detects service versions
- ip a ==> displays all netwoerk interfaces and their ip addresses.
 ## OBSERVATIONS
 - i discovered multiple devices on my network
 - Each device has a unique IP
 - # KEY LEARNING
 - nmap can discover active devices
 - it shows open port
 - it reveals running testing
 ## REAL USE
   Used in reconnaissance phase of penetration testing

---

# DEEP RECONNAISSANCE WITH NMAP

## AGGRESSIVE SCAN 
Command:
nmap -A <10.0.2.2>
Example:
nmap -A 10.0.2.2
## PURPOSE OF -A
The `-A` option enables:
- OS detection
- Service version detection
- Script scanning
- Traceroute
Used for gathering deeper intelligence about a target system.
## PORT STATE
 OPEN
- A service is actively running and accepting connections
- Does NOT automatically mean vulnerable
Example:
445/tcp open smb
 CLOSED
- The port is reachable
- But no service is listening
 FILTERED
- The port is hidden or blocked
- Usually caused by firewall or NAT filtering
## IMPORTANT SECURITY CONCEPT
Open Port ≠ Vulnerability
An open port only means:
- A service is available
- Further investigation is required
## PENETRATION TESTER THINKING 
When discovering an open port:
1. What service is running?
2. What version is running?
3. Is it outdated or vulnerable?
4. Is authentication weak?
5. Can the service be interacted with?
# COMMON PORTS
| Port | Service | Purpose |
|------|----------|----------|
| 22 | SSH | Remote login |
| 80 | HTTP | Website traffic |
| 443 | HTTPS | Secure website traffic |
| 445 | SMB | File sharing |
| 53 | DNS | Domain name resolution |
## KEY LEARNING
Nmap is not just for scanning ports. It is used for:
- Reconnaissance
- Service identification
- OS fingerprinting
- Security analysis
- Infrastructure discovery
