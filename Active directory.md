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
- The AD DS data store contains the database files and processes that store and manage directory information for users, services and applications.
- It consists of the Ntds.dit file.
- It is stored by default in the %SystemRoot%\NTDS folder on all domain controllers.
- It is accessible only through the domain controller processes and protocols. 

## Logical AD Components 
## 1. AD DS Schema
- Define every type of object that can be stored in a directory.
- enforce rule regarding object creation and configuration. 
## 2. Domains
- domain are used to group and manage object in an organization.
## 3. Trees
- A domain tree is a hierarchy of domain in AD DS.
## 4. Forest 
- A forest is a collection of one or more domain trees.
## 5. Organizational Units
- OUs are Active directory containers that can contain users,group,computer and other OUs.
## 6.Trust
- Trust provide a mechanism fro users to gain access to resource  in other domain. 


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