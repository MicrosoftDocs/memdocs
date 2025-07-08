---
# required metadata

title: Intune data platform schema
description: Overview of Intune data platform schema.
keywords: 
ms.author: smbhardwaj
author: smritib17 
manager: dougeby
ms.date: 06/23/2025
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Abby Starr 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
---

# Intune data platform

*Applies to: Microsoft Intune*

This article goes over the properties supported in the Intune Data Platform. The Intune Data Platform can be accessed via Device query for single devices, Inventory, and Device query for Multiple Devices.

Each table (entity) in this page lists the types of queries that are supported.

For entities that include Android data, the following platforms are supported:

- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned work profile (COPE)

## AppleAutoSetupAdminAccounts

**Description**: Provides basic account information on Apple devices

**Supported platforms**: iOS, iPadOS, macOS

**Supported for**: Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| AccountGUID | String | The generated GUID of the administrator account |macOS|
| AccountShortName | String | The short name of the administrator account |macOS|

## AppleDeviceStates

**Description**: Apple device state information

**Supported platforms**: iOS, iPadOS, macOS

**Supported for**: Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- | --- |
|  ActivationLockSupported  |  bool  |  Specifies if activation lock is available  |iOS, iPadOS, macOS|
|  AwaitingConfiguration  |  bool  |  If true on the device channel, the device is still waiting for a DeviceConfiguredCommand to continue through Setup Assistant. |iOS, iPadOS, macOS|
|  EraseAllContentAndSettingsPreFlight  |  string  |  Specifies if a device can perform Erase Device Command using Erase All Content and Settings (EACS)  |macOS|
|  MdmLostModeEnabled  |  bool  |  Specifies if Managed Lost Mode has been enabled  |iOS, iPadOS|
|  PinRequiredForDeviceLock  |  bool  |  Is a PIN required for device lock scenarios  |macOS|
|  PinRequiredForEraseDevice  |  bool  |  Is a PIN required before erasing the device  |macOS|
|  Supervised  |  bool  |  If true, it’s a supervised device. |iOS, iPadOS, macOS|
|  SupportsiOSAppInstalls  |  bool  |  Are iOS app installs supported on this device  |macOS|
|  SystemIntegrityProtectionEnabled  |  bool  |  System Integrity Protection (SIP) is a security technology on Mac that prevents malicious software from modifying protected resources  |macOS|

## AppleUpdateSettings

**Description**: Determines update settings for Apple devices

**Supported platforms**: iOS, iPadOS, macOS

**Supported for**: Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- | --- |
| AutoCheckEnabled | bool | The preference to automatically check for app updates. |macOS|
| AutomaticAppInstallationEnabled | bool | The preference to automatically install app updates. |macOS|
| AutomaticOSInstallationEnabled | bool | The preference to automatically install operating system updates. |macOS|
| AutomaticSecurityUpdatesEnabled | bool | The preference to automatically install system data files and security updates. |macOS|
| BackgroundDownloadEnabled | bool | The preference to download app updates in the background. |
| CatalogUrl | string | The URL to the software update catalog the client is using. |macOS|
| IsDefaultCatalog | bool | If true, CatalogURL is the default catalog. |macOS|
| PerformPeriodicCheck | bool | If true, start a new scan. |macOS|
| PreviousScanDateTime | DateTime | The date of the last software update scan. |macOS|
| PreviousScanResult | string | The result code of last software update scan; ”0” = success. |macOS|

## Battery

**Description**: Provides details about battery and battery health.

**Supported Platforms**: Android, iOS, iPadOS, macOS, Windows.

**Supported for**: Device query for multiple devices, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| CycleCount | Long | The number of times a battery has gone through a full charge and discharge. Can be used to assess the battery state|Android, Windows|
| DesignCapacity | Long (milliwatt hours) | The theoretical capacity of the battery when new.|Windows|
| FullChargedCapacity | Long (milliwatt hours) | Full charge capacity of the battery.|Windows|
| Health | string | Assessment of battery health |Android, iOS, iPadOS, macOS, Windows|
| InstanceName| String | Name used to identify the battery instance.|Android, iOS, iPadOS, macOS, Windows|
| Manufacturer| String | Manufacturer of the battery.|Windows|
| Model| String | Display name of the battery.|Windows|
| SerialNumber| String | Battery serial number that is assigned by the manufacturer.|Android|

## BiosInfo 

**Description**: Provides basic BIOS information.

**Supported platforms**: Windows

**Supported for**:  Device query for multiple devices, single device query on-demand, inventory. 

| **Property** | **Type** | **Description** | **Platform** |
|----|----|----|----|
| BiosName | String | Name used to identify the BIOS instance. | Windows multi-device query |
| Manufacturer | String | Manufacturer of this BIOS/software element. | Windows single device query, Windows multi-device query |
| ReleaseDateTime | DateTime (UTC) | BIOS release date. | Windows single device query, Windows multi-device query |
| SerialNumber | String | The assigned serial number of this BIOS element. | Windows single device query, Windows multi-device query |
| SmBiosVersion | String | BIOS version as reported by SMBIOS. | Windows single device query, Windows multi-device query |
| SoftwareElementId | String | Identifier for the BIOS instance | Android, iOS, iPadOS, macOS, Windows multi-device query |
| SoftwareElementState | String | State of the BIOS instance. | Android, iOS, iPadOS, macOS, Windows multi-device query |
| TargetOperatingSystem | String | Target operating system of the owning software element. | Android, iOS, iPadOS, macOS, Windows multi-device query |



## Bluetooth

**Description**: Provides Bluetooth device information.

**Supported platforms**: iOS, iPadOS, macOS

**Supported for**: Device Query for Multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| MacAddress | string | Bluetooth media access control (MAC) address. |iOS, iPadOS, macOS|

## Celluar

**Description**: Provides celluar information about mobile devices

**Supported platforms**: Androd, iOS, iPadOS, macOS

**Supported for**: Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- | --- |
| CellularTechnology | string | The cellular technology type |Android, iOS, iPadOS|
| DataRoamingEnabled | bool | If true, the device has enabled data roaming |iOS, iPadOS|
| HotspotEnabled | bool | If true, the device has enabled Personal Hotspot, which isn’t available for all carriers. |iOS, iPadOS|
| ModemFirmwareVersion | string | The modem firmware version |iOS, iPadOS|
| NetworkTethered | bool | If true, the device is network-tethered. |iOS, iPadOS|

## Certificate

**Description**: Certificate Authorities installed in Keychains/ca-bundles. Only certificates for computers are returned.

**Supported platforms**: Windows

**Supported for**: Device query for single device (on-demand).  

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |---|
| SubjectName| string | Certificate distinguished name |Windows|
| Issuer | string | Certificate issuer distinguished name |Windows|
| CommonName | string | Certificate CommonName |Windows|
| IsCa | bool | 1 if CA: true (certificate is an authority) else 0 |Windows|
| SelfSigned| bool | 1 if self-signed, else 0 |Windows|
| ValidFromDateTime| datetime (UTC) | Lower bound of valid date |Windows|
| ValidToDateTime| datetime (UTC) | Certificate expiration data |Windows|
| SigningAlgorithm | string (max length 256 characters) | Signing algorithm used |Windows|
| KeyAlgorithm | string (max length 256 characters) | Key algorithm used |Windows|
| KeyStrength | long | Key size used for RSA/DSA, or curve name |Windows|
| KeyUsage | string (max length 256 characters) | Certificate key usage and extended key usage |Windows|
| SerialNumber | string (max length 256 characters) | Certificate serial number |Windows|
| StoreLocation | string (max length 256 characters) | Certificate system store location |Windows|
| StoreName | string (max length 256 characters) | Certificate system store |Windows|

## CPU

**Description**: Retrieves CPU hardware info on the machine.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| ProcessorId | string (max length 256 characters) | The DeviceID of the CPU. |Windows single device query, Windows multi device query  |
| Model | string (max length 256 characters) | The model of the CPU. |Windows single device query, Windows multi device query  |
| Manufacturer | string (max length 256 characters) | The manufacturer of the CPU. | Windows single device query, Windows multi device query |
| ProcessorType | string | The processor type, such as Central, Math, or Video. |Windows single device query, Windows multi device query  |
| Architecture | String (max length 20 characters) | Processor architecture used by the platform. |Windows single device query, Windows multi device query  |
| CpuStatus | string (max 256 length 256 characters) | The current operating status of the CPU. |Windows single device query, Windows multi device query  |
| CoreCount | long | The number of cores of the CPU. |
| LogicalProcessorCount | long | The number of logical processors of the CPU. |Windows single device query, Windows multi device query  |
| AddressWidth | long | The width of the CPU address bus. |Windows single device query, Windows multi device query |
| CurrentClockSpeed | long | The current frequency of the CPU. | Windows single device query|
| MaxClockSpeed | long | The maximum possible frequency of the CPU. |Windows single device query, Windows multi device query |
| SocketDesignation | string (max length 256 characters) | The assigned socket on the board for the given CPU. | Windows single device query, Windows multi device query |
| Availability | string(max length 256 characters) | The availability and status of the CPU. |Windows single device query |

## DeviceStorage

**Description**: Provides basic information about device storage.

**Supported platforms**: Android, iOS, iPadOS, macOS

**Supported for**: Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| DeviceCapacityBytes | long | Total device storage capacity ||
| Encrypted | bool | Details whether encryption is on or off ||


## DiskDrive

**Description**: Retrieves basic information about the physical disks of a system.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| DriveId | string (max length 256 characters) | The unique identifier of the drive on the system. ||
| PartitionCount | long | Number of detected partitions on disk. ||
| DriveIndex | long | Physical drive number of the disk. |
| InterfaceType | string (max length 256 characters) | The interface type of the disk. ||
| PnpDeviceId | string (max 256 length 256 characters) | The unique identifier of the drive on the system. ||
| SizeBytes | long | Size of the disk. ||
| Manufacturer | string (max length 256 characters) | The manufacturer of the disk. ||
| Model | string (max length 256 characters) | Hard drive model. ||
| DiskName | string (max length 256 characters) | The label of the disk object. ||
| SerialNumber | string (max length 256 characters) | The serial number of the disk. ||
| Description | string (max length 256 characters) | The OS's description of the disk. ||

## EncryptableVolume

**Description**: Retrieves encryptable volume status of the machine.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| VolumeId | string(Max length 256 characters) | ID of the encrypted volume. ||
| WindowsDriveLetter | string(Max length 5 characters) | Drive letter of the encrypted drive. ||
| PersistentVolumeId | string(Max length 38 characters) This is a Guid | Persistent ID of the drive. ||
| ProtectionStatus | string (max length 256 characters) | The BitLocker protection status of the drive. ||
| EncryptionMethod | string(256) | The encryption type of the device. ||
| EncryptionPercentage | long (An integer from 0 to 100 inclusive) | The percentage of the drive that is encrypted. ||
| Locked | bool | The accessibility status of the drive from Windows. ||

## FileInfo

**Description**: Lists all file info of the passed file or files under the passed directory.

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

> [!NOTE]
> This is a parameterized entity where you must pass in the path of the File you want to query. For example, pass in `FileInfo('c:\windows\system32\drivers\etc\hosts') | take 10`. If a directory is passed, it will return info on the files in the directory and sub-directories.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| Path | string(Max Length 260 characters) | Absolute file path ||
| Directory | string (Max Length 4096 characters) | Directory of file(s) ||
| FileName | string(Max Length 260 characters) | Namxxe portion of file path ||
| SizeBytes | long | Size of file in bytes ||
| LastAccessDateTime | datetime(UTC) | Last access time ||
| LastModifiedDateTime | datetime(UTC) | Last modification time ||
| LastStatusChangeDateTime | datetime(UTC) | Last status change time ||
| CreatedDateTime | datetime(UTC) | (B)irth or (cr)eate time ||
| Attributes | string | File attribute string. See: [https://ss64.com/nt/attrib.html](https://ss64.com/nt/attrib.html) ||
| FileVersion | string(Max length 256 characters) | File version ||
| ProductVersion | string(Max length 256 characters) | File product version ||
| ProductName | string(Max length 256 characters) | File Product Name ||
| OriginalName | string(Max length 256 characters) | (Executable files only) Original filename ||

## LocalGroup

**Description**: Lists local user groups.  

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| GroupId | long, Result should be (\>=0) | Group ID ||
| GroupName | String(Max length 256 characters) | Group Name ||
| WindowsSid | String(Max length 256 characters) | sid of group on windows ||

## LocalUserAccount

**Description**: Lists local user accounts.

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| UserId | long, Result should be (\>=0) | User ID ||
| Username | string(max length 256 characters) | Username ||
| UserDescription | string(max length 256 characters) | Optional user description ||
| HomeDirectory | string(max length 4096 characters) | User's home directory ||
| WindowsSid | string(max length 256 characters) | Windows Sid ||

## LogicalDrive

**Description**: Details for logical drives on the system. A logical drive generally represents a single partition.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| DriveIdentifier | string (Max length 5 characters) | The drive ID, usually the drive name. For example, 'C:'. ||
| DriveType | string(Max length 100 character) | Drive type such as local disk or removal disk ||
| DiskDescription | string (Max length 256 characters) | The canonical description of the drive. For example, 'Logical Fixed Disk', 'CD-ROM Disk'. ||
| FreeSpaceBytes | long, Result should be (\>=0) | The amount of free space, in bytes, of the drive (-1 on failure). ||
| DiskSizeBytes | long, Result should be (\>=0) | The total amount of space, in bytes, of the drive (-1 on failure). ||
| FileSystem | string(Max length 256 characters) | The file system of the drive. ||

## MemoryInfo

**Description**: Memory Information.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.
Note that PhysicalMemoryFreeBytes and VirtualMemoryFreeBytes properties are only supported for single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| PhysicalMemoryTotalBytes | Long, Result should be (\>=0) | Total amount of physical memory available to the operating system. This value doesn't necessarily indicate the true amount of physical memory, but what is reported to the operating system as available to it. ||
| PhysicalMemoryFreeBytes | LongResult should be (\>=0) |Number of bytes of physical memory currently unused and available. ||
| VirtualMemoryTotalBytes | Long, Result should be (\>=0) | Number of bytes of virtual memory. ||
| VirtualMemoryFreeBytes | Long, Result should be (\>=0) | Number of bytes of virtual memory currently unused and available. ||  

## NetworkAdapter

**Description**: Provides basic network adapter information.

**Supported Features**: Inventory, Device query for multiple devices.

**Supported Platforms**: Windows

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| Identifier | String | Unique identifier of the adapter from other devices on the system. ||
| Manufacturer | String | Name of the network adapter's manufacturer. ||
| Type | String | Network medium in use. ||

> [!NOTE]
> Inventory will only report up to 20 network adapters per device.

## OsVersion

**Description**: A single row containing the operating system name and version.

**Supported platforms**: Android, iOS, iPadOS, Windows

**Supported for**: Device query for multiple devices, Single device query on-demand (Windows only), Inventory .

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| OsName | string (max length 256 characters) | Distribution or product name ||
| OsVersion | string (max length 40characters) | Pretty, suitable for presentation, OS version ||
| MajorVersion | Long | Major release version ||
| MinorVersion | Long | Minor release version ||
| PatchVersion | long | Optional patch release ||
| BuildVersion | string | Optional build-specific or variant string ||
| Architecture | string(max length 256 characters) | OS Architecture ||
| InstallDateTime | datetime (UTC) | The install date time of the OS. ||

## Process

**Description**: All running processes on the host system.  

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| ProcessId | long | Process ID ||
| ProcessName | string (max 260 characters) | The name of process ||
| Path | string (max 4096 characters) | Path to executed binary ||
| CommandLine | string (max 4096 characters) | Complete argv ||
| CurrentWorkingDirectory | string (max 256 characters) | Process current working directory ||
| WorkingSetSizeBytes | long | Bytes of private memory used by process ||
| TotalSizeBytes | long | Total virtual memory size ||
| DiskBytesRead | long | Bytes read from disk ||
| DiskBytesWritten | long | Bytes written to disk ||
| ParentProcessId | long | Process parent's PID ||
| Priority | long | Process nice level (-20 to 20, default 0) ||
| UserTimeMilliseconds | long | CPU time in milliseconds spent user space ||
| SystemTimeMilliseconds | long | CPU time in milliseconds spent in kernel space ||
| StartDateTime | Datetime(UTC)Need to convert this value to datetime | Process start datetime in UTC ||
| ElapsedTimeMilliseconds | long | Elapsed time in seconds this process has been running. ||
| ProcessorTimePercent | long | Returns elapsed time that all of the threads of this process used the processor to execute instructions in 100-nanoseconds ticks. ||
| ThreadCount | long | Number of threads used by process ||
| HandleCount | long | Total number of handles that the process has open. This number is the sum of the handles currently opened by each thread in the process. ||
| WindowsUserAccount | string | The owner of the process ||
| OnDisk | boolNullable\<System.Boolean\>  | The process path exists yes=1, no=0, unknown=-1 ||

## SharediPad

**Description**: Details for Shared iPad devices.

**Supported platforms**: iPadOS

**Supported for**: Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| EstimatedResidentUsersCount | long | Estimated number of users that can share the device based on space. ||
| IsMultiUser | bool | iPad set up as multi user ||
| IsTemporarySessionOnly | bool | The device only allows temporary sessions. ||
| ManagedAppleIdDefaultDomains | string | The list of domains that the device suggests on the Shared iPad login screen. ||
| OnlineAuthenticationGracePeriodDays | long | The grace period for Shared iPad online authentication (in days). A value of 0 indicates that the device requires online authentication for every login ||
| QuotaSizeBytes | long | The quota size in bytes for each user on this shared iPad device ||
| ResidentUsersCount | long | The number of users currently on this shared iPad device. ||
| SkipLanguageAndLocaleSetupForNewUsers | bool | If true, skip the language and country/region panes for new users on Shared iPad. ||
| TemporarySessionTimeoutSeconds | long | The timeout interval for the temporary session. A value of 0 indicates that there’s no timeout. ||
| UserSessionTimeoutSeconds | long | The timeout interval for the user session. A value of 0 indicates that there’s no timeout. ||



## SystemEnclosure

**Description**: Displays information pertaining to the chassis and its security status.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

> [!NOTE]
> Chassis Types property is currently not supported for Inventory or Device query for multiple devices.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| SerialNumber | string (max 64 characters) | The serial number of the chassis. ||
| AudibleAlarmEquipped | bool | If TRUE, the frame is equipped with an audible alarm. ||
| BreachDescription | string(max 256 characters) | If provided, gives a more detailed description of a detected security breach. ||
| ChassisTypes | Array[string] | A comma-separated list of chassis types, such as Desktop or Laptop. ||
| ExtendedDescription | string(max 256 characters) | An extended description of the chassis if available. ||
| LockEquipped | bool | If TRUE, the frame is equipped with a lock. ||
| Manufacturer | string (max 256 characters) | The manufacturer of the chassis. ||
| Model | string (max 256 characters) | The model of the chassis. ||
| SecurityBreach | string(max 256 characters) | The physical status of the chassis such as Breach Successful, Breach Attempted, etc. ||
| SmBiosAssetTag | string (max 120 characters) | The assigned asset tag number of the chassis. ||
| Sku | string (max 64 characters) | The Stock Keeping Unit number if available. ||
| Status | string(256 characters) | If available, gives various operational or nonoperational statuses such as OK, Degraded, and Pred Fail. ||
| VisibleAlarmEquipped | bool | If TRUE, the frame is equipped with a visual alarm. ||

## SystemInfo

**Description**: System information of the device.  

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| FqdnHostname | string (max 256) | Network hostname including domain ||
| Uuid | string (max 36 characters) | Unique ID provided by the system ||
| ComputerName | string (max 256 characters) | Friendly computer name (optional) ||
| PhysicalProcessorCount | Long | Number of physical processors ||
| ProcessorArchitecture | string(40 characters) | CPU type ||
| HardwareManufacturer | string (max 256 characters) | Hardware vendor ||
| HardwareModel | string (max 256 characters) | Hardware model ||

## SimInfo

**Description**: Information on the Sim cards found on the device

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| WindowsESimId | String | The ID of an eSIM found on the device ||
| Eid | String | The electronic identification number of the device ||
| isActive | Boolean | Whether the eSIM is active or not ||

## Tpm

**Description**: Provides TPM related information of the device.  

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| Activated | bool | TPM is activated ||
| Enabled | bool | TPM is enabled ||
| Owned | bool | TPM is owned ||
| Manufacturer | string (max 256 characters) | TPM manufacturers name ||
| ManufacturerVersion | string (max 256 characters) | TPM version ||
| ManufacturerId | long | TPM manufacturers ID ||
| ProductName | string (max 256 characters) | Product name of the TPM ||
| PhysicalPresenceVersion | string (max 256 characters) | Version of the Physical Presence Interface ||
| SpecVersion | string (max 256 characters) | Trusted Computing Group specification that the TPM supports ||  

## Time

**Description**: Provides basic time information.

**Supported Features**: Inventory, device query for multiple devices.

**Supported Platforms**: Windows

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| TimeZone | String | Describes the device's time zone. |Windows|

## VideoController

**Description**: Provides video controller and graphics information.

**Supported Features**: Inventory, Device query for multiple devices.

**Supported Platforms**: Windows

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| AdapterDacType | String | Name or identifier of the digital-to-analog converter (DAC) chip. The character set of this property is alphanumeric. |Windows|
| AdapterRam | Long | Memory size of the video adapter. |Windows|
| CurrentScanMode | String | Current scan mode. |Windows|
| GraphicsModel | String | Provides manufacturer and model information of graphics card. |Windows|
| Identifier | String | Identifier (unique to the computer system) for this video controller. |Windows|
| VideoModeDescription | String | Current resolution, color, and scan mode settings of the video controller. |Windows|

## WindowsAppCrashEvent

**Description**: Provides App Crash info in Windows event log file Application in look back time.

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| ReportId(Key) | string (max 256 characters) | Report ID of the App crash |
| --- | --- | --- |
| AppPath | string (max 256 characters) | Application path ||
| AppName | string (max 256 characters) | Application file name ||
| AppVersion | string (max 40 characters) | Application version ||
| LoggedDateTime | datetime (UTC) | System UTC time at which the event occurred ||
| WindowsUserAccount | string (max 256 characters) | User account associated with this app crash ||

## WindowsDriver

**Description**: Details for in-use Windows device drivers. This doesn't display installed but unused drivers.

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| DriverDeviceId(Key) | string (Max 256 characters) | Device ID ||
| FriendlyName | string(Max 256 characters) | Such as "Microsoft Device Association Root Enumerator" ||
| DriverDescription | string (Max 256 characters) | Driver description ||
| DriverVersion | string (Max 20 characters) | Driver version ||
| InfName | string (Max 260 characters) | Associated inf file ||
| Class | string (Max 256 characters) | Device/driver class name ||
| ProviderName | string (Max 256 characters) | Driver provider ||
| Manufacturer | string (Max 256 characters) | Device manufacturer ||
| BuildDate[Win32\_PnPSignedDriver class (Windows) | Microsoft Learn](/previous-versions/windows/desktop/legacy/aa394354(v=vs.85)) | datetime(UTC) | Driver date ||
| Signed | bool | Whether the driver is signed or not ||

## WindowsEvent

**Description**: Get Windows Event logs in the specified log name and look back in time.  

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

> [!NOTE]
> When constructing the query, you must specify the log name and look back time, for example: `WindowsEvent(Application, 1d) | take 1`.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| LogName | string (max 256 characters) | the name of log ||
| EventId | long | event ID |Windows|
| Level | string string (max 30 characters) | Level display name
possible value:CRITICAL\_ERROR,ERROR,WARNING,INFORMATION,VERBOSE |Windows|
| LoggedDateTime | datetime (UTC) | System UTC time at which the event occurred |Windows|
| Message | string (max 32766 characters) | The event messages |Windows|
| ProviderName | string (max 256 characters) | Provider name of event |Windows|
| WindowsUserAccount | string (max 256) | User account associated with this event |Windows|

## WindowsQfe

**Description**: Information about security patches on the device.

**Supported platforms**: Windows

**Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description |**Platform**|
| --- | --- | --- |--- |
| HotFixId (key) | string (max 256 characters) | Unique identifier associated with a particular update. |Windows|
| ComputerName                   | string (max 256 characters) | The name of the computer the patch is installed on. |Windows|
| Caption | string (max 256 characters) | A short textual description of the object. |Windows|
| QfeDescription | string (max 256 characters) | A textual description of the object. |Windows|
| FixComments | string (max 256 characters) | More comments about the Qfe. |Windows|
| InstalledByUserAccount | string (max 256 characters) | User account who installed the update. If this value is unknown, the property is empty. |Windows|
| InstalledDate | datetime (UTC) | Date that the update was installed. If this value is unknown, the property is empty. |Windows|

## WindowsRegistry

**Description**: Lists registry under the passed registry key.  

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

> [!NOTE]
> You must pass in the registry key you are trying to query. For example, `WindowsRegistry('HKEY_LOCAL_MACHINE\\ServiceLastKnownStatus')`.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| RegistryKey | string (max 16638 characters) | Full path to the value |Windows|
| ValueName | string (max 16383 characters) | Name of the registry value entry |Windows|
| ValueType | string (max 255) | Type of the registry value, or 'subkey' if item is a subkey |Windows|
| ValueData | string (max size 1 MB) | Data content of registry value |Windows|

## WindowsService

**Description**: Lists all installed Windows services and their relevant data.

**Supported platforms**: Windows

**Supported for**: single device query on-demand.

| **Property** | **Type** | **Description** |**Platform**|
| --- | --- | --- |--- |
| ServiceName | string (max 256 characters) | Service name |Windows|
| ServiceType | string (max 40)[Win32\_Service class - Win32 apps | Microsoft Learn](/windows/win32/cimwin32prov/win32-service) | Service Type such as: OWN\_PROCESS, SHARE\_PROCESS, or Interactive |Windows|
| DisplayName | string (max 256 characters) | Service Display name |Windows|
| State | string (max 40 characters) | Service Current status such as STOPPED, START\_PENDING, STOP\_PENDING, RUNNING, CONTINUE\_PENDING, PAUSE\_PENDING, PAUSED |Windows|
| ProcessId | long | the Process ID of the service |Windows|
| StartMode | string (Max 40 characters) | Service start type: BOOT\_START, SYSTEM\_START, AUTO\_START, DEMAND\_START, DISABLED |Windows|
| ExitCode | long | The error code that the service uses to report an error that occurs when it is starting or stopping |Windows|
| ServiceSpecific ExitCode | long | The service-specific error code that the service returns when an error occurs while the service is starting or stopping|Windows|
| Path | string (max 4096 characters) | Path to Service Executable |Windows|
| ModulePath | string (max 4096 characters) | Path to ServiceDll |Windows|
| ServiceDescription | string (max 256 characters) | Service Description |Windows|
| WindowsUserAccount | string (max 256 characters) | The name of the account that the service process is logged on as when it runs. This name can be of the form Domain\UserName |Windows|




