---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
---

<!--This file is shared by the CMPivot script samples articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

> [!Important]
> - File retrieval entities aren't supported when you run CMPivot from Microsoft Endpoint Manager.
## Count of operating systems

Gets a count of operating systems and presents it in a bar chart.

```kusto
// Sample query for OS count
OperatingSystem
| summarize count() by Caption
| order by count_ asc
| render barchart
```

## Recently used applications

The following query renders the most recently used applications as a bar chart:

```kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

## Time chart for device start times

The following query shows when devices have started in the last seven days:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

## Free disk space by device

The following query shows free disk space by device:

```kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

## Device information 

Show device, manufacturer, model, and OSVersion:

```kusto 
ComputerSystem
| project Device, Manufacturer, Model
| join (OperatingSystem | project Device, OSVersion=Caption)
```

## Boot times for a device

Show a graph of boot times for a device:

```kusto
SystemBootData
| where Device == 'MyDevice'
| project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
| order by SystemStartTime desc
| render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
```

## Authentication failures

Search all event logs on all clients in your enterprise for authentication failures.

```kusto
EventLog('Security')
| where  EventID == 4673
| summarize count() by Device
| order by count_ desc
```

## Event log errors for Windows Hello for Business

Lists errors in the event log for Windows Hello for Business within the last day.

```kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

## ProcessModule(\<processname>)  

Enumerates all the modules (dlls) loaded by a given process. ProcessModule is useful when hunting for malware that hides in legitimate processes.  

```kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

## Azure Active Directory identity information

Get the current Azure Active Directory identity information from a device.

```kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

## Antimalware software status

Gets the status of antimalware software installed on the computer.

```kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
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

## <a name="bkmk_File"></a> Get file content(\<filename>)

Gets the contents of a text file.

```kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

## Find 'Scripts' in the CCM logs in the last hour

The following query will look at events in the last 1 hour:

```kusto
CcmLog('Scripts',1h)
```