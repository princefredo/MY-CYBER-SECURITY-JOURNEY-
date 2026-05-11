### DAY 1
## WHAT I DID
- Created Github repository
- Set up my cybersecurity learning plan 
## WHAT I LEARNED 
- How Github works 
- How to create and commit files
## CHALLENGES
- Had difficulties creating folders on mobile phone while using Github
## SOLUTION
- Switched to laptop and used correct file naming format
## NEXT STEP
- Install virtualBox
- Install KaliLinux
- Start TryHackMe
- Begin first Lab

### DAY 2
# PORT SCANNING AND RECONNAISSANCE

## OBJECTIVE
To perform network reconnaissance and identify open ports and services.
## COMMANDS USED
- nmap -sn 10.0.2.0/24
- nmap -sV 10.0.2.2
## NETWORK DISCOVERY
Hosts Found:
- 10.0.2.2
- 10.0.2.3
- 10.0.2.15 (My Kali Machine)
## PORT SCAN RESULT
Target: 10.0.2.2
Open Ports:
- 135/tcp
- 445/tcp
Services:
- MSRPC (Microsoft Remote Procedure Call)
- SMB (Microsoft Directory Services)
## ANALYSIS
- The target system is likely running Windows
- Port 445 (SMB) is a known attack surface
- Open ports indicate potential entry points for attackers
## KEY LEARNING
- Reconnaissance is the first phase of penetration testing
- Nmap can discover hosts, ports, and services
- Not all open ports are vulnerable, but they require investigation
## REFLECTION
This exercise helped me understand how attackers gather information before launching attacks and how important reconnaissance is in cybersecurity.

### Day 3 
## DEEP RECCONNAISSANCE WITH NMAP( AGGRESSIVE SCAN -A)

## OBJECTIVES
To perform deep reconnaissance on a target system using aggressive scanning techniques and understand how to interpret scan results professionally.
## COMMANDS USED
nmap -A 10.0.2.2
## WHAT THE COMMAND DOES
The `-A` flag enables:
- OS Detection
- Service Version Detection
- Script Scanning
- Traceroute
This helps gather detailed intelligence about a target system.
## HOST STATUS
Host is up with very low latency.
## OPEN PORTS
| Port | State | Service |
|------|--------|----------|
| 135 | Open | MSRPC |
| 445 | Open | Microsoft-DS (SMB) |
## PORT 135 - MSRPC
- Used for communication between Windows services
- Indicates a likely Windows-related system
## PORT 445 - SMB
- Used for file and printer sharing
- Commonly targeted in real-world attacks
- High-value attack surface
## FILTERED PORTS
998 TCP ports were filtered.
## MEANING;
- The ports gave no useful response
- Likely protected by firewall or NAT filtering
- Filtered does not mean closed
## OS DETECTION ANALYSIS
Nmap could not accurately determine the operating system because:
- Most ports were filtered
- Nmap prefers at least one open and one closed port for accurate fingerprinting
Possible detections included:
- Oracle VirtualBox NAT bridge
- QEMU user mode gateway
## IMPORTANT DISCOVERY
The target (10.0.2.2) is likely:
- A VirtualBox NAT gateway
- Not a real Windows machine
This demonstrates how reconnaissance can reveal network infrastructure.
## SMB SECURITY INFORMATION
SMB signing was:
- Enabled
- But not required
This means some protection exists, but it is not strictly enforced.
## KEY LESSONS LEARNED
- Open ports do not automatically mean vulnerabilities
- Open ports indicate services that require investigation
- Filtered ports usually indicate firewalls or NAT behavior
- Reconnaissance is about gathering and interpreting information
- Aggressive scans provide deeper system intelligence
## PENTESTER MINDSET
When discovering an open port:
1. Identify the service
2. Determine the version
3. Check for vulnerabilities
4. Analyze security configurations
5. Investigate further before making assumptions
## REFLECTION
Today I learned how to interpret deep reconnaissance scans instead of simply reading port results. I also learned the difference between open, closed, and filtered ports and how infrastructure devices can appear during scanning.

### Day 4 
## Enumeration & Vulnerability Thinking

## OBJECTIVE
To understand the difference between reconnaissance and enumeration and begin thinking like a penetration tester by analyzing services and possible weaknesses.

# RECONNAISSANCE vs ENUMERATION/VULNERABILITY THINKING

## RECONNAISSANCE
Reconnaissance is the process of gathering basic information about a target.
Examples:
- Discovering live hosts
- Identifying open ports
- Detecting services
Example:
Finding that port 445 is open.
## ENUMERATION
Enumeration is the process of extracting deeper information from discovered services.
Examples:
- Detecting OS information
- Discovering SMB details
- Identifying configurations
- Gathering service information
Example:
Trying to discover SMB details using Nmap NSE scripts.
## COMMAND USED
nmap --script smb-os-discovery 10.0.2.2
## PURPOSE OF COMMAND 
The SMB OS Discovery script attempts to gather:
- Operating system information
- Computer name
- Workgroup/domain information
- SMB details
## SCAN RESULTS
Open Ports:
- 135/tcp → MSRPC
- 445/tcp → SMB (Microsoft-DS)
Filtered Ports:
- 998 TCP ports filtered
## ANALYSIS
The script did not reveal detailed SMB information.
Possible reasons:
- The target is likely a VirtualBox NAT gateway
- SMB information disclosure may be restricted
- NAT/firewall filtering limits enumeration
- The target is not a full Windows SMB server
## IMPORTANT DISCOVERIES
OPEN PORT DO NOT MEAN VULNERABILITY
An open port only means:
- A service is running
- Further investigation is required
## FILTERED PORTS
Filtered ports indicate:
- Firewall or NAT protection
- Hidden or blocked services
- Limited visibility during scanning
## VULNERABILITY THINKING
A pentester should not immediately assume:
"Open port = exploitable"
Instead, a pentester should ask:
1. What service is running?
2. What version is running?
3. Is the service outdated?
4. Is authentication weak?
5. Are there security misconfigurations?
## SMB UNDERSTANDING
SMB (Server Message Block):
- Used for file sharing
- Used for printer sharing
- Common on Windows systems
- Often targeted in real-world attacks
Not all systems use SMB.
Different systems expose different services depending on:
- Operating system
- Purpose
- Configuration
## KEY LESSONS LEARNED
- Enumeration is deeper than reconnaissance
- Enumeration may not always reveal information
- Limited scan results are still meaningful
- Different systems expose different ports and services
- Open ports require analysis, not assumptions
- Firewalls and NAT affect scanning results
## REFLECTION
Today I learned how penetration testers move from reconnaissance into enumeration and vulnerability thinking. I also learned that every system behaves differently and that filtered ports and limited enumeration results still provide valuable information.


# Day 5 
# WEB APPLICATION BASICS AND HTTP ENUMERATION

## OBJECTIVE
To understand how web applications communicate using HTTP/HTTPS and learn how to perform basic HTTP enumeration using curl.

# WHAT I LEARNED
Today I learned:
- How browsers communicate with web servers
- The difference between HTTP and HTTPS
- What requests and responses are
- What HTTP headers are
- What HTTP status codes mean
- How to use curl for web enumeration
- The structure of an HTTP response
- The difference between headers and body content
# HTTP BASICS
## HTTP
HTTP stands for:
HyperText Transfer Protocol
It is the protocol used for communication between:
- Browsers
- Web servers
HTTP usually uses:
- Port 80
## HTTPS
HTTPS is the secure version of HTTP.
It encrypts communication using SSL/TLS.
HTTPS usually uses:
- Port 443
# REQUEST AND RESPONSE
## REQUEST
A request is sent from the browser/client to the web server.
Example:
The browser asks for a webpage.
## RESPONSE
The server replies with:
- Status line
- Headers
- Body (optional)
# HTTP RESPONSE STRUCTURE
1. Status Line
2. Headers
3. Body
# PRACTICAL COMMANDS USED

## REQUESTING A WEBPAGE
curl http://google.com
## VIEWING HTTP HEADERS ONLY
curl -I https://google.com
# RESULTS AND ANALYSIS

## GOOGLE RESPONSE
Status Code:
301 Moved Permanently
Meaning:
Google redirected the request to:
https://www.google.com
# HTTP STATUS CODE LEARNED
| Code | Meaning |
|------|----------|
| 200 | Success |
| 301 | Redirect |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Server Error |
# IMPORTANT HHEADERS OBSERVED

## LOCATION:
Used for redirects.
Example:
location: https://www.google.com/
## CONTENT TYPE:
Shows the type of content returned.
Example:
text/html
## SERVER:
Reveals information about the web server.
Example:
gws (Google Web Server)
## X-FRAME OPTIONS:
Security header used to prevent clickjacking attacks.
## CONTENT-SECURITY-POLICY:
Security mechanism used to reduce malicious script execution.
## UNDERSTANDING HEADERS
HTTP headers contain metadata and instructions about:
- Security
- Content
- Redirects
- Server behavior
Headers are important during web enumeration because they may reveal:
- Technologies
- Security configurations
- Server information
## UNDERSTANDING THE BODY
The body contains the actual content returned by the server.
Examples:
- HTML webpages
- JSON data
- Files
- Error messages
The body is what browsers visually render.
## KEY LESSONS LEARNED
- Web applications communicate using HTTP/HTTPS
- HTTP responses contain status lines, headers, and bodies
- curl can be used for web enumeration
- Headers reveal important security and server information
- Redirects are common on modern websites
- Pentesters analyze headers and responses for information leakage
## REFLECTION
Today I learned the foundation of web communication and how penetration testers analyze web server responses. I also learned that HTTP headers reveal important information about server behavior and security configurations.
