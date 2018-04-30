---
title: "AMTOperateForMachines Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2331c06d-65d8-4f20-961b-562afc88fc6b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# AMTOperateForMachines Method in Class SMS_Collection
The `AMTOperateForMachines` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, executes an Intel Active Management (AMT) operation on a set of computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AMTOperateForMachines(      
     UInt32 CollectionID,  
     UInt32 ResourceIDs[],  
     UInt32 Opcode,  
     UInt32 extData  
);  
```  

#### Parameters  
 `CollectionID`  
 Data type: `String`  

 Qualifiers: [in]  

 Unique auto-generated ID containing eight characters. The default value is "".  

 The format of the collection ID is the site code that created the collection followed by a five-digit hexadecimal serial number, for example, "JAX0002C". The default Configuration Manager collections, created during the installation, use the "SMS" prefix, for example, "SMS00001".  

 `ResourceIDs[]`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Array of `SMS_R_System.ResourceID` values. The items in the array represent the computers that the AMT operation is executed on.  

 `Opcode`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The AMT operation to execute. The following table provides the list of supported actions:  

|Value|Description|  
|-----------|-----------------|  
|1|WakeUp: Brings a sleeping computer back into the powered-on state.|  
|2|Restart: Causes a hard reset of the computer, and the computer is then powered on. This does not shut the operating system down.|  
|3|Shutdown: Causes a hard reset of the computer. This does not shut the operating system down.|  
|8|DiscoveryBMC: Detects the AMT capability from an Out of Band service point. This populates the AMTStatus and AMTFullVersion properties of the corresponding SMS_R_System record.|  
|16|ReinventoryBMC: Currently unimplemented.|  
|32|PartialUnprovision: Resets the AMT device for the computer to the factory default settings, except for the following types of properties:<br /><br /> -   Keys, passwords, and user names<br />-   The current host name<br />-   Provisioning server IP and port, FQDN, and DNS suffix<br />-   Domain name<br />-   Customized hashes|  
|64|FullUnprovision: Resets the AMT device of the computer to the factory default settings.|  
|128|Provision: Currently unimplemented.|  
|256|ReProvision: Provision the computer for AMT operation. If the current System Center Configuration Manager infrastructure is configured correctly, this happens automatically. See [How to Provision Computers for AMT](http://go.microsoft.com/fwlink/?LinkId=127174) for more details.|  
|544|FullUnprovisionSuppressAuto: The same as 64 FullUnprovision, except this also sets the SuppressAutoProvision flag, which prevents automatic provisioning from taking place when the computer is in an `SMS_Collection` with the Enable Auto Provision setting set to `true`.|  
|576|PartialUnprovisionSuppressAuto: The same as 32 PartialUnprovision, except this will also set the SuppressAutoProvision flag which, prevents any automatic provisioning from taking place when the computer is in an SMS_Collection with the Enable Auto Provision setting set to `true`.|  
|1024|ClearSuppressAutoProvision:|  
|2048|EnableAudit: Enable audit logging.|  
|4096|DisableAudit: Disable audit logging.|  
|8192|ClearAuditLog: Clear audit log entries.|  

 `extData`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Use 0 for this value.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
