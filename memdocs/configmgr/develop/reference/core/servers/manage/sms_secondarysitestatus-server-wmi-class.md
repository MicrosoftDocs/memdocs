---
description: The SMS_SecondarySiteStatus WMI class is an SMS Provider server class, in Configuration Manager, that represents secondary site installation or uninstallation status.
title: "SMS_SecondarySiteStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: fc28e42f-09f5-41aa-870a-28a673dfe6bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SecondarySiteStatus Server WMI Class
The `SMS_SecondarySiteStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents secondary site installation or uninstallation status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SecondarySiteStatus : SMS_BaseClass  
{  
    String Description;  
    DateTime MessageTime;  
    String SiteCode;  
    UInt32 SiteInstallID;  
    String Status;  
    UInt32 StatusID;  
};  
```  

## Methods  
 The `SMS_SecondarySiteStatus` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Description of the status for secondary installation or uninstallation status.  

 `MessageTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: [key]  

 Time of the message reported for the secondary site installation or uninstallation.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Site code of the secondary site.  

 `SiteInstallID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Site installation or uninstallation identifier.  

 `Status`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Secondary site installation or uninstallation status.  

 `StatusID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Identifier for the status.  

## Remarks  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
