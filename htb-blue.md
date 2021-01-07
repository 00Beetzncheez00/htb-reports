# Hack The Box Target Report (Blue)
For this write-up report we will be going thru the vulnerable machine from Hack The Box named Blue. The rating matrix for this target is in range of Enumeration, Real-Life, and CVE ratings.
| Target Name    | Rating Matrix        |
| ------------- |:-------------:|
| ![](https://github.com/00Beetzncheez00/images/blob/main/blue-1.png)  | ![](https://github.com/00Beetzncheez00/images/blob/main/blue-2.png) |

# Legal Things
- The following write-up, document, whatever you won't call it is for educational purposes **ONLY!!!**
- Do not perform any tasks in these write-ups on systems that you **DO NOT own!!!**
- If you need an environment to practice, look up the plethora of sites out there (Hack The Box, Vulnhub, OSCP Labs, etc...)

# Rules Of Engagement
- Do not perform any DOS (Denial Of Service) based attacks against the target.
- Only perform publicly available exploits in the target.
- No Zero-Days are to be run on the target.

# Document Overview
In this document I'll be utilizing the following methodologies. This target is one of the "Retired" targets from Hack The Box, however, I won't be posting the **USER** and **ROOT** hashes because those can be found doing your own research. This is simple a demonstration of working with these methodologies while practicing on a vulnerable target. The goal is approach this as if a final report is being given to a client.

The **Mitre Attack Framework** ([**Enterprise**](https://attack.mitre.org/tactics/enterprise/) & [**Mobile**](https://attack.mitre.org/tactics/mobile/)) to detail out which TTP's are used against that target.

| Enterprise    | Mobile        |
| ------------- |:-------------:|
| ![](https://github.com/00Beetzncheez00/images/blob/main/mitre-attack-enterprise.png)  | ![](https://github.com/00Beetzncheez00/images/blob/main/mitre-attack-mobile.png) |

The [**Penetration Testing Execution Standard**](http://www.pentest-standard.org/index.php/Main_Page) (PTES for short) to detail out which the corresponding number is being used on the target.

![](https://github.com/00Beetzncheez00/images/blob/main/ptes-image.png)

The [**Confidentiality, Integrity, and Availability**](https://en.wikipedia.org/wiki/Information_security#Basic_principles) (CIA Triad for short) will give a rating on what is exposed on the target.

![](https://github.com/00Beetzncheez00/images/blob/main/cia-triad-logo.png)

And finally, any afterthoughts on the target, what can possibly be done to secure the system thru recommendations.

# Document Details
- Mitre TTP(s) Enterprise Used: TA0001, TA0002, TA0004, TA0007, TA0009, TA0010
- PTES Identifiers Used: 1, 2, 4, 5, 6, 7
- CIA Rating: 1, 2

1. The target is running a Windows Operating System (Attachment 1). This was gathered from the HTB information listed from the control panel. Also the IP address of the target is listed in the HTB control panel (Attachment 2).
- **Attachment 1**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-3.png)

- **Attachment 2**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-4.png)

2. Initial enumeration shows a number of Microsoft RPC, Netbios, and DS related TCP ports (Attachment 3). UDP ports look to be all filtered so there isn't anything there of interest at this time (Attachment 3).

- **Attachment 3**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-5.png)

3. The MSF module **exploit/smb/ms17_010_psexec** has a check feature that can be used to further detect the Windows OS version along with seeing if the target is vulnerable. (Attachment 4)

- **Attachment 4**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-6.png)

**NOTE:** At this point I would establish contact with the client to inform them that I would be beginning my exploit attempts on the target systems if this was a white or gray box type of engagement.

4. Let's try to run the exploit against the target. Reason behind this is you might as well see if it works during an engagement because either way it will have to go into the report. Successful or not. (Attachment 5)

- **Attachment 5**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-7.png)

5. The exploit in Attachment 5 did not work because we didn't have a username, password, or hash to work with. However not all is lost because we got a piece of information from the target. The OS version and service pack. This can aid in further enumeration and exploitation.
7. Since the target is running Windows 7 SP1 64-bit. Let's try the Eternal Blue exploit on the target and see if we can gain access. (Attachment 6)

- **Attachment 6**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-8.png)

6. We have access to the target system. Let's see if we can get a meterpreter session out of this. And if so migrate the to a more stable process (say lsass), and pull some usernames and password hashes for later use. (Attachments 7 - 11)

**NOTE:** As stated above. Depending on the type of engagement (White or Gray Box) type. I would establish contact, again, with the client notifying them that I have gained a foothold on the target and see if they would like me to proceed further.

- **Attachment 7**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-9.png)

- **Attachment 8**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-10.png)

- **Attachment 9**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-11.png)

- **Attachment 10**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-12.png)

- **Attachment 11**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-13.png)

**NOTE:** At this point I would be running more enumeration activities on the target such as taking a deeper dive and trying to gather more information. See what's on it. See what it's connected to. See what services are running. Here are a couple of sites that can help.
- https://www.fuzzysecurity.com/tutorials/16.html
- https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/

7. Now that we have SYSTEM / Admin access to the system let's proceed to dump the password hashes of the users on the system (Attachments 12 - 14). These can be used for later items on the system. As you can imagine now that the hashes are taken the sky is the limit when it comes to doing what we want with the target.

**NOTE:** Once SYSTEM / Admin access has been had to the target the client would be then notified of what needs to be done to plug the security hole. Then the client will have to determine if the system needs to be patched immediately based on business risk.

- **Attachment 12**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-14.png)

- **Attachment 13**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-15.png)

- **Attachment 14**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-16.png)

8. Since mimikatz worked on dumping the user hashes you can attempt to either crack them. Or do PTH operations on it. As shown below (Attachments 15 - 18) psexec can work now. And if you don't want to use MSF for any of the work there are other options.

- **Attachment 15**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-17.png)

- **Attachment 16**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-18.png)

- **Attachment 17**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-19.png)

- **Attachment 18**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-20.png)

9. Finally since this is a Hack The Box target the flags must be captured and the trophy gained. Again this target is a retired machine, yes you can get the flags via other write-ups out there (Google them).

- **User Flag**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-21.png)

- **Root/Admin/System Flag**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-22.png)

- **Trophy**

![](https://github.com/00Beetzncheez00/images/blob/main/blue-23.png)

# After Thoughts
All in all this was a fun first box to play with. It has a good amount of "real life" aspect to it with the Eternal Blue vulnerable targets. I hope this write-up has given a clear understanding of how the PTES standard applies, how the MITRE Attack TTPs work along with cyber kill chain, and finally how the CIA triad ratings can apply.

# Recommendations
- Keep the system up to date on operating system and application patches.
- Implement complex password usage with the requirement to change the passwords on a regular basis.
- Implement endpoint protection for monitoring of system activities along with logging these activities to a central system.
