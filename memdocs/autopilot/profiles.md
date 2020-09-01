---
title: Configure Autopilot profiles
description: Learn how to configure device profiles for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
---


# Configure Autopilot profiles

**Applies to**

-  Windows 10

For each device that's been defined to the Windows Autopilot deployment service, a settings profile must be applied that specifies the device's exact deployment behavior. For detailed procedures on how to configure profile settings and register devices, see [Registering devices](add-devices.md#registering-devices).

## Profile settings

The following profile settings are available:

-  **Skip Cortana, OneDrive, and OEM registration setup pages**. All devices registered with Autopilot will automatically skip these pages during the out-of-box experience (OOBE) process.

-  **Automatically set up for work or school**. All devices registered with Autopilot are automatically considered work or school devices, so this question won't appear during the OOBE process.

-  **Sign in experience with company branding**. Instead of presenting a generic Azure AD sign-in page, all Autopilot-registered devices will present a customized sign-in page. This page shows the organization’s name, logo, and additional help text, as configured in Azure AD. See [Add company branding to your directory](/azure/active-directory/customize-branding#add-company-branding-to-your-directory) to customize these settings.

-  **Skip privacy settings**. This optional Autopilot profile setting enables organizations to not ask about privacy settings during the OOBE process. This setting is typically desirable so that the organization can configure these settings via Intune or other management tool.

-  **Disable local admin account creation on the device**. Organizations can decide whether the user setting up the device should have administrator access once the process is complete.

-  **Skip End User License Agreement (EULA)**. In Windows 10 version 1709 and later, organizations can decide to skip the EULA page presented during the OOBE process. Skipping the EULA page means that organizations accept the EULA terms for their users.

-  **Disable Windows consumer features**. In Windows 10 version 1803 and later, organizations can disable Windows consumer features. If so disabled, the device doesn't automatically install any additional Microsoft Store apps when the user first signs into the device. For more information, see the [MDM documentation](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## Related topics

[Profile download](troubleshooting.md#profile-download)<br>
[Registering devices](add-devices.md)