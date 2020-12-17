# Hack The Box Target Report #2 (Arctic)
Quick description of what this document is.

For this write-up report we will be going thru the vulnerable machine from Hack The Box named Arctic. The rating matrix for this target is in range of Enumeration, Real-Life, CVE ratings, and a teeny bit of Custom Exploitation.
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
- Mitre TTP(s) Used: TA0001, TA0002, TA0004, TA0007, TA0009, TA0010
- PTES Identifiers Used: 1, 2, 3, 4, 5, 7
- CIA Rating: 1, 2, 3

1. The target is running a Windows Operating System (Attachment 1). This was gathered from the HTB information listed from the control panel. Also the IP address of the target is listed in the HTB control panel (Attachment 2). Remember enumeration (Passive or Active) can come from all sources related to your target. 
- **Attachment 1**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-3.png)

- **Attachment 2**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-4.png)

2. Initial enumeration (**Command Used:** nmap -T4 -sV -sC -O -A -n -vv -Pn -p- 10.10.10.11 -d --reason) shows 3 ports open **(135, 8500, 40154)**. If you know your port numbers you will know right away that port 135 is Microsoft's COM/DCOM/RPC Endpoint mapper port. A simple google search can show you what all information and exploitation you can get from this port. It also looks like the high number port 49154 has been identified also as an RPC port (Attachment 3). Despite nmap displaying the service as "fmtp?" a quick search shows that is the port used by the Coldfusion Web Server software (Attachment 4). It is important to note that your scanning tools will give you false positive's and negative's. It is a good idea to have multiple ways to verify the information you are getting.

- **Attachment 3**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-5.png)

- **Attachment 4**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-6.png)

3. Let's narrow down on the ColdFusion software on this target. Doing a simple web browser to the page shows there are two folders being indexed (Attachment 5). If we go into the CFIDE folder we are presented with the Coldfusion login page (Attachment 6). Also shown is the version number (Version 8). This can be used to lookup any vulnerabilities or exploits.

- **Attachment 5**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-7.png)

- **Attachment 6**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-8.png)



# After Thoughts
Afterthoughts need to include recommendations on what is needed to secure the target along with any personal touches added to the document. Personal opinions on the steps taken, difficulty, etc...

# Recommendations
- Disable web server indexing in all locations.
- Keep the system up to date on operating system and application patches.
- Implement complex password usage with the requirement to change the passwords on a regular basis.
- Implement endpoint protection for monitoring of system activities along with logging these activities to a central system.

