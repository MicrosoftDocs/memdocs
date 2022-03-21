---
title: "SMS_R_UserGroup Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1d72e0a2-b590-4bc6-b5d4-6546a3290227
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_R_UserGroup Server WMI Class
The `SMS_R_UserGroup` Windows Management (WMI) class is an SMS Provider server class, in Configuration Manager, that is generated dynamically at SMS Provider run time and contains discovery data for user group objects.  

 The following syntax is not defined in Managed Object Format (MOF) code.  

## Syntax  

```  
Class SMS_R_UserGroup : SMS_Resource  
{  
   String   ActiveDirectoryContainerName[];  
   String   ActiveDirectoryOrganizationalUnit[];  
   String   ADDomainName;  
   String   AgentName[];  
   String   AgentSite[];  
   DateTime AgentTime[];  
   DateTime CreationDate;  
   UInt32   GroupType;  
   String   Name;  
   String   NetworkOperatingSystem;   
   UInt8    ObjectGUID[];  
   UInt32   ResourceID;  
   UInt32   ResourceType;  
   String   SID;  
   String   UniqueUsergroupName;  
   String   UsergroupName;  
   String   WindowsNTDomain;  
};  
```  

## Methods  
 The `SMS_R_UserGroup` class does not define any methods.  

## Properties  
 `ActiveDirectoryContainerName`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 Active Directory container name for the group resource.  

 `ActiveDirectoryOrganizationalUnit`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 Active Directory Organizational Unit for the group resource.  

 `ADDomainName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Name of the Active Directory domain for the group resource.  

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

 `Creation Date`  
 Data type: **DateTime** Array  

 Access type: Read-only  

 Qualifiers: None  

 Date and time of creation.  

 `GroupType`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: None  

 Type of group resources on the site.  

 `Name`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Group name displayed in the Configuration Manager console.  

 `NetworkOperatingSystem`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Free-form string describing the operating system.  

 `ObjectGUID`  
 Data type: **UInt8** Array  

 Access type: Read-only  

 Qualifiers: None  

 Object GUID of the group resource retrieved from Active Directory.  

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

 The Active Directory security ID for the group.  

 `UniqueUsergroupName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Unique user group name in the form domain\group name.  

 `UsergroupName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Unique user group name that represents the resource within the Windows NT domain.  

 `WindowsNTDomain`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 String representing the Windows NT domain associated with the resource.  

## Remarks  
 You cannot create or update resource instances by using WMI, but must create or update resources using discovery data records. Note, however, that you can delete resource instances by using WMI.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md)
