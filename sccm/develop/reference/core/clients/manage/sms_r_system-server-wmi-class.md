---
title: "SMS_R_System Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: a3bfa9cf-2aa0-4fcc-be1e-50983a1fb432searchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_R_System Server WMI Class
The `SMS_R_System` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that is generated dynamically at SMS Provider run time and contains discovery data for all discovered system resources.  

 The following syntax is not defined in Managed Object Format (MOF) code.  

## Syntax  

```  
Class SMS_R_System : SMS_Resource   
{   
   UInt32 Active;   
   String ADSiteName;   
   String AgentName[];   
   String AgentSite[];   
   DateTime AgentTime[];   
   UInt32 AlwaysInternet;   
   String AMTFullVersion;   
   UInt32 AMTStatus;   
   UInt32 Client;   
   UInt32 ClientType;   
   String ClientVersion;   
   String CPUType;   
   DateTime CreationDate;   
   UInt32 Decommissioned;   
   String DistinguishedName;   
   String EASDeviceID;   
   String HardwareID;   
   UInt32 InternetEnabled;   
   String IPAddresses[];   
   String IPSubnets[];   
   String IPv6Addresses[];   
   String IPv6Prefixes[];   
   Boolean IsAssignedToUser;   
   UInt32 IsClientAMT30Compatible;   
   Boolean IsMachineChangesPersisted;   
   Boolean IsVirtualMachine;   
   String LastLogonUserDomain;   
   String LastLogonUserName;   
   DateTime LastLogonTimestamp;   
   String MACAddresses[];   
   String MDMDeviceCategory;  
   String Name;   
   String NetbiosName;   
   UInt8 ObjectGUID[];   
   UInt32 Obsolete;   
   String OperatingSystemNameandVersion;   
   String PreviousSMSUUID;   
   UInt32 PrimaryGroupID;   
   String ResourceDomainORWorkgroup;   
   UInt32 ResourceID;   
   String ResourceNames[];   
   UInt32 ResourceType;   
   String SecurityGroupName[];   
   String SID;   
   String SMBIOSGUID;   
   String SMSAssignedSites[];   
   String SMSInstalledSites[];   
   String SMSResidentSites[];   
   String SMSUniqueIdentifier;   
   DateTime SMSUUIDChangeDate;   
   String SNMPCommunityName;   
   UInt32 SuppressAutoProvision;   
   String SystemContainerName[];   
   String SystemGroupName[];   
   String SystemOUName[];   
   String SystemRoles[];   
   UInt32 Unknown;   
   UInt32 UserAccountControl;   
   String VirtualMachineHostName;   
   UInt32 WipeStatus;   
};  
```  

## Methods  
 The `SMS_R_System` class does not define any methods.  

## Properties  
 `Active`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Flag that indicates the state of the client on the network. Although it is usually set to 1, this flag is set to 0 by the client health tools when it is determined that the client is not healthy or not actively participating on the network.  

 `ADSiteName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The Active Directory site name that is assigned to the client.  

 `AgentName`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of the names of discovery agents that found the resource.  

 `AgentSite`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of sites from which the discovery agents run.  

 `AgentTime`  
 Data type: `DateTime` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of discovery dates and times.  

 `AlwaysInternet`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 ….  

 `AMTFullVersion`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Provides the Intel Active Management Technology (Intel AMT) firmware version of this computer. The format is: MAJOR.MINOR.MICRO.  

 `AMTStatus`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Status of the Intel AMT component of this computer. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|NULL|Unknown.|  
|0|Computer is not supported.|  
|1|Computer is detected.|  
|2|Computer is not provisioned.|  
|3|Computer is provisioned.|  

 `Client`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Value that indicates whether a computer has System Center Configuration Manager client software installed. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|A computer that has no client software installed.|  
|1|A computer that has client software installed.|  

 `ClientType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 The type of the client that is installed on the computer. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|Legacy|  
|1|Advanced Client|  
|3|Device Client|  

 `ClientVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Version of the installed client software.  

 `CPUType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The CPU type, for example, StrongARM. Currently, only device clients report this value.  

 `CreationDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 The date the record was first created, when the resource was first discovered.  

 `Decommissioned`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Flag that identified whether the resource is decommissioned or not.   

 `DistinguishedName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The distinguished name of the account.   

 `EASDeviceID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 EASDeviceID ….   

 `HardwareID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 An ID that uniquely describes the hardware on which the client is installed. This ID remains unchanged through re-imaging or through successive installations of the operating system or client. This differs from the System Center Configuration Manager unique ID, which might change under these circumstances.  

 `InternetEnabled`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 ….   

 `IPAddresses`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of the IP addresses that are associated with the resource. More than one address is listed if the resource has multiple network cards installed.  

 `IPSubnets`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of the subnet masks that are associated with the resource IP addresses.  

 `IPv6Addresses`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of the IPv6 addresses of the resource. ….  

 `IPv6Prefixes`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of the IPv6 prefixes of the resource.  

 `IsAssignedToUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the resource is assigned to a user.  

 `IsClientAMT30Compatible`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Value that indicates the presence of the AMT firmware on the computer. The Out of Band service point determines this value when it tries to establish a connection to the computer during provisioning and discovery scenarios.  

|Value|Description|  
|-----------|-----------------|  
|0|AMT firmware does not exist.|  
|1|AMT firmware does exist.|  

 `IsMachineChangesPersisted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if computer changes are persisted.  

 `IsVirtualMachine`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the resource is a virtual machine.  

 `LastLogonUserDomain`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Domain used by the last logged-on user at the time the discovery agent ran.  

 `LastLogonTimestamp`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 The date of the last user logon.   

 `LastLogonUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the last logged-on user at the time the discovery agent ran.  

 `MACAddresses`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of the media.  

 Media access controller (MAC) addresses of the resource.  

 `MDMDeviceCategory`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 If a device is assigned a device category, this property holds the GUID key associated with `CategoryID`, defined in [SMS_MDMDeviceCategory Server WMI Class](../../../../../develop/reference/mdm/sms_mdmdevicecategory-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the resource.  

 `NetbiosName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name used by the NetBIOS protocol.  

 `ObjectGUID`  
 Data type: `UInt8 Array`  

 Access type: Read-only  

 Qualifiers: None  

 Object GUID of the resource retrieved from Active Directory.  

 `Obsolete`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Value identifying the state of the record. Although it is usually set to 0, this value is set to 1 when the server detects that the record has been superseded by another record for the same computer. If several records have the same `HardwareID` value (same computer), the older records are marked as obsolete.  

 `OperatingSystemNameandVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Free-form string that describes the operating system.  

 `PreviousSMSUUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 ID of the hardware. If the client determines that the hardware has changed significantly (that is, that the client has most likely been moved from one computer to another), it generates a new GUID for itself and reports the old one in this property. The server also marks the old record as obsolete.  

 `PrimaryGroupID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Primary group of the resource retrieved from Active Directory.  

 `ResourceDomainORWorkgroup`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Domain or workgroup to which the resource belongs.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md).  

 `ResourceNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of non-NetBIOS names.  

 `ResourceType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Type of resources on the site. For more information, see [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md).  

 `SecurityGroupName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 SecurityGroupName  

 `SID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 SID of the resource retrieved from Active Directory.  

 `SMBIOSGUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 BIOS GUID of a client computer.  

 `SMSAssignedSites`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of site codes for sites to which the resource is assigned, based on the site boundaries. Even though a resource is assigned to a site, it might not be functioning as a client if the client software is not yet installed.  

 `SMSInstalledSites`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of codes for sites to which the resource is reporting data. Eventually, this list should match the list of assigned sites.  

 `SMSUniqueIdentifier`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Unique ID that comes from the client computer. This ID is unique across sites.  

 `SMSUUIDChangeDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 The date of when the client generated a new GUID.  

 `SNMPCommunityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 SNMP community name used in network discovery to discover the resource.  

 `SuppressAutoProvision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Suppress auto provision on AMT enabled client computer.  

 `SystemContainerName`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 An array of Active Directory container names to which the system belongs.  

 `SystemGroupName`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 An array of Active Directory group names to which the system belongs.  

 `SystemSystemOUName`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 An array of organizational units (OUs) to which the system belongs.  

 `SystemRoles`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 List of site system roles that the resource performs in the Configuration Manager installation, such as a distribution point. Only resources that perform one or more specific site system roles have a value for this property.  

 `Unknown`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Unknown.   

 `UserAccountControl`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 User account control value retrieved from Active Directory.  

 `VirtualMachineHostName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Virtual machine host name.  

 `WipeStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Wipe status of the device, as reported through Exchange Active Sync (EAS).  

|||  
|-|-|  
|1|Wipe Pending|  
|2|Wipe Cancelling|  
|3|Wipe Confirmed/Registered|  

## Remarks  
 You cannot create or update resource instances by using WMI, but you must create or update resources by using data discovery records. However, you can delete resource instances by using WMI.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md)
