---
title: Move Your Intune Data Warehouse Account Data
description: Understand how to back up your Intune Data Warehouse data when moving your account.
ms.date: 06/09/2025
ms.topic: reference
ms.reviewer: jamiesil
ms.collection:
- M365-identity-device-management
---

# Move Your Intune Data Warehouse Account Data

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

By requesting an account move, you're requesting that your data center is changed to another location. After the move, your Data Warehouse will reset and begin recording data at the new location based on the specified day your move begins. To back up your previous Data Warehouse data, complete the following steps **prior** to your account move. Most Data Warehouse tables retain data for 30 days, so any data gap in these tables will no longer be available 30 days after your account move. To learn more about the retention periods for specific tables, see [Data Warehouse data model](reports-ref-data-model.md).

## Back up your Data Warehouse data

To back up your Data Warehouse data, you must save your Data Warehouse data into a *.csv* file using the  Data Warehouse API:

1. Follow the one-time process in [Get data from the Intune Data Warehouse API with a REST client](reports-proc-data-rest.md) if you’re using the Data Warehouse API for the first time.
2. Download all your data as CSV files by using the PowerShell sample [Access the Intune Data Warehouse with PowerShell](https://github.com/Microsoft/Intune-Data-Warehouse/tree/master/Samples/PowerShell).

## Back up your trend charts from the Microsoft Intune admin center

Some trend charts in your view of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) resets. You can back up these charts by running the following script in **Graph**:  

### Terms & Conditions Acceptance reports
1. In the[Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Terms & Conditions**.
2. For each **Terms & Condition** item that you select, select **Acceptance Report** > **Export**.
3. Save the report locally.

### App Protection reports
1. Select **Apps** -> **Monitor** -> **App protection status** in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. To save each report, select the download icon ( ⤓ ).

### Device Configuration charts
1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Export**.
2. Using Microsoft [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), download the data behind the charts.
    - For deployment status of all device configuration profiles for all devices, see [Device deployment status](https://graph.microsoft.com/beta/reports/deviceConfigurationDeviceActivity/content).

    - For deployment status of all device configuration profiles for all users, see [User deployment status](https://graph.microsoft.com/beta/reports/deviceConfigurationUserActivity/content).

    - For profile deployment status, see [Provide deployment status](https://graph.microsoft.com/beta/deviceManagement/deviceConfigurations?$select=id,displayName,lastModifiedDateTime,deviceStatusOverview&$expand=deviceStatusOverview).

    > [!NOTE]
    > You must have a valid authentication token to access the device configuration and deployment status information.

## Device Enrollment charts
1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Assignment status** > **Export**.
2. Using Microsoft [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), download the data behind the charts.
    - For enrollment status, copy this [enrollment status query](https://graph.microsoft.com/beta/reports/managedDeviceEnrollmentFailureTrends()/content) and paste it into [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
    - For top enrollment failures this week, copy this [enrollment failures query](https://graph.microsoft.com/beta/reports/managedDeviceEnrollmentTopFailures(period=null)/content) and paste it into [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).

    > [!NOTE]
    > You must have a valid authentication token to access the device enrollment data.

## After a Data Warehouse account move

After the Data Warehouse account move, you'll see in Intune that the Data Warehouse was reset. You need to update your Intune Data Warehouse API URL with the new tenant location for data to refresh. See [API URL structure](reports-api-url.md#api-url-structure).

## Data Warehouse move example

Customer X requests an account move to begin on January 6, 2018. In response to the request, the customer receives a link to see documentation detailing steps to take if they wish to back up their previous Data Warehouse. On January 6, 2018, the Data Warehouse and the charts it supports will reset and begin storing data in the new data center.

## Next steps

- Learn [what's new each week in Intune](../fundamentals/whats-new.md). You can also find out about upcoming changes, important notices about the service, and information about past releases.
- Read the [Microsoft Intune Blog](https://techcommunity.microsoft.com/t5/microsoft-intune-blog/bg-p/MicrosoftEndpointManagerBlog).
