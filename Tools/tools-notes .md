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

- ---

### ENUMERATION WITH NMAP

## WHAT IS ENUMERATION
Enumeration is the process of extracting detailed information from discovered services after reconnaissance.
Examples:
- OS information
- Service details
- Workgroups/domains
- Security configurations

---

### SMB ENUMERATION

## SMB OS DISCOVERY SCRIPT
Command:
nmap --script smb-os-discovery <target>
Example:
nmap --script smb-os-discovery 10.0.2.2
## PURPOSE OF SMB ENUMERATION
The script attempts to discover:
- Operating system
- SMB information
- Computer name
- Workgroup/domain
## IMPORTANT ENUMERATION CONCEPT
Enumeration may:
- Return detailed information
OR
- Return limited/no information
Both outcomes are meaningful.
Limited results may indicate:
- Firewalls
- NAT filtering
- Hardened systems
- Infrastructure devices
## VULNERABILITY THINKING
Open Port ≠ Vulnerability
An open port means:
- A service is running
- Investigation is required
## PENTESTER ANALYSIS
When discovering an open port:
1. Identify the service
2. Determine the version
3. Check for vulnerabilities
4. Analyze configurations
5. Investigate security protections
## COMMON PORTS STATE
OPEN
A service is actively accepting connections.
CLOSED
The port is reachable, but no service is listening.
FILTERED
The port is hidden or blocked by firewall/NAT.
## IMPORTANT LEARNING
Different systems expose different services.
Examples:
- Windows systems may expose SMB
- Linux systems commonly expose SSH
- Web servers commonly expose HTTP/HTTPS
Reconnaissance and enumeration help identify the role of a target system.


## WEB APPLICATION BASICS & HTTP ENUMERATION

## HTTP
HTTP stands for:
HyperText Transfer Protocol
Used for communication between:
- Browsers
- Clients
- Web servers
Default Port:
80
## HTTPS
HTTPS is the secure encrypted version of HTTP.
Uses SSL/TLS encryption.
Default Port:
443
## HTTP COMMUNICATION FLOW
1. Client sends a request
2. Server processes the request
3. Server sends a response
## HTTP Response Structure
# 1. STATUS LINE
Contains:
- HTTP version
- Status code
Example:
HTTP/2 301
# 2. HEADERS
Contain metadata and instructions.
Examples:
- content-type
- server
- location
- cache-control
Headers may reveal:
- Technologies
- Security settings
- Redirects
- Server information
# 3. BODY
Contains the actual content returned by the server.
Examples:
- HTML
- JSON
- Error messages
- Files
## COMMON HTTP STATUS CODES 
| Code | Meaning |
|------|----------|
| 200 | Success |
| 301 | Redirect |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Server Error |
## CURL
curl is a command-line tool used to communicate directly with web servers.
Used for:
- Web enumeration
- Testing responses
- Viewing headers
- API interaction
## IMPORTANT CURL COMMAND
# REQUEST A WEBPAGE
curl <url>
Example:
curl http://google.com
## VIEW  HTTP HEADERS ONLY
curl -I <url>
Example:
curl -I https://google.com
## SECURITY HEADERS LEARNED
# CONTENT SECURITY POLICY (CSP)
Helps prevent malicious script execution.
# X-FRAME-OPTIONS
Helps prevent clickjacking attacks.
## ENUMERATION MINDSET
When analyzing a website, a pentester should ask:
1. What server is running?
2. Are redirects present?
3. What technologies are used?
4. Are security headers configured?
5. Is information leakage present?
## IMPORTANT LEARNING
Headers are valuable sources of intelligence during web reconnaissance and security analysis.
