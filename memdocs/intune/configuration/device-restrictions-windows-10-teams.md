---
# required metadata

title: Surface Hub Windows 10 Team device restrictions in Microsoft Intune
description: Add or configure Surface Hub devices settings running Windows 10 Team. Add a wake-up screen, create a maintenance window, use Miracast, and more in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Windows 10 Team settings to allow or restrict features on Surface Hub devices using Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article describes some of the Microsoft Intune device restrictions settings that you can configure for Surface Hub devices running [Windows 10 Team](/surface-hub/differences-between-surface-hub-and-windows-10-enterprise).

## Before you begin

- Create a [Windows 10 Teams device restrictions configuration profile](device-restrictions-configure.md#create-the-profile).

## Apps and experience

These settings use the [SurfaceHub CSP](/windows/client-management/mdm/surfacehub-csp).

- **Wake screen when someone in room**: **Block** prevents the screen from waking automatically when its sensor detects someone in the room. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Meeting information displayed on welcome screen**: Select the information that shows on the Meetings tile of the Welcome screen. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Organizer and time only**: Shows the organizer and time of the meeting.
  - **Organizer, time, and subject (subject hidden for private meetings)**: Shows the organizer, time, and subject of the meeting. The subject is hidden for private meetings.
- **Welcome screen background image URL**: Enter the URL of a `.png` image. On Windows 10 Team devices, this image shows as the background during user sessions, and on the **Welcome** screen. The image must be in PNG format, and the URL must begin with `https://`.
- **Auto-launch Connect**: **Block** prevents the Connect app from automatically opening when a projection is started. If blocked, users can manually launch the Connect app from the Hub's settings. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Sign-in suggestions**: **Block** disables autofilling the sign-in dialog with invitees from scheduled meetings. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **My meetings and files**: **Block** disables the **My meetings and files** feature in the Start menu. This feature shows the signed-in user's meetings and files from Microsoft 365. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Azure operational insights

- **Azure Operational Insights**: **Enable** collects, stores, and analyzes log data from Windows 10 Team devices with Azure Operational Insights. Azure Operational Insights is part of the Microsoft Operations Manager suite. Enter the **Workspace ID** and **Workspace Key** to connect to Azure Operational insights.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not collect this data.

## Maintenance

These settings use the [SurfaceHub CSP](/windows/client-management/mdm/surfacehub-csp).

- **Maintenance window for updates**: **Enable** creates a maintenance window when updates can be installed. Enter the maintenance window **Start time**, and the **Duration in hours**, from 1-5 hours.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

## Session

These settings use the [SurfaceHub CSP](/windows/client-management/mdm/surfacehub-csp).

- **Volume**: Enter the default volume value for a new session, from 0-100. When left blank, Intune doesn't change or update this setting. By default, the OS might set the volume to 45.
- **Screen timeout**: Enter the number of minutes until the Hub screen turns off.
- **Session timeout**: Enter the number of minutes until the session times out.
- **Sleep timeout**: Enter the number of minutes until the Hub enters sleep mode.
- **Session resume**: **Block** prevents users from resuming a session when the session times out. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Wireless projection

These settings use the [SurfaceHub CSP](/windows/client-management/mdm/surfacehub-csp).

- **PIN for wireless projection**: **Require** forces users to enter a PIN before using the wireless projection features on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Miracast wireless projection**: **Block** prevents using Miracast-enabled devices to project. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Miracast wireless projection channel**: Select the Miracast channel that establishes the connection.

## Related articles

- [Create a device restriction configuration profile](device-restrictions-configure.md).

- [Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
