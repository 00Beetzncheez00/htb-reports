# Hack The Box Target Report #2 (Arctic)
Quick description of what this document is.

For this write-up report we will be going thru the vulnerable machine from Hack The Box named Blue. The rating matrix for this target is in range of Enumeration, Real-Life, and CVE ratings.
| Target Name    | Rating Matrix        |
| ------------- |:-------------:|
| ![](https://github.com/00Beetzncheez00/images/blob/main/arctic-1.png)  | ![](https://github.com/00Beetzncheez00/images/blob/main/arctic-2.png) |

# Legal Things
- The following write-up, document, whatever you won't call it is for educational purposes **ONLY!!!**
- Do not perform any tasks in these write-ups on systems that you **DO NOT own!!!**
- If you need an environment to practice look up the plethora of sites out there (Hack The Box, Vulnhub, OSCP Labs, etc...)

# Rules Of Engagement
- Do not perform any DOS (Denial Of Service) based attacks against the target.
- Only perform publicly available exploits in the target.
- No Zero-Days are to be run on the target.

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

Insert what was done to the target in all aspects of the identified MITRE TTPs, PTES classifications, and how the CIA rating was obtained. Include any and all steps with objective evidence (log output, screenshots, etc...)

# After Thoughts
Afterthoughts need to include recommendations on what is needed to secure the target along with any personal touches added to the document. Personal opinions on the steps taken, difficulty, etc...

# Recommendations
- Keep the system up to date on operating system and application patches.
- Implement complex password usage with the requirement to change the passwords on a regular basis.
- Implement endpoint protection for monitoring of system activities along with logging these activities to a central system.

