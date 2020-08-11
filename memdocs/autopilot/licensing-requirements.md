---
title: Windows Autopilot licensing requirements
ms.reviewer: 
manager: laurawi
description: Inform yourself about licensing requirements for Windows Autopilot deployment.
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


# Windows Autopilot licensing requirements

**Applies to: Windows 10**

Windows Autopilot depends on specific capabilities available in Windows 10 and Azure Active Directory. It also requires an MDM service such as Microsoft Intune. These capabilities can be obtained through various editions and subscription programs:

To provide needed Azure Active Directory (automatic MDM enrollment and company branding features) and MDM functionality, one of the following is required:
- [Microsoft 365 Business Premium subscription](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 or F3 subscription](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 Academic A1, A3, or A5 subscription](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3 or E5 subscription](https://www.microsoft.com/microsoft-365/enterprise), which include all Windows 10, Office 365, and EM+S features (Azure AD and Intune).
- [Enterprise Mobility + Security E3 or E5 subscription](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), which include all needed Azure AD and Intune features.
- [Intune for Education subscription](https://docs.microsoft.com/intune-education/what-is-intune-for-education), which include all needed Azure AD and Intune features.
- [Azure Active Directory Premium P1 or P2](https://azure.microsoft.com/services/active-directory/) and [Microsoft Intune subscription](https://www.microsoft.com/cloud-platform/microsoft-intune) (or an alternative MDM service).

> [!NOTE]
> Even when using Microsoft 365 subscriptions, you still need to [assign Intune licenses to the users](https://docs.microsoft.com/intune/fundamentals/licenses-assign).

Additionally, the following are also recommended (but not required):
- [Microsoft 365 Apps for enterprise](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), which can be deployed easily via Intune (or other MDM services).
- [Windows Subscription Activation](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation), to automatically step up devices from Windows 10 Pro to Windows 10 Enterprise.

## Next steps

[Windows Autopilot configuration requirements](configuration-requirements.md)

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

## Related topics

[Overview of Windows Autopilot](windows-Autopilot.md)
