---
# required metadata
title: Alerts in Windows 365
titleSuffix:
description: Learn how view, create, and customize alerts in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 9/26/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: feadebay
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Alerts in Windows 365

The Windows 365 Alerts system notifies you when specific events occur in your Cloud PC environment, like connection, provisioning, or image upload failures. By default, these alerts appear in the Microsoft Intune admin center as pop-up notifications (you can also turn on email notifications). You can customize the built-in alert rules:

- Set conditions and thresholds for triggering alerts.
- Define the severity of alerts.
- Turn each alert rule on or off.
- Configure each alert to notify you in the console and/or by email.

## View alerts

To view the list of recent alerts, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Alerts (preview)**.

![Screenshot of view alerts](./media/alerts/view-alerts.png)

## Customize alert rule

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Alerts (preview)** > **Alert rules**.
    ![Screenshot of view alert rules.](./media/alerts/view-alert-rules.png)

2. Select a rule in the list.
3. On the **System rule** page, make any changes that you want in the **Conditions**, **Settings**, and **Notifications** sections.
    ![Screenshot of system rule.](./media/alerts/system-rule.png)
4. Select **Apply** to save the changes to the rule.

<!-- ########################## -->
## Next steps

For more troubleshooting information, see [Troubleshooting](troubleshooting.md).
