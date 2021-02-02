# Something Something Template (Use This Section To Describe What This Document Is For)
Quick description of what this document is.

As an example: (**Note:** Feel free to change any of this)
**Legal things** will describe things that need to be said in attempts to keep law enforcement away and anyone's lawyers at bay, or happy, depending on how you look at it.
**Document overview** explains at a high level what is going on with what you will be reading.
**Document details** is the section that you use to, well, explain in various amounts of details (your choice of course) what the heck you are doing.

# Legal Things
- The following write-up, document, whatever you won't call it is for educational purposes **ONLY!!!**
- Do not perform any tasks in these write-ups on systems that you **DO NOT own!!!**
- If you need an environment to practice look up the plethora of sites out there (Hack The Box, Vulnhub, OSCP Labs, etc...)

# Rules Of Engagement
- Do not perform any DOS (Denial Of Service) based attacks against the target.
- Only perform publicly available exploits in the target.
- No Zero-Days are to be run on the target.
- Client notification at each point when accessing a target. (Foothold, Exploitation, Root/SYSTEM access)
- Client approval to continue upon access to a target is obrtained with instructions on how to proceed.

# Executive Summary
The in-scope target was found to be running older versions of the following that need to be patched and/or updated.

# Issues Include The Following:
- INSERT ISSUES

# High Level Recommendations
- INSERT HIGH LEVEL RECOMMENDATIONS

# Document Overview
Targets in this document will be engaged via the following methodologies.

The **Mitre Attack Framework** ([**Enterprise**](https://attack.mitre.org/tactics/enterprise/) & [**Mobile**](https://attack.mitre.org/tactics/mobile/)) to detail out which TTP's are used against that target.

| Enterprise    | Mobile        |
| ------------- |:-------------:|
| ![](https://github.com/00Beetzncheez00/images/blob/main/mitre-attack-enterprise.png)  | ![](https://github.com/00Beetzncheez00/images/blob/main/mitre-attack-mobile.png) |

The [**Penetration Testing Execution Standard**](http://www.pentest-standard.org/index.php/Main_Page) (PTES for short) to detail out which the corresponding number is being used on the target.

![](https://github.com/00Beetzncheez00/images/blob/main/ptes-image.png)

The [**Confidentiality, Integrity, and Availability**](https://en.wikipedia.org/wiki/Information_security#Basic_principles) (CIA Triad for short) will give a rating on what is exposed on the target.

![](https://github.com/00Beetzncheez00/images/blob/main/cia-triad-logo.png)

And finally, any afterthoughts on the target, what can possibly be done to secure the system.

# Document Details
- Mitre TTP(s) Used: TA0009, TA0007, TA0002
- PTES Identifiers Used: 1, 2, 4, 5, 7
- CIA Rating: 1, 3

| Open Ports    | Services        |
| ------------- |:-------------:|
| 22 | SSH |
| 443 | HTTP-SSL |

Insert what was done to the target in all aspects of the identified MITRE TTPs, PTES classifications, and how the CIA rating was obtained. Include any and all steps with objective evidence (log output, screenshots, etc...)

# After Thoughts
Afterthoughts need to include recommendations on what is needed to secure the target along with any personal touches added to the document. Personal opinions on the steps taken, difficulty, etc...

# Recommendations
- Keep the system up to date on operating system and application patches.
- Implement complex password usage with the requirement to change the passwords on a regular basis.
- Implement endpoint protection for monitoring of system activities along with logging these activities to a central system.
