# Project 1: Windows Active Directory Security and Group Policy Lab

[Portfolio home](../README.md) · [Browse all screenshots](Screenshots/README.md)

## Project Overview

This project documents the deployment and security hardening of a Windows Active Directory (AD) lab in VMware Workstation.
I configured a Windows Server domain controller named DC01, deployed Active Directory Domain Services (AD DS) and Domain Name System (DNS) services, organized users and computers with organizational units (OUs) and security groups, and joined a Windows client named CLIENT01 to the domain.

I also implemented Group Policy settings for password security, account lockouts, Microsoft Defender, Windows Firewall, workstation security, and advanced auditing. The configuration was validated through domain-user logins, applied-policy results, effective audit-policy checks, and Windows Security event logs.

## Project Objectives

- Build a virtualized Windows enterprise lab using VMware.
- Configure Windows Server as an Active Directory domain controller and DNS server.
- Organize domain resources with organizational units, users, and security groups.
- Create a separate privileged administrative account.
- Join a Windows client workstation to the domain and validate domain authentication.
- Implement security-focused Group Policy Objects (GPOs) for accounts, endpoints, and auditing.
- Verify that the security policies were successfully applied.
- Confirm process-creation auditing through Windows Security Event ID 4688.

## Lab Environment and Technologies

| Component | Role in the Lab |
| --- | --- |
| VMware Workstation | Hosted the virtualized Windows lab environment. |
| DC01 | Windows Server domain controller providing AD DS, DNS, and Group Policy management. |
| CLIENT01 | Domain-joined Windows workstation used for authentication and policy testing. |
| Active Directory Domain Services | Provided centralized identity, computer, and access management. |
| Domain Name System | Allowed domain resources to locate and communicate with the domain controller. |
| Group Policy Management | Created and enforced domain-wide account, endpoint, and auditing policies. |
| Microsoft Defender and Windows Firewall | Provided endpoint protection and network security controls. |
| PowerShell and Command Prompt | Configured services and validated networking, identity, and applied policies. |
| Windows Event Viewer | Verified security auditing and process-creation events. |

## Lab Architecture

The lab was hosted in VMware Workstation and consisted of a Windows Server domain controller and a Windows client workstation. DC01 provided centralized identity, DNS resolution, authentication, and Group Policy settings to CLIENT01.

## Implementation

### 1. Domain Controller Deployment and Network Configuration

I created DC01 as a Windows Server virtual machine in VMware Workstation. After installing Windows Server, I renamed the system, configured its network settings, and validated connectivity before deploying the domain services.

![DC01 virtual machine hardware configuration](Screenshots/01_DC01_VM_Hardware.png)

*DC01 virtual machine hardware configuration in VMware Workstation.*

![DC01 network validation](Screenshots/04_DC01_Network_Validation.png)

*Network configuration and connectivity validation performed on DC01.*

### 2. Active Directory and DNS Deployment

I installed Active Directory Domain Services, promoted DC01 to a domain controller, and configured the Active Directory forest and integrated DNS services. I then validated the domain and DNS configuration to confirm that the required records and zones were operating correctly.

![Active Directory forest and DNS zones](Screenshots/05_AD_Forest_and_DNS_Zones.png)

*Active Directory forest and DNS zones hosted by DC01.*

![Active Directory and DNS health validation](Screenshots/06_AD_DNS_Health_Validation.png)

*Command-line validation of the domain controller and DNS services.*

### 3. Organizational Structure and Identity Management

After deploying the domain, I created a logical organizational unit structure to separate departments, users, security groups, and workstations. I created departmental security groups to support role-based access and configured a separate privileged administrative account to reduce the use of highly privileged credentials during normal operations. I then validated the Active Directory objects with PowerShell.

![Active Directory organizational unit structure](Screenshots/07_AD_OU_Structure.png)

*Organizational unit structure used to separate and manage resources.*

![Active Directory security groups](Screenshots/08_AD_Security_Groups.png)

*Departmental security groups created to support role-based access control.*

![Separate privileged administrative account](Screenshots/10_AD_Privileged_Account.png)

*Separate administrative account created for privileged domain-management tasks.*

![Active Directory identity validation](Screenshots/11_AD_Identity_Validation.png)

*PowerShell validation of organizational units, users, and security groups.*

### 4. Client Workstation Domain Integration

I configured CLIENT01 with the network and DNS settings required to communicate with DC01. I then joined the workstation to the domain, verified its secure channel, placed its computer object in the Workstations organizational unit, and successfully authenticated using a domain-user account.

![CLIENT01 domain-join validation](Screenshots/13_CLIENT01_Domain_Join_Validation.png)

*CLIENT01 successfully joined to the Active Directory domain.*

![CLIENT01 computer object in the Workstations OU](Screenshots/14_CLIENT01_Workstations_OU.png)

*CLIENT01 organized within the dedicated Workstations organizational unit.*

![CLIENT01 domain-user login](Screenshots/15_CLIENT01_Domain_User_Login.png)

*Successful domain-user authentication on CLIENT01.*

### 5. Group Policy Security Hardening

#### Account Security Policies

I created domain-level Group Policy Objects to enforce password and account-lockout requirements. These controls strengthened authentication security and reduced the risk of weak passwords and repeated password-guessing attempts. I then validated the effective domain account policy from the command line.

![Domain password policy](Screenshots/16_GPO_Password_Policy.png)

*Domain password requirements configured through Group Policy.*

![Domain account-lockout policy](Screenshots/17_GPO_Account_Lockout_Policy.png)

*Account-lockout controls configured to limit repeated authentication attempts.*

![Domain account-policy validation](Screenshots/18_GPO_Domain_Account_Policy_Validation.png)

*Effective domain password and account-lockout policies validated from the command line.*

#### Endpoint Protection and Firewall Policies

I created a workstation security baseline that included Windows security options, Microsoft Defender protections, security-intelligence updates, and Windows Firewall settings. The policies were applied centrally to CLIENT01 through Group Policy.

![CLIENT01 workstation-baseline validation](Screenshots/22_CLIENT01_Workstation_Baseline_Validation.png)

*Workstation security baseline successfully applied to CLIENT01.*

![Microsoft Defender real-time protection policy](Screenshots/23_GPO_Defender_Real_Time_Protection.png)

*Microsoft Defender real-time protection centrally configured through Group Policy.*

![Windows Firewall profile policies](Screenshots/26_GPO_Windows_Firewall_Profiles.png)

*Windows Firewall enabled and configured across the Domain, Private and Public profiles.*

### 6. Advanced Audit Policy and Event Validation

I configured Advanced Audit Policy through Group Policy to record logon and logoff activity, process creation, account management, policy changes, privilege use, and system events. I also enabled command-line information in process creation events to provide context during security investigations.

After applying the policies, I verified the complete set of security GPOs on CLIENT01, reviewed the effective audit configuration, and confirmed that Windows generated Security Event ID 4688 when a new process was created.

![Advanced audit command-line configuration](Screenshots/34_GPO_Advanced_Audit_Command_Line.png)

*Process command-line information enabled to provide additional detail in process-creation events.*

![All security GPOs applied to CLIENT01](Screenshots/35_CLIENT01_All_Security_GPOs_Applied.png)

*Group Policy results confirming that the security GPOs were applied to CLIENT01.*

![CLIENT01 effective audit policy](Screenshots/36_CLIENT01_Effective_Audit_Policy.png)

*Effective Advanced Audit Policy settings validated on CLIENT01.*

![Windows Security Event ID 4688](Screenshots/37_CLIENT01_4688_Process_Creation_Event.png)

*Security Event ID 4688 confirming that process-creation auditing was operating successfully.*

## Key Results

- Deployed a functional Active Directory domain with integrated DNS services.
- Centralized users, computers, security groups, and privileged accounts through Active Directory.
- Joined CLIENT01 to the domain and verified its secure connection to DC01.
- Enforced password, account-lockout, workstation, Microsoft Defender, and Windows Firewall policies through Group Policy.
- Enabled detailed Windows security auditing and command-line process logging.
- Validated the environment through PowerShell, Group Policy results, effective audit settings, and Security Event ID 4688.

## Skills Demonstrated

- Windows Server and Active Directory Domain Services
- DNS configuration and domain networking
- Organizational unit and security-group administration
- Identity and access management
- Group Policy creation and troubleshooting
- Endpoint protection and firewall policy management
- Advanced Audit Policy configuration
- Windows Security event validation

## Lessons Learned

Building the domain showed me how DNS, authentication, and Group Policy depend on one another. I checked domain connectivity and policy results at each stage so I could identify configuration problems before moving on.

I also learned to verify security controls through their results. Applied GPOs, effective audit settings, and Event ID 4688 provided different checks that the configuration was working.

## Screenshot Index

[Browse the complete screenshot index](Screenshots/README.md) for the remaining setup, investigation, and validation evidence.
