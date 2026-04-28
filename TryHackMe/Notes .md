THIS FOLDER WILL CONTAIN MY TRYHACKME NOTES AND PROGRESS.
## DAY 1
### ROOM:(OFFENSIVE SECURITY INTRO + FAKEBANK)
 ## WHAT I LEARNED
- What offensive Security is all about (thinking like an attacker)
- How web applications can expose hidden pages
- Basics of directory brute forcing using "dirb"
 ## TOOLS USED
 -dirb
 ## COMMANDS USED
 - dirb http://fakebank. thm
  ## WHAT I DID
  - Launched the fakebank application
  - Identified account number
  - Used "dirb" to find hidden directories
  - Discovered admin panel
  - Accessed functionality to manipulate account balance
   ## VULNERABILITY IDENTIFIED
   - Broken access control (admin panel exposed without restriction)
     ## CHALLENGES
    - Difficulty in understanding how terminal commands work 
    - Not knowing what each commands does initially
     ## SOLUTION
    - Took time to understand each command before running it.
    - Practiced reading instructions carefully.
    ## DAY 2
    ### ROOM (DEFENSIVE SECURITY)
    ## WHAT I LEARNED 
    - Defensive security focuses on protecting systems 
    - Soc analysts monitor and detect suspicious activity
    - Attacks like port scanning and web discovery can be identified
    ## PRACTICAL SKILLS 
    - Reviewed alerts on a dashboard 
    - Identified suspicious Ip address
    -Inveestigated attack pattern 
    ## KEY CONCEPTS
    - Detection
    - Investigation 
    - Responses
    ## MY EXPERIENCE
    This was my first real exposure to how defenders work in cybersecurtiy.
    ## DAY 3
    ### ROOM (WHAT IS NETWORKING)
    ## WHAT I DID
    -Started networking on tryhackme
    ## WHAT I LEARNED 
    - Definition of a network(A group of devices connected together)
    - Definition of internet(A group of network connected together)
    - types of network
    - Identifying devices on a network
    - What an IP address is(A way of identifying a host on a network)
    - W.W.W worrld wide web
    - Practiced PING command in kali linux 
    - Observed how devices respond on a network
    ## COMMANDS USED 
    - Ping 192.168.1.1
    - MAC address a4:f0:85:ac:2d
    - PING 8.8.8.8
    ## WHAT I OBSERVED 
    - My system has an IP address 
    - Network interfaces control communication.
