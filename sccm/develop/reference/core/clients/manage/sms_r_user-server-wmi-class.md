---
title: "SMS_R_User Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: e5fee610-39c3-4502-a782-822767f15cb4searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_R_User Server WMI Class
The `SMS_R_User` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that is generated dynamically at SMS Provider run time and contains data discovery for users within a System Center Configuration Manager site hierarchy.  

 The following syntax is not defined in Managed Object Format (MOF) code.  

## Syntax  

```  
Class SMS_R_User : SMS_Resource  
{  
   String   AgentName[];  
   String   AgentSite[];  
   DateTime  AgentTime[];  
   DateTime  CreationDate;  
   String   DistinguishedName;  
   String   FullUserName;  
   String   Mail;  
   String   Name;  
   String   NetworkOperatingSystem;  
   UInt8   ObjectGUID;  
   UInt32   PrimaryGroupID;  
   UInt32   ResourceID;  
   UInt32   ResourceType;  
   String   SID;  
   String   UniqueUserName;  
   UInt32   UserAccountControl;  
   String   UserContainerName[];  
   String   UserGroupName[];  
   String   UserName;  
   String   UserOUName[];  
   String   WindowsNTDomain;  
};  
```  

## Methods  
 The `SMS_R_User` class does not define any methods.  

## Properties  
 `AgentName`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 List of discovery agents that found this resource.  

 `AgentSite`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 List of sites from which the discovery agents ran.  

 `AgentTime`  
 Data type: **DateTime** Array  

 Access type: Read-only  

 Qualifiers: None  

 List of discovery times.  

 `CreationDate`  
 Data type: **DateTime**  

 Access type: Read-only  

 Qualifiers: None  

 The date the record was first created, which is the date when the resource was discovered.  

 `DistinguishedName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Distinguished name of the user resource retrieved from Active Directory.  

 `FullUserName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 For Windows NT users, the value of the **Full Name** property of User Properties; for Windows 2000 users, the value of the **Display Name** property in Active Directory.  

 `Mail`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Mail address of the user resource retrieved from Active Directory.  

 `Name`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 User name displayed in the System Center Configuration Manager console. Its format is UniqueUserName (FullUserName), where FullUserName is included only if it contains a value.  

 `NetworkOperatingSystem`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Free-form string describing the operating system.  

 `ObjectGUID`  
 Data type: **UInt8**  

 Access type: Read-only  

 Qualifiers: None  

 Object GUID of the user resource retrieved from Active Directory.  

 `PrimaryGroupID`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: None  

 Primary group ID of the user resource retrieved from Active Directory.  

 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md).  

 `ResourceType`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: None  

 Type of resources on the site. For more information, see [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md).  

 `SID`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Security identifier of the user resource retrieved from Active Directory.  

 `UniqueUserName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Unique user name in the form domain\user name.  

 `UserAccountControl`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: None  

 User account control value retrieved from Active Directory.  

 `UserContainerName`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 An array of Active Directory container names to which the user belongs.  

 `UserGroupName`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 An array of Active Directory group names to which the user belongs.  

 `UserName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 User logon name.  

 `UserOUName`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 An array of Active Directory organizational units (OUs) to which the user belongs.  

 `WindowsNTDomain`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Windows NT domain that is associated with the resource.  

## Remarks  
 You cannot create or update resource instances by using WMI, but must create or update resources by using data discovery records. Note, however, that you can delete resource instances by using WMI.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md)
