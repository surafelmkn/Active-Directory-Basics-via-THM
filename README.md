# Active-Directory-Basics-via-THM
Hands-on walkthrough of core Active Directory administration, including OUs, security groups, delegation, GPOs, and Kerberos/NTLM authentication. Completed through TryHackMe's Windows AD Basics room.

<br><h2>Overview</h2>
This lab is a hands-on walkthrough of Active Directory basics, done in a real Windows domain controller lab through TryHackMe's Windows AD Basics room. AD is what most companies use to manage logins, permission, and devices across their network, so this covers the stuff a help desk tech actually deals with day to day: organizing users into OUs, managing security groups, delegating limited admin rights like password resets, setting up Group Policy, and understandin how Kerberos and NTLM authentication work. Each step below has a screenshot and a short explanation of what I did and why it matters for IT support work.

<br><h2>1. Directory Structure Overvie</h2>
<img width="476" height="470" alt="01-aduc-ou-structure" src="https://github.com/user-attachments/assets/3ea8c743-dea9-468d-8c86-8f9777584c41" />

