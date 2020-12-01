# PSCCMClient PowerShell Module

## What is it?
PSCCMClient is a PowerShell module focused around interaction with the Microsoft Endpoint Manager Configuration Manager (MEMCM/MECM/ConfigMgr/SCCM/SMS) client. The general theme is to provide functions that 'work as expected' in that they accept pipeline where possible, such as with the below examples, as well as an array of Computer Names, CimSessions, or PSSessions.

```Powershell
Get-CCMUpdate | Invoke-CCMUpdate
Get-CCMPackage -PackageName 'Install Company Software' -ComputerName Workstation1 | Invoke-CCMPackage
Get-CCMServiceWindow | ConvertFrom-CCMSchedule
Get-CCMBaseline -BaselineName 'Cache Management' -CimSession $CimSession1 | Invoke-CCMBaseline
Get-CCMApplication -ApplicationName '7-Zip' -ComputerName Workstation1 | Invoke-CCMApplication -Method Uninstall
```

Largely this is leveraging CIM to gather info, and act upon it. This is why there are custom functions to make registry edits, and gather registry info via CIM. By consistently using CIM, we can ensure that a CimSession can be used for efficiency.  A PSSession parameter is also available on all functions for an alternative remote connection. In some cases, invoking CIMMethods over a CIMSession does not function well for the MEMCM client. This can be seen with the methods on SMS_CLIENT in the root\CCM Namespace and by trying to invoke updates remotely with CIM. In previous iterations of this module, I was executing arbitrary code via the Win32_Process:CreateProcess method. In order to do this, code was being converted to, and from Base64. This was commonly a red flag for enterprise AV. I have since removed the code that does Base64 conversion, but I am open to creative ideas!

## [Usage](docs)

## [Contributing](CONTRIBUTING.md)

## List of functions:

* ConvertFrom-CCMLogFile
    * Alias: Get-CCMLogFile
* ConvertFrom-CCMSchedule
* ConvertTo-CCMLogFile
* Get-CCMApplication
* Get-CCMBaseline
    * Alias: Get-CCMCB
* Get-CCMCacheContent
* Get-CCMCacheInfo
* Get-CCMCimInstance
* Get-CCMClientDirectory
* Get-CCMClientInfo
* Get-CCMClientVersion
* Get-CCMCurrentManagementPoint
    * Alias: Get-CCMCurrentMP
    * Alias: Get-CCMMP
* Get-CCMCurrentSoftwareUpdatePoint
    * Alias: Get-CCMCurrentSUP
    * Alias: Get-CCMSUP
* Get-CCMCurrentWindowAvailableTime
* Get-CCMDNSSuffix
* Get-CCMExecStartupTime
* Get-CCMGUID
* Get-CCMLastHardwareInventory
    * Alias: Get-CCMLastHINV
* Get-CCMLastHeartbeat
    * Alias: Get-CCMLastDDR
* Get-CCMLastScheduleTrigger
* Get-CCMLastSoftwareInventory
    * Alias: Get-CCMLastSINV
* Get-CCMLoggingConfiguration
* Get-CCMMaintenanceWindow
    * Alias: Get-CCMMW
* Get-CCMPackage
* Get-CCMPrimaryUser
* Get-CCMProvisioningMode
* Get-CCMRegistryProperty
    * Alias: Get-CIMRegistryProperty
* Get-CCMServiceWindow
* Get-CCMSite
* Get-CCMSoftwareUpdate
    * Alias: Get-CCMUpdate
* Get-CCMSoftwareUpdateGroup
    * Alias: Get-CCMSUG
* Get-CCMSoftwareUpdateSettings
* Get-CCMTaskSequence
* Invoke-CCMApplication
* Invoke-CCMBaseline
* Invoke-CCMClientAction
* Invoke-CCMCommand
* Invoke-CCMPackage
* Invoke-CCMResetPolicy
* Invoke-CCMSoftwareUpdate
    * Alias: Invoke-CCMUpdate
* Invoke-CCMTaskSequence
* Invoke-CCMTriggerSchedule
* Invoke-CIMPowerShell
* New-LoopAction
* Remove-CCMCacheContent
* Repair-CCMCacheLocation
* Set-CCMCacheLocation
* Set-CCMCacheSize
* Set-CCMClientAlwaysOnInternet
* Set-CCMDNSSuffix
* Set-CCMLoggingConfiguration
* Set-CCMManagementPoint
    * Alias: Set-CCMMP
* Set-CCMProvisioningMode
* Set-CCMRegistryProperty
    * Alias: Set-CIMRegistryProperty
* Set-CCMSite
* Test-CCMIsClientAlwaysOnInternet
* Test-CCMIsClientOnInternet
* Test-CCMIsWindowAvailableNow
* Test-CCMStaleLog
* Write-CCMLogEntry
