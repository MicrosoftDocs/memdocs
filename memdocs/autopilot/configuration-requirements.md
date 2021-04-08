---
title: Windows Autopilot configuration requirements
ms.reviewer: 
manager: laurawi
description: Inform yourself about configuration requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 3/21/2021
ms.collection: M365-modern-desktop
ms.topic: conceptual
ms.custom: 
- CI 116757
- CSSTroubleshooting
---


# Windows Autopilot configuration requirements

**Applies to**

- Windows 10
- Windows Holographic, version 2004 or later

> [!NOTE]
> For more information about using Windows Autopilot to deploy HoloLens 2 devices, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

Before Windows Autopilot can be used, some configuration tasks are required to support the common Autopilot scenarios. 

- Configure Azure Active Directory automatic enrollment. For Microsoft Intune, see [Enable Windows 10 automatic enrollment](/intune/windows-enroll#enable-windows-10-automatic-enrollment) for details. If using a different MDM service, contact the vendor for the specific URLs or configuration needed for those services.
- Configure Azure Active Directory custom branding. To display an organization-specific logon page, you must configure Azure Active Directory with the images and text that you want to be displayed. For more information, see [Quickstart: Add company branding to your sign-in page in Azure AD](/azure/active-directory/fundamentals/customize-branding). Key elements for Autopilot include the "square logo", "sign-in page text", and Azure Active Directory tenant name. The tenant name is configured separately in the Azure AD tenant properties.
- The first logon user needs to have Azure Active Directory join permissions for all deployment scenarios.
- Optional: To automatically step up from Windows 10 Pro to Windows 10 Enterprise, enable [Windows Subscription Activation](/windows/deployment/windows-10-enterprise-subscription-activation).

Specific scenarios will then have additional requirements. Generally, there are two specific tasks:

- Device registration. Devices must be added to Windows Autopilot to support most Windows Autopilot scenarios. For more information, see [Adding devices to Windows Autopilot](add-devices.md).
- Profile configuration. Once devices have been added to Windows Autopilot, a profile of settings needs to be applied to each device. See [Configure Autopilot profiles](profiles.md) for details.  Microsoft Intune can automate this profile assignment. For more information, see [Create an Autopilot device group](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) and [Assign an Autopilot deployment profile to a device group](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group).

For more information, see [Windows Autopilot Scenarios](windows-Autopilot-scenarios.md).

For a walkthrough for some of these and related steps, see this video:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


There are no additional hardware requirements to use Windows 10 Autopilot, beyond the [requirements to run Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

**Next steps**

[Overview of Windows Autopilot](windows-autopilot.md)