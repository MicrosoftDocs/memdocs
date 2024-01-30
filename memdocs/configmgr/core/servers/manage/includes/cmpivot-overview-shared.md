---
ms.author: gokarthi
author: gowdhamankarthikeyan
ms.service: configuration-manager
ms.topic: include
ms.date: 08/02/2021
ms.localizationpriority: medium
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Intune tenant attach and Configuration Manager-->

## Queries

Queries can be used to search terms, identify trends, analyze patterns, and provide many other insights based on your data. CMPivot uses a subset of the [Azure Log Analytics](/azure/kusto/query) data flow model for the tabular expression statement. The typical structure of a tabular expression statement is a composition of client entities and tabular data operators (such as filters and projections). The composition is represented by the pipe character (|), giving the statement a regular form that visually represents the flow of tabular data from left to right. Each operator accepts a tabular data set "from the pipe", and additional inputs (including other tabular data sets) from the body of the operator, then emits a tabular data set to the next operator that follows:
`entity | operator1 | operator2 | ...`

In the following example, the entity is `CCMRecentlyUsedApplications` (a reference to the recently used applications), and the operator is where (which filter out records from its input according to some per-record predicate):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## Entities

Entities are objects that can be queried from the client. We currently support the following entities:


|Entity|Description|
|---|---|
|AadStatus|Status of Microsoft Entra ID|
|Administrators|Members of the local administrators group|
|AppCrash|Recent application crash reports|
|AppVClientApplication|AppV Client Application|
|AppVClientPackage|AppV Client Package|
|AutoStartSoftware|Software that starts automatically with, or immediately after, the operating system|
|BaseBoard|BaseBoard|
|Battery|Battery|
|Bios|System BIOS information|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker Encryption Details|
|BitLockerPolicy|BitLocker Policy|
|BootConfiguration|Boot Configuration|
|BrowserHelperObject|Browser Helper Object|
|BrowserUsage|Browser Usage|
|CcmLog()|Lines within 24 hours (by default) from a Ccm Log file|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Recently Used Applications|
|CCMWebAppInstallInfo|Web Applications|
|CDROM|CDROM Drive|
|ClientEvents|Client Events|
|ComputerSystem|Computer System|
|ComputerSystemEx|Computer System Ex|
|ComputerSystemProduct|Computer System Product|
|ConnectedDevice|Connected Device|
|Connection|An active Tcp connection in or out of the device|
|Desktop|Desktop|
|DesktopMonitor|Desktop Monitor|
|Device|Basic information about the device|
|Disk|Local storage device information on a computer system running Windows|
|DMA|DMA|
|DMAChannel|DMA Channel|
|DriverVxD|Driver - VxD|
|EmbeddedDeviceInformation|Embedded Device Information|
|Environment|Environment|
|EPStatus|Status of antimalware software on the computer gathered by the `Get-MpComputerStatus` cmdlet. Supported on Windows 10 and Server 2016, or later with defender running. <!--7643613-->|
|EventLog()|Events within 24 hours (by default) from an event log|
|File()|Information about a specific file|
|FileShare|Active file share information|
|Firmware|Firmware|
|IDEController|IDE Controller|
|InstalledExecutable|Installed Executable|
|InstalledSoftware|An application installed on the device|
|IPConfig|Gets network configuration, including usable interfaces, IP addresses, and DNS servers|
|IRQTable|IRQ Table|
|Keyboard|Keyboard|
|LoadOrderGroup|Load Order Group|
|LogicalDisk|Logical Disk|
|MDMDevDetail|Device Information|
|Memory|Memory|
|Modem|Modem|
|Motherboard|Motherboard|
|NetworkAdapter|Network Adapter|
|NetworkAdapterConfiguration|Network Adapter Configuration|
|NetworkClient|Network Client|
|NetworkLoginProfile|Network Login Profile|
|NTEventlogFile|NT Eventlog File|
|Office365ProPlusConfigurations|Office 365 Apps Configurations|
|OfficeAddin|Office add-ins|
|OfficeClientMetric|Office Client Metric|
|OfficeDeviceSummary|Office Device Summary|
|OfficeDocumentMetric|Office document metrics|
|OfficeDocumentSolution|Office Document Solution|
|OfficeMacroError|Office Macro Error|
|OfficeProductInfo|Office Product Info|
|OfficeVbaRuleViolation|Office Vba Rule Violation|
|OfficeVbaSummary|Office VBA scan summary|
|OperatingSystem|Operating System|
|OperatingSystemEx|Operating System Ex|
|OperatingSystemRecoveryConfiguration|Operating System Recovery Configuration|
|OptionalFeature|Optional Feature|
|OS|Basic information about the operating system|
|PageFileSetting|Page File Setting|
|ParallelPort|Parallel Port|
|Partition|Disk Partitions|
|PCMCIAController|PCMCIA Controller|
|PhysicalDisk|PhysicalDisk|
|PhysicalMemory|Physical Memory|
|PNPDEVICEDRIVER|PNP Device Driver|
|PointingDevice|Pointing Device|
|PortableBattery|Portable Battery|
|Ports|Ports|
|PowerCapabilities|Power Capabilities|
|PowerClientOptOutSettings|Power Management Exclusion Settings|
|PowerConfigurations|Power Configuration|
|PowerManagementDaily|Power Management Daily Data|
|PowerManagementInsomniaReasons|Power Insomnia Reasons|
|PowerManagementMonthly|Power Management Monthly Data|
|PowerSettings|Power Settings|
|PrinterConfiguration|Printer Configuration|
|PrinterDevice|Printer Device|
|PrintJobs|Print Jobs|
|Process|A process on an operating system|
|ProcessModule()|Modules loaded by specified processes|
|Processor|Processor|
|ProtectedVolumeInformation|Protected Volume Information|
|Protocol|Protocol|
|QuickFixEngineering|Quick Fix Engineering|
|Registry|All values for a specific registry key<!--7371183--> </br></br>Starting in version 2107, Key value was added to the Registry() entity <!--9966861-->|
|SCSIController|SCSI Controller|
|SerialPortConfiguration|Serial Port Configuration|
|SerialPorts|Serial Ports|
|ServerFeature|Server Feature|
|Service|A service on a computer system running Windows|
|Services|Services|
|Shares|Shares|
|SMBConfig|SMB Configuration of a device|
|SMSAdvancedClientPorts|Configuration Manager Client Ports|
|SMSAdvancedClientSSLConfigurations|Configuration Manager Client SSL Configurations|
|SMSAdvancedClientState|Configuration Manager Client State|
|SMSDefaultBrowser|Default Browser|
|SMSSoftwareTag|Software Tag|
|SMSWindows8Application|Windows app|
|SMSWindows8ApplicationUserInfo|Windows app User Info|
|SoftwareShortcut|Software Shortcut|
|SoftwareUpdate|A software update applicable but not installed on the device|
|SoundDevices|Sound Devices|
|SWLicensingProduct|Software Licensing Product|
|SWLicensingService|Software Licensing Service|
|SystemAccount|System Account|
|SystemBootData|System Boot Data|
|SystemBootSummary|System Boot Summary|
|SystemConsoleUsage|System Console Usage|
|SystemConsoleUser|System Console User|
|SystemDevices|System Devices|
|SystemDrivers|System Drivers|
|SystemEnclosure|System Enclosure|
|TapeDrive|Tape Drive|
|TimeZone|Time Zone|
|TPM|TPM|
|TPMStatus|TPM Status|
|TSIssuedLicense|TS Issued License|
|TSLicenseKeyPack|TS License Key Pack|
|UninterruptiblePowerSupply|Uninterruptible Power Supply|
|USBController|USB Controller|
|USBDevice|USB Device|
|User|A user account with an active connection to the device|
|USMFolderRedirectionHealth|Folder Redirection Health|
|USMUserProfile|User Profile Health|
|VideoController|Video Controller|
|VirtualMachine|Virtual Machine|
|VirtualMachine64|Virtual Machine (64)|
|Volume|Volume|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Windows Update Agent Version|
|WinEvent()|Events within 24 hours (by default) from a Windows event log|
|WriteFilterState|Write Filter State|

## Table operators

Table operators can be used filter, summarize, and transform data streams. Currently the following operators are supported:

|Table operators|Description|
|---|---|
|count|Returns a table with a single record containing the number of records|
|distinct|Produces a table with the distinct combination of the provided columns of the input table|
|join|Merge the rows of two tables to form a new table by matching row for the same device|
|order by|Sort the rows of the input table into order by one or more columns|
|project|Select the columns to include, rename or drop, and insert new computed columns|
|take|Return up to the specified number of rows|
|top|Returns the first N records sorted by the specified columns|
|where|Filters a table to the subset of rows that satisfy a predicate|

## Scalar Operators

The following table summarizes operators:

|Operators|Description|Example
|---|---|---|
|==|Equal|`1 == 1, 'aBc' == 'AbC'`|
|!=|Not Equal|`1 != 2, 'abc' != 'abcd'`|
|< |Less|`1 < 2, 'abc' < 'DEF'`|
|> |Greater|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Less or Equal|`1 <= 2, 'abc' <= 'abc'`|
|>=|Greater or Equal|`2 >= 1, 'abc' >= 'ABC'`|
|+|Add|`2 + 1, now() + 1d`|
|-|Subtract|`2 - 1, now() - 1h`|
|*|Multiply|`2 * 2`|
|/|Divide|`2 / 1`|
|%|Modulo|`2 % 1`|
|like|Left Hand Side (LHS) contains a match for Right Hand Side (RHS)|`'abc' like '%B%'`|
|!like|LHS doesn't contain a match for RHS|`'abc' !like '_d_'`|
|contains|RHS occurs as a subsequence of LHS|`'abc' contains 'b'`|
|!contains|RHS doesn't occur in LHS|`'team' !contains 'i'`|
|startswith|RHS is an initial subsequence of LHS|`'team' startswith 'tea'`|
|!startswith|RHS isn't an initial subsequence of LHS|`'abc' !startswith 'bc'`|
|endswith|RHS is a closing subsequence of LHS|`'abc' endswith 'bc'`|
|!endswith|RHS isn't a closing subsequence of LHS|`'abc' !endswith 'a'`|
|and|True if and only if RHS and LHS are true|`(1 == 1) and (2 == 2)`|
|or|True if and only if RHS or LHS is true|`(1 == 1) or (1 == 2)`|

## Aggregation functions

Aggregation functions can be used with the summarize table operator to calculated summarized values. Currently the following aggregation functions are supported:

|Function|Description|
|---|---|
|avg()|Returns the average of the values across the group|
|count()|Returns a count of the records per summarization group|
|countif()|Returns a count of rows for which Predicate evaluates to true|
|dcount()|Returns the number of distinct values in the group|
|max()|Returns the maximum value across the group|
|maxif()|Starting in version 2107, you can use [maxif](/azure/data-explorer/kusto/query/maxif-aggfunction) with the summarize table operator. <!--9966861--> </br></br>Returns the maximum value across the group for which *Predicate* evaluates to `true`. |
|min()|Returns the minimum value across the group|
|minif()|Starting in version 2107, you can use [minif](/azure/data-explorer/kusto/query/minif-aggfunction) with the summarize table operator. <!--9966861--> </br></br>Returns the minimum value across the group for which *Predicate* evaluates to `true`. |
|percentile()|Returns an estimate for the specified nearest-rank percentile of the population defined by Expr|
|sum()|Returns the sum of the values across the group|
|sumif()|Returns a sum of Expr for which Predicate evaluates to true|

## Scalar functions

Scalar functions can be used in expressions. Currently the following scalar functions are supported:

|Function|Description|
|---|---|
|ago()|Subtracts the given timespan from the current UTC clock time|
|bin()|Rounds values down to a number of datetime multiple of a given bin size|
|case()|Evaluates a list of predicates and returns the first result expression whose predicate is satisfied|
|datetime_add()|Calculates a new datetime from a specified datepart multiplied by a specified amount, added to a specified datetime|
|datetime_diff()|Calculates the difference between two date time values|
|iif()|Evaluates the first argument and returns the value of either the second or third arguments depending on whether the predicate evaluated to true (second) or false (third)|
|indexof()|Function reports the zero-based index of the first occurrence of a specified string within input string|
|isnotnull()|Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a non-null value|
|isnull()|Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a null value|
|now()|Returns the current UTC clock time|
|strcat()|Concatenates between 1 and 64 arguments|
|strlen()|Returns the length, in characters, of the input string|
|substring()|Extracts a substring from a source string starting from some index to the end of the string|
|tostring()|Converts input to a string representation|

## <a name="bkmk_onprem_only"></a> Additional entities, operators, and functions for CMPivot from Configuration Manager

> [!Important]
> These items aren't supported when you run CMPivot from Microsoft Intune admin center.

|Type|Item|Description|
|--|--|---|
|Entity|AccountSID|Account SID|
|Entity|FileContent()|Content of a specific file|
|Entity|NAPClient|NAP Client|
|Entity|NAPSystemHealthAgent|NAP System Health Agent|
|Entity|RegistryKey()| Returns all registry keys matching the given expression (starting in version 2107)<!--9966861-->|
|Table operator|render|Renders results as graphical output|
