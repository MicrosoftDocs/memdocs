---
# required metadata

title: Use Update Compliance reports for Windows Updates in Microsoft Intune
titleSuffix: Microsoft Intune
description: Use OMS Update Compliance to view report data for Windows Updates you deploy with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Intune compliance reports for updates

When you use Intune to deploy Windows update to Windows 10 devices, view details about update compliance by using Intune or a free solution called *Update Compliance*. Update Compliance is part of the Microsoft Operations Management Suite (OMS).

## Use Intune

To review a policy report on the deployment status for the Windows 10 update rings that you've configured:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Overview** > **Software update status**. You can see general information about the status of any update rings you assigned.

3. To view additional details, select **Monitor**. Then below **Software updates**, select **Per update ring deployment state** and choose the deployment ring to review.

   In the **Monitor** section, choose from the following reports to view more detailed information about the update ring:

   - **Device status**- This will show the device configuration status, for details see [Update deviceConfigurationDeviceStatus]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **User status**- This will show the user name, status, and last report date, for details see [List deviceConfigurationUserStatuses](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **End-user update status**- This will show the Windows device update state, for details see [windowsUpdateState](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## Use Update Compliance

You can monitor Windows 10 update rollouts by using [Update Compliance](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor). Update Compliance is offered through the Azure portal and is available free for devices that meet its [prerequisites](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites).  

When you use this solution, you deploy a commercial ID to any of your Intune managed Windows 10 devices for which you want to report update compliance.  

In Intune, you use the OMA-URI settings of a custom policy to configure the commercial ID. See [Use custom settings for Windows 10 devices in Intune](../configuration/custom-settings-windows-10.md).

The OMA-URI (case sensitive) path for configuring the commercial ID is: *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*

For example, you can use the following values in **Add or edit OMA-URI Setting**:

- **Setting Name**: Windows Analytics Commercial ID
- **Setting Description**: Configuring commercial ID for Windows Analytics solutions
- **OMA-URI** (case sensitive): *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*
- **Data Type**: String
- **Value**: \<Use the GUID shown on the Windows Telemetry tab in your OMS workspace>

> [!NOTE]
> For more information about MS DM Server, see [DMClient configuration service provider (CSP)]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).

## Next steps

[Manage software updates in Intune](windows-update-for-business-configure.md)
