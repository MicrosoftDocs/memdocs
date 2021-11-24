---
title: SMS_TaskSequence_NetworkAdapterSettings class
titleSuffix: Configuration Manager
description: Details of the SMS_TaskSequence_NetworkAdapterSettings server WMI class
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7283c9dc-4098-4bce-9c72-56a30f263c58
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_NetworkAdapterSettings server WMI class

The `SMS_TaskSequence_NetworkAdapterSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies the settings to apply to a physical network adapter.  

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_NetworkAdapterSettings  
{  
      String DNSServerList[];  
      Boolean EnableDHCP;  
      Boolean EnableDNSRegistration;  
      Boolean EnableFullDNSRegistration;  
      Boolean EnableIPProtocolFiltering;  
      Boolean EnableLMHOSTS;  
      Boolean EnableTCPFiltering;  
      Boolean EnableUDPFiltering;  
      Boolean EnableWINS;  
      UInt32 GatewayCostMetric;  
      String Gateways[];  
      UInt32 Index;  
      String IPAddressList[];  
      String IPProtocolFilterList[];  
      String MACAddress;  
      String Name;  
      String SubnetMask[];  
      SInt32 TCPFilterPortList[];  
      UInt32 TcpipNetbiosOptions;  
      SInt32 UDPFilterPortList[];  
      String WINSServerList[];  
};  
```  

## Methods  
 The `SMS_TaskSequence_NetworkAdapterSettings` class does not define any methods.  

## Properties  
 `DNSServerList`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of Domain Name System (DNS) servers for the adapter.  

 `EnableDHCP`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to enable Dynamic Host Configuration Protocol (DHCP) for the adapter.  

 `EnableDNSRegistration`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to register the IP address for the adapter in DNS.  

 `EnableFullDNSRegistration`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to register the IP address for the adapter in DNS under the full DNS name for the computer.  

 `EnableIPProtocolFiltering`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to enable IP protocol filtering on the adapter.  

 `EnableLMHOSTS`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to use local lookup files for Windows Internet Name Service (WINS) resolution.  

 `EnableTCPFiltering`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to enable TCP port filtering for the adapter.  

 `EnableUDPFiltering`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to enable User Datagram Protocol (UDP) port filtering for the adapter.  

 `EnableWINS`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to use WINS for name resolution.

> [!IMPORTANT]
> WINS is a deprecated service. For more information, see [Windows Internet Name Service (WINS)](/windows-server/networking/technologies/wins/wins-top).

 `GatewayCostMetric`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 List of integer cost metrics. This property is ignored unless `EnableDHCP` is set to `false`.  

 `Gateways`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of IP gateway addresses. This property is ignored unless `EnableDHCP` is set to `false`.  

 `Index`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Index of the network adapter settings in the array of settings. See the `Adapters` property of [SMS_TaskSequence_ApplyNetworkSettingsAction Server WMI Class](../../../develop/reference/osd/sms_tasksequence_applynetworksettingsaction-server-wmi-class.md).  

 `IPAddressList`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of IP addresses for the adapter. This property is ignored unless `EnableDHCP` is set to `false`.  

 `IPProtocolFilterList`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of protocols allowed to run over IP. This property is ignored if `EnableIPProtocolFiltering` is set to `false`.  

 `MACAddress`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Media access controller (MAC) address used to match settings to physical network adapter.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 Name of the network connection as it appears in the network connections control panel program. The name is between 0 and 255 characters in length.  

 `SubnetMask`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of subnet masks. This property is ignored unless `EnableDHCP` is set to `false`.  

 `TCPFilterPortList`  
 Data type: `SInt32` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of ports to be granted access permissions for TCP. This property is ignored if `EnableTCPFiltering` is set to `false`.  

 `TcpipNetbiosOptions`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Options for NetBIOS over TCP/IP. Possible values are:  

| Value | NetBIOS options |  
| ----- | --------------- |  
|0|Use NetBIOS settings from DHCP server.|  
|1|Enable NetBIOS over TCP/IP.|  
|2|Disable NetBIOS over TCP/IP.|  

 `UDPFilterPortList`  
 Data type: `SInt32` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of ports to be granted access permissions for UDP. This property is ignored if `EnableUDPFiltering` is set to `false`.  

 `WINSServerList`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of WINS server IP addresses. This property is ignored unless `EnableWINS` is set to `true`.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
