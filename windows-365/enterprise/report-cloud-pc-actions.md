---
# required metadata
title: Cloud PC actions report for Windows 365
titleSuffix:
description: Learn about the Cloud PC actions report in for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/30/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;
ms.collection:
- M365-identity-device-management
- tier2
---

# Cloud PC actions report (preview)

This report shows you the status and completion progress of actions admins have taken on Cloud PCs, for both:

- Single actions on the **Devices** tab.
- Multiple devices using **Bulk device actions** on the **Bulk batches** tab.

 The report shows action statuses for the last 90 days.

The Cloud PC actions report is in [public preview](..\public-preview.md).

## Use the Cloud PC actions report

To get to the **Cloud PC actions** report, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Cloud PC actions (preview)**.

## Devices tab

:::image type="content" source="./media/report-cloud-pc-actions/report.png" alt-text="Screenshot of the Cloud PC actions report." lightbox="./media/report-cloud-pc-actions/report.png":::

The tab shows the following columns:

- **Device name**
- **Primary user UPN**
- **Action**: The following actions are included in the report:
  - Create Snapshot
  - Move Region
  - Place Under Review
  - Power On/Off (W365 Frontline only)
  - Reprovision
  - Resize
  - Restart
  - Restore
  - Troubleshoot
- **Status**: There are four possible statuses for an action:
  - **Succeeded**: The action completed successfully.
  - **Failed**: The action didn't complete. When available, you can select **Retry** to try again.
  - **Pending**: The action is in progress. Don't make changes to the Cloud PC (like removing the license).
  - **Review required**: An admin must take action to complete the action. For example, assigning a target license to a device in **Resize Pending License** state for the **Resize** action.
- **Date initiated**

## Bulk batches tab

When an admin takes an action on multiple Cloud PCs at once using **Bulk device actions**, the actions are combined into a batch.

The tab shows the following columns:

- **Batch name** - An automatically generated name for a batch of devices undergoing a remote action.
- **Action** - Same as **Devices** tab.
- **Completion** - The progress of the action on the batch of devices.
- **Date initiated**

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
