## What is Active directory?
- It is a directory service developed by microsoft to manage windows domain networks.
- It stores information related to objects such as computers, users,printers,servers,etc.
- Authenticates using kerberos tickests.
- AD is system used by an organization to manage their acomputer,users and access permission form one central place. 
- Instead of handling every computer and employee separately, Active Directory allows everything to be controlled in a structured and organized way. 
- At its core, Active Directory answers three basic questions for a company’s network: who are you, which computer are you using, and what are you allowed to access. Every time a user logs in to a system, opens a file, or accesses an application, Active Directory plays a role in deciding whether that action is allowed or denied.
## Physical AD Components
### 1.Domain controllers
- A domain controller is a windows server that acts as the central authority in an AD environment.
- It is a server that store all information about users, computers and security rules.
- Whenever someone logs in, the DC checks the credentials and decides whether access should be granted. 
- Its main roles are :
	- Host a copy of the AD domain services.
	- Provide Authentication and authorization services.
	- Replicate updates to other domain controllers in the domain and forest.
	- Allow administrative access to manage user accounts and network resources. 
### 2.AD DS Data Store
- The AD DS data store contains the database files and processes that store and manage directory information for users, groups,permissions, services and applications.
- When someone logs in to company computer , ADDS checks the username and password and decides whether the login in is allowed.
- **AD DS (Active Directory Domain Services)** = the **service/role** that provides Active Directory functionality.
- **DC (Domain Controller)** = a **server/computer running AD DS**.
- It consists of the Ntds.dit file.
- It is stored by default in the %SystemRoot%\NTDS folder on all domain controllers.
- It is accessible only through the domain controller processes and protocols. 

## Logical AD Components 

## AD CS (Active Directory Certificate Services)
- AD CS is used to issue digital certificate. These certificates proves identity and  allow secure communication between system , users and services. Certificates are used for secure logins, encrypted communication, and device authentication.
## AD FS (Active Directory Federation Services)
- Active Directory Federation Services allows users to log in once and access multiple applications, including cloud services, without entering their password again. This is commonly used for single sign-on with services like Office 365, Azure, or third-party applications.
## AD RMS (Active Directory Rights Management Services)
- Active Directory Rights Management Services is used to protect sensitive documents and emails. It controls who can open, copy, print, or forward a file, even after it leaves the company network.
## AD DS Schema
- Define every type of object that can be stored in a directory.
- enforce rule regarding object creation and configuration. 
## Group Policy Objects (GPOs)
- Group Policy Objects are rules that automatically apply settings to users and computers. These settings control security, software installation, system configuration, and user behavior.
- For example, a company can enforce strong passwords, disable USB storage, or install antivirus software on all computers using GPOs. Once configured, these rules apply automatically.
- This is useful because it ensures consistency and security across the organization. From an attacker’s perspective, GPOs are extremely powerful. If attackers gain control over GPOs, they can deploy malware to every computer, disable security tools, or create backdoor accounts across the entire network.
## Replication and Fault Tolerance 
- Active Directory uses multiple Domain Controllers to ensure availability. All Domain Controllers replicate data between each other so that changes made on one are reflected across the network.
- In real life, this is like having multiple copies of a company database stored in different offices. If one office goes down, another can still operate.
- This feature is useful because it prevents downtime and data loss. However, attackers can abuse replication. If an attacker compromises one Domain Controller, malicious changes can spread automatically to all others, making cleanup difficult and allowing persistence.
## Delegation and Administrative Control
- AD allows administrators to delegate specific tasks without giving full control . For example, a helpdesk employee maybe allow to reset password but not modify domain settings.
- **Delegation** allows you to grant users specific privileges to perform advanced tasks on OUs without needing a Domain Administrator to step in.
## Auditing and Logging
- Active Directory records login attempts, permission changes, and administrative actions. These logs help organizations detect suspicious activity.
- This feature is useful for defense and compliance. Attackers often attempt to disable logging or blend in with normal activity to avoid detection after compromising Active Directory.
## Kerberos Authentication
- Kerberos is the primary and most important authentication protocol used in Active Directory environments. It is designed to be secure, fast, and scalable.
- In simple terms, Kerberos works like a ticket system. When a user logs in, they first prove their identity to the Domain Controller. If the credentials are valid, the Domain Controller issues a ticket. This ticket is then used to access different services without repeatedly sending the password.
- In real life, Kerberos is similar to getting a wristband at an event. Once you get the wristband, you can enter different areas without showing your ID again.
- Kerberos is useful because passwords are not constantly transmitted over the network. However, attackers target Kerberos heavily. If attackers obtain password hashes or service tickets, they can perform attacks like Kerberoasting. By cracking these tickets offline, attackers can recover service account passwords, which often have high privileges and weak security.
## NTLM Authentication
- NTLM is an older authentication protocol that still exists for backward compatibility. It is less secure than Kerberos and relies on challenge-response mechanisms.
- In NTLM, the password hash is used to prove identity rather than a ticket system. This makes NTLM more vulnerable to attacks.
- Attackers love NTLM because it enables attacks like pass-the-hash. In these attacks, the attacker does not need the actual password. If they steal the hash, they can authenticate as the user. Many real-world breaches start with NTLM abuse, especially in legacy environments.
##  Domains
- domain are used to group and manage object in an organization.
## Trees
- A domain tree is a hierarchy of domain in AD DS.
## Forest 
- A forest is a collection of one or more domain trees.
## Organizational Units
- OUs are Active directory containers that can contain users,group,computer and other OUs.
## Trust
- Trust provide a mechanism fro users to gain access to resource  in other domain.
- Large organizations often have multiple domains that trust each other. Trust relationships allow users in one domain to access resources in another.
- This is useful for collaboration across departments or subsidiaries. Attackers abuse trust relationships to move from one domain to another, turning a small compromise into a large breach.

## REMINDER NOTES
- authentication is the process of proving who you are, Authorization is the process of deciding what you are allowed to do. AD handles both. when a user enter username and password , AD verifies their identity. once verified, it check's the user's permissions and allows or denies access to resources  

## Attacking Active Directory Initial Attack Vectors
### LLMNR(**Link-Local Multicast Name Resolution**) Poisoning
#### What is LLMNR
- Used to identify hosts when DNS fails to do so.
- It's a network protocol used by computers to resolve hostnames on a local network when DNS isn't available or doesn't have the answer.
- LLMNR poisoning is an attack where a malicious device on the same local network pretends to be the computer or server another device is trying to find.
- The best defence is to disable LLMNR and NBT-NS.
#### What is SMB relay?
- Instead of cracking hashes gathered with responder, we can instead relay those hashes to specific machines and potentially gain access. 
- Signing must be disabled on the target and relayed user credential must be admin on machine. 
- SMB relay do not involve cracking passwords.instead, they abuse trust during authentication.
- If you see "Message siging enabled but **not required** " then it means its vulnerable to smb relay.
---
## DNS Takeover Attacks 
- DNS is one of the most trusted services in Active Directory. Almost everything depends on DNS, including authentication and service discovery.
- DNS takeover attacks occur when attackers gain control over DNS records or DNS servers. This can happen through weak permissions, compromised DNS admins, or misconfigured AD-integrated DNS.
- Once attackers control DNS, they can redirect users and systems to malicious servers. This allows credential harvesting, malware delivery, and traffic interception.
- In real life, this is like changing office signboards so employees walk into the wrong rooms without realizing it.
- DNS takeover is extremely dangerous because it affects the entire domain silently. Attackers can impersonate critical services, capture authentication traffic, and persist without touching endpoints.
## Kerberoasting Attacks
- Kerberoasting is one of the most effective Active Directory attacks and works because of how Kerberos authentication is designed.
- In Kerberos, services use special accounts called service accounts. These accounts have Service Principal Names (SPNs). When a user wants to access a service, Active Directory issues a service ticket encrypted with the service account's password hash.
- Any authenticated user can request these tickets. Attackers do not need special privileges.
- Once attackers obtain the ticket, they extract it and crack it offline. If the service account uses a weak password, it can be cracked quickly.
- In real life, this is like requesting a locked document that uses a weak lock and taking it home to break it quietly.
- Kerberoasting is effective because service accounts often have high privileges and rarely change passwords. Once cracked, attackers can gain powerful access and move toward domain admin privileges.
- Tools like Mimikatz are used to extract tickets from memory or request them directly.

## Pass-the-Hash Attacks
- Pass-the-hash attacks allow attackers to authenticate without knowing the actual password.
- Windows stores password hashes in memory for authentication purposes. If attackers extract these hashes using tools like Mimikatz, they can reuse them to authenticate to other systems.
- In real life, this is like copying a fingerprint instead of knowing the PIN code.
- Pass-the-hash is effective because many systems still rely on NTLM authentication. As long as the hash is valid, the system accepts it.
- Attackers use pass-the-hash to move laterally across the network, escalate privileges, and maintain persistence.

## Token Impersonation Attacks
- Windows uses security tokens to represent user sessions. These tokens define what actions a user can perform.
- If an attacker gains access to a system and finds tokens belonging to higher-privileged users, they can impersonate those tokens.
- In real life, this is like stealing someone's access badge after they log in and using it to enter restricted areas.
- Token impersonation often occurs on compromised servers where administrators log in frequently. Attackers wait for a privileged user to log in, then steal the token.
- This allows attackers to execute commands as that user without knowing their password.

## Attcaking AD Post-Compromise Attack
### Pass the Password/Pass the hash
- if we crack a password and/or dump the SAM hash, we can leverage both for lateral movement in network.