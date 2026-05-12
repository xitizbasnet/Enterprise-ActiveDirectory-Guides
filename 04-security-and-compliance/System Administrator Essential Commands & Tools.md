# 🧑‍💻 L2 System Administrator

## 200 Essential Commands & Tools

### Covering AD, GPO, Troubleshooting, Network, Server & IIS

---

## 📘 Document Overview

This document is a **comprehensive reference guide** for L2 System Administrator interview preparation. It includes **200 essential commands and tools** across core IT infrastructure domains.

---

## 📊 Contents Overview

| Domain                     | Command Count |
| -------------------------- | ------------- |
| Active Directory (AD)      | 40            |
| Group Policy Objects (GPO) | 30            |
| Basic IT Troubleshooting   | 30            |
| Network Troubleshooting    | 35            |
| Server Troubleshooting     | 35            |
| IIS Server Management      | 30            |
| **Total Commands**         | **200**       |

---

## 📅 Document Metadata

* **Generated Date:** April 29, 2026

---

# 🟦 Active Directory (AD) — 40 Commands

## 👤 User & Object Management

```text id="ad1"
dsquery user
```

Query users in Active Directory

```text id="ad2"
dsget user
```

Get user properties from AD

```text id="ad3"
dsadd user
```

Add new users to Active Directory

```text id="ad4"
dsmod user
```

Modify user properties in AD

```text id="ad5"
dsrm
```

Remove objects from Active Directory

```text id="ad6"
dsquery computer
```

Query computers in AD

---

## 🧑‍💻 PowerShell AD Commands

```powershell id="ad7"
Get-ADUser
```

Retrieve AD user objects and properties

```powershell id="ad8"
Get-ADComputer
```

Get computer objects from Active Directory

```powershell id="ad9"
New-ADUser
```

Create new AD user account

```powershell id="ad10"
Set-ADUser
```

Modify AD user properties

```powershell id="ad11"
Remove-ADUser
```

Delete AD user account

```powershell id="ad12"
Set-ADAccountPassword
```

Reset user password in AD

```powershell id="ad13"
Unlock-ADAccount
```

Unlock locked AD user accounts

```powershell id="ad14"
Enable-ADAccount
```

Enable disabled AD accounts

```powershell id="ad15"
Disable-ADAccount
```

Disable active AD accounts

---

## 👥 Groups & OUs

```powershell id="ad16"
Get-ADGroup
```

Retrieve AD group objects

```powershell id="ad17"
New-ADGroup
```

Create new security/distribution groups

```powershell id="ad18"
Add-ADGroupMember
```

Add members to AD groups

```powershell id="ad19"
Remove-ADGroupMember
```

Remove members from groups

```powershell id="ad20"
Get-ADGroupMember
```

List group membership

```powershell id="ad21"
Get-ADOrganizationalUnit
```

Query organizational units

```powershell id="ad22"
Move-ADObject
```

Move AD objects between OUs

---

## 🔧 AD Utilities

```text id="ad23"
dsquery group
```

Find groups in Active Directory

```text id="ad24"
net group
```

Manage local/domain groups

```text id="ad25"
net user
```

Manage user accounts

```text id="ad26"
whoami /groups
```

Display group membership

```text id="ad27"
whoami /upn
```

Show UPN of user

```text id="ad28"
whoami /logonid
```

Display logon ID

```text id="ad29"
gpresult /h
```

Generate GPO report

```text id="ad30"
repadmin /syncall
```

Force AD replication

```text id="ad31"
repadmin /showrepl
```

Show replication status

```text id="ad32"
repadmin /replsum
```

Replication summary

```text id="ad33"
netdom query fsmo
```

Show FSMO roles

```text id="ad34"
dcdiag
```

Domain controller diagnostics

```text id="ad35"
ntdsutil
```

AD database management

```text id="ad36"
ldifde
```

Import/export AD objects

```text id="ad37"
csvde
```

CSV-based AD import/export

```text id="ad38"
Get-ADReplicationPartnerMetadata
```

Replication metadata

```text id="ad39"
Test-ADServiceAccount
```

Validate service accounts

---

# 🟨 Group Policy Objects (GPO) — 30 Commands

```text id="gpo1"
gpupdate /force
```

Force GPO update

```text id="gpo2"
gpupdate /force /boot
```

Force update with reboot

```text id="gpo3"
gpupdate /target:user
```

User policy update

```text id="gpo4"
gpupdate /target:computer
```

Computer policy update

```text id="gpo5"
gpedit.msc
```

Local Group Policy Editor

```text id="gpo6"
gpmc.msc
```

Group Policy Management Console

```powershell id="gpo7"
Get-GPO
```

List GPOs

```powershell id="gpo8"
Get-GPOReport
```

Generate GPO report

```powershell id="gpo9"
New-GPO
```

Create GPO

```powershell id="gpo10"
Set-GPRegistryValue
```

Set registry via GPO

```powershell id="gpo11"
Remove-GPO
```

Delete GPO

```powershell id="gpo12"
New-GPLink
```

Link GPO to OU

```powershell id="gpo13"
Remove-GPLink
```

Remove GPO link

```powershell id="gpo14"
Set-GPLink
```

Modify GPO link

```powershell id="gpo15"
Get-GPLink
```

View GPO links

```powershell id="gpo16"
Invoke-GPUpdate
```

Remote GPO update

```text id="gpo17"
gpresult /h report.html
```

GPO report

```text id="gpo18"
gpresult /user domain\\username /h
```

User GPO report

```text id="gpo19"
gpresult /computer computername /h
```

Computer GPO report

```text id="gpo20"
gpresult /scope:user
```

User policy scope

```text id="gpo21"
gpresult /scope:computer
```

Computer policy scope

```text id="gpo22"
dcgpofix /ignoredomain
```

Restore default GPOs

```text id="gpo23"
dsacls
```

AD permissions

```powershell id="gpo24"
Backup-GPO
```

Backup GPO

```powershell id="gpo25"
Restore-GPO
```

Restore GPO

---

# 🟩 Basic IT Troubleshooting — 30 Commands

```text id="it1"
ipconfig /all
```

Network configuration

```text id="it2"
ipconfig /flushdns
```

Clear DNS cache

```text id="it3"
nslookup hostname
```

DNS lookup

```text id="it4"
ping -t hostname
```

Continuous ping

```text id="it5"
tracert hostname
```

Trace route

```text id="it6"
netstat -ano
```

Active connections

```text id="it7"
tasklist
```

Running processes

```text id="it8"
taskkill /pid PID
```

Kill process

```text id="it9"
systeminfo
```

System details

```text id="it10"
msinfo32
```

System info GUI

```text id="it11"
services.msc
```

Services console

```text id="it12"
net start servicename
```

Start service

```text id="it13"
sfc /scannow
```

System repair

```text id="it14"
dism /online /cleanup-image /restorehealth
```

Windows repair

```text id="it15"
chkdsk /f /r
```

Disk check

---

# 🌐 Network Troubleshooting — 35 Commands

```text id="net1"
ping 8.8.8.8
```

Internet test

```text id="net2"
tracert 8.8.8.8
```

Route trace

```text id="net3"
pathping hostname
```

Advanced ping

```text id="net4"
route print
```

Routing table

```text id="net5"
arp -a
```

ARP table

```text id="net6"
telnet hostname port
```

Port test

```powershell id="net7"
Test-NetConnection
```

Network test

```powershell id="net8"
Resolve-DnsName
```

DNS resolution

```powershell id="net9"
Get-NetAdapter
```

Network adapters

```powershell id="net10"
Get-NetIPConfiguration
```

IP configuration

---

# 🖥️ Server Troubleshooting — 35 Commands

```powershell id="srv1"
Get-Process
```

Process monitoring

```powershell id="srv2"
Get-Service
```

Service status

```powershell id="srv3"
Restart-Computer
```

Reboot server

```powershell id="srv4"
Get-EventLog
```

System logs

```powershell id="srv5"
Get-WinEvent
```

Security logs

```powershell id="srv6"
Get-Disk
```

Disk info

---

# 🌐 IIS Server Management — 30 Commands

```text id="iis1"
iisreset
```

Restart IIS

```text id="iis2"
appcmd list site
```

List websites

```text id="iis3"
appcmd list apppool
```

App pools

```text id="iis4"
appcmd add site
```

Create site

```text id="iis5"
appcmd delete site
```

Delete site

```powershell id="iis6"
Get-IISSite
```

IIS sites

```powershell id="iis7"
New-IISSite
```

Create site (PS)

```powershell id="iis8"
Start-WebSite
```

Start site

```powershell id="iis9"
Stop-WebSite
```

Stop site

---

# 📌 Summary

This document provides a **200-command L2 System Administrator reference guide** covering:

* Active Directory (AD)
* Group Policy (GPO)
* System troubleshooting
* Network diagnostics
* Server administration
* IIS management

It is designed as a **job-ready interview preparation and operational reference manual** for enterprise IT environments.
