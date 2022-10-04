---
description: Learn how to use the SMS_PendingRegistrationRecord Windows Management Instrumentation (WMI) class, in Configuration Manager, that describes hardware conflicts between two computers.
title: SMS_PendingRegistrationRecord Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c1e1b321-2d60-490e-a9ae-83f370f5cc88
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_PendingRegistrationRecord Server WMI Class
The `SMS_PendingRegistrationRecord` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes hardware conflicts between two computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PendingRegistrationRecord   
{   
      string AgentName;   
      string Certificate;   
      string ClientVersion;   
      string ConflictSMSID;   
      string FQDN;   
      string HardwareID;   
      boolean IsAlwaysInternet;   
      boolean IsIntegratedAuth;   
      boolean IsInternetEnabled;   
      string IssuedTo;   
      sint32 KeyType;   
      string NetBiosName;   
      string PublicKey;   
      string SiteCode;   
      string SMSID;   
      string Thumbprint;   
      datetime ValidFrom;   
      datetime ValidUntil;   
};  
```  

## Methods  
 The following table lists the methods in the `SMS_PendingRegistrationRecord` class.  

|Method|Description|  
|------------|-----------------|  
|[ResolvePendingRegistrationRecord Method in Class SMS_PendingRegistrationRecord](../../../../../develop/reference/core/clients/manage/resolvependingregistrationrecord-method-in-class-sms_pendingregistrationrecord.md)|Resolves the conflicts for the pending registration records.|  

## Properties  
 `AgentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The internal agent name of the client.  

 `Certificate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The encoded certificate of the client.  

 `ClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the installed client.  

 `ConflictSMSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The Configuration Manager unique identifier of a client that registered on the current site with the same `HardwareID`  

 `FQDN`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The fully qualified domain name of the computer.  

 `HardwareID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The calculated hardware identifier of the computer this client belongs to.  

 `IsAlwaysInternet`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the resource is always associated with the Internet.  

 `IsIntegratedAuth`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if integrated authentication is enabled.  

 `IsInternetEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if this client is an Internet-facing client.  

 `IssuedTo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The certificate subject name.  

 `KeyType`  
 Data type: `Sint32`  

 Access type: Read/Write  

 Qualifiers: enumeration("self-sign(1), issued (2)")  

 Public key type of certificate. The following values are possible.  

|Value|Description|  
|-----------|-----------------|  
|1|Self-signed certificate.|  
|2|Certificate was issued by a certification authority.|  

 `NetBiosName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The NetBIOS name of the computer.  

 `PublicKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: lazy  

 The public key of the certificate, which reflects the globally unique SHA-1 hash thumbprint indicated by the `Thumbprint` property.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The Configuration Manager site this client belongs to.  

 `SMSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: key  

 The unique identifier of the client that sent the pending registration record.  

 `Thumbprint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: Lazy  

 The hash value of the certificate.  

 `ValidFrom`  
 Data type: `Datetime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time when the certificate becomes effective.  

 `ValidUntil`  
 Data type: `Datetime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time when the certificate expires.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
