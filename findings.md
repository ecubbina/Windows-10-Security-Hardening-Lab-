# Windows 10 Security Hardening Findings Summary

## 1. Windows Firewall Disabled

**Initial State:**  
Windows Defender Firewall was disabled across Domain, Private, and Public network profiles.

**Risk:**  
Disabling the host firewall increases exposure to unsolicited inbound network connections.

**Remediation:**  
Enabled Windows Defender Firewall for all profiles and configured default inbound traffic to Block while allowing normal outbound traffic.

**Validation:**  
Confirmed all firewall profiles were enabled using PowerShell.

---

## 2. Weak Password Policy

**Initial State:**  
The workstation had no minimum password length configured.

**Risk:**  
Weak password requirements increase the likelihood of password guessing and brute-force attacks.

**Remediation:**  
Configured:
- Minimum password length: 12 characters
- Maximum password age: 90 days
- Minimum password age: 1 day
- Password history: 10
- Account lockout threshold: 5 attempts
- Lockout duration: 15 minutes
- Observation window: 15 minutes

**Validation:**  
Verified the new settings using `net accounts`.

---

## 3. Administrator Account Password Requirement

**Initial State:**  
The active Admin account did not require a password.

**Risk:**  
An administrator account without enforced password authentication can expose the workstation to unauthorized access.

**Remediation:**  
Enabled password requirements and configured password expiration for the Admin account.

**Validation:**  
Verified using `Get-LocalUser`.

---

## 4. SMBv1 Protocol Review

**Initial State:**  
SMBv1 was checked as part of protocol hardening.

**Result:**  
SMBv1 was already disabled.

**Security Benefit:**  
Disabling SMBv1 reduces exposure to vulnerabilities associated with the legacy SMB protocol.

**Validation:**  
Verified using Windows Optional Features and SMB Server configuration.

---

## 5. Security Auditing

**Initial State:**  
Security auditing was reviewed to improve visibility into authentication and account activity.

**Remediation:**  
Enabled Success and Failure auditing for:
- Logon
- Account Lockout
- User Account Management
- Security Group Management

**Validation:**  
Confirmed using `auditpol`.

---

## 6. Failed Logon Investigation

**Test:**  
Generated controlled failed authentication attempts using a temporary lab account.

**Detection:**  
Windows recorded failed logon activity as Security Event ID 4625.

**Investigation:**  
Reviewed failed authentication events using Windows Event Viewer.

**Security Value:**  
Demonstrated basic endpoint monitoring and investigation of suspicious authentication activity.
