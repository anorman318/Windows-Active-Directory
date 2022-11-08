# Windows-Active-Directory
Used Active Directory tools to create organizational units, users, and groups.
A Day in the Life of a Windows Sysadmin  

You will create domain-hardening GPOs and revisit some PowerShell fundamentals.  

**Task 1: Create a GPO - Disable Local Link Multicast Name Resolution (LLMNR)**   
For this first task, you will investigate and mitigate one of the attack vectors that exists within a Windows domain. Local Link Multicast Name Resolution (LLMNR) is a vulnerability, so you will disable it on your Windows 10 machine (via the GC Computers OU).  

**Instructions**  

Create a Group Policy Object that prevents your domain-joined Windows machine from using LLMNR.  

1. On the top right of the Server Manager screen, open the Group Policy Management tool to create a new GPO.  
2. Right-click Group Policy Objects and select New.  
3. Name the Group Policy Object No LLMNR.  
4. Right-click the new No LLMNR GPO listing and select Edit to open the Group Policy Management Editor and find policies.  
5.In the Group Policy Management Editor, you want the policy at the following path: Computer Configuration\Policies\Administrative Templates\Network\DNS Client.  
  * Find the policy called Turn Off Multicast Name Resolution.  
  * Enable this policy.  
6. Exit the Group Policy Management Editor and link the GPO to the GC Computers organizational unit that you previously created.  

<img width="797" alt="GPOs" src="https://user-images.githubusercontent.com/106919343/200668112-034763c2-ac4a-445d-a8f4-ca32505f1b6f.png">  

**Task 2: Create a GPO - Account Lockout**  
For security and compliance reasons, the CIO needs you to implement an account lockout policy on your Windows workstation. An account lockout disables access to an account for a set period of time after a specific number of failed login attempts. This policy defends against brute-force attacks, in which attackers can enter a million passwords in just a few minutes.  

**Instructions**  

Create what you believe to be a reasonable account lockout Group Policy for the Windows 10 machine.  
* Name the Group Policy Object Account Lockout.  
* You can use Microsoft's 10/15/15 recommendation if you'd like.  
* When editing policies for this new GPO, keep in mind that you want computer configuration policies to apply to your GC Computers OU. Also, these policies involve Windows security settings and accounts.  
* Don't forget to link the GPO to your GC Computers organizational unit.  

<img width="620" alt="Account-Lockout-Policies" src="https://user-images.githubusercontent.com/106919343/200669055-cec22fa5-36c4-47c9-bd69-ac1a92c87bac.png">  

**Task 3: Create a GPO - Enabling Verbose PowerShell Logging and Transcription**  

**Instructions**  

Create a Group Policy Object to enable PowerShell logging and transcription. This GPO will combine multiple policies into one, although they are all under the same policy collection.  
1. Name the Group Policy Object PowerShell Logging.  
2. Enable Turn on Module Logging and do the following:  
*   Click Show next to Module Names.  
*   Since you want to log all PowerShell modules, enter an asterisk * (wildcard) for the Module Name, then click OK.  
3. Enable the Turn on PowerShell Script Block Logging policy.  
4. Enable the Turn on Script Execution policy and do the following:  
*   Set Execution Policy to Allow all scripts.  
5. Enable the Turn on PowerShell Transcription policy and do the following:  
*   Leave the Transcript output directory blank (this defaults to the user's ~\Documents directory).  
* Check the Include invocation headers option. This will add timestamps to the command transcriptions.  
6. Leave the Set the default source path for Update-Help policy as Not configured.  
7.  Link this new PowerShell Logging GPO to the GC Computers OU.  
<img width="869" alt="Windows-Powershell-Policies" src="https://user-images.githubusercontent.com/106919343/200669871-eda20951-4543-4b9b-86f7-4c34b28835cb.png">  


**Task 4: Create a Script - Enumerate Access Control List**  

Create a PowerShell script that will enumerate the Access Control List of each file or subdirectory within the current working directory. To do so, complete the following steps:  
1. Create a foreach loop.  
2. Above the foreach condition, set a variable, $directory, to the contents of the current directory.  
3. Replace the script block placeholder with the command to enumerate the ACL of a file, using the $item variable in place of the file name.  
4. Save this script in C:\Users\sysadmin\Documents as enum_acls.ps1.  
5. Test this script by moving to any directory (cd C:\Windows), and running C:\Users\sysadmin\Documents\enum_acls.ps1 (enter the full path and file name).  

<img width="718" alt="enum_acls_ps1" src="https://user-images.githubusercontent.com/106919343/200670699-9724f39b-10e6-4431-9365-55ece6df4eac.png">  

<img width="635" alt="Powershell-logs" src="https://user-images.githubusercontent.com/106919343/200670725-97a67492-c2cb-47bd-8adf-057873ccee91.png">  

<img width="838" alt="Powershell-logs-cont" src="https://user-images.githubusercontent.com/106919343/200670740-19739d23-8ad9-4a42-84c5-50dc6817d63d.png">  




 



