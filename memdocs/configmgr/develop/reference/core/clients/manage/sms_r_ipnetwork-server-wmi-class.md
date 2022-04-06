---
description: The SMS_R_IPNetwork WMI class is an SMS Provider server class, in Configuration Manager, that is generated dynamically and contains data for resources discovered by the Network Discovery Agent. 
title: "SMS_R_IPNetwork Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 05cbc962-ac74-4b55-b58f-f2ccd4a9fe75
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_R_IPNetwork Server WMI Class
The `SMS_R_IPNetwork` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is generated dynamically at SMS Provider run time and contains discovery data for resources discovered by the Network Discovery Agent.  

 The following syntax is not defined in the Managed Object Format (MOF) code.  

## Syntax  

```  
Class SMS_R_IPNetwork : SMS_Resource  
{  
     String AgentName[];  
     String AgentSite[];  
     DateTime AgentTime[];  
     DateTime CreationDate;  
     String Name;  
     UInt32 ResourceID;  
     UInt32 ResourceType;  
     String SubnetAddress;  
     String SubnetMask;  
     String SubnetName;  
     String SubnetTopology;  
};  
```  

## Methods  
 The `SMS_R_IPNetwork` class does not define any methods.  

## Properties  
 `AgentName`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 Names of agents that discovered the resource.  

 `AgentSite`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 List of sites from which the agent ran.  

 `AgentTime`  
 Data type: **DateTime** Array  

 Access type: Read-only  

 Qualifiers: None  

 List of discovery times.  

 `CreationDate`  
 Data type: **DateTime**  

 Access type: Read-only  

 Qualifiers: None  

 Creation time stamp of the discovered resource.  

 `Name`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Name of the resource. This value might be blank.  

 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md).  

 `ResourceType`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: None  

 Type of resources on the site. Because other types of resources might be added before network discovery is enabled, this property might be set to any value equal to or greater than 6.  

 `SubnetAddress`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 IP network address. This value can contain wildcards.  

 `SubnetMask`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Subnet mask for the subnet number.  

 `SubnetName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Name of the subnet.  

 `SubnetTopology`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Topology of the subnet.  

## Remarks  
 This class is not available on sites where the agent is not enabled. The Network Discovery Agent is not enabled at the time Configuration Manager is installed. You must enable the agent by using the Configuration Manager console or by updating the site control file.  

 Although you can specify an IP network resource type for a collection, you cannot distribute software to its resources.  

 You cannot create or update an instance of this class, but you can delete an instance.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Resource Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md)   
 [About the site control file](../../../../core/understand/about-the-configuration-manager-site-control-file.md)
