---
title: "SMS_G_System_SYSTEM Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6627a103-4207-4c05-9fd6-ab0edf7d1c58
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_G_System_SYSTEM Server WMI Class
The `SMS_G_System_SYSTEM` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that contains information about hardware inventory related to a client computer operating system.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_SYSTEM : SMS_G_System_Current  
{  
     String Domain;  
     UInt32 GroupID;  
     String Name;  
     UInt32 ResourceID;  
     UInt32 RevisionID;  
     String SMSID;  
     String SystemRole;  
     String SystemType;  
     DateTime TimeStamp;  
};  
```  

## Methods  
 The `SMS_G_System_SYSTEM` class does not define any methods.  

## Properties  
 `Domain`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the Windows NT domain to which the operating system account belongs.  

 `GroupID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the client computer.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `RevisionID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `SMSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Unique System Center Configuration Manager ID of the client.  

 `SystemRole`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The system role played by the computer operating system. Possible values are:  

- Workstation  

- Server  

  `SystemType`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: None  

  Description of the operating system, for example, "X86-based PC".  

  `TimeStamp`  
  Data type: `DateTime`  

  Access type: Read/Write  

  Qualifiers: None  

  See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

  For this class, the default value of this property is `null`.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class was added in SMS 2.0 Service Pack 1. It does not have a Win32 class equivalent.  

## See Also  
 [Hardware Inventory Server WMI Classes](../../../../../develop/reference/core/clients/manage/hardware-inventory-server-wmi-classes.md)   
 [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md)
