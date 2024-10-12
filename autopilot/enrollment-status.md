---
title: Windows Autopilot Enrollment Status Page
description: Gives an overview of the Enrollment Status Page capabilities, configuration.
ms.subservice: autopilot
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---


# Windows Autopilot Enrollment Status Page

When a user signs into a device for the first time, the Enrollment Status Page (ESP) displays the device's configuration progress. The ESP also makes sure the device is in the expected state before the user can access the desktop for the first time.

The ESP tracks the installation of applications, security policies, certificates, and network connections.

## ESP profiles

An administrator can deploy ESP profiles to a licensed Intune user and configure specific settings within the ESP profile. A few of these settings include:

- Force the installation of specified applications.
- Allow users to collect troubleshooting logs.
- Specify what a user can do if device setup fails.

For more information, see [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status).

:::image type="content" source="images/enrollment-status-page.png" alt-text="Screenshot that shows Enrollment Status Page":::

## Related content

- [FirstSyncStatus details in the DMClient CSP](/windows/client-management/mdm/dmclient-csp#deviceproviderprovideridfirstsyncstatus).
- [Support Tip: Office C2R installation is now tracked during ESP](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-office-c2r-installation-is-now-tracked-during-esp/ba-p/295514).
