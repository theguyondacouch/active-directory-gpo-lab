# active-directory-gpo-lab
Active Directory and Group Policy lab with role-based GPO design and validation

--SETUP--
*Diagnosed BIOS virtualization
*Resolved EFI boot fialures
*Corrected Virtual box config
*Installed a server OS from Scratch

* built a virtualization lab from scrath
*resolved BIOS + hypervisor conflicts
*installed windows server manualy
*Completed first-boot Config


*Deployed Active Directory Domain Service on Windows server 2022
*Designed OU Structure aligned

User policy validation was inittially performed on the 
domain controler due to workstation availability.A Domain-joined
Windows workstation was later added to fully validate user-side GPO behavior. 

Standard domain users are intentionaly denied interactive logon
 to Domain Controlers via Group Policy. Login failure confrims correct
 enforcement of least privaliged access.


musicguy1985@gmail.com
5:18 PM (3 minutes ago)
to me

# Active Directory & Group Policy Lab

## Overview
This lab demonstrates the deployment of a Windows Server 2022 domain controller, Active Directory structure design, and Group Policy configuration in a virtualized lab environment.

The goal was to simulate a small enterprise domain while following best practices for:
- OU design
- Least privilege
- Group Policy security filtering
- Change control using VM snapshots

## Environment
- Hypervisor: VirtualBox
- Server OS: Windows Server 2022
- Domain: lab.local
- Roles:
  - Active Directory Domain Services
  - DNS
  - Group Policy Management

## Lab Phases

### Phase A – Active Directory Setup
- Installed Windows Server 2022
- Promoted server to Domain Controller
- Configured DNS
- Created Organizational Unit (OU) structure
- Created security groups

### Phase B – Group Policy Design
- Created baseline GPOs:
  - Standard Users
  - IT Users
- Linked GPOs to appropriate OUs
- Implemented security filtering
- Validated permissions

### Phase C – Policy Validation
- Used Group Policy Modeling (Planning Mode)
- Verified GPO scope and precedence
- Identified and corrected security filtering issues
- Documented expected vs actual behavior

## Key Skills Demonstrated
- Active Directory administration
- Group Policy Management
- OU and security group design
- Troubleshooting authentication and policy issues
- Change management using VM snapshots

## Status
Lab is actively expanding. Future phases will include:
- Client workstation VMs
- User-based policy testing
- Login restrictions validation

# Phase A – Active Directory Setup

## Objective
Deploy a Windows Server 2022 domain controller and establish a clean AD foundation.

## Steps Completed
1. Installed Windows Server 2022 in VirtualBox
2. Enabled virtualization and EFI boot
3. Assigned static IPv4 configuration
4. Installed AD DS and DNS roles
5. Promoted server to domain controller
6. Created domain: lab.local

## OU Structure

# Active Directory & Group Policy Lab

## Overview
This lab demonstrates the design, implementation, and validation of Active Directory Group Policy in a Windows Server environment. The project emphasizes **enterprise best practices**, including least-privilege access, role-based policy targeting, and controlled validation before client rollout.

The lab is structured into clear phases to reflect how Group Policy is deployed and tested in real-world environments.

---

## Phase B – Group Policy Design & Targeting

### Objective
Design and deploy role-based Group Policy Objects (GPOs) using Organizational Units (OUs) and security filtering to ensure precise policy application.

### Key Activities
- Created separate baseline GPOs for each user role:
  - Standard Users
  - IT Users
  - HR Users
- Linked each GPO to its corresponding OU
- Applied security filtering using role-based security groups
- Removed `Authenticated Users` to prevent unintended policy scope
- Added `Domain Computers` to maintain required read permissions

### Design Principles
- Policies are **scoped by OU** and **authorized by group membership**
- Default Domain Policy was not modified
- Each role receives only the policies intended for it

### Outcome
Group Policy Objects were correctly scoped and filtered, ensuring clean separation of policy behavior across user roles.

---

## Phase C – Policy Validation & Verification

### Objective
Validate Group Policy behavior prior to deploying client workstations.

### Validation Method
Because client workstation VMs were not yet deployed, validation was performed using:
- **Group Policy Modeling (Planning Mode)**
- Controlled test user accounts
- Observed authentication behavior on the Domain Controller

### Key Findings
- Group Policy Modeling confirmed correct policy application based on:
  - OU placement
  - Security group membership
- Standard users were intentionally denied interactive logon to the Domain Controller
- Login denial confirmed enforcement of least-privilege security controls

### Important Observation
User login restrictions on the Domain Controller were **intentional and expected**. 
In production environments, Domain Controllers are reserved for administrative access only.

### Outcome
Policies behaved exactly as designed, validating:
- GPO linking
- Security filtering
- Policy precedence
- Least-privilege enforcement
