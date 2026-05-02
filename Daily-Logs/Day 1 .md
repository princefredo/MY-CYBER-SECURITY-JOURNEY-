
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

---

## ANALYSIS

- The target system is likely running Windows
- Port 445 (SMB) is a known attack surface
- Open ports indicate potential entry points for attackers

---

## KEY LEARNING

- Reconnaissance is the first phase of penetration testing
- Nmap can discover hosts, ports, and services
- Not all open ports are vulnerable, but they require investigation

---

## REFLECTION

This exercise helped me understand how attackers gather information before launching attacks and how important reconnaissance is in cybersecurity.
