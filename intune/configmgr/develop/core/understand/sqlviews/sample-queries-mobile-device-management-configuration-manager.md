---
title: Sample queries for mobile device management
titleSuffix: Configuration Manager
description: Sample queries that show how to join mobile device management views to other views when the device is managed by Configuration Manager.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to


ms.assetid: 03f6d6c0-6ef3-4de9-9ae4-a3ad8142ac57
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for mobile device management in Configuration Manager

The following sample queries demonstrate how to join mobile device management views to other views when the device is managed by Configuration Manager. Mobile device management views will most often be joined to other views by using the **ResourceID** and **DeviceClientID** columns.

## Joining mobile device management hardware inventory and discovery views

The following query retrieves all mobile device Configuration Manager clients, by NetBIOS name, the operating system, the amount of storage space on the device, and the amount of free storage space on the device. The results are sorted by the NetBIOS name. The query joins the **v_GS_DEVICE_COMPUTER_SYSTEM** mobile device management hardware inventory view with the **v_R_System** discovery view by using the **ResourceID** column, and it joins the **v_GS_DEVICE_COMPUTER_SYSTEM** and **v_GS_DEVICE_MEMORY** mobile device management hardware inventory views by using the **ResourceID** column.

```sql
    SELECT v_R_System.Netbios_Name0, 
    ��v_R_System.Operating_System_Name_and0, 
    ��v_GS_DEVICE_MEMORY.Storage0, 
    ��v_GS_DEVICE_MEMORY.StorageFree0 
    FROM v_GS_DEVICE_COMPUTER_SYSTEM INNER JOIN v_R_System ON 
    ��v_GS_DEVICE_COMPUTER_SYSTEM.ResourceID = v_R_System.ResourceID 
    ��INNER JOIN v_GS_DEVICE_MEMORY ON 
    ��v_GS_DEVICE_COMPUTER_SYSTEM.ResourceID = v_GS_DEVICE_MEMORY.ResourceID 
    ORDER BY v_R_System.Netbios_Name0 
```

## Joining mobile device management and status views

The following query retrieves the deployment state for all mobile device Configuration Manager clients, including the state name and description, NetBIOS name for the device, IP address, assigned site code, and deployment date and time. The results are sorted by the deployment state and then the NetBIOS name. The query joins the **v_DeviceClientDeploymentState** mobile device management view with the **v_StateNames** status view by using the **StateID** column. The retrieved information is filtered by the topic type of 800, which includes state messages for client deployment.

```sql
    SELECT v_StateNames.StateName AS [Deployment State], 
    ��v_StateNames.StateDescription AS Description, 
    ��v_DeviceClientDeploymentState.DeviceNetBiosName AS [Device Name], 
    ��v_DeviceClientDeploymentState.IPAddress AS [IP Address], 
    ��v_DeviceClientDeploymentState.AssignedSiteCode AS [Assigned Site], 
    ��v_DeviceClientDeploymentState.DeviceDeploymentTime AS [Time Deployed] 
    FROM v_DeviceClientDeploymentState INNER JOIN v_StateNames ON 
    ��v_DeviceClientDeploymentState.DeviceDeploymentState = v_StateNames.StateID 
    WHERE (v_StateNames.TopicType = 800) 
    ORDER BY [Deployment State], [Device Name] 
```

## See also

[Mobile device management views in Configuration Manager](mobile-device-management-views-configuration-manager.md)
