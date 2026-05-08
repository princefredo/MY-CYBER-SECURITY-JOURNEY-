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
