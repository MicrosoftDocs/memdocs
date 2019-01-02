---
title: "SMS_FullCollectionMembership Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c8c0f370-89b4-4fcf-9057-0867d1f6dc3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_FullCollectionMembership Server WMI Class
The `SMS_FullCollectionMembership` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists all member resources of a specific collection.  

## Syntax  

```  
Class SMS_FullCollectionMembership : SMS_BaseClass   
{   
      String AMTFullVersion;  
      UInt32 AMTStatus;  
      UInt32 ClientCertType;  
      UInt32 ClientType;   
      String ClientVersion;   
      String CollectionID;   
      String DeviceCategory;  
      UInt32 DeviceOwner;   
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
      Boolean IsVirtualMachine;  
      String Name;   
      UInt32 Priority;  
      UInt32 ResourceID;   
      UInt32 ResourceType;   
      String SiteCode;   
      String SMSID;  
      Boolean SuppressAutoProvision;  
};  
```  

## Methods  
 The `SMS_FullCollectionMembership` class does not define any methods.  

## Properties  
 `AMTFullVersion`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Starting with Configuration Manager version 1606, this property is no longer used.  

 `AMTStatus`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Starting with Configuration Manager version 1606, this property is no longer used.  

 `ClientCertType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client certificate type. Possible values are:  

|Self-signed Certificate|  
|PKI Certificate|  

 `ClientType`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Type of client. Possible values are:  

|Value|Definition|
|----|----|
|1|Client|  
|3|Device|  

 `ClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Version of the installed client software.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 ID of the collection to which the member belongs.  

 `DeviceCategory`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Category of the device.  

 `DeviceOwner`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Owner of the device. Possible values are:  

|Value|Definition|
|----|----|
|1|Company|  
|2|Personal|  

 `Domain`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Domain to which the resource belongs.  

 `IsActive`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the client is active.  

 `IsAlwaysInternet`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if this is an Internet-facing client.  

 `IsApproved`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Whether the resource is approved. Possible values are:  

|Value|Definition|
|----|----|
|0|Not approved|  
|1|Approved|  
|2|Not applicable|  

 `IsAssigned`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the client is assigned to any site.  

 `IsBlocked`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the client is blocked.  

 `IsClient`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if this is a client.  

 `IsDecommissioned`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the record is deleted.  

 `IsDirect`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the client is a member through a direct rule, represented by [SMS_CollectionRuleDirect Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionruledirect-server-wmi-class.md); otherwise `false` or `null`.  

 `IsInternetEnabled`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the client can be Internet-enabled.  

 `IsObsolete`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if this is an obsolete record.  

 `IsVirtualMachine`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if this is a virtual machine.  

 `Name`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Name of the resource.  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Priority of the client settings.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [key]  

 Unique ID supplied by Configuration Manager for the resource. This ID is not unique across sites.  

 `ResourceType`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Type of resource. Possible values are:  

- System  

- User groups  

- User  

  `SiteCode`  
  Data type: `String`  

  Access type: Read Only  

  Qualifiers: [SizeLimit("3")]  

  Site code of the site that created the collection.  

  `SMSID`  
  Data type: `String`  

  Access type: Read Only  

  Qualifiers: None  

  Configuration Manager unique ID.  

  `SuppressAutoProvision`  
  Data type: `Boolean`  

  Access type: Read Only  

  Qualifiers: None  

  When set to `true` and when this resource belongs to a collection configured for automatic provisioning, prevents the resource from being automatically provisioned by an Out of Band service point.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Collections](../../../../../develop/core/clients/collections/collections.md)
