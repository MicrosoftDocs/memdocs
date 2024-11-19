---
# required metadata
title: Connected Frontline Cloud PCs report for Windows 365
titleSuffix:
description: Learn about the Connected Frontline Cloud PCs report in for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: anushareddy
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;
ms.collection:
- M365-identity-device-management
- tier2
---

<!--Erikje todo: review UI closer to release and update, update caps-->

# Connected Frontline Cloud PCs report (preview)

This report helps you:

- Understand the maximum number of concurrent connections for each Cloud PC license size that you own (maximum concurrency limit).
- See which users are currently connected to their Frontline Cloud PC and see their session length.
- Restart Frontline Cloud PCs to get concurrency below the set threshold.
- Make sure you have purchased the right number of licenses for your peak usage.

The Connected Frontline Cloud PCs report is in [public preview](..\public-preview.md).

## Maximum concurrency limit

The maximum concurrency limit is set by the total number of Frontline licenses that you've purchased. If this limit is reached, subsequent users won't be able to connect to their Cloud PCs.

In such cases, you can do any of the following to unblock users:

- Restart some Cloud PCs to reduce concurrency. You can use the session length information to help identify which Cloud PCs to Restart.
- Redistribute licenses across the Microsoft Entra group assignment.
- Purchase more licenses.

If the total number of connections exceeds the maximum concurrency limit, it means that you're using the concurrency buffer (for Frontline Cloud PCs in dedicated mode only).

## Requirements

The following permissions are required to view this report:

- SharedUseLicenseUsageReport
- SharedUseServicePlans

To assign these permissions, go to **Tenant administration** > **Roles** > **Create** > **Windows 365 role**.

## Use the Connected Frontline Cloud PCs report

To get to the **Connected Frontline Cloud PCs** report, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Cloud PC overview** > **Connected Frontline Cloud PCs** > select a Cloud PC size.

:::image type="content" source="./media/report-connected-frontline-cloud-pcs/view-report.png" alt-text="Screenshot of getting to the Cloud PC utilization report." lightbox="./media/report-connected-frontline-cloud-pcs/view-report.png":::

If you have provisioned Frontline Cloud PCs in shared mode the related assignments are displayed under the selected Cloud PC size.

## Report data

The report shows the following data aggregated for the last 28 days:

- **Current connections**: Number of currently connected Frontline Cloud PCs.
- **Concurrent connection history**: This graph can help you decide if you need to purchase more licenses to increase your concurrency limit.
- **Most concurrent connections**: Highest number of connected Frontline Cloud PCs for the filtered range:
    - Daily for past 7 or 28 days.
    - Hourly for the past one, three, or seven days.
- **Limit**: Maximum concurrency limit, which is equal to the number of licenses purchased.
- **Reached concurrency limit**: Warnings for approaching and reaching the maximum concurrency limit.

To see which users are currently connected, select **Connected**.

This report is specific to Windows 365 Frontline dedicated and shared mode. It doesn't apply to other Windows 365 plans. If you haven't purchased any Windows 365 Frontline licenses for your tenant, no data is displayed in the report.

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
