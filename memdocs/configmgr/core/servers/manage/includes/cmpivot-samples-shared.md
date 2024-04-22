---
ms.author: gokarthi
author: gowdhamankarthikeyan
ms.service: configuration-manager
ms.topic: include
ms.date: 02/25/2021
ms.localizationpriority: medium
---

<!--This file is shared by the CMPivot script samples articles for both Microsoft Intune tenant attach and Configuration Manager-->


## Operating system

Gets operating system information.

```kusto
// Sample query for OS information
OperatingSystem
```

## Recently used applications

The following query gets recently used applications (last 2 hours):

```kusto
CCMRecentlyUsedApplications
| where (LastUsedTime > ago(2h))
| project CompanyName, ProductName, ProductVersion, LastUsedTime
```

## Device start times

The following query shows when were the devices started in the last seven days:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
```

## Free disk space

The following query shows free disk space:

```kusto
LogicalDisk
| project Device, DeviceID, Name, Description, FileSystem, Size, FreeSpace
| order by DeviceID asc
```

## Device information

Show device, manufacturer, model, and OSVersion:

```kusto 
ComputerSystem
| project Device, Manufacturer, Model
| join (OperatingSystem | project Device, OSVersion=Caption)
```

## Boot times for a device

Show boot times for devices:

```kusto
SystemBootData
| project Device, SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
| order by SystemStartTime desc
```

## Authentication failures

Search the event logs for authentication failures.

```kusto
EventLog('Security')
| where  EventID == 4673
```

## ProcessModule(\<processname>)  

Enumerates all the modules (dlls) loaded by a given process. ProcessModule is useful when hunting for malware that hides in legitimate processes.  

```kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

## Antimalware software status

Gets the status of antimalware software installed on the computer gathered by the `Get-MpComputerStatus` cmdlet. The entity is supported on Windows 10 and Server 2016, or later with Defender running. <!--7643613-->|

```kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
```

## Find BIOS Manufacturer that contains any word like Micro

```kusto
Bios
// Find BIOS Manufacturer that contains any word like Micro, such as Microsoft
| where Manufacturer like '%Micro%'
```

## Find file by its hash

Search for a file by hash.

```kusto
Device
| join kind=leftouter ( File('%windir%\\system32\\*.exe')
| where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
| project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
```

## Find 'Scripts' in the CCM logs in the last hour

The following query looks at events in the last 1 hour:

```kusto
CcmLog('Scripts',1h)
```

## Find information in the registry

Search for registry information.

```kusto
// Change the path to match your desired registry hive query
// The RegistryKey entity (added in version 2107) isn't supported with CMPivot for tenant attached devices.  

Registry('hklm:\SOFTWARE\Microsoft\EnterpriseCertificates\Root\Certificates\*')
RegistryKey('hklm:\SOFTWARE\Microsoft\EnterpriseCertificates\Root\Certificates\*')

RegistryKey('hklm:\SOFTWARE\Microsoft\SMS\*')
Registry('hklm:\SOFTWARE\Microsoft\SMS\*')
```
