# Key Commands Used

> Run relevant commands from an elevated PowerShell session in an authorized lab environment.

## Baseline and Validation
```powershell
Get-ComputerInfo | Select WindowsProductName, WindowsVersion, OsBuildNumber
Get-NetFirewallProfile | Select Name, Enabled
Get-MpComputerStatus | Select AntivirusEnabled, RealTimeProtectionEnabled, BehaviorMonitorEnabled, IoavProtectionEnabled
Get-LocalUser
net accounts
```

## Account Policy
```powershell
net accounts /minpwlen:12
net accounts /maxpwage:90
net accounts /minpwage:1
net accounts /uniquepw:10
net accounts /lockoutthreshold:5
net accounts /lockoutduration:15
net accounts /lockoutwindow:15
```

## Firewall
```powershell
Set-NetFirewallProfile -Profile Domain,Private,Public -Enabled True
Set-NetFirewallProfile -Profile Domain,Private,Public -DefaultInboundAction Block -DefaultOutboundAction Allow
Set-NetFirewallProfile -Profile Domain,Private,Public -LogBlocked True
Set-NetFirewallProfile -Profile Domain,Private,Public -LogMaxSizeKilobytes 4096
```

## Defender
```powershell
Set-MpPreference -DisableRealtimeMonitoring $false
Set-MpPreference -DisableBehaviorMonitoring $false
Set-MpPreference -DisableIOAVProtection $false
Set-MpPreference -PUAProtection Enabled
```

## UAC, Remote Desktop and SMB
```powershell
Get-ItemProperty HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System | Select EnableLUA,ConsentPromptBehaviorAdmin,PromptOnSecureDesktop
Get-ItemProperty "HKLM:\System\CurrentControlSet\Control\Terminal Server" | Select fDenyTSConnections
Get-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
Get-SmbServerConfiguration | Select EnableSMB1Protocol,EnableSMB2Protocol
```

## Security Auditing
```powershell
auditpol /set /subcategory:"Logon" /success:enable /failure:enable
auditpol /set /subcategory:"Account Lockout" /success:enable /failure:enable
auditpol /set /subcategory:"User Account Management" /success:enable /failure:enable
auditpol /set /subcategory:"Security Group Management" /success:enable /failure:enable
```
