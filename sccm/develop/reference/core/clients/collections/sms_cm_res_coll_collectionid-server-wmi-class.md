---
title: "SMS_CM_RES_COLL_CollectionID Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ad11fe22-620e-4259-b71d-c393e464f3ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CM_RES_COLL_CollectionID Server WMI Class
The `SMS_CM_RES_COLL_CollectionID` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a particular member of an [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object by collection ID.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_RES_COLL_CollectionID : SMS_CollectionMember  
{  
      UInt32 ClientType;  
      String Domain;  
      Boolean IsActive;  
      Boolean IsAlwaysInternet;  
      UInt32 IsApproved;  
      Boolean IsAssigned;  
      Boolean IsBlocked;  
      Boolean IsClient;  
      Boolean IsDecommissioned;  
      Boolean IsDirect;  
      Boolean IsInternetEnabled;  
      Boolean IsObsolete;  
      String Name;  
      UInt32 ResourceID;  
      UInt32 ResourceType;  
      String SiteCode;  
      String SMSID;  
};  
```  

## Methods  
 The `SMS_CM_RES_COLL_CollectionID` class does not define any methods.  

## Properties  
 `ClientType`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Type of client. Possible values are:  

|||  
|-|-|  
|1|Advanced|  
|3|Device|  

 `Domain`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `IsActive`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the collection member is active.  

 `IsAlwaysInternet`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` to always use the Internet.  

 `IsApproved`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Whether the resource is approved. Possible values are:   

|||  
|-|-|  
|0|Not approved|  
|1|Approved|  
|2|Not applicable|  

 `IsAssigned`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `IsBlocked`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the collection member is blocked.  

 `IsClient`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `IsDecommissioned`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the collection member is decommissioned.  

 `IsDirect`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `IsInternetEnabled`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the collection member is enabled for the Internet.  

 `IsObsolete`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the collection member is obsolete.  

 `Name`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [key]  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `ResourceType`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `SiteCode`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [SizeLimit("3")]  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

 `SMSID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 See [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md).  

## Remarks  
 The `CollectionID` property of a collection is the unique collection identifier assigned when the collection is created. The SMS Provider creates several default `SMS_CM_RES_COLL_``CollectionID` classes at installation time for collection IDs with values beginning with "SMS". For example, SMS_CM_RES_COLL_`SMS00004` identifies all Windows NT Workstation systems.  

 This class is deleted automatically if the associated collection is deleted.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_CollectionMember Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionmember-server-wmi-class.md)
