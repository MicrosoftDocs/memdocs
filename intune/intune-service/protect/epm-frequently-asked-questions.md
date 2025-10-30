---
title: Frequently asked questions for Endpoint Privilege Management
description: A list of frequently asked questions for customers deploying Microsoft Intune Endpoint Privilege Management
author: brenduns
ms.author: brenduns
ms.date: 09/10/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.subservice: suite
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Frequently asked questions for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [intune-epm-overview](includes/intune-epm-overview.md)]

The following sections of this article discuss frequently asked questions for Endpoint Privilege Management (EPM).

## Frequently asked questions

### Why is my virtual device not onboarding to Endpoint Privilege Management?

Currently, Endpoint Privilege Management isn't supported with Azure Virtual Desktop. This issue will be fixed in future release.

Support for Windows 365 was added in September 2023.

### Why is my elevation settings policy showing error/not applicable?

The elevation settings policy controls the enablement of EPM and the configuration of the client side components. When this policy is in error or shows not applicable, it indicates the device had an issue enabling EPM. The two most common reasons are missing the [required Windows updates](../protect/epm-plan.md#requirements) or failure to communicate with required [Intune Endpoints for Endpoint Privilege Management](../fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management).

### What happens when someone with administrative privileges uses a device that is enabled for EPM?

Endpoint Privilege Management doesn't manage elevation requests by users that have administrative permissions on a device. If an administrator launches a file with a matching elevation rule, the application launches as it normally does for the administrator and will be reported as an unmanaged elevation.

### What files can be elevated to administrator?

Endpoint Privilege Management supports executable files with `.exe` `.msi` extensions and `.ps1` PowerShell scripts.

### Why doesn't 'Run with elevated access" show on start menu items?

Certain items that reside in the start menu or taskbar have a curated right-click menu and the EPM right-click context menu isn't able to be added to those menus. We plan to fix this issue in a future release.

### Can I launch multiple files as elevated with the "Run with elevated access" right-click context menu?

Only one file can be elevated at a time. To launch multiple files elevated, right-click each file individually and select *Run with elevated access*.

### What is the difference between Microsoft EPM and Windows Administrator protection?

EPM allows standard users to perform tasks that require elevated privileges without granting them full admin rights. Windows Administrator protection secures admin accounts from token theft.

### Do I need additional licensing for EPM?

Yes, Endpoint Privilege Management requires specific licensing. For more information, see [Intune add-ons](../fundamentals/intune-add-ons.md).

### How does EPM and Windows Defender Application Control (WDAC) differ?

EPM and WDAC compliment each other. EPM allows apps to elevate, while WDAC ensures only approved/blocked apps (elevated or not) can run.
