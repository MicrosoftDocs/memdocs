---
# required metadata
title: Connected Frontline Cloud PCs report for Windows 365
titleSuffix:
description: Learn about the Connected Frontline Cloud PCs report in for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/04/2024
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

# Connected Frontline Cloud PCs report (preview)

This report helps you:

- Understand the number of concurrent connections for each Cloud PC size.
- Make sure you have purchased the right number of licenses for your peak usage.

By reviewing the maximum concurrent connections, you can decide if you need to purchase more licenses to ensure your end users aren't blocked from using their Frontline Cloud PCs.

The Connected Frontline Cloud PCs report is in [public preview](..\public-preview.md).

## Requirements

The following permissions are required to view this report:

- SharedUseLicenseUsageReport
- SharedUseServicePlans

To assign these permissions, go to **Tenant administration** > **Roles** > **Create** > **Windows 365 role**.

## Use the Connected Frontline Cloud PCs report

To get to the **Connected Frontline Cloud PCs** report, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Cloud PC performance (preview)** > **View report** (under **Connected Frontline Cloud PCs**) > select a Cloud PC size.

:::image type="content" source="./media/report-connected-frontline-cloud-pcs/view-report.png" alt-text="Screenshot of getting to the Cloud PC utilization report." lightbox="./media/report-connected-frontline-cloud-pcs/view-report.png":::

## Report data

The report shows the following data aggregated for the last 28 days:

- **Current connections**: Number of currently connected Frontline Cloud PCs.
- **Most concurrent connections**: Highest number of connected Frontline Cloud PCs for the filtered range:
    - Daily for past 7 or 28 days.
    - Hourly for the past one, three, or seven days.
- **Limit**: Maximum concurrency limit, which is equal to the number of licenses purchased.
- **Reached concurrency limit**: Warnings for approaching and reaching the maximum concurrency limit.

This report is specific to Windows 365 Frontline and doesn't apply to other Windows 365 plans. If no Windows 365 Frontline licenses have been purchased on your tenant, no data is in the report.

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
