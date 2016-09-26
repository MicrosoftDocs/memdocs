---
title: "Capabilities in Technical Preview 1609 for System Center Configuration Manager"
description: "This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1609."
ms.custom: na
ms.date: 08/25/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
caps.latest.revision: 2
author: Brenduns
---
# Capabilities in Technical Preview 1609 for System Center Configuration Manager


This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1609. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    



**The following are new features you can try out with this version.**  


## Improved monitoring experience for management points
The 1608 Technical Preview introduces a new dashboard that provides an improved monitoring experience for management points in your hierarchy. At a glance, the dashboard provides details about how individual management points are performing. This information can inform you as to when a management point is operating as expected and help you determine when it might be overused or have delays in processing client data that you might want to investigate.

To view the dashboard, in the console go to **Monitoring** > **Management Point Status**.  Then, from the Management Point drop-down, select the management point you want to view.  The dashboard displays details about that management point, including:  
 - **The total number of clients** that are connected to the management point. This number is based on clients that use this management point for client notification. If you have turned off client notification, the number of clients will show as zero.
 - **The amount of CPU** that is in use by the management point on that server . This is based on performance counter data that is automatically collected every 10 minutes.
- **How much memory is available** on the server that hosts the management point. This is based on performance counter data that is automatically collected every 10 minutes.

The dashboard also displays tiles with details about client activity and data submissions. Details like success or failure rates for the following tiles are a historical percentage for that management point and are cumulative from when the management point was installed. (When you update to a new technical preview version, management points automatically reinstall. This resets the date range for these reports):  
 -             **Hardware and Software inventory reports** - The percentage of records the management point received from clients and successfully processed, was unable to process, or that were rejected.
-  **Discovery Data manager** – The percentage of discovery data records from clients the management point has successfully processed.
 - **Get Policy Requests** – The success rate for clients that have requested policy from the management point.
- **Registration Requests** - The success rate for clients that have attempted to register with the site (and hierarchy) by using this management point.
 - **State Message processing** – The percentage of state messages successfully processed by this management point.


## Office 365 servicing dashboard
The Configuration Manager 1608 Technical Preview introduces a new dashboard that allows you to track Office 365 clients, Office 365 client channels, and automatic deployment rules that have Office 365 Client selected in the set of available products. To view the dashboard, in the console go to **Software Library** > **Overview** > **Office 365 Servicing**. At the top of the dashboard, use the **Collection** drop-down setting to filter the dashboard data by members of a specific collection. On the lower-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new ADR or  click **Create Client Agent Settings** to open Client Agent settings.

For more information about Office 365 ProPlus updates, see [Manage Office 365 ProPlus updates with Configuration Manager](../../sum/deploy-use/manage-office-365-proplus-updates.md).






## See Also
[Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md)
