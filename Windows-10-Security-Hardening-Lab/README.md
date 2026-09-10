# Windows 10 Security Hardening Lab

## Overview
This home lab demonstrates a practical Windows 10 workstation hardening workflow. I established a baseline, applied security controls, enabled logging and auditing, and validated the final configuration with PowerShell and Windows Event Viewer.

## Lab Environment
- Windows 10 Pro 22H2 (Build 19045)
- VMware Workstation
- Windows PowerShell
- Microsoft Defender Antivirus
- Windows Defender Firewall
- Windows Event Viewer

## Objectives
- Establish a security baseline before making changes
- Strengthen local password and account-lockout policies
- Secure the local administrator account
- Enable and configure Windows Defender Firewall
- Enable firewall logging for blocked traffic
- Validate Microsoft Defender protections and PUA protection
- Verify UAC and Remote Desktop security settings
- Confirm SMBv1 is disabled while SMBv2+ remains enabled
- Enable security auditing for authentication and account-management events
- Investigate failed logon activity using Windows Security Event ID 4625

## Hardening Performed

### 1. Baseline Assessment
The initial review showed that Windows Defender was active, but all three Windows Firewall profiles were disabled. The local password policy also had no minimum password length configured.

### 2. Password and Account-Lockout Policy
Configured the workstation with:
- Minimum password length: 12 characters
- Minimum password age: 1 day
- Maximum password age: 90 days
- Password history: 10 passwords
- Account lockout threshold: 5 failed attempts
- Account lockout duration: 15 minutes
- Lockout observation window: 15 minutes

### 3. Local Administrator Hardening
Verified that the built-in Administrator and Guest accounts were disabled. The active Admin account was configured to require a password and use password expiration.

### 4. Windows Defender Firewall
Enabled Domain, Private and Public firewall profiles. Configured default inbound traffic to Block and default outbound traffic to Allow.

Firewall logging for blocked traffic was enabled for all profiles with a 4096 KB log size.

### 5. Microsoft Defender
Validated that antivirus, real-time protection, behavior monitoring and downloaded-file protection were enabled. Potentially Unwanted Application (PUA) protection was also enabled.

### 6. UAC and Remote Access
Confirmed User Account Control was enabled, administrative prompts used the secure desktop, and Remote Desktop was disabled because it was not required for the lab workstation.

### 7. Legacy Protocol Review
Verified that SMBv1 was disabled and SMBv2+ remained enabled.

### 8. Security Auditing and Event Investigation
Enabled Success and Failure auditing for:
- Logon
- Account Lockout
- User Account Management
- Security Group Management

Generated controlled failed logon attempts using a temporary lab account and investigated Windows Security Event ID **4625 - An account failed to log on** in Event Viewer.

## Before vs After
| Control | Before | After |
|---|---|---|
| Domain Firewall | Disabled | Enabled |
| Private Firewall | Disabled | Enabled |
| Public Firewall | Disabled | Enabled |
| Default inbound firewall action | Not enforced with firewall disabled | Block |
| Minimum password length | 0 / None | 12 characters |
| Lockout threshold | 10 attempts | 5 attempts |
| Lockout duration | 10 minutes | 15 minutes |
| Admin password required | No | Yes |
| Firewall blocked-traffic logging | Not configured | Enabled |
| PUA protection | Baseline not relied upon | Enabled |
| SMBv1 | Disabled | Verified disabled |
| Security auditing | Baseline not relied upon | Success and Failure enabled |
| Failed-logon investigation | Not performed | Event ID 4625 validated |

## Evidence
Screenshots in the `screenshots/` folder document the baseline, configuration changes and final validation.

## Skills Demonstrated
Windows security hardening, endpoint security, Microsoft Defender, Windows Defender Firewall, local account security, password policy, PowerShell, security auditing, Event Viewer, authentication-event analysis, SMB security and workstation administration.

## Scope and Ethics
This project was performed only in my own isolated virtual lab for educational and defensive security practice.
