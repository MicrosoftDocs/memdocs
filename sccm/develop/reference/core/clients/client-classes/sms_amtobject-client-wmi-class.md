---
title: "SMS_AMTObject Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e5ffb7f3-970d-4a04-94e4-cc749f028c3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AMTObject Client WMI Class
The `SMS_AMTObject` Windows Management Instrumentation (WMI) class in Configuration Manager contains Intel Active Management technology (Intel AMT) information, which is utilized by the Configuration Manager Hardware Inventory client component for reporting purposes. The information is supplied by the Intel HECI driver component, which is owned by Intel. Most properties in this class are AMT hardware-specific.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class class SMS_AMTObject   
{   
      string AMT;   
      string AMTApps;   
      string BiosVersion;   
      string BuildNumber;   
      uint32 DeviceID;   
      string Flash;   
      string LegacyMode;   
      string Netstack;   
      uint32 ProvisionMode;   
      uint32 ProvisionState;   
      string RecoveryBuildNum;   
      string RecoveryVersion;   
      string Sku;   
      uint32 TLSMode;   
      string VendorID;   
      uint32 ZTCEnabled;   
};  
```  

## Methods  
 The `class SMS_AMTObject` class does not define any methods.  

## Properties  
 `AMT`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Firmware version of the AMT component in XX.YY.ZZZZ format.  

 `AMTApps`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Firmware version of the AMTApps component in XX.YY.ZZZZ format.  

 `BiosVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Version of the AMT bios. There is no version format.  

 `BuildNumber`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Build number of the AMT component in XXXX format.  

 `DeviceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: key, SMS_Report (TRUE)  

 Universally unique identifier (UUID) of the AMT firmware.  

 `Flash`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Firmware version of the AMT flash component in XX.YY.ZZZZ format.  

 `LegacyMode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 A string value that when set to “True��? indicates the Intel AMT component is operating in legacy mode, otherwise, set to “False��?. This only applies when the AMT component is version 2.0 or greater.  

 `Netstack`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Firmware version of the AMT netstack component in XX.YY.ZZZZ format.  

 `ProvisionMode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Specifies the provisioning mode that is currently selected by the AMT device.  

|Value|Description|  
|-----------|-----------------|  
|1|Enterprise provisioning mode|  
|2|Small business provisioning mode|  

 `ProvisionState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Current provisioning state.  

|Value|Description|  
|-----------|-----------------|  
|0|Factory set-up mode|  
|1|Set-up mode|  
|2|Operational mode|  

 `RecoveryBuildNum`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Recovery build number of the AMT component in XXXX format.  

 `RecoveryVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Firmware version of the AMT recovery component in XX.YY.ZZZZ format.  

 `Sku`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Part number of the AMT component.  

 For AMT firmware 2.0, the value of the `Sku` property is a decimal number, and can be one of the following values.  

|Value|Description|  
|-----------|-----------------|  
|0|Active Management Technology (AMT), Alert Standard Format (ASF), and Intel Quiet System Technology (iQST)|  
|1|ASF and Fujitsu Siemens Computers (FSC)|  
|2|FSC|  

 For AMT firmware 2.5, the value of the `Sku` property is a decimal number where the bit values of that number determine the value. The following bit values are defined.  

|Bit|Decimal|Hexadecimal|Description|  
|---------|-------------|-----------------|-----------------|  
|1|2|0x00000002|iQST|  
|2|4|0x00000004|ASF|  
|3|8|0x00000008|Intel AMT Pro|  

 For AMT firmware 5.0, the value of the `Sku` property contains the bit values from AMT firmware 2.5 and the following bit values.  

|Bit|Decimal|Hexadecimal|Description|  
|---------|-------------|-----------------|-----------------|  
|4|16|0x00000010|Intel Standard Manageability|  
|5|32|0x00000020|TPM|  
|7|128|0x00000080|Finger Print Sensor|  

 `TLSMode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Transport Layer Security (TLS) mode of the AMT component. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|No Authorization|  
|1|Transport Layer Security|  
|2|Mutual Authorization|  

 `VendorID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 USB vendor ID.  

 `ZTCEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: SMS_Report (TRUE)  

 Indicates the Zero-Touch Configuration (ZTC) component is enabled or disabled.  

|Value|Description|  
|-----------|-----------------|  
|0|Disabled|  
|1|Enabled|  

## Remarks  
 Class qualifiers for this class include:  

-   dynamic  

-   provider("AMTInvProvider")  

-   SMS_Class_ID ("MICROSOFT&#124;AMT_AGENT&#124;1.0")  

-   SMS_Group_Name ("AMT Agent")  

-   SMS_Namespace (TRUE)  

-   SMS_Report (TRUE)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Supporting Classes](../../../../../develop/reference/misc/supporting-server-wmi-classes.md)   
 [About Configuration Manager Inventory](../../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md)
