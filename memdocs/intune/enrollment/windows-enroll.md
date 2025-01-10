---
# required metadata

title: Enable MDM automatic enrollment for Windows | Microsoft Intune
titleSuffix:
description: Enable Intune automatic enrollment for Windows devices joining or registering with your Microsoft Entra ID.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/25/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa  
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

Simplify device enrollment by enabling *automatic enrollment* in Microsoft Intune. This enrollment method enables devices to enroll automatically when they join or register in Microsoft Entra ID. Enrollment in Intune occurs when:  

* A Microsoft Entra user adds their work or school account to their personal device.  
* A corporate-owned device joins to your Microsoft Entra ID.  

Automatic enrollment can be used in the following device management and provisioning scenarios:  

* Bring-your-own-device (BYOD), personal devices   
* Bulk enrollment 
* Group Policy
* Windows Autopilot (user driven and self-deploying)
* Co-management with Configuration Manager    

This article describes how to enable automatic mobile device management (MDM) enrollment for personal and corporate-owned devices.   

## Prerequisites
You must have: 
- A [Microsoft Entra ID P1 or P2 subscription](/azure/active-directory/active-directory-get-started-premium) or [Premium trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845) for automatic MDM enrollment and custom company branding.  
- A Microsoft Intune subscription.  
- A Microsoft Entra Global Administrator role. For more information about role-based-access-control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).  

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]  

## Support for device users  

The Microsoft Intune user help docs provide conceptual information, tutorials, and how-to guides for employees and students setting up their devices for work. You can point people directly to the Intune docs, or use these articles as guidance when developing and updating your own device management docs.  

Users on personal devices running Windows 11 or Windows 10 can automatically enroll by adding their work or school account on their device, or by using the Intune Company Portal app. Devices running earlier versions of Windows must enroll using the Intune Company Portal app.  For more information, see [Enroll Windows 10/11 devices](../user-help/enroll-windows-10-device.md).  

You can also let unlicensed admins sign in to the Intune admin center to help with troubleshooting and support. For more information, see [Unlicensed admins](../fundamentals/unlicensed-admins.md).  

## Best practices and troubleshooting   

* Device users must access the Company Portal website through Microsoft Edge to view apps assigned for specific versions of Windows. Other browsers such as Google Chrome, Mozilla Firefox, and Internet Explorer do not support this type of filtering.  

* After enrollment, you'll see two records in the Microsoft Intune admin center if automatic MDM enrollment is disabled and devices are joined to Microsoft Entra ID. To stop the duplicate records, instruct users on joined devices to **Settings** > **Accounts** > **Access work or school**. Then they can **Connect** using the same account.

* Devices that were already Entra ID-joined before Automatic Enrollment was enabled won't automatically enroll. To trigger enrollment on these devices, run **"deviceenroller.exe /c /AutoEnrollMDM"** from an administrative command prompt.

## Next steps  

For information about how to integrate and use automatic enrollment when provisioning devices, see:  

* [Windows Autopilot scenarios](/autopilot/tutorial/autopilot-scenarios)  
* [Enroll a Windows client device automatically using Group Policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)
* [Enable co-management in Configuration Manager](../../configmgr/comanage/how-to-enable.md)  

If you're not using automatic enrollment as part of your enrollment or provisioning solution, we recommend creating a domain name server (DNS) alias (known as a *CNAME* record type) that redirects enrollment requests to Intune servers. For more information, see [Enable automatic discovery of Intune enrollment server](../enrollment/windows-enrollment-create-cname.md).
