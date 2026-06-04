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

### DAY 6 – WEB VULNERABILITY FUNDAMENTALS AND HTTP METHOD
# OBJECTIVE
To understand how web vulnerabilities occur, how attackers manipulate user input, and how HTTP methods are used in web communication.
### WEB VULNERABILITY FUNDAMENTAL

## WHAT IS A VULNERABILITY?
A vulnerability is a weakness in a system or web application that can be abused by attackers.
Examples:
- Weak authentication
- Unsafe file uploads
- Outdated software
- Poor input validation
## IMPORTANT SECURITY PRINCIPLE

## NEVER TRUST USER INPUT
Web applications constantly receive input from users such as:
- Search boxes
- Login forms
- URLs
- Comment sections
- File uploads
If an application trusts user input too much without proper validation, vulnerabilities may occur.
### COMMON BEGINNER WEB VULNERABILITY LEARNED

## 1. CROSS-SITE SCRIPTING (XSS)
Occurs when attackers inject malicious JavaScript into a webpage.
Usually caused by:
- Poor input sanitization
## 2. SQL INJECTION
Occurs when attackers manipulate database queries through user input.
Usually caused by:
- Unsafe handling of user-controlled data
## 3. FILE UPLOAD VULNERABILITIES
Occurs when applications allow dangerous files to be uploaded.
Potential risks:
- Remote code execution
- Malware upload
- Web shell upload
## 4. INFORMATION DISCLOSURE
Occurs when applications expose sensitive information such as:
- Server versions
- Errors
- Internal paths
- Debug information
## ATTACKER MINDSET
A pentester should ask:
- What input can I control?
- Can I manipulate the input?
- Does the server validate the data properly?
- What happens if unexpected data is sent?

---
### HTTP METHODS AND REQUEST 

## WHAT ARE HTTP METHHODS?
HTTP methods are instructions sent from the client/browser to the server to tell the server what action to perform.
## GET METHOD

# PURPOSE
Used to retrieve information from a server.
Example:
Viewing a webpage.
## CHARACTERISTICS
- Parameters appear in the URL
- Easy to manipulate
- Commonly used for browsing and fetching data
Example:
https://site.com/profile?id=25
## WHY GET REQUEST MATTERS IN PENETRATION TESTING
GET parameters are important because attackers may manipulate them to test:
- Access control
- Information disclosure
- SQL injection
- IDOR vulnerabilities
Example:
Changing:
id=25
to:
id=1
to test whether another user's data can be accessed.
## POST METHOD
# PURPOSE
Used to send data to the server.
Commonly used for:
- Login forms
- Registration forms
- File uploads
# CHARACTERISTICS
- Data is sent inside the request body
- Data is not directly visible in the URL
- Commonly used for sensitive information
# IMPORTANT LESSONS
POST requests are NOT automatically secure.
Security depends on:
- HTTPS encryption
- Proper server-side validation
## GET vs POST
| GET | POST |
|------|------|
| Retrieves data | Sends data |
| Data appears in URL | Data sent in body |
| Easy to manipulate | Commonly used for forms |
## KEY LESSONS LEARNED
- Web vulnerabilities often happen because applications trust user input too much
- Attackers manipulate requests and parameters to test application behavior
- GET requests expose parameters directly in URLs
- POST requests send data inside the request body
- Understanding requests and user input is foundational in web pentesting
## REFLECTION
Today I learned how attackers think about web applications and how vulnerabilities often begin from unsafe handling of user input. I also learned the difference between GET and POST requests and why request manipulation is important in penetration testing.

# DAY 7 – HTTP PARAMETERS & REQUEST MANIPULATION

## OBJECTIVE
To understand how web applications use parameters and how attackers manipulate requests during web penetration testing.
## KEY CONCEPTS LEARNED
### WHAT ARE HTTP PARAMETERS?
Parameters are pieces of data sent from the browser to the server.
Example:
https://site.com/profile?id=25
- Parameter Name: id
- Parameter Value: 25
## WHY PARAMETERS MATTERS
Attackers target parameters because:
- users can control them
- they influence server behavior
- poor validation can lead to vulnerabilities
## TYPES OF PARAMETER
### 1. URL PARAMETER (GET PARAMETERS)
Visible inside URLs.
Example:
?id=25
Used to retrieve information.
### 2. FORM PARAMETERS (POST PARAMETER)
Sent through forms.
Example:
username=admin
password=1234
Usually sent in request body.
### 3. HIDDEN PARAMETERS
Parameters hidden inside forms.
Example:
<input type="hidden" name="role" value="user">
Attackers may still manipulate them.
## PARAMETER TAMPERING
Parameter tampering is modifying parameters to test how the server behaves.
Example:
role=user → role=admin
This may lead to privilege escalation if validation is weak.
## PENTESTER THINKING
When seeing parameters, a pentester should ask:
- Can I modify this?
- Does the server validate it?
- Can I access unauthorized data?
- Can I change roles or permissions?
- Can I manipulate application behavior?
## IDOR INTRODUCTION
IDOR (Insecure Direct Object Reference) happens when users can access resources they should not access.
Example:
profile?id=25 → profile?id=1
If another user profile loads, it may indicate broken access control.
## KEY LEARNING
- Applications should never trust user input
- Parameters are common attack surfaces
- Request manipulation is a core web pentesting skill
- Proper server-side validation is critical
## REFLECTION
This lesson helped me understand how attackers manipulate requests and why parameter validation is important in web security.

# Day 8 – COOKIES, SESSIONS & AUTHENTICATION BASICS
## OBJECTIVE
To understand how websites authenticate users and maintain login sessions using cookies and session IDs.
## WHAT IS AUTHENTICATION?
Authentication is the process of verifying a user's identity.
Example:
- Username
- Password
The server checks if the credentials are correct.
## WHAT IS HTTP STATELESSNESS?
HTTP is stateless, meaning the server does not naturally remember previous requests.
Because of this:
- websites use sessions
- cookies help maintain identity
## WHAT IS A SESSION?
A session is a server-side record that keeps track of an authenticated user.
Example:
sessionID=abc123
The server links this session ID to the logged-in user.
## WHAT IS A COOKIE?
A cookie is small data stored in the browser.
Websites use cookies to:
- maintain login sessions
- remember users
- store preferences
## AUTHENTICATION FLOW
### STEP 1 – USER LOGS IN
The browser sends:
username + password
### STEP 2 – SERVER AUTHENTICATES USER
The server verifies the credentials.
### STEP 3 – SERVER CREATES SESSION
Example:
sessionID=abc123
### STEP 4 – SESSION STORED AS COOKIE
The server sends:
Set-Cookie: sessionID=abc123
The browser stores it.
### STEP 5 – BROWSER SENDS COOKIE AUTOMATICALLY
Future requests send:
Cookie: sessionID=abc123
The server recognizes the authenticated user.
## IMPORTANT UNDERSTANDING
The cookie usually stores:
- session ID
The cookie usually does NOT store:
- raw password
## LOGOUT PROCESS
When a user logs out:
- the session should be destroyed
- the session cookie should become invalid
The user must login again to become authenticated.
## COOKIE SECURITY FLAGS
### SECURE
Cookie only sent over HTTPS.
### HTTPONLY
Prevents JavaScript from accessing cookies.
### SAMESITE
Helps reduce cross-site request attacks.
## SESSION HI-JACKING
If attackers steal session cookies, they may impersonate the user without knowing the password.
Example:
sessionID=abc123
This is called session hijacking.
## PENTESTER THINKING
A pentester should ask:
- Are session IDs predictable?
- Are cookies protected?
- Does logout destroy sessions?
- Can sessions be hijacked?
- Is authentication secure?
## KEY LEARNING
- Authentication verifies identity
- Sessions maintain logged-in state
- Cookies store session identifiers
- Session security is critical in web applications
## REFLECTION
This lesson helped me understand how websites remember users and why session security is very important in web application penetration testing.

# DAY 9
### BURP SUITE FUNDAMENTALS
## OBJECTIVE
Learn the purpose of Burp Suite and understand how penetration testers use it to inspect, intercept, and manipulate web application traffic.
## WHAT IS BURP SUITE?
Burp Suite is a web application security testing tool commonly used by penetration testers. It acts as a proxy between a web browser and a web server, allowing testers to capture, inspect, modify, and forward HTTP requests and responses.
    A simple way to think about Burp Suite is that it allows a penetration tester to observe web traffic and understand how an application behaves behind the scenes.
### KEY CONCEPTS LEARNED 
## PROXY
The Proxy feature intercepts traffic between the browser and the web server.
A penetration tester can:
- Capture requests
- Inspect requests
- Modify requests
- Forward or drop requests
The proxy allows visibility into how a web application communicates.
## HTTP REQUEST AND RESPONSES
While using Burp Suite, I observed:
- Request methods (GET and POST)
- Headers
- Cookies
- Parameters
- HTTP versions
- Server responses
This helped me understand how browsers communicate with web servers.
## REPEATER
Repeater is used to manually resend requests multiple times without refreshing the browser.
A penetration tester can:
- Modify parameters
- Change headers
- Observe application behavior
- Compare server responses
Repeater is useful for testing how an application reacts to different inputs.
## HTTP HISTORY
HTTP History records requests and responses observed by Burp Suite.
It helps a tester:
- Review previous requests
- Identify interesting endpoints
- Locate parameters
- Discover application functionality
HTTP History acts as a record of web traffic captured during testing.
## PENTESTER MINDSET LEARNED 
While reviewing requests, I learned to ask:
- What can I control?
- What parameters exist?
- What happens if I change them?
- Is the application validating user input?
- Does the response change?
These questions help identify potential security weaknesses.
## PRACTICAL ACTIVITIES PERFROMED
- Intercepted browser traffic using Burp Proxy
- Observed GET requests
- Examined cookies and headers
- Sent requests to Repeater
- Modified selected parameters
- Observed different server responses
- Explored HTTP History
## KEY TAKEAWAY
Burp Suite is one of the most important tools used in web application penetration testing. It provides visibility into requests and responses and allows a tester to analyze application behavior by inspecting and modifying web traffic.


# DAY 10 
### Burp Suite Target Scope and Site Map

## OBJECTIVE
Learn how Burp Suite helps penetration testers identify application functionality, organize discovered endpoints, and focus testing efforts on authorized targets.
## WHAT IS TARGET SCOPE?
Target Scope defines which websites, domains, or applications are authorized for testing.
It helps penetration testers focus only on approved targets and avoid testing systems outside the assessment scope.
EXAMPLE:
In Scope:
https://example.com
Out of Scope:
https://google.com
Understanding scope is important because penetration testing should only be performed on systems where permission has been granted.
## WHAT IS SITE MAP?
Site Map is a Burp Suite feature that automatically organizes discovered application content.
As a tester browses an application, Burp Suite records pages and endpoints and displays them in a structured tree format.
EXAMPLE:
/
├── /login
├── /profile
├── /account
├── /upload
└── /admin
This helps testers understand the structure of an application.
## WHY SITE MAP IS IMPORTANT
Site Map helps penetration testers:
- Discover endpoints
- Identify application functionality
- Locate user-controlled input
- Find areas worth investigating
Instead of manually remembering pages, Burp Suite organizes them automatically.
## INTERESTING ENDPOINTS IDENTIFIED
During learning, I discovered that some endpoints usually deserve more attention than others.
Examples:
### HIGH INTEREST
- /login
- /upload
- /admin
- /api/users
- /api/orders
These endpoints often involve authentication, authorization, file handling, or sensitive functionality.
### LOWER INTEREST
- /logo.png
- /style.css
These are typically static resources and are usually lower priority during testing.
## PENTESTER MINDSET LEARNED
When reviewing a Site Map, I learned to ask:
- Which endpoints are sensitive?
- What functionality does this endpoint provide?
- Are there user-controlled parameters?
- Can I modify anything?
- Can I access data I should not access?
## PRACTICAL EXAMPLES
Example Endpoint:
GET /employee?id=15
Questions a tester may ask:
- What happens if id=16?
- Can I access another employee record?
- Does the application validate authorization?
Example Endpoint:
/admin
Questions a tester may ask:
- Can unauthorized users access it?
- Are access controls properly enforced?
## KEY TAKEAWAYS
Target Scope ensures testing remains focused on authorized systems, while Site Map helps organize discovered functionality and identify areas that deserve deeper security testing. Site Map acts as a map of an application's attack surface and helps penetration testers prioritize their investigations.


### DAY 11  - WEB APPLICATION SECURITY FUNDAMENTALS
# TOPICS COVERED
1. Attack Surface Discovery Fundamentals
2. Authentication & Authorization Testing
3. IDOR (Insecure Direct Object References)

# 1. ATTACK SURFACE DISCOVERY FUNDAMENTAL
## DEFINITION
Attack Surface Discovery is the process of identifying all accessible functionality, endpoints, parameters, inputs, and features within a web application that may be tested for security weaknesses.
## WHY IT IS IMPORTANT
A penetration tester cannot test what they have not discovered. Before looking for vulnerabilities, a tester must understand how the application works and identify areas worth investigating.
## COMMON AREAS OF INTEREST
### AUTHENTICATION ENDPOINTS
/login
/register
/reset-password
### AUTHORIZATION ENDPOINTS
/role
/admin
/admin/users
### USER DATA ENDPOINTS
/profile?id=15
/account?id=5
/employee?id=10
### FILE UPLOAD ENDPOINTS
/upload
### SEARCH ENDPOINTS
/search?q=laptop
### API ENDPOINTS
/api/users
/api/orders
## PENTESTER MINDSET
When discovering an endpoint, ask:
- What does this endpoint do?
- What can I control?
- Are there any parameters?
- Can I modify the parameters?
- Does the server validate my changes?
- Can I access unauthorized functionality?
## INTERESTING ENDPOINTS
Examples:
/admin
/profile?id=15
/upload
/search?q=phone
/api/users
## LESS INTERESTING ENDPOINT
Examples:
/logo.png
/style.css
/favicon.ico
These are usually static resources and often contain less security-relevant functionality.

# 2. AUTHENTICATION & AUTHORIZATION TESTING

## AUTHENTICATION
### DEFINITION
Authentication is the process of proving a user's identity.
### PURPOSE
Authentication answers the question:
Who are you?
### Examples
- Username and Password
- One-Time Password (OTP)
- Passkeys
- Biometrics
### PENTESTER QUESTIONS
- Can login be bypassed?
- How are sessions created?
- How are cookies handled?
- Can authentication mechanisms be abused?
## AUTHORIZATION

### DEFINITION
Authorization determines what an authenticated user is allowed to access or perform.
### PURPOSE
Authorization answers the question:
What are you allowed to do?
### EXAMPLES
A normal user should not access:
/admin
/admin/users
/admin/settings
### PENTESTER QUESTIONS
- Can I access another user's data?
- Can I access admin functionality?
- Can I perform actions outside my privileges?
- Can I view restricted resources?

## AUTHENTICATION & AUTHORIZATION
### AUTHENTICATION
Who are you?
Example:
Username + Password
### AUTHORIZATION
What are you allowed to do?
Example:
Can this user access /admin?
## EXAMPLE SCENARIO
Request:
http
GET /profile?id=15
User changes it to:
http
GET /profile?id=16
If another user's profile becomes accessible:
Authorization Failure

# 3. IDOR (Insecure Direct Object References)
## DEFINITION
IDOR (Insecure Direct Object Reference) is an authorization vulnerability that occurs when a user can access or modify resources they should not have access to by changing identifiers such as IDs, account numbers, invoice numbers, or profile references.
## COMMON EXAMPLES
### USER PROFILE
http
GET /profile?id=15
Modified:
http
GET /profile?id=16
### INVOICE ACCESS
http
GET /invoice?id=120
Modified:
http
GET /invoice?id=121
### EMPLOYEE RECORD
http
GET /employee?id=5
Modified:
http
GET /employee?id=6
## WHY IDOR HAPPENS
The application verifies that the user is logged in but fails to verify ownership of the requested resource.
The server checks:
Is the user authenticated?
But fails to check:
Does this user own this resource?
## PENTESTER MINDSET
Whenever a parameter references:
id=
user=
account=
invoice=
document=
employee=
profile=
order=
Ask:
What happens if I change it?
Examples:
id=15 → id=16
id=120 → id=121
user=5 → user=6
## SIGNS OF POTENTIAL IDOR
- User identifiers in URLs
- Account numbers in requests
- Invoice references
- Document references
- Employee records
- Profile identifiers
## KEY LESSONS
Finding:
http
/profile?id=15
is Attack Surface Discovery.
Accessing another user's profile after modifying the ID is an IDOR vulnerability caused by an authorization failure.
# PERSONAL TAKEAWAYS
- Attack Surface Discovery helps identify functionality worth testing.
- Authentication verifies identity.
- Authorization determines permissions.
- IDOR is a common authorization vulnerability.
- Whenever an identifier appears in a request, a pentester should consider whether modifying it could expose unauthorized data.
  THE FIRST QUESTION A PENTESTER SHOULD ASK IS:
  What happens if I modify this parameter?
