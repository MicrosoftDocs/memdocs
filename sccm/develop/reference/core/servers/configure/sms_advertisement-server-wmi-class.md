---
title: "SMS_Advertisement Class"
ms.custom: ""
ms.date: "04/27/2017"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 463bed7d-80e4-4fd9-a7d7-dfb10b538a43
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 18
author: "lleonard-msft"
ms.author: "alleonar"
manager: "angrobe"
---
# SMS_Advertisement server WMI class
The `SMS_Advertisement` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents an advertisement used to announce software package programs that are available for running on clients.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Advertisement : SMS_BaseClass  
{  
      UInt32 ActionInProgress;  
      UInt32 AdvertFlags;  
      String AdvertisementID;  
      String AdvertisementName;  
      SMS_ScheduleToken AssignedSchedule[];  
      Boolean AssignedScheduleEnabled;  
      Boolean AssignedScheduleIsGMT;  
      UInt32 AssignmentID;  
      String CollectionID;  
      String Comment;  
      UInt32 DeviceFlags;  
      DateTime ExpirationTime;  
      Boolean ExpirationTimeEnabled;  
      Boolean ExpirationTimeIsGMT;  
      String HierarchyPath;  
      Boolean IncludeSubCollection;  
      UInt8 ISVData[];  
      UInt32 ISVDataSize;  
      String ISVString;  
      UInt32 MandatoryCountdown;  
      UInt32 OfferType;  
      String PackageID;  
      DateTime PresentTime;  
      Boolean PresentTimeEnabled;  
      Boolean PresentTimeIsGMT;  
      UInt32 Priority;  
      String ProgramName;  
      UInt32 RemoteClientFlags;  
      String SourceSite;  
      UInt32 TimeFlags;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_Advertisement` class.  

|Method|Description|  
|------------|-----------------|  
|[GetAdvertisements Method in Class SMS_Advertisement](../../../../../develop/reference/core/servers/configure/getadvertisements-method-in-class-sms_advertisement.md)|Gets the advertisement IDs that are targeted to the resource.|  
|[GetNextID Method in Class SMS_Advertisement](../../../../../develop/reference/core/servers/configure/getnextid-method-in-class-sms_advertisement.md)|Retrieves the ID number that will be used for the next advertisement created.|  
|[RiskyDeploymentStatusMessage Method in Class SMS_Advertisement](../../../../../develop/reference/core/servers/configure/riskydeploymentstatusmessage-method-in-class-sms_advertisement.md)|Sends a warning status message about a user deployment to a risky collection.|  
|[SetNextID Method in Class SMS_Advertisement](../../../../../develop/reference/core/servers/configure/setnextid-method-in-class-sms_advertisement.md)|Sets the ID number that will be used for the next advertisement created.|  
|[SetSourceSite Method in Class SMS_Advertisement](../../../../../develop/reference/core/servers/configure/setsourcesite-method-in-class-sms_advertisement.md)|Sets the source site code for the advertisement.|  
|[Unlock Method in Class SMS_Advertisement](../../../../../develop/reference/core/servers/configure/unlock-method-in-class-sms_advertisement.md)|Sets the source site to the current site, unlocking the advertisement. **Warning:**  This method is deprecated.|  

## Properties  
### `ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 Current action being performed on the package by Configuration Manager. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|NONE|  
|1|UPDATE|  
|2|ADD|  

### `AdvertFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags indicating how the advertisement should be announced to the user. Possible values are listed below. The default value is 0.  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x00000020 (5)|IMMEDIATE. Announce the advertisement to the user immediately.|  
|0x00000100 (8)|ONSYSTEMSTARTUP. Announce the advertisement to the user on system startup.|  
|0x00000200 (9)|ONUSERLOGON. Announce the advertisement to the user on logon.|  
|0x00000400 (10)|ONUSERLOGOFF. Announce the advertisement to the user on logoff.|  
|0x00008000 (15)|WINDOWS_CE. The advertisement is for a device client.|  
|0x00010000 (16)|ENABLE_PEER_CACHING <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  
|0x00020000 (17)|DONOT_FALLBACK. Do not fall back to unprotected distribution points.|  
|0x00040000 (18)|ENABLE_TS_FROM_CD_AND_PXE. The task sequence is available to removable media and the pre-boot execution environment (PXE) service point.|  
|0x00100000 (20)|OVERRIDE_SERVICE_WINDOWS. Override maintenance windows in announcing the advertisement to the user.|  
|0x00200000 (21)|REBOOT_OUTSIDE_OF_SERVICE_WINDOWS. Reboot outside of maintenance windows.|  
|0x00400000 (22)|WAKE_ON_LAN_ENABLED. Announce the advertisement to the user with Wake On LAN enabled.|  
|0x00800000 (23)|SHOW_PROGRESS. Announce the advertisement to the user showing task sequence progress.|  
|0x02000000 (25)|NO_DISPLAY. The user should not run programs independently of the assignment.|  
|0x04000000 (26)|ONSLOWNET. Assignments are mandatory over a slow network connection.|  

 These flags must be coordinated with the flags that are specified in the `ProgramFlags` property of the advertised program. For example, if you set ONUSERLOGOFF, the NOUSERLOGGEDIN flag in the program must be set. If the flag settings do not match, the program is not advertised. For more information, see [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md).  

 Setting IMMEDIATE, ONUSERLOGON, or ONUSERLOGOFF or providing an `AssignedSchedule` value makes the advertised program mandatory. A mandatory program is run automatically after the client has received the advertisement. The client cannot reject or postpone the installation.  

 Set the NO_DISPLAY and ONSLOWNET bits only when the IMMEDIATE, ONUSERLOGON, or ONUSERLOGOFF bit is set or the program has an `AssignedSchedule` value.  

 Set NO_DISPLAY when you do not want the user to run programs independently of the assignment. If you do not set this flag, the advertisement is shown in the list of advertisements and can be run independently of the assignment. The program can still be mandatory.  

 Set ONSLOWNET when assignments are mandatory over a slow network connection, for example, when a computer connects using a modem.  

### `AdvertisementID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, ResID(801), ResDLL("SMS_RSTT.dll")]  

 Unique auto-generated key that identifies the advertisement. The default value is "".  

### `AdvertisementName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 Unique user-friendly name for the advertisement.  

 `AssignedSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type: Read/Write  

 Qualifiers: [max(15), lazy]  

 [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) objects indicating the time when the advertisement becomes mandatory on the clients.  

### `AssignedScheduleEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if the schedule defined in the `AssignedSchedule` property is active. The default value is `false`.  

### `AssignedScheduleIsGMT`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if the schedule defined in the `AssignedSchedule` property is in Universal Metric Time (UMT). The default value is `false`.  

### `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 ID of the assignment associated with the advertisement.  

### `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 Existing collection to which the advertisement is targeted.  

### `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Simple description or note about the advertisement. The default value is "".  

### `DeviceFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flags describing the device. Possible values are listed below. The default value is 0.  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x01000000 (24)|Always assign program to the client.|  
|0x02000000 (25)|Assign only if the device is currently connected to a high-bandwidth connection (default above 60 KBps).|  
|0x04000000 (26)|Assign only if the device is docked, that is, it is attached to a desktop that is using ActiveSync.|  

### `ExpirationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the advertisement is no longer available to clients. The default value is 19900101000000.000000+****.  

### `ExpirationTimeEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if the advertisement expires at the time indicated by the `ExpirationTime` property. The default value is `false`.  

### `ExpirationTimeIsGMT`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if the time defined in the `ExpirationTime` property is in UMT. The default value is `false`.  

### `HierarchyPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved.  

### `IncludeSubCollection`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` (default) if the advertisement is advertised to the subcollections of the specified collection.  

### `ISVData`  
 Data type: `Uint8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 Information that allows a single ISV to store data relating to an `SMS_Program` instance. There are no restrictions or defined formats for this data. However, it is important to not overwrite the property after its ISV ownership has been established. Therefore, the calling application should read the existing data in this property first. If the data does not belong to the application, it should not be modified. Any ISV or application owner who is using this property should include an identifier in the data so that ownership can be easily established.  

### `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The size of the data represented by the `ISVData` property. The default value is 0.  

### `ISVString`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 String for partner extensibility.  

### `MandatoryCountdown`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Duration, in minutes, to show operating system deployment user notification mandatory schedule countdown. The default value is 0.  

### `OfferType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Advertisement type that indicates that the advertisement is targeted to users.  

|Value|Description|  
|-----------|-----------------|  
|0|Required|  
|2|Available|  

### `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 ID for an existing package associated with the advertisement. The value must be in uppercase.  

### `PresentTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the advertisement is made available to clients. The default value is 19900101000000.000000+****.  

### `PresentTimeEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` (default) if the present time is enforced by Configuration Manager.  

### `PresentTimeIsGMT`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if the time defined in the `PresentTime` property is in UMT. The default value is `false`.  

### `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 The priority used in replicating the advertisement to child sites. Possible values are listed below. The default value is NORMAL (2).  

|Value|Description|  
|-----------|-----------------|  
|1|HIGH|  
|2|NORMAL|  
|3|LOW|  

### `ProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 A program within the specified package (`PackageID`) to be advertised.  

### `RemoteClientFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags specifying how the program should run when the client is connected either locally or remotely to a distribution point. Possible values are listed below. The default value is 48.  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x00000001 (0)|BATTERY_POWER. Run the program by using battery power. This value is currently unused.|  
|0x00000002 (1)|RUN_FROM_CD. Run the program from CD. This value is currently unused.|  
|0x00000004 (2)|DOWNLOAD_FROM_CD. Download the program from CD. This value is currently unused.|  
|0x00000008 (3)|RUN_FROM_LOCAL_DISPPOINT. Run the program from the local distribution point.|  
|0x00000010 (4)|DOWNLOAD_FROM_LOCAL_DISPPOINT. Download the program from the local distribution point.|  
|0x00000020 (5)|DONT_RUN_NO_LOCAL_DISPPOINT. Do not run the program if there is no local distribution point.|  
|0x00000040 (6)|DOWNLOAD_FROM_REMOTE_DISPPOINT. Download the program from the remote distribution point.|  
|0x00000080 (7)|RUN_FROM_REMOTE_DISPPOINT. Run the program from the remote distribution point.|  
|0x00000100 (8)|DOWNLOAD_ON_DEMAND_FROM_LOCAL_DP. Download the program on demand from the local distribution point. This is only applicable for task sequences.|  
|0x00000200 (9)|DOWNLOAD_ON_DEMAND_FROM_REMOTE_DP. Download the program on demand from the remote distribution point. This is only applicable for task sequences.|  
x00000400 (10)|BALLOON_REMINDERS_REQUIRED. Balloon reminders are required.|  
|0x00000800 (11)|RERUN_ALWAYS. Always rerun the program.|  
|0x00001000 (12)|RERUN_NEVER. Never rerun the program.|  
|0x00002000 (13)|RERUN_IF_FAILED. Rerun the program if execution previously failed.|  
|0x00004000 (14)|RERUN_IF_SUCCEEDED. Rerun the program if execution previously succeeded.|  
|0x00008000 (15)|PERSIST_ON_WRITE_FILTER_DEVICES <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  
|0x00020000 (17)|DON’T_FALLBACK <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  
|0x00040000 (18)|DP_ALLOW_METERED_NETWORK <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  

### `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Three-letter site code of the site where the advertisement originates.  

### `TimeFlags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, bits]  

 Reserved for internal use. Flags that duplicate the information in the time-related properties. Possible values are listed below. For example, ENABLE_PRESENT is set when `PresentTimeEnabled` equals `true`.  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x00000001 (0)|ENABLE_PRESENT|  
|0x00000002 (1)|ENABLE_EXPIRATION|  
|0x00000004 (2)|ENABLE_AVAILABLE|  
|0x00000008 (3)|ENABLE_UNAVAILABLE|  
|0x00000010 (4)|ENABLE_MANDATORY|  
|0x00000020 (5)|GMT_PRESENT|  
|0x00000040 (6)|GMT_EXPIRATION|  
|0x00000080 (7)|GMT_AVAILABLE|  
|0x00000100 (8)|GMT_UNAVAILABLE|  
|0x00000200 (9)|GMT_MANDATORY|  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Although there are no other key properties, the properties `AdvertisementName`, `CollectionID`, `PackageID`, and `ProgramName` are qualified as NOT_NULL, and values must be supplied. Your application cannot update these properties after a class instance is created. To change these values, the application must delete the instance and create a new instance with the correct values.  

## Requirements  

## Runtime requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)
