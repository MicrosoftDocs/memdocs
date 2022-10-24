---
title: SMS_Admin server WMI class
titleSuffix: Configuration Manager
description: Details of the SMS_Admin server WMI class
ms.date: 09/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ddc3da5e-2d17-4e03-9987-d7fc5c06f25d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_Admin server WMI class

The `SMS_Admin` WMI class is an SMS provider server class in Configuration Manager that represents the role-based administration (RBA) user.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```  
Class SMS_Admin : SMS_BaseClass  
{  
    UInt32 AccountType;  
    UInt32 AdminID;  
    String AdminSid;  
    String Categories[];  
    String CategoryNames[];  
    String CollectionNames[];  
    String CreatedBy;  
    DateTime CreatedDate;  
    String DisplayName;  
    String DistinguishedName;  
    SMS_AdminExtendedData ExtendedData[];  
    Boolean IsCovered;  
    Boolean IsDeleted;  
    Boolean IsGroup;  
    String LastModifiedBy;  
    DateTime LastModifiedDate;  
    String LogonName;  
    SMS_APermission Permissions[];  
    String RoleNames[];  
    String Roles[];  
    String SKey;  
    String SourceSite;  
};  
```  

## Methods

The `SMS_Admin` class includes the following methods:

- [GetAdminExtendedData method in class SMS_Admin](getadminextendeddata-method-in-class-sms_admin.md): Returns extended data the current user and its groups have for a given type.

## Properties

 `AccountType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The type of account. The possible values are:  

|Value|Account type|  
|-|-|  
|0|User|  
|1|Group|  
|2|Machine|  
|128|UnverifiedUser|  
|129|UnverifiedGroup|  
|130|UnverifiedMachine|  

 `AdminID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The ID of the admin object. This value is auto-generated when the object is created and never changed afterward. The default value is 0.  

 `AdminSid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy, not_null, unique]  

 The SID of the user, when the admin is created.  

 `Categories`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 The RBA secured categories associated with this account.  

 `CategoryNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the RBA secured categories associated with this account.  

 `CollectionNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the collections associated with this account.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("512")]  

 The name of the user that created this account.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date when this account was created.  

 `DisplayName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit ("512")]  

 The display name of the account.  

 `DistinguishedName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit("4000")]  

 The distinguished name of the account. If the distinguished name is not null, `LogonName` and `AdminSid` will be ignored.  

 `ExtendedData`  
 Data type: `SMS_AdminExtendedData` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Reserved for internal use.  

 `IsCovered`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 `true` if the current user has more permissions than this account.  

 `IsDeleted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if the account has been deleted from Active Directory.  

 `IsGroup`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if the account is an Active Directory security group.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("512")]  

 The name of the user that last modified this account.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date the account was last modified.  

 `LogonName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, sizelimit]  

 The logon name of the account. This could be a Windows NT 4 name (ADS_NAME_TYPE_NT4) or a simple domain name (ADS_NAME_TYPE_DOMAIN_SIMPLE).  

 `Permissions`  
 Data type: `SMS_APermission` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The list of permission assigned to this account.  

 `RoleNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 The list of role names associated with the current user.  

 The following table lists the built-in role identifiers and names:

|Role identifier|Role name|  
|---------------------|---------------|  
|SMS0001R|Full Administrator|  
|SMS0002R|Read-only Analyst|  
|SMS0003R|Remote Tools Operator|  
|SMS0004R|Asset Manager|  
|SMS0006R|Compliance Settings Manager|  
|SMS0007R|Application Deployment Manager|  
|SMS0008R|Application Author|  
|SMS0009R|Application Administrator|  
|SMS000AR|Operating System Deployment Manager|  
|SMS000BR|Infrastructure Manager|  
|SMS000CR|Software Update Manager|  
|SMS000ER|Operations Administrator|  
|SMS000FR|Security Administrator|  
|SMS000GR|EndPoint Protection Manager|
|SMS000HR|Company Resource Access Manager|

 `Roles`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 The ID of roles associated with the current user.  

 For a list of the the built-in role identifiers and names, see the `RoleNames` property.

 `SKey`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Reserved for internal use.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, sizelimit("3")]  

 The site where the account was created.  

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../../../develop/core/reqs/server-development-requirements.md).
