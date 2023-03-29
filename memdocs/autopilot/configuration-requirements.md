---
title: Windows Autopilot configuration requirements
description: Inform yourself about configuration requirements for Windows Autopilot deployment.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
ms.custom: 
  - CI 116757
  - CSSTroubleshooting
---

# Windows Autopilot configuration requirements

*Applies to:*

- Windows 11
- Windows 10
- Windows Holographic, version 2004 or later

> [!NOTE]
> For more information about using Windows Autopilot to deploy HoloLens 2 devices, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

Before Windows Autopilot can be used, some configuration tasks are required to support the common Autopilot scenarios.

- Configure Azure Active Directory automatic enrollment. For Microsoft Intune, see [Enable Windows automatic enrollment](../intune/enrollment/windows-enroll.md#enable-windows-automatic-enrollment) for details. If using a different MDM service, contact the vendor for the specific URLs or configuration needed for those services.
- Configure Azure Active Directory custom branding. To display an organization-specific logon page, you must configure Azure Active Directory with the images and text that you want to be displayed. For more information, see [Quickstart: Add company branding to your sign-in page in Azure AD](/azure/active-directory/fundamentals/customize-branding). Key elements for Autopilot include the "square logo", "sign-in page text", and Azure Active Directory tenant name. The tenant name is configured separately in the Azure AD tenant properties.
- The first logon user needs to have Azure Active Directory join permissions for all deployment scenarios, except for Windows Autopilot self-deployment mode as this method works in a userless context.
- Optional: To automatically step up from Windows Pro to Windows Enterprise, enable [Windows Subscription Activation](/windows/deployment/windows-10-enterprise-subscription-activation).

Specific scenarios will then have additional requirements. Generally, there are two specific tasks:

- Device registration. Devices must be added to Windows Autopilot to support most Windows Autopilot scenarios. For more information, see [Adding devices to Windows Autopilot](add-devices.md).
- Profile configuration. Once devices have been added to Windows Autopilot, a profile of settings needs to be applied to each device. See [Configure Autopilot profiles](profiles.md) for details.  Microsoft Intune can automate this profile assignment. For more information, see [Create an Autopilot device group](enrollment-autopilot.md) and [Assign an Autopilot deployment profile to a device group](profiles.md).

For more information, see [Windows Autopilot Scenarios](windows-Autopilot-scenarios.md).

For a walkthrough for some of these and related steps, see this video:

> [!VIDEO https://www.youtube.com/embed/KYVptkpsOqs]

There are no additional hardware requirements to use Autopilot, beyond the requirements to run [Windows 11](https://www.microsoft.com/windows/windows-11-specifications) or [Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

**Next steps**

[Overview of Windows Autopilot](windows-autopilot.md)
