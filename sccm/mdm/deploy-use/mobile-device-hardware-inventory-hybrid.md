---
title: "Configure hardware inventory | mobile devices"
description: "Configure hardware inventory for mobile devices enrolled by Microsoft Intune and System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: 7
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to configure hardware inventory for mobile devices enrolled by Microsoft Intune and System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

In Configuration Manager, you can collect the hardware inventory on iOS, Android, and Windows devices by using the Microsoft Intune connector. For information about how to configure hardware inventory, see [How to extend hardware inventory in System Center Configuration Manager](../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 For information about how to enroll devices in Microsoft Intune, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

## Hardware inventory for mobile devices  
 The following tables list the inventory classes available for hardware inventory across commonly used mobile platforms.  

 **iOS**  

|Hardware Inventory Class|iOS|  
|------------------------------|---------|  
|Name|Device_ComputerSystem.DeviceName|  
|Unique Device ID|Device_ComputerSystem.UDID|  
|Serial Number|Device_ComputerSystem.SerialNumber|  
|Email Address|Device_Email.OwnerEmailAddress|  
|Operating System Type|Not applicable|  
|Operating System Version|Device_OSInformation.OSVersion|  
|Build Version|Not applicable|  
|Service Pack Major Version|Not applicable|  
|Service Pack Minor Version|Not applicable|  
|Operating System Language|Not applicable|  
|Total Storage Space|Device_Memory.DeviceCapacity|  
|Free Storage Space|Device_Memory.AvailableDeviceCapacity|  
|International Mobile Equipment Identity or IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Mobile Equipment Identifier (MEID)|Device_ComputerSystem.MEID|  
|Manufacturer|Not applicable|  
|Model|ModelName|  
|Phone Number<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Subscriber Carrier|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Cellular Technology|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **NOTE:** Android inventory classes are available when using the Android Company Portal app.  

|Hardware Inventory Class|Android|  
|------------------------------|-------------|  
|Name|Not applicable|  
|Unique Device ID|Not applicable|  
|Serial Number|Device_ComputerSystem.SerialNumber|  
|Email Address|Not applicable|  
|Operating System Type|Device_OSInformation.Platform|  
|Operating System Version|Device_OSInformation.Version|  
|Build Version|Not applicable|  
|Service Pack Major Version|Not applicable|  
|Service Pack Minor Version|Not applicable|  
|Operating System Language|Not applicable|  
|Total Storage Space|Device_Memory.StorageTotal|  
|Free Storage Space|Device_Memory.StorageFree|  
|International Mobile Equipment Identity or IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Mobile Equipment Identifier (MEID)|Not applicable|  
|Manufacturer|Device_Info.Manufacturer|  
|Model|Device_Info.Model|  
|Phone Number<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Subscriber Carrier|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Cellular Technology|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|Hardware Inventory Class|Windows Phone 8 and Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Name|Device_ComputerSystem.DeviceName|  
|Unique Device ID|Device_ComputerSystem.DeviceClientID|  
|Serial Number|Not applicable|  
|Email Address|Device_Email.OwnerEmailAddress|  
|Operating System Type|Device_OSInformation.Platform|  
|Operating System Version|Device_ComputerSystem.SoftwareVersion|  
|Build Version|Not applicable|  
|Service Pack Major Version|Not applicable|  
|Service Pack Minor Version|Not applicable|  
|Operating System Language|Device_OSInformation.Language|  
|Total Storage Space|Not applicable|  
|Free Storage Space|Not applicable|  
|International Mobile Equipment Identity or IMEI (IMEI)|Not applicable|  
|Mobile Equipment Identifier (MEID)|Not applicable|  
|Manufacturer|Device_ComputerSystem.DeviceManufacturer|  
|Model|Device_ComputerSystem.DeviceModel|  
|Phone Number<sup>1</sup>|Not applicable|  
|Subscriber Carrier|Not applicable|  
|Cellular Technology|Not applicable|  
|Wi-Fi MAC|Not applicable|  

 **Windows RT**  

|Hardware Inventory Class|Windows RT|  
|------------------------------|----------------|  
|Name|Device_ComputerSystem.DeviceName|  
|Unique Device ID|Device_ComputerSystem.DeviceName|  
|Serial Number|Not applicable|  
|Email Address|Device_Email.OwnerEmailAddress|  
|Operating System Type|CCM_OperatingSystem .SystemType|  
|Operating System Version|Win32_OperatingSystem.Version|  
|Build Version|Win32_OperatingSystem.BuildNumber|  
|Service Pack Major Version|Win32_OperatingSystem.ServicePackMajorVersion|  
|Service Pack Minor Version|Win32_OperatingSystem.ServicePackMinorVersion|  
|Operating System Language|Not applicable|  
|Total Storage Space|Win32_PhysicalMemory.Capacity|  
|Free Storage Space|Win32_OperatingSystem.FreePhysicalMemory|  
|International Mobile Equipment Identity or IMEI (IMEI)|Not applicable|  
|Mobile Equipment Identifier (MEID)|Not applicable|  
|Manufacturer|Win32_ComputerSystem.Manufacturer|  
|Model|Win32_ComputerSystem.Model|  
|Phone Number<sup>1</sup>|Not applicable|  
|Subscriber Carrier|Not applicable|  
|Cellular Technology|Not applicable|  
|Wi-Fi MAC|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> The phone number is masked with * except for the last 4 digits.  

 For inventory to collect the phone number, the device must have a SIM card inserted, and a phone number provisioned by the carrier to that SIM.  
