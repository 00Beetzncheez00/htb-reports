# Hack The Box Target Report (Arctic)

For this write-up report, we will be going thru the vulnerable machine from Hack The Box named Arctic. The rating matrix for this target is in the range of Enumeration, Real-Life, CVE ratings, and a teeny bit of Custom Exploitation.
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

1. The target is running a Windows Operating System (Attachment 1). This was gathered from the HTB information listed from the control panel. Also, the IP address of the target is listed in the HTB control panel (Attachment 2). Remember enumeration (Passive or Active) can come from all sources for your target.
- **Attachment 1**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-3.png)

- **Attachment 2**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-4.png)

2. Initial enumeration (**Command Used:** nmap -T4 -sV -sC -O -A -n -vv -Pn -p- 10.10.10.11 -d --reason) shows 3 ports open **(135, 8500, 40154)**. If you know your port numbers you will know right away that port 135 is Microsoft's COM/DCOM/RPC Endpoint mapper port. A simple google search can show you all information and exploitation you can get from this port. It also looks like the high number port 49154 has been identified also as an RPC port (Attachment 3). Despite nmap displaying the service as "fmtp?" a quick search shows that is the port used by the ColdFusion Web Server software (Attachment 4). It is important to note that your scanning tools will give you false positives and negatives. It is a good idea to have multiple ways to verify the information you are getting.

- **Attachment 3**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-5.png)

- **Attachment 4**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-6.png)

3. Let's narrow down the ColdFusion software on this target. Doing a simple web browser to the page shows there are two folders being indexed (Attachment 5). If we go into the CFIDE folder we are presented with the ColdFusion login page (Attachment 6). Also shown is the version number (Version 8). This can be used to lookup any vulnerabilities or exploits.

**NOTE:** At this point I would establish contact with the client to tell them that I would be beginning my exploit attempts on the target system(s) if this was a white or gray box engagement.

- **Attachment 5**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-7.png)

- **Attachment 6**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-8.png)

4. Doing some research on Adobe's ColdFusion software yields a few vulnerabilities (https://www.cvedetails.com/vulnerability-list/vendor_id-53/product_id-8739/Adobe-Coldfusion.html). This can be one reason to recommend a client not to use this application. Specifically for this target the CVE that will be utilized is **CVE-2010-2861** (https://www.cvedetails.com/cve/CVE-2010-2861/).

5. The next item to be done is to take advantage of the LFI/RFI directory traversal vulnerability (Attachment 7).

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-9.png)

6. Attachments 7 - 8 prove the exposure of the admin hash credentials from the web interface and source code. Attachments 9 - 11 prove the cracking of the admin hash, successful login to the ColdFusion Application, and the current version with what updates have been installed.

- **Attachment 7**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-10.png)

- **Attachment 8**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-11_1.png)

- **Attachment 9**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-12.png)

- **Attachment 10**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-13.png)

- **Attachment 11**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-14.png)

**NOTE:** At this point the engagement would pause and I would establish contact with the client to tell them that have gained access to the application with administrative level credentials. If the system is in production and the severity is great enough a request to update/patch/or offline the system would be made. Otherwise, it will be the client's call on how to proceed. For the sake of this write-up, we will be proceeding.

7. At this time during an engagement I would try to gain a foothold on the target. Since we have administrative access to the ColdFusion application I would do some research on how this could be done. Through thru enumeration of the application, we know that it is Java-based (Attachment 11). Since time is usually of the essence on an engagement let's try a quick way to obtain a reverse shell from the application.

8. This version of ColdFusion has a task scheduler. I wonder if we can generate a payload file that connects back to the attacking machine, have ColdFusion pull the file, and have the webserver execute the payload thus making our connection? Let's give it a whirl, shall we?

9. Using Msfvenom a payload file can be created (Attachment 12). This is creating a generic java payload that when viewed/executed will connect back to the attacking computer and hopefully give me a shell to work with.

- **Attachment 12**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-15.png)

10. ColdFusion needs a way to pull the payload when the scheduled task is running. This can be done simply by running the Python SimpleHTTP server. (Attachment 13) There are other easier ways along with running in a C&C environment. But for simplicity's sake, I'm sticking to the basics.
 
- **Attachment 13**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-16.png)

11. Time to set up a scheduled task to run in ColdFusion to pull the generated payload file. (Attachments 14 & 15)

- **Attachment 14**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-17.png)

- **Attachment 15**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-18.png)

11. Run the ColdFusion scheduled task (Attachment 16), make sure it pulled from the attacking webserver (Attachment 17), and show that it's on the target (Attachment 18).

- **Attachment 16**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-19.png)

- **Attachment 17**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-20.png)

- **Attachment 18**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-21.png)

12. Start a generic Netcat listener for when the reverse shell call home (Attachment 19), navigate to the .jsp page with a web browser (Attachment 18), and voilà a reverse shell (Attachment 20).

- **Attachment 19**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-22.png)

- **Attachment 20**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-23.png)

**NOTE:** At this point the engagement would pause and I would establish contact with the client to tell them that I have gained a foothold on the server that the ColdFusion application resides on with what looks to be like USER level credentials. If the system is in production and the severity is great enough a request to update/patch/or offline the system would be made. Otherwise, it will be the client's call on how to proceed. For the sake of this write-up, we will be proceeding.

**NOTE:** At this point of the engagement, I would be running more enumeration activities on the target such as taking a deeper dive and trying to gather more information. See what is on it. See what it is connected to. See what services are running. Here are a couple of sites that can help. With this information, I can make further recommendations on what needs to be done on the target.
- https://www.fuzzysecurity.com/tutorials/16.html
- https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/

13. Looking around the system via port 135 that was shown to be open (Attachment 3) a couple if tools (ifmap & rpcdump) were run to see what is possibly exposed.

- **Attachment 21**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-24.png)

- **Attachment 22**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-25.png)

- **Attachment 23**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-26.png)

- **Attachment 24**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-27.png)

14. After running windows exploit suggester on the target it reveals a few patches missing (Attachment 25). It is important to note that this target enumeration was done via the low-priv user. This was done by pulling the SYSTEMINFO details from the target, outputting it to a text file, and using that data with the exploit suggestion program.

- **Attachment 25**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-28.png)

15. ADMIN or SYSTEM rights were obtained on the target via a number of steps. 1st the aforementioned steps to gain the foothold via the ColdFusion application were executed. 2nd, using the Metasploit Console (msfconsole) foothold session was upgraded to a meterpreter session via the /multi/script/web_delivery module, and 3rd utilizing the ms10_092 exploit to elevate rights to NT AUTHORITY\SYSTEM (Attachments 26 - 33)

- **Attachment 26**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-29.png)

- **Attachment 27**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-30.png)

- **Attachment 28**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-31.png)

- **Attachment 29**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-32.png)

- **Attachment 30**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-33.png)

- **Attachment 31**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-34.png)

- **Attachment 32**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-35.png)

- **Attachment 33**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-36.png)

- **Trophy**

![](https://github.com/00Beetzncheez00/images/blob/main/arctic-37.png)

# After Thoughts
Another fun box to play with. It has a good amount of "real life" aspect to it with being it is running an old application along with system patches not up to date making it a vulnerable target. I hope this write-up has given anyone reading a clear understanding of how the PTES standard applies, how the MITRE Attack TTPs work along with the cyber kill chain, and finally how the CIA triad ratings can apply to targets in a simulated engagement.

# Recommendations
- Disable web server indexing in all locations.
- Close ports or disable services that are not needed.
- Upgrade ColdFusion to the latest version if the system is still in production. Otherwise, decommission the system.
- Keep the system up to date on operating system and application patches.
- Implement complex password usage with the requirement to change the passwords on a regular basis.
- Implement endpoint protection for monitoring of system activities along with logging these activities to a central system.
