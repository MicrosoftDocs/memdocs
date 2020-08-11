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
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: 
- CI 116757
- CSSTroubleshooting
---


# Windows Autopilot configuration requirements

**Applies to: Windows 10**

Before Windows Autopilot can be used, some configuration tasks are required to support the common Autopilot scenarios.  

- Configure Azure Active Directory automatic enrollment.  For Microsoft Intune, see [Enable Windows 10 automatic enrollment](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) for details.  If using a different MDM service, contact the vendor for the specific URLs or configuration needed for those services.
- Configure Azure Active Directory custom branding.  In order to display an organization-specific logon page during the Autopilot process, Azure Active Directory needs to be configured with the images and text that should be displayed.  See [Quickstart: Add company branding to your sign-in page in Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) for more details.  Note that the "square logo" and "sign-in page text" are the key elements for Autopilot, as well as the Azure Active Directory tenant name (configured separately in the Azure AD tenant properties).
- Enable [Windows Subscription Activation](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation) if desired, in order to automatically step up from Windows 10 Pro to Windows 10 Enterprise.

Specific scenarios will then have additional requirements.  Generally, there are two specific tasks:

- Device registration.  Devices need to be added to Windows Autopilot to support most Windows Autopilot scenarios.  See [Adding devices to Windows Autopilot](add-devices.md) for more details.
- Profile configuration.  Once devices have been added to Windows Autopilot, a profile of settings needs to be applied to each device.  See [Configure Autopilot profiles](profiles.md) for details.  Note that Microsoft Intune can automate this profile assignment; see [Create an Autopilot device group](https://docs.microsoft.com/intune/enrollment-Autopilot#create-an-Autopilot-device-group) and [Assign an Autopilot deployment profile to a device group](https://docs.microsoft.com/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group) for more information.

See [Windows Autopilot Scenarios](windows-Autopilot-scenarios.md) for additional details.

For a walkthrough for some of these and related steps, see this video:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


There are no additional hardware requirements to use Windows 10 Autopilot, beyond the [requirements to run Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

## Next steps

[Overview of Windows Autopilot](windows-Autopilot.md)
