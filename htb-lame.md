# Hack The Box Target Report (Lame)
For this write-up report, we will be going thru the vulnerable machine from Hack The Box named Lame. Funny name right? The rating matrix for this target is in the range of Enumeration, Real-Life, CVE ratings.
| Target Name    | Rating Matrix        |
| ------------- |:-------------:|
| ![](https://github.com/00Beetzncheez00/images/blob/main/lame-2.png)  | ![](https://github.com/00Beetzncheez00/images/blob/main/lame-1.png) |

# Legal Things
- The following write-up, document, whatever you want to call it is for educational purposes **ONLY!!!**
- Do not perform any tasks in these write-ups on systems that you **DO NOT own!!!**
- If you need an environment to practice look up the plethora of sites out there (Hack The Box, Vulnhub, OSCP Labs, etc...)

# Rules Of Engagement
- Do not perform any DOS (Denial Of Service) based attacks against the target.
- Only perform publicly available exploits in the target.
- No Zero-Days are to be run on the target.
- Client notification at each point when accessing a target. (Foothold, Exploitation, Root/SYSTEM access)
- Client approval to continue upon access to a target is obtained with instructions on how to proceed.

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
- Mitre TTP(s) Used: TA0001, TA0002, TA0004, TA0007
- PTES Identifiers Used: 1, 2, 4, 5, 7
- CIA Rating: 1, 2, 3

| Open Ports    | Services        |
| ------------- |:-------------:|
| 21 tcp | ftp |
| 22 tcp | ssh |
| 139 tcp | netbios-ssn |
| 445 tcp | microsoft-ds |
| 3632 tcp | distccd |

1. The target is running a Linux Operating. This was gathered from the HTB information listed in the control panel. Remember enumeration (Passive or Active) can come from all sources for your target.

![](https://github.com/00Beetzncheez00/images/blob/main/lame-3.png)

2. Initial enumeration (Scan was performed by an automated tool Sn1per) shows 5 TCP ports open (21, 22, 139, 445, 3632).

![](https://github.com/00Beetzncheez00/images/blob/main/lame-4.png)

3. Starting with the FTP service let's try the vsFTPd backdoor exploit. As you can see from the screenshot this exploit attempt was not successful.

![](https://github.com/00Beetzncheez00/images/blob/main/lame-5.png)

**NOTE:** It's important to document all the work being done on an engagement. The reason for this is to keep track of what you are doing, being able to put objective evidence into a report for a client to show what was done, and finally, it's a CYA move on your part.

4. One reason to keep good recon and enumeration notes is so you have the ability to go back thru them and see what was found, done, etc. In this case, it was noticed that the tool tried to run an exploit on a service that was found.

![](https://github.com/00Beetzncheez00/images/blob/main/lame-6.png)

**NOTE:** Pay attention to your ROE when using tools that attempt to run auto-exploitation. This is important to pay attention to. Even more so when the engagement is just an assessment and not a pen test.

5. After performing some research on this particular SAMBA service version an MSF exploit was found and attempted on the target. As shown by the screenshots this exploit was successful in obtaining a command shell on the target. This command shell was then migrated to an MSF meterpreter shell.

![](https://github.com/00Beetzncheez00/images/blob/main/lame-7.png)
![](https://github.com/00Beetzncheez00/images/blob/main/lame-8.png)

6. This is showing that a foothold has been obtained on the target.

![](https://github.com/00Beetzncheez00/images/blob/main/lame-9.png)

**NOTE:** At this point the engagement would be paused and the client would be contacted, given the information that we have obtained a foothold on the target, and wait for further instructions as to what the client would want. For the sake of this write-up, we are going to move forward.

**NOTE:** I would be running more enumeration activities on the target such as taking a deeper dive and trying to gather more information. See what is on it. See what it is connected to. See what services are running. Then I can make further recommendations on what needs to be done on the target.

7. Knowing that the target is running an older version of Samba with multiple exploits available. After doing some more research it another MSF exploit was located and run. As you can see this exploit netted ROOT access to the system. The above screenshots show the path taken to execute the MSF exploit, update the command shell to a meterpreter shell, interact with the shell, and show further objective evidence that ROOT access has been obtained on the target.

![](https://github.com/00Beetzncheez00/images/blob/main/lame-10.png)
![](https://github.com/00Beetzncheez00/images/blob/main/lame-11.png)
![](https://github.com/00Beetzncheez00/images/blob/main/lame-12.png)
![](https://github.com/00Beetzncheez00/images/blob/main/lame-13.png)

# After Thoughts
Another fun box to play with. It has a good amount of "real life" aspect to it as it shows out of date and patches not kept up to date. This also shows how using automated recon and enumeration tools can aid in time-saving on an engagement when time is of the essence. I hope this write-up has given anyone reading a clear understanding of how the PTES standard applies, how the MITRE Attack TTPs work along with the cyber kill chain, and finally how the CIA triad ratings can apply to targets in a simulated engagement.

# Recommendations
- Keep the system up to date on operating system and application patches.
- De-commission old systems and take them offline. Security thru obscurity isn't a thing!!!
- Implement complex password usage with the requirement to change the passwords on a regular basis.
- Implement endpoint protection for monitoring of system activities along with logging these activities to a central system.

