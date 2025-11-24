---
title: Intune Data Platform Schema
description: Review the Intune data platform schema for device query and inventory, including supported properties and data types in Microsoft Intune.
ms.date: 10/09/2025
ms.topic: reference
---

# Intune data platform schema

This article goes over the properties supported in the Intune Data Platform. The Intune Data Platform can be accessed via Device query for single devices, Inventory, and Device query for Multiple Devices.

Each table (entity) in this page lists the types of queries that are supported with the following information:

- Property: The name of the variable we collect and store.
- Type: The data type you can expect to see, such as *string* or *boolean*.
- Description: The purpose of the property.
- Platform:  The operating systems that support the property.

For entities that include Android data, the following platforms are supported:

- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned work profile (COPE)

## `AppleAutoSetupAdminAccounts`

> **Description**: Provides basic account information on Apple devices\
> **Supported platforms**: iOS, iPadOS, macOS\
> **Supported for**: Device query for multiple devices.

| Property | Type | Description | Platform |
| --- | --- | --- |--- |
| `AccountGUID` | String | The generated GUID of the administrator account |macOS|
| `AccountShortName` | String | The short name of the administrator account |macOS|

## `AppleDeviceStates`

> **Description**: Apple device state information\
> **Supported platforms**: iOS, iPadOS, macOS\
> **Supported for**: Device query for multiple devices.

| Property | Type | Description | Platform |
| --- | --- | --- | --- |
|  `ActivationLockSupported`  |  bool  |  Specifies if activation lock is available  |iOS, iPadOS, macOS|
|  `AwaitingConfiguration`  |  bool  |  If true on the device channel, the device is still waiting for a DeviceConfiguredCommand to continue through Setup Assistant. |iOS, iPadOS, macOS|
|  `EraseAllContentAndSettingsPreFlight`  |  string  |  Specifies if a device can perform Erase Device Command using Erase All Content and Settings (EACS)  |macOS|
|  `MdmLostModeEnabled`  |  bool  |  Specifies if Managed Lost Mode is enabled  |iOS, iPadOS|
|  `PinRequiredForDeviceLock`  |  bool  |  Is a PIN required for device lock scenarios  |macOS|
|  `PinRequiredForEraseDevice`  |  bool  |  Is a PIN required before erasing the device  |macOS|
|  `Supervised`  |  bool  |  If true, it's a supervised device. |iOS, iPadOS, macOS|
|  `SupportsiOSAppInstalls`  |  bool  |  Are iOS app installs supported on this device  |macOS|
|  `SystemIntegrityProtectionEnabled`  |  bool  |  System Integrity Protection (SIP) is a security technology on Mac that prevents malicious software from modifying protected resources  |macOS|

## `AppleUpdateSettings`

> **Description**: Determines update settings for Apple devices\
> **Supported platforms**: iOS, iPadOS, macOS\
> **Supported for**: Device query for multiple devices.

| Property | Type | Description | Platform |
| --- | --- | --- | --- |
| `AutoCheckEnabled` | bool | The preference to automatically check for app updates. |macOS|
| `AutomaticAppInstallationEnabled` | bool | The preference to automatically install app updates. |macOS|
| `AutomaticOSInstallationEnabled` | bool | The preference to automatically install operating system updates. |macOS|
| `AutomaticSecurityUpdatesEnabled` | bool | The preference to automatically install system data files and security updates. |macOS|
| `BackgroundDownloadEnabled` | bool | The preference to download app updates in the background. |macOS|
| `CatalogUrl` | string | The URL to the software update catalog the client is using. |macOS|
| `IsDefaultCatalog` | bool | If true, CatalogURL is the default catalog. |macOS|
| `PerformPeriodicCheck` | bool | If true, start a new scan. |macOS|
| `PreviousScanDateTime` | DateTime | The date of the last software update scan. |macOS|
| `PreviousScanResult` | string | The result code of last software update scan; "0" = success. |macOS|

## `Battery`

> **Description**: Provides details about battery and battery health.\
> **Supported platforms**: Android, iOS, iPadOS, macOS, Windows.\
> **Supported for**: Device query for multiple devices, Inventory.

| Property | Type | Description | Platform |
| --- | --- | --- |--- |
| `CycleCount` | Long | The number of times a battery completed a full charge and discharge. Can be used to assess the battery state.|Android, Windows|
| `DesignCapacity` | Long (milliwatt hours) | The theoretical capacity of the battery when new.|Windows|
| `FullChargedCapacity` | Long (milliwatt hours) | Full charge capacity of the battery.|Windows|
| `Health` | string | Assessment of battery health |Android, iOS, iPadOS, macOS, Windows|
| `InstanceName`| String | Name used to identify the battery instance.|Android, iOS, iPadOS, macOS, Windows|
| `Manufacturer`| String | Manufacturer of the battery.|Windows|
| `Model`| String | Display name of the battery.|Windows|
| `SerialNumber`| String | The battery serial number that the manufacturer assigned.|Android|

## `BiosInfo`

> **Description**: Provides basic BIOS information.\
> **Supported platforms**: Windows\
> **Supported for**:  Device query for multiple devices, single device query on-demand, inventory.

| Property | Type | Description | Platform |
|----|----|----|----|
| `BiosName` | String | Name used to identify the BIOS instance. | Windows multi-device query |
| `Manufacturer` | String | Manufacturer of this BIOS/software element. | Windows single device query, Windows multi-device query |
| `ReleaseDateTime` | DateTime (UTC) | BIOS release date. | Windows single device query, Windows multi-device query |
| `SerialNumber` | String | The assigned serial number of this BIOS element. | Windows single device query, Windows multi-device query |
| `SmBiosVersion` | String | BIOS version as reported by SMBIOS. | Windows single device query, Windows multi-device query |
| `SoftwareElementId` | String | Identifier for the BIOS instance | Android, iOS, iPadOS, macOS, Windows multi-device query |
| `SoftwareElementState` | String | State of the BIOS instance. | Android, iOS, iPadOS, macOS, Windows multi-device query |
| `TargetOperatingSystem` | String | Target operating system of the owning software element. | Android, iOS, iPadOS, macOS, Windows multi-device query |



## `Bluetooth`

> **Description**: Provides Bluetooth device information.\
> **Supported platforms**: iOS, iPadOS, macOS\
> **Supported for**: Device Query for Multiple devices.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `MacAddress` | string | Bluetooth media access control (MAC) address. |iOS, iPadOS, macOS|

## `Cellular`

> **Description**: Provides cellular information about mobile devices.\
> **Supported platforms**: Android, iOS, iPadOS, macOS\
> **Supported for**: Device query for multiple devices.

| Property | Type | Description | Supported platforms |
| --- | --- | --- | --- |
| `CellularTechnology` | string | The cellular technology type. |Android, iOS, iPadOS|
| `DataRoamingEnabled` | bool | If true, the device enables data roaming. |iOS, iPadOS|
| `HotspotEnabled` | bool | If true, the device enables Personal Hotspot, which isn't available for all carriers. |iOS, iPadOS|
| `ModemFirmwareVersion` | string | The modem firmware version. |iOS, iPadOS|
| `NetworkTethered` | bool | If true, the device is network-tethered. |iOS, iPadOS|

## `Certificate`

> **Description**: Certificate Authorities installed in Keychains/ca-bundles. Only certificates for computers are returned.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for single device (on-demand).

| Property | Type | Description | Supported platforms |
| --- | --- | --- |---|
| `SubjectName`| string | Certificate distinguished name |Windows|
| `Issuer` | string | Certificate issuer distinguished name |Windows|
| `CommonName` | string | Certificate CommonName |Windows|
| `IsCa` | bool | 1 if CA: true (certificate is an authority) else 0 |Windows|
| `SelfSigned`| bool | 1 if self-signed, else 0 |Windows|
| `ValidFromDateTime`| datetime (UTC) | Lower bound of valid date |Windows|
| `ValidToDateTime`| datetime (UTC) | Certificate expiration data |Windows|
| `SigningAlgorithm` | string (max length 256 characters) | Signing algorithm used |Windows|
| `KeyAlgorithm` | string (max length 256 characters) | Key algorithm used |Windows|
| `KeyStrength` | long | Key size used for RSA/DSA, or curve name |Windows|
| `KeyUsage` | string (max length 256 characters) | Certificate key usage and extended key usage |Windows|
| `SerialNumber` | string (max length 256 characters) | Certificate serial number |Windows|
| `StoreLocation` | string (max length 256 characters) | Certificate system store location |Windows|
| `StoreName` | string (max length 256 characters) | Certificate system store |Windows|

## `CPU`

> **Description**: Retrieves CPU hardware info on the machine.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `ProcessorId` | string (max length 256 characters) | The DeviceID of the CPU. |Windows single device query, Windows multi device query  |
| `Model` | string (max length 256 characters) | The model of the CPU. |Windows single device query, Windows multi device query  |
| `Manufacturer` | string (max length 256 characters) | The manufacturer of the CPU. | Windows single device query, Windows multi device query |
| `ProcessorType` | string | The processor type, such as Central, Math, or Video. |Windows single device query, Windows multi device query  |
| `Architecture` | String (max length 20 characters) | Processor architecture used by the platform. |Windows single device query, Windows multi device query  |
| `CpuStatus` | string (max length 256 characters) | The current operating status of the CPU. |Windows single device query, Windows multi device query  |
| `CoreCount` | long | The number of cores of the CPU. |Windows single device query, Windows multi device query |
| `LogicalProcessorCount` | long | The number of logical processors of the CPU. |Windows single device query, Windows multi device query  |
| `AddressWidth` | long | The width of the CPU address bus. |Windows single device query, Windows multi device query |
| `CurrentClockSpeed` | long | The current frequency of the CPU. | Windows single device query|
| `MaxClockSpeed` | long | The maximum possible frequency of the CPU. |Windows single device query, Windows multi device query |
| `SocketDesignation` | string (max length 256 characters) | The assigned socket on the board for the given CPU. | Windows single device query, Windows multi device query |
| `Availability` | string (max length 256 characters) | The availability and status of the CPU. |Windows single device query |

## `DeviceStorage`

> **Description**: Provides basic information about device storage.\
> **Supported platforms**: Android, iOS, iPadOS, macOS\
> **Supported for**: Device query for multiple devices.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `DeviceCapacityBytes` | long | Total device storage capacity |Android, iOS, iPadOS, macOS|
| `Encrypted` | bool | Details whether encryption is on or off |Android|


## `DiskDrive`

> **Description**: Retrieves basic information about the physical disks of a system.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `DriveId` | string (max length 256 characters) | The unique identifier of the drive on the system. |Windows|
| `PartitionCount` | long | Number of detected partitions on disk. |Windows|
| `DriveIndex` | long | Physical drive number of the disk. |Windows|
| `InterfaceType` | string (max length 256 characters) | The interface type of the disk. |Windows|
| `PnpDeviceId` | string (max length 256 characters) | The unique identifier of the drive on the system. |Windows|
| `SizeBytes` | long | Size of the disk. |Windows|
| `Manufacturer` | string (max length 256 characters) | The manufacturer of the disk. |Windows|
| `Model` | string (max length 256 characters) | Hard drive model. |Windows|
| `DiskName` | string (max length 256 characters) | The label of the disk object. |Windows|
| `SerialNumber` | string (max length 256 characters) | The serial number of the disk. |Windows|
| `Description` | string (max length 256 characters) | The OS's description of the disk. |Windows|

## `EncryptableVolume`

> **Description**: Retrieves encryptable volume status of the machine.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `VolumeId` | string (max length 256 characters) | ID of the encrypted volume. |Windows|
| `WindowsDriveLetter` | string (max length 5 characters) | Drive letter of the encrypted drive. |Windows|
| `PersistentVolumeId` | string (max length 38 characters) This is a Guid | Persistent ID of the drive. |Windows|
| `ProtectionStatus` | string (max length 256 characters) | The BitLocker protection status of the drive. |Windows|
| `EncryptionMethod` | string (256) | The encryption type of the device. |Windows|
| `EncryptionPercentage` | long (An integer from 0 to 100 inclusive) | The percentage of the drive that is encrypted. |Windows|
| `Locked` | bool | The accessibility status of the drive from Windows. |Windows|

## `FileInfo`

> **Description**: Lists all file info of the passed file or files under the passed directory.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

> [!NOTE]
> This is a parameterized entity where you must pass in the path of the File you want to query. For example, pass in `FileInfo('c:\windows\system32\drivers\etc\hosts') | take 10`. If a directory is passed, it will return information about the files in the directory and subdirectories.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `Path` | string (max length 260 characters) | Absolute file path |Windows|
| `Directory` | string (max length 4,096 characters) | Directory of files |Windows|
| `FileName` | string (max length 260 characters) | Name portion of file path |Windows|
| `SizeBytes` | long | Size of file in bytes |Windows|
| `LastAccessDateTime` | datetime (UTC) | Last access time |Windows|
| `LastModifiedDateTime` | datetime (UTC) | Last modification time |Windows|
| `LastStatusChangeDateTime` | datetime (UTC) | Last status change time |Windows|
| `CreatedDateTime` | datetime (UTC) | (B)irth or (cr)eate time |Windows|
| `Attributes` | string | File attribute string. See: [https://ss64.com/nt/attrib.html](https://ss64.com/nt/attrib.html) |Windows|
| `FileVersion` | string (max length 256 characters) | File version |Windows|
| `ProductVersion` | string (max length 256 characters) | File product version |Windows|
| `ProductName` | string (max length 256 characters) | File Product Name |Windows|
| `OriginalName` | string (max length 256 characters) | (Executable files only) Original filename |Windows|

## `LocalGroup`

> **Description**: Lists local user groups.\
> **Supported platforms**: Windows\
> **Supported for**: Single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `GroupId` | long, Result should be (\>=0) | Group ID |Windows|
| `GroupName` | String (max length 256 characters) | Group Name |Windows|
| `WindowsSid` | String (max length 256 characters) | SID of group on Windows |Windows|

## `LocalUserAccount`

> **Description**: Lists local user accounts.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `UserId` | long, Result should be (\>=0) | User ID |Windows|
| `Username` | string (max length 256 characters) | Username |Windows|
| `UserDescription` | string (max length 256 characters) | Optional user description |Windows|
| `HomeDirectory` | string (max length 4,096 characters) | User's home directory |Windows|
| `WindowsSid` | string (max length 256 characters) | Windows Sid |Windows|

## `LogicalDrive`

> **Description**: Details for logical drives on the system. A logical drive generally represents a single partition.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `DriveIdentifier` | string (max length 5 characters) | The drive ID, usually the drive name. For example, 'C:'. |Windows |
| `DriveType` | string (max length 100 character) | Drive type such as local disk or removal disk |Windows |
| `DiskDescription` | string (max length 256 characters) | The canonical description of the drive. For example, 'Logical Fixed Disk', 'CD-ROM Disk'. |Windows |
| `FreeSpaceBytes` | long, Result should be (\>=0) | The amount of free space, in bytes, of the drive (-1 on failure). |Windows |
| `DiskSizeBytes` | long, Result should be (\>=0) | The total amount of space, in bytes, of the drive (-1 on failure). |Windows |
| `FileSystem` | string (max length 256 characters) | The file system of the drive. |Windows |

## `MemoryInfo`

> **Description**: Memory Information.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.
PhysicalMemoryFreeBytes and VirtualMemoryFreeBytes properties are only supported for single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `PhysicalMemoryTotalBytes` | Long, Result should be (\>=0) | Total amount of physical memory available to the operating system. This value doesn't necessarily indicate the true amount of physical memory, but what is reported to the operating system as available to it. |Windows single device query, Windows multi device query |
| `PhysicalMemoryFreeBytes` | Long, Result should be (\>=0) |Number of bytes of physical memory currently unused and available. |Windows single device query |
| `VirtualMemoryTotalBytes` | Long, Result should be (\>=0) | Number of bytes of virtual memory. |Windows single device query, Windows multi device query |
| `VirtualMemoryFreeBytes` | Long, Result should be (\>=0) | Number of bytes of virtual memory currently unused and available. |Windows single device query |

## `NetworkAdapter`

> **Description**: Provides basic network adapter information.\
> **Supported Features**: Inventory, Device query for multiple devices.\
> **Supported platforms**: Windows

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `Identifier` | String | Unique identifier of the adapter from other devices on the system. |Windows|
| `MacAddress`| String | Hardware identification number that uniquely identifies each device on a network. |Android, iOS, iPadOS, macOS |
| `Manufacturer` | String | Name of the network adapter's manufacturer. |Windows|
| `Type` | String | Network medium in use. |Windows|

> [!NOTE]
> Inventory only reports up to 20 network adapters per device.

## `OsVersion`

> **Description**: A single record containing the operating system name and version of the device.\
> **Supported platforms**: Android, iOS, iPadOS, Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand (Windows only), Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `OsName` | string (max length 256 characters) | Distribution or product name |Android, iOS, iPadOS, Windows|
| `OsVersion` | string (max length 40 characters) | Pretty, suitable for presentation, OS version |Android, iOS, iPadOS, Windows|
| `MajorVersion` | Long | Major release version |Android, iOS, iPadOS, Windows single device query, Windows multi device query |
| `MinorVersion` | Long | Minor release version |Android, iOS, iPadOS, Windows single device query, Windows multi device query |
| `PatchVersion` | long | Optional patch release |Android, iOS, iPadOS, macOS, Windows single device query |
| `BuildVersion` | string | Optional build-specific or variant string |Android, iOS, iPadOS, macOS,  Windows single device query |
| `Architecture` | string (max length 256 characters) | OS Architecture |Windows single device query, Windows multi device query |
| `InstallDateTime` | datetime (UTC) | The install date time of the OS. |Windows single device query, Windows multi device query |
|`AppleSupplementalOSVersion` |String |The OS version that contains the Rapid Security Response version, which is designated by a letter. |iOS, iPadOS, macOS |
|`AppleSupplementalBuildVersion` |String |The OS build version that contains the Rapid Security Response version, which is designated by a letter. |iOS, iPadOS, macOS |

## `Process`

> **Description**: All running processes on the host system.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `ProcessId` | long | Process ID |Windows|
| `ProcessName` | string (max 260 characters) | The name of process |Windows|
| `Path` | string (max 4,096 characters) | Path to executed binary |Windows|
| `CommandLine` | string (max 4,096 characters) | Complete argv |Windows|
| `CurrentWorkingDirectory` | string (max 256 characters) | Process current working directory |Windows|
| `WorkingSetSizeBytes` | long | Bytes of private memory used by process |Windows|
| `TotalSizeBytes` | long | Total virtual memory size |Windows|
| `DiskBytesRead` | long | Bytes read from disk |Windows|
| `DiskBytesWritten` | long | Bytes written to disk |Windows|
| `ParentProcessId` | long | Process parent's PID |Windows|
| `Priority` | long | Process nice level (-20 to 20, default 0) |Windows|
| `UserTimeMilliseconds` | long | CPU time in milliseconds spent user space |Windows|
| `SystemTimeMilliseconds` | long | CPU time in milliseconds spent in kernel space |Windows|
| `StartDateTime` | Datetime(UTC)Need to convert this value to datetime | Process start datetime in UTC |Windows|
| `ElapsedTimeMilliseconds` | long | Elapsed time in seconds this process has been running. |Windows|
| `ProcessorTimePercent` | long | Returns elapsed time that all of the threads of this process used the processor to execute instructions in 100-nanoseconds ticks. |Windows|
| `ThreadCount` | long | Number of threads used by process |Windows|
| `HandleCount` | long | Total number of handles that the process has open. This number is the sum of the handles currently opened by each thread in the process. |Windows|
| `WindowsUserAccount` | string | The owner of the process |Windows|
| `OnDisk` | boolNullable\<System.Boolean>  | The process path exists yes=1, no=0, unknown=-1 |Windows|

## `SharediPad`

> **Description**: Details for Shared iPad devices.\
> **Supported platforms**: iPadOS\
> **Supported for**: Device query for multiple devices.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `EstimatedResidentUsersCount` | long | Estimated number of users that can share the device based on space. |iPadOS|
| `IsMultiUser` | bool | iPad set up as multiuser |iPadOS|
| `IsTemporarySessionOnly` | bool | The device only allows temporary sessions. |iPadOS|
| `ManagedAppleIdDefaultDomains` | string | The list of domains that the device suggests on the Shared iPad login screen. |iPadOS|
| `OnlineAuthenticationGracePeriodDays` | long | The grace period for Shared iPad online authentication (in days). A value of 0 indicates that the device requires online authentication for every login |iPadOS|
| `QuotaSizeBytes` | long | The quota size in bytes for each user on this shared iPad device |iPadOS|
| `ResidentUsersCount` | long | The number of users currently on this shared iPad device. |iPadOS|
| `SkipLanguageAndLocaleSetupForNewUsers` | bool | If true, skip the language and country/region panes for new users on Shared iPad. |iPadOS|
| `TemporarySessionTimeoutSeconds` | long | The timeout interval for the temporary session. A value of 0 indicates that there's no timeout. |iPadOS|
| `UserSessionTimeoutSeconds` | long | The timeout interval for the user session. A value of 0 indicates that there's no timeout. |iPadOS|

## `SystemEnclosure`

> **Description**: Displays information pertaining to the chassis and its security status.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

> [!NOTE]
> Chassis Types property is currently not supported for Inventory or Device query for multiple devices.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `SerialNumber` | string (max 64 characters) | The serial number of the chassis. |Windows single device query, Windows multi device query |
| `AudibleAlarmEquipped` | bool | If TRUE, the frame is equipped with an audible alarm. |Windows single device query, Windows multi device query |
| `BreachDescription` | string (max 256 characters) | If provided, gives a more detailed description of a detected security breach. |Windows single device query, Windows multi device query |
| `ChassisTypes` | Array[string] | A comma-separated list of chassis types, such as Desktop or Laptop. |Windows single device query|
| `ExtendedDescription` | string (max 256 characters) | An extended description of the chassis if available. |Windows single device query, Windows multi device query |
| `LockEquipped` | bool | If TRUE, the frame is equipped with a lock. |Windows single device query, Windows multi device query |
| `Manufacturer` | string (max 256 characters) | The manufacturer of the chassis. |Windows single device query, Windows multi device query |
| `Model` | string (max 256 characters) | The model of the chassis. |Windows single device query, Windows multi device query |
| `SecurityBreach` | string (max 256 characters) | The physical status of the chassis such as Breach Successful, Breach Attempted, etc. |Windows single device query, Windows multi device query |
| `SmBiosAssetTag` | string (max 120 characters) | The assigned asset tag number of the chassis. |Windows single device query, Windows multi device query |
| `Sku` | string (max 64 characters) | The Stock Keeping Unit number if available. |Windows single device query, Windows multi device query |
| `Status` | string (256 characters) | If available, gives various operational or nonoperational statuses such as OK, Degraded, and Pred Fail. |Windows single device query, Windows multi device query |
| `VisibleAlarmEquipped` | bool | If TRUE, the frame is equipped with a visual alarm. |Windows single device query, Windows multi device query |

## `SystemInfo`

> **Description**: System information of the device.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `FqdnHostname` | string (max 256) | Network hostname including domain |Windows single device query |
| `Uuid` | string (max 36 characters) | Unique ID provided by the system |Windows single device query |
| `ComputerName` | string (max 256 characters) | Friendly computer name (optional) |Windows single device query |
| `PhysicalProcessorCount` | Long | Number of physical processors |Windows single device query |
| `ProcessorArchitecture` | string(40 characters) | CPU type |Windows single device query |
| `HardwareManufacturer` | string (max 256 characters) | Hardware vendor |Windows single device query |
| `HardwareModel` | string (max 256 characters) | Hardware model |Windows single device query |

## `SimInfo`

> **Description**: Information on the Sim cards found on the device\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `WindowsESimId` | String | The ID of an eSIM found on the device |Windows|
| `Eid` | String | The electronic identification number of the device |Windows|
| `isActive` | Boolean | Whether the eSIM is active or not |Windows|

## `Time`

> **Description**: Provides basic time information.\
> **Supported Features**: Inventory, device query for multiple devices.\
> **Supported platforms**: Windows

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `TimeZone` | String | Describes the device's time zone. |Windows|

## `TPM`

> **Description**: Provides TPM related information of the device.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `Activated` | bool | TPM is activated |Windows|
| `Enabled` | bool | TPM is enabled |Windows|
| `Owned` | bool | TPM is owned |Windows|
| `Manufacturer` | string (max 256 characters) | TPM manufacturers name |Windows|
| `ManufacturerVersion` | string (max 256 characters) | TPM version |Windows|
| `ManufacturerId` | long | TPM manufacturers ID |Windows|
| `ProductName` | string (max 256 characters) | Product name of the TPM |Windows|
| `PhysicalPresenceVersion` | string (max 256 characters) | Version of the Physical Presence Interface |Windows|
| `SpecVersion` | string (max 256 characters) | Trusted Computing Group specification that the TPM supports |Windows|

## `VideoController`

> **Description**: Provides video controller and graphics information.\
> **Supported Features**: Inventory, Device query for multiple devices.\
> **Supported platforms**: Windows

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `AdapterDacType` | String | Name or identifier of the digital-to-analog converter (DAC) chip. The character set of this property is alphanumeric. |Windows|
| `AdapterRam` | Long | Memory size of the video adapter. |Windows|
| `CurrentScanMode` | String | Current scan mode. |Windows|
| `GraphicsModel` | String | Provides manufacturer and model information of graphics card. |Windows|
| `Identifier` | String | Identifier (unique to the computer system) for this video controller. |Windows|
| `VideoModeDescription` | String | Current resolution, color, and scan mode settings of the video controller. |Windows|

## `WindowsAppCrashEvent`

> **Description**: Provides App Crash info in Windows event log file Application in look back time.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |---|
| `ReportId (Key)` | string (max 256 characters) | Report ID of the app crash event. |Windows|
| `AppPath` | string (max 256 characters) | Application path of the crashed app. |Windows|
| `AppName` | string (max 256 characters) | Application file name of the crashed app. |Windows|
| `AppVersion` | string (max 40 characters) | Application version of the crashed app. |Windows|
| `LoggedDateTime` | datetime (UTC) | System UTC time at which the event occurred and was logged. |Windows|
| `WindowsUserAccount` | string (max 256 characters) | User account associated with this app crash, if any. |Windows|

## `WindowsDriver`

> **Description**: Details for in-use Windows device drivers. This doesn't display installed but unused drivers.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

| Property | Type | Description | Supported platforms |
|--|--|--|--|
| `DriverDeviceId(Key)` | string (max 256 characters) | Device ID | Windows |
| `FriendlyName` | string (max 256 characters) | Such as "Microsoft Device Association Root Enumerator" | Windows |
| `DriverDescription` | string (max 256 characters) | Driver description | Windows |
| `DriverVersion` | string | Driver version | Windows |
| `InfName` | string (max 260 characters) | Associated inf file | Windows |
| `Class` | string (max 256 characters) | Device/driver class name | Windows |
| `ProviderName` | string (max 256 characters) | Driver provider | Windows |
| `Manufacturer` | string (max 256 characters) | Device manufacturer | Windows |
| `BuildDate[Win32\PnPSignedDriver class` - [Microsoft Learn](/previous-versions/windows/desktop/legacy/aa394354(v=vs.85)) | datetime(UTC) | Driver date | Windows |
| `Signed` | bool | Whether the driver is signed or not | Windows |

## `WindowsEvent`

> **Description**: Get Windows Event logs in the specified log name and look back in time.\
> **Supported platforms**: Windows\
> **Supported for**: Single device query on-demand.

> [!NOTE]
> When constructing the query, you must specify the log name and look back time, for example: `WindowsEvent(Application, 1d) | take 1`.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `LogName` | string (max 256 characters) | Name of the Windows event log|Windows|
| `EventId` | long | Event ID number |Windows|
| `Level` | string  | Level display name for the event. Possible value:CRITICAL\_ERROR,ERROR,WARNING,INFORMATION,VERBOSE |Windows|
| `LoggedDateTime` | datetime (UTC) | System UTC time at which the event occurred |Windows|
| `Message` | string (max 32,766 characters) | The event messages |Windows|
| `ProviderName` | string (max 256 characters) | Provider name of event |Windows|
| `WindowsUserAccount` | string (max 256) | User account associated with this event |Windows|

## `WindowsQfe`

> **Description**: Information about security patches on the device.\
> **Supported platforms**: Windows\
> **Supported for**: Device query for multiple devices, Single device query on-demand, Inventory.

| Property | Type | Description |**Supported platforms**|
| --- | --- | --- |--- |
| `HotFixId (key)` | string (max 256 characters) | Unique identifier associated with a particular update. |Windows|
| `ComputerName` | string (max 256 characters) | The name of the computer the patch is installed on. |Windows|
| `Caption` | string (max 256 characters) | A short textual description of the object. |Windows|
| `QfeDescription` | string (max 256 characters) | A textual description of the object. |Windows|
| `FixComments` | string (max 256 characters) | More comments about the Qfe. |Windows|
| `InstalledByUserAccount` | string (max 256 characters) | User account who installed the update. If this value is unknown, the property is empty. |Windows|
| `InstalledDate` | datetime (UTC) | Date that the update was installed. If this value is unknown, the property is empty. |Windows|

## `WindowsRegistry`

> **Description**: Lists registry under the passed registry key.\
> **Supported platforms**: Windows\
> **Supported for**: single device query on-demand.

> [!NOTE]
> You must pass in the registry key you're trying to query. For example, `WindowsRegistry('HKEY_LOCAL_MACHINE\\ServiceLastKnownStatus')`.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `RegistryKey` | string (max 16,638 characters) | Full path to the value |Windows|
| `ValueName` | string (max 16,383 characters) | Name of the registry value entry |Windows|
| `ValueType` | string (max 255 characters) | Type of the registry value, or 'subkey' if item is a subkey |Windows|
| `ValueData` | string (max size 1 MB) | Data content of registry value |Windows|

## `WindowsService`

> **Description**: Lists all installed Windows services and their key properties.\
> **Supported platforms**: Windows\
> **Supported for**: Single device query on-demand.

| Property | Type | Description | Supported platforms |
| --- | --- | --- |--- |
| `ServiceName` | string (max 256 characters) | Service name |Windows|
| `ServiceType` | string (max 40 characters) | Service Type, such as OWN\_PROCESS, SHARE\_PROCESS, or Interactive |Windows|
| `DisplayName` | string (max 256 characters) | Service display name |Windows|
| `State` | string (max 40 characters) | Current status of the services, such as STOPPED, START\_PENDING, STOP\_PENDING, RUNNING, CONTINUE\_PENDING, PAUSE\_PENDING, PAUSED |Windows|
| `ProcessId` | long | The Process ID of the service, if running |Windows|
| `StartMode` | string (max 40 characters) | Service start type: BOOT\_START, SYSTEM\_START, AUTO\_START, DEMAND\_START, DISABLED |Windows|
| `ExitCode` | long | The error code that the service uses to report an error that occurs when it is starting or stopping |Windows|
| `ServiceSpecific ExitCode` | long | The service-specific error code that the service returns when an error occurs while the service is starting or stopping|Windows|
| `Path` | string (max 4,096 characters) | Path to Service Executable |Windows|
| `ModulePath` | string (max 4,096 characters) | Path to ServiceDll |Windows|
| `ServiceDescription` | string (max 256 characters) | Service Description |Windows|
| `WindowsUserAccount` | string (max 256 characters) | The name of the account that the service process is logged on as when it runs. This name can be of the form Domain\UserName |Windows|
