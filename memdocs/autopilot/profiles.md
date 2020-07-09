---
title: Configure Autopilot profiles
description: Learn how to configure device profiles while performing a Windows Autopilot deployment.
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

-   Windows 10

For each device that has been defined to the Windows Autopilot deployment service, a profile of settings needs to be applied that specifies the exact behavior of that device when it is deployed. For detailed procedures on how to configure profile settings and register devices, see [Registering devices](add-devices.md#registering-devices).

## Profile settings

The following profile settings are available:

-   **Skip Cortana, OneDrive, and OEM registration setup pages**. All devices registered with Autopilot will automatically skip these pages during the out-of-box experience (OOBE) process.

-   **Automatically set up for work or school**. All devices registered with Autopilot are automatically considered work or school devices, so this question will not appear during the OOBE process.

-   **Sign in experience with company branding**. Instead of presenting a generic Azure Active Directory sign-in page, all devices registered with Autopilot will present a customized sign-in page with the organization’s name, logo, and additional help text, as configured in Azure Active Directory. See [Add company branding to your directory](https://docs.microsoft.com/azure/active-directory/customize-branding#add-company-branding-to-your-directory) to customize these settings.

-   **Skip privacy settings**. This optional Autopilot profile setting enables organizations to not ask about privacy settings during the OOBE process. This is typically desirable so that the organization can configure these settings via Intune or other management tool.

-   **Disable local admin account creation on the device**. Organizations can decide whether the user setting up the device should have administrator access once the process is complete.

-   **Skip End User License Agreement (EULA)**. In Windows 10 version 1709 and later, organizations can decide to skip the EULA page presented during the OOBE process. This means that organizations accept the EULA terms on behalf of their users.

-   **Disable Windows consumer features**. In Windows 10 version 1803 and later, organizations can disable Windows consumer features so that the device does not automatically install any additional Microsoft Store apps when the user first signs into the device. For more information, see the [MDM documentation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## Related topics

[Profile download](troubleshooting.md#profile-download)<br>
[Registering devices](add-devices.md)
