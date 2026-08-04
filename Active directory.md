## What is Active directory?
- It is a directory service developed by microsoft to manage windows domain networks.
- It stores information related to objects such as computers, users,printers,etc.
- Authenticates using kerberos tickests.
## Physical AD Components
### 1.Domain controllers
- A domain controller is a windows server that acts as the central authority in an AD environment.
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