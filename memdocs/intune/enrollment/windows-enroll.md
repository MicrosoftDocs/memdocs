---
# required metadata

title: Enable MDM automatic enrollment for Windows | Microsoft Intune
titleSuffix:
description: Enable Intune automatic enrollment for Windows devices joining or registering with your Azure AD.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/06/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up automatic enrollment for Windows devices  

**Applies to**

- Windows 10
- Windows 11

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Simplify Windows enrollment for you and device users by enabling *automatic enrollment* in Microsoft Intune. This enrollment method enables devices to enroll automatically when they join or register in your Azure Active Directory. 

Automatic enrollment can be used in the following onboarding and provisioning scenarios:

* Bring-your-own-device  
* Bulk enrollment 
* Group Policy
* Windows Autopilot (user driven and self-deploying)
* Co-management  

This article describes how to enable MDM automatic enrollment for personal and corporate-owned devices.   

## Prerequisites

- Requires [Azure AD Premium](/azure/active-directory/active-directory-get-started-premium) or [Premium trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845) for automatic MDM enrollment and custom company branding    
- Microsoft Intune subscription  
- Global Administrator permissions  

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]  

## Support for device users  

The Microsoft Intune user-help docs provide conceptual information, tutorials, and how-to guides for employees and students setting up their devices for work. You can point people directly to the Intune docs, or use these articles as guidance when developing and updating your own device management docs.  

Users on personal devices running Windows 11 or Windows 10 can automatically enroll by adding their work or school account on their device, or by using the Intune Company Portal app. Devices running earlier versions of Windows must enroll using the Intune Company Portal app.

For more information, see [Enroll Windows 10/11 devices](../user-help/enroll-windows-10-device.md).    

### Best practices and troubleshooting   

* Device users must access the Company Portal website through Microsoft Edge to view Windows apps that you've assigned for specific versions of Windows. Other browsers, including Google Chrome, Mozilla Firefox, and Internet Explorer do not support this type of filtering.

* If you do not have Auto-MDM enrollment enabled, but you have Windows 10/11 devices that have been joined to Azure AD, two records will be visible in the Microsoft Endpoint Manager admin center after enrollment. You can stop this by making sure that users with Azure AD joined devices go to **Accounts** > **Access work or school** and **Connect** using the same account.  

## Next steps  

For information about how to integrate and use automatic enrollment when provisioning devices, see:  

* [Tutorial: Use Windows Autopilot to enroll devices in Intune](../enrollment/tutorial-use-autopilot-enroll-devices.md)
* [Enroll a Windows client device automatically using Group Policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)
* [Enable co-management in Configuration Manager](../../configmgr/comanage/how-to-enable.md)  

If you're not using automatic enrollment as part of your enrollment or provisioning solution, we recommend creating a domain name server (DNS) alias (known as a *CNAME* record type) that redirects enrollment requests to Intune servers. For more information, see [Enable auto-discovery of Intune enrollment server](../enrollment/windows-enrollment-create-cname.md).    




