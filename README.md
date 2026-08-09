# Active-Directory-Basics-via-THM
Hands-on walkthrough of core Active Directory administration, including OUs, security groups, delegation, GPOs, and Kerberos/NTLM authentication. Completed through TryHackMe's Windows AD Basics room.

<br><h2>Overview</h2>
This lab is a hands-on walkthrough of Active Directory basics, done in a real Windows domain controller lab through TryHackMe's Windows AD Basics room. AD is what most companies use to manage logins, permission, and devices across their network, so this covers the stuff a help desk tech actually deals with day to day: organizing users into OUs, managing security groups, delegating limited admin rights like password resets, setting up Group Policy, and understand in how Kerberos and NTLM authentication work. Each step below has a screenshot and a short explanation of what I did and why it matters for IT support work.

<br><h2>1. Directory Structure Overview</h2>
<img width="476" height="470" alt="01-aduc-ou-structure" src="https://github.com/user-attachments/assets/3ea8c743-dea9-468d-8c86-8f9777584c41" />

The domain is organized into Organization Units (OUs) based on each department: IT, Management, Marketing, Research and Development, Sales, and a Students OU that I created to practice building the directory structure myself. Organiing accounts this way makes it easier to manage permissions and policies for an entire department instead of setting everything up for each user one at a time. This is important for a help desk team because they may have to manage a lot of users at once. Understanding how the domain is organized is one of the first things a support tech needs to know. It helps them safely reset passwords, move devices, and troubleshoot access problems without accidentally changing something that could affect other users or departments.

<br><h2>2. Reviewing User Accounts in Sales</h2>
<img width="473" height="473" alt="02-sales-ou-users" src="https://github.com/user-attachments/assets/0798f076-13fb-42f9-b943-1294314931ab" />

I reviewed the Sales OU to check the accounts that were already there. I also created a test account using my own name so I could get more comfortable with the account creation process. Being able to quickly find a specific OU and check which users have accounts is an important part of help desk work. It also helps when setting up accounts for new employees, removing accounts for people who leave, or checking a user's access while helping them with an issue.

<br><h2>3. Identifying and Disabling a Stale Account</h2>
<img width="475" height="473" alt="03-disable-stale-account" src="https://github.com/user-attachments/assets/9e1ea75a-a0fc-436e-ad0b-84785ebec937" />

I found an account that was still active for someone who no longer worked at the company, so I disabled the account instead of deleting it. This stopped the user from being able to log in while keeping the account in case it was needed later for auditing or recovery. Disabling an account instead of deleting it is a common part of the employee offboarding process. It also shows that I understand how to manage user accounts safely instead of just deleting accounts without considering what might be needed later.

<br><h2>4. Removing a Deprecated OU</h2>
<img width="473" height="473" alt="04-delete-protected-ou" src="https://github.com/user-attachments/assets/84e004ae-e477-4a6d-8b9c-95e4ceaf9b25" />

Active Directory protects OUs from being accidentally deleted by default. Since the Research and Development OU was no longer needed, I had to enable Advanced Features and turn off the “Protect object from accidental deletion” option before I could remove it. This helped me understand how Active Directory's built-in safety features work and why they are there. It also showed me that managing Active Directory is more than just clicking around the interface. You need to understand what the safety settings do and when it is appropriate to change them.

<br><h2>5. Organizing Devices into a Workstations OU</h2>
<img width="465" height="475" alt="05-workstations-ou" src="https://github.com/user-attachments/assets/784e48e8-dd98-4c72-99d3-093c7b30acf2" />

I created a dedicated Workstations OU and moved all of the end-user computers into it, keeping them separate from the servers. This makes it easier to apply device-specific policies, such as screen lock timers and restart settings, without affecting the servers. This is similar to what a help desk tech would do when setting up a new computer for an employee. Each new computer needs to be placed in the correct OU so it can automatically get the right security settings and policies.

<br><h2>6. Delegating Password Reset Rights</h2>
<img width="474" height="472" alt="06-delegate-control-wizard" src="https://github.com/user-attachments/assets/4cbe27f7-6354-4683-a8db-2fc965071180" />

I used the Delegation of Control Wizard to give a help desk account permission to reset passwords and require users to change their passwords. These permissions were limited to the Sales OU instead of giving the account full access to the entire domain. This helped me understand how least-privilege access works in a real IT environment. Help desk accounts should only have the permissions they need to do their job, which helps keep the rest of the network secure.

<br><h2>7a. Resetting a Password via PowerShell</h2>
<img width="476" height="472" alt="07a-powershell-password-reset" src="https://github.com/user-attachments/assets/ae75a7af-8143-497d-93a3-b46b4454ab44" />

I used the delegated account to run `Set-ADAccountPassword` in PowerShell and reset another user's password. I then confirmed that the password reset worked successfully. Learning how to do this through PowerShell is useful because help desk tasks can often be automated or handled through scripts instead of doing everything manually in Active Directory. This showed me that I can use the command line when needed instead of relying only on the graphical interface.

<br><h2>7b. Resetting a Password via PowerShell</h2>
<img width="475" height="470" alt="07b-login-verification" src="https://github.com/user-attachments/assets/0098b095-bfca-4425-80d1-ef4ab2c7cd45" />

I logged in as the affected user using the new password to make sure the reset actually worked. This was an important final step because a help desk ticket is not really solved just because the command runs successfully. The user also needs to be able to log back into their account. Checking this helps make sure the issue is fully resolved and can prevent the user from having to submit another ticket for the same problem.

<br><h2>8. Enforcing a Stronger Password Policy</h2>
<img width="473" height="499" alt="08-gpo-password-length" src="https://github.com/user-attachments/assets/71fd8279-be26-4519-8f81-8d48496a6a2a" />

In the Group Policy Management Editor, I changed the domain's minimum password length from 8 to 12 characters. This makes the password requirement stronger and helps protect accounts from common attacks. Changing security settings like this is a simple way to improve the overall security of the domain. It also helped me practice identifying a weak default setting and knowing when it should be changed instead of just following instructions.

<br><h2>9. Applying the Policy Change</h2>
<img width="474" height="471" alt="09-gpupdate-force-success" src="https://github.com/user-attachments/assets/6bf228b2-bd18-4529-8683-bd6b2d84f5a2" />

I ran 'gpupdate /force' and confirmed that the computer policy update completed successfully. This forced the new password policy to apply right away instead of waiting for the normal policy refresh. This is a useful command for help desk work because it can help when a new policy or setting is not showing up on a user's computer. It also gave me hands-on practice with Group Policy instead of only learning about it in theory.





















