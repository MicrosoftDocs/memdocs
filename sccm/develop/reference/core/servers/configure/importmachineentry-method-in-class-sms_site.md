---
title: "ImportMachineEntry Method"
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
ms.assetid: 89d8d59f-79b1-4be7-85a8-43e741528a8esearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ImportMachineEntry Method in Class SMS_Site
The `ImportMachineEntry` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that imports computer information.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 ImportMachineEntry   
{  
    [IN]    String NetbiosName  
    [IN]    String SMBIOSGUID  
    [IN]    String MACAddress  
    [IN]    Boolean OverwriteExistingRecord  
    [IN]    String FQDN  
    [IN]    Boolean IsAMTMachine  
    [IN]    String MEBxPassword  
    [IN]    String AdminPassword  
    [IN]    Boolean AddToCollection  
    [IN]    SMS_CollectionRule CollectionRule  
    [IN]    String CollectionId  
    [IN]    String WTGUniqueKey  
    [OUT]   Boolean MachineExists  
    [OUT]   UInt32 ResourceID  
    [OUT]   String SMSUniqueIdentifier  
};  
```  

## Parameters  
 `NetbiosName`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 The NetBIOS name for the computer.  

 `SMBIOSGUID`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 The GUID for the system management BIOS (SMBIOS).  

 `MACAddress`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 The media access controller (MAC) address. The MAC address must be for a network adapter that has a driver in Windows PE. The MAC address must be in colon format. For example, 00:00:00:00:00:00. Other formats prevent the client from receiving policy.  

 `OverwriteExistingRecord`  
 Data type: `Boolean`  

 Qualifiers: [id("3"), in]  

 `true` to overwrite the existing record.  

 `FQDN`  
 Data type: `String`  

 Qualifiers: [id("4"), in, optional]  

 Fully qualified domain name of this computer.  

 `IsAMTMachine`  
 Data type: `Boolean`  

 Qualifiers: [id("5"), in, optional]  

 Enable out of band functionality on this computer.  

 `MEBxPassword`  
 Data type: `String`  

 Qualifiers: [id("6"), in, optional]  

 Management Engine BIOS extension (MEBx) password for the built-in Intel Active Management Technology (Intel AMT) firmware administrative user.  

 `AdminPassword`  
 Data type: `String`  

 Qualifiers: [id("7"), in, optional]  

 The changed password of the MEBx password that can occur during out of band provisioning.  

 `AddToCollection`  
 Data type: `Boolean`  

 Qualifiers: [id("8"), in, optional]  

 `true` to add the computer to a collection.  

 `CollectionRule`  
 Data type: `SMS_CollectionRule`  

 Qualifiers: [id("9"), in, optional]  

 Adds the collection rule to a specified collection. The default value is NULL.  

 `CollectionId`  
 Data type: `String`  

 Qualifiers: [id("10"), in, optional]  

 The collection identifier for the collection which the computer is added to. The default value is empty.  

 `WTGUniqueKey`  
 Data type: `String`  

 Qualifiers: [id("11"), in, optional]  

 For a Windows To Go deployment, this is the USB unique key that will be used to identify the client, instead of the SMBIOS and MAC address.  

 `MachineExists`  
 Data type: `Boolean`  

 Qualifiers: [id("12"), out]  

 `true` if the computer exists.  

 `ResourceID`  
 Data type: `UInt32`  

 Qualifiers: [id("13"), out]  

 Resource identifier for the computer.  

 `SMSUniqueIdentifier`  
 Data type: `String`  

 Qualifiers: [id("14"), out]  

 Unique identifier of Configuration Manager.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
