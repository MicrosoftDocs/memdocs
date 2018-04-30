---
title: "SMS_AMTMachineInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ca6b551f-e376-4c75-a1c6-1139e86794a8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AMTMachineInfo Server WMI Class
The `SMS_AMTMachineInfo` Windows Management Instrumentation (WMI) class, in System Center Configuration Manager, represents known information about a computer that supports Intel Active Management Technology (Intel AMT).  

> [!IMPORTANT]
>  This class is deprecated.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AMTMachineInfo : SMS_BaseClass   
{   
      string Addn;   
      string AdminPassword;   
      string AdminUserName;   
      boolean EnableKerberos;   
      string FQDN;   
      string HostName;   
      string IP;   
      uint32 MachineID;   
      uint32 ProvisionOpType;   
      datetime ProvisionTime;   
      uint32 TlsMode;   
};  
```  

## Methods  
 The `SMS_AMTMachineInfo` class does not define any methods.  

## Properties  
 `Addn`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Active Directory Distinguished Name (ADDN) of the computer account that is created by System Center Configuration Manager for this AMT computer. The value is determined with the Active Directory (AD) container settings in the site control file.  

 `AdminPassword`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The encrypted password of the built-in administration account of the AMT firmware.  

 `AdminUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the built-in administration account of the AMT firmware.  

 `EnableKerberos`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` when the computer is Kerberos-enabled.  

 `FQDN`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The fully qualified domain name (FQDN) of the AMT firmware. This should be synchronized with the host computer’s FQDN value.  

 `HostName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The computer name known to the AMT firmware. This should be synchronized with the name of the host computer.  

 `IP`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The IP address known to the AMT firmware. This should be synchronized with the host computer’s IP address.  

 `MachineID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: key  

 Identifier value that is mapped to the `SMS_R_System` class property `ResourceId`.  

 `ProvisionOpType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: enumeration("Unprovision(1),PartialUnprovision(2),Provision(3),UnprovisionS(4),PartialUnprovisionS(5)")  

 Provisioning operation type. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|1|Unprovision|  
|2|Partial Unprovision|  
|3|Provision|  
|4|Unprovision, suppressing future automatic provision.|  
|5|Partial unprovision, suppressing future automatic provision.|  

 `ProvisionTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 The latest provision date of the AMT Machine  

 `TlsMode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: enumeration("NoAuth(0), Tls(1), MutualAuth(2)")  

 The TLS Mode of the host computer. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|No Authorization|  
|1|Server-side Authorization|  
|2|Mutual Authorization|  

## Remarks  
 Class qualifiers for this class include:  

-   Description("The class contains the AMT computer related properties.")  

-   DisplayName("AMT Machine Properties")  

-   Dynamic  

-   Provider("ExtnProv")  

-   Read  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Collections](../../../develop/core/clients/collections/collections.md)   
 [Configuration Manager Supporting Classes](../../../develop/reference/misc/supporting-server-wmi-classes.md)   
 [AMTOperateForCollection Method in Class SMS_Collection](../../../develop/reference/core/clients/collections/amtoperateforcollection-method-in-class-sms_collection.md)   
 [AMTOperateForMachines Method in Class SMS_Collection](../../../develop/reference/core/clients/collections/amtoperateformachines-method-in-class-sms_collection.md)
