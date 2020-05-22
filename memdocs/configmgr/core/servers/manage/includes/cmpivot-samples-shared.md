---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
---

<!--This file is shared by the CMPivot script samples articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->


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

The following query shows when devices have started in the last seven days:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
```

## Free disk space by device

The following query shows free disk space by device:

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

Gets the status of antimalware software installed on the computer.

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

The following query will look at events in the last 1 hour:

```kusto
CcmLog('Scripts',1h)
```

