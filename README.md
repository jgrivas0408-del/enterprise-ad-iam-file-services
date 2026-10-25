# Enterprise Active Directory, IAM & File Services Lab

**Author:** Joshua Gonzalez Rivas  
**Environment:** VMware • Windows Server 2022 • Windows 11

## Overview

I built a three-VM Windows domain to practice identity administration, delegated access, Group Policy, and secure departmental file services. This home lab developed skills relevant to IT support, systems administration, and IAM.

This repository documents a completed home lab. It currently contains documentation; original screenshots, scripts, and configuration exports have not been added. The implementation summary comes from my completed project record, rather than a fresh inspection of the VMs.

## Environment

| System | Role |
| --- | --- |
| DC01 | Active Directory Domain Services and DNS |
| FILE01 | Departmental SMB services and File Server Resource Manager |
| CLIENT01 | Domain-joined Windows workstation for access and policy checks |

## Implementation

### Active Directory and IAM

- Deployed AD DS and DNS and joined systems to the domain.
- Created tiered OUs, users, security groups, service and administrative accounts.
- Applied RBAC, least privilege, and AGDLP: Accounts → Global groups → Domain Local groups → Permissions.
- Separated Tier 0 and Tier 1 administrative responsibilities.
- Delegated Help Desk password reset and account unlock tasks.
- Practiced account recovery and domain sign-in verification.

### Group Policy

- Created and linked GPOs for account policies and workstation security settings.
- Configured server-local administrative access through Group Policy.
- Tested policy application through domain user sign-in and workstation checks.

### File services

- Configured departmental SMB services on a dedicated NTFS volume.
- Configured a hidden, encrypted SMB share with access-based enumeration.
- Applied group-based share and NTFS ACLs.
- Configured FSRM 3 GB quotas and active executable-file screening.
- Practiced file access checks and event-log validation.

Hidden shares still require authorization; hiding a share is not an access control. SMB encryption protects data in transit, and does not establish encryption at rest.

## Validation

During the lab I checked domain sign-in, password resets and account unlocks, Group Policy application, and SMB/NTFS access after permission adjustments. Raw outputs and screenshots are not yet included.

See the [validation and evidence checklist](docs/validation-and-evidence.md) for checks to capture when revisiting the lab. Expected results in that checklist are acceptance criteria, not newly executed test results.

## Skills

Windows Server • Active Directory • DNS • IAM • RBAC • AGDLP • Group Policy • Delegation • SMB • NTFS permissions • FSRM • Troubleshooting • Documentation

## Next improvements

- Add sanitized screenshots and configuration exports from the original VMs.
- Capture authorized and unauthorized departmental access results.
- Record effective Group Policy and FSRM enforcement results.
- Add automation after testing it in an isolated lab.

## Contact

[GitHub](https://github.com/jgrivas0408-del) · [LinkedIn](https://www.linkedin.com/in/joshua-gonzalez-rivas-7857b6393)
