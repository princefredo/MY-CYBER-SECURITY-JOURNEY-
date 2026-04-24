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
    - Practiced reading instructions carefully
