---
# required metadata
title: Move your Intune Data Warehouse account data  
titleSuffix: Microsoft Intune
description: Understand how to back up your Intune Data Warehouse data when moving your account.
keywords: 
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/18/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: ee3ccbf9-82fc-4fbf-9d3d-8f05e431d090

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier2
- M365-identity-device-management
---

# Move your Intune Data Warehouse account data 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

By requesting an account move, you're requesting that your data center is changed to another location. After the move, your Data Warehouse will reset and begin recording data at the new location based on the specified day your move begins. To back up your previous Data Warehouse data, complete the following steps **prior** to your account move. Most Data Warehouse tables retain data for 30 days, so any data gap in these tables will no longer be available 30 days after your account move. To learn more about the retention periods for specific tables, see [Data Warehouse data model](reports-ref-data-model.md). 

## Back up your Data Warehouse data 

To back up your Data Warehouse data, you must save your Data Warehouse data into a *.csv* file using the  Data Warehouse API:  

1. If you're a first-time user of the Data Warehouse API, follow the one-time process provided in the following article, [Get data from the Intune Data Warehouse API with a REST client](reports-proc-data-rest.md).
2. Use the PowerShell sample titled [Access the Intune Data Warehouse with PowerShell](https://github.com/Microsoft/Intune-Data-Warehouse/tree/master/Samples/PowerShell) to download all your data into CSV files. 

## Back up your trend charts from the Microsoft Intune admin center

Some trend charts in your view of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) resets. You may back up these charts by running the following script in **Graph**:   

### Terms & Conditions Acceptance reports
1. In the[Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Terms & Conditions**.
2. For each **Terms & Condition** item that you select, select **Acceptance Report** > **Export**.
3. Save the report locally.
 
### App Protection reports  
1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** -> **Monitor** -> **App protection status**.
2. Select the download icon ( ⤓ ) to save each report.

### Device Configuration charts 
1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Export**.
2. Using Microsoft [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), download the data behind the charts. 
    - For deployment status of all device configuration profiles for all devices, see [Device deployment status](https://graph.microsoft.com/beta/reports/deviceConfigurationDeviceActivity/content).

    - For deployment status of all device configuration profiles for all users, see [User deployment status](https://graph.microsoft.com/beta/reports/deviceConfigurationUserActivity/content).

    - For profile deployment status, see [Provide deployment status](https://graph.microsoft.com/beta/deviceManagement/deviceConfigurations?$select=id,displayName,lastModifiedDateTime,deviceStatusOverview&$expand=deviceStatusOverview).
 
    > [!NOTE]
    > You must have a valid authenticaltion token to access the device configuration and deployment status information.

## Device Enrollment charts
1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Assignment status** > **Export**.
2. Using Microsoft [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), download the data behind the charts.
    - For enrollment status, copy this [enrollment status query](https://graph.microsoft.com/beta/reports/managedDeviceEnrollmentFailureTrends()/content) and paste it into [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
    - For top enrollment failures this week, copy this [enrollment failures query](https://graph.microsoft.com/beta/reports/managedDeviceEnrollmentTopFailures(period=null)/content) and paste it into [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).

    > [!NOTE]
    > You must have a valid authenticaltion token to access the device enrollment data. 

## After a Data Warehouse account move

After the Data Warehouse account move, you'll see in Intune that the Data Warehouse was reset, and your data is now stored in the new location. The charts and export options reset, and you see a notification, which upon clicking will direct you to an article explaining why the charts have reset.  

## Data Warehouse move example 

Customer X requests an account move to begin on 1/06/2018. In response to the request, the customer receives a link to see documentation detailing steps to take if they wish to back up their previous Data Warehouse. On 1/06/2018, the Data Warehouse and the charts it supports will reset and begin storing data in the new data center. 

## Next steps

- Learn [what's new each week in Intune](../fundamentals/whats-new.md). You can also find out about upcoming changes, important notices about the service, and information about past releases.
- Read the [Microsoft Intune Blog](https://techcommunity.microsoft.com/t5/microsoft-intune-blog/bg-p/MicrosoftEndpointManagerBlog).
