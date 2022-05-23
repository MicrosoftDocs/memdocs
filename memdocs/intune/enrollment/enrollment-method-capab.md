---
# required metadata

title: Intune enrollment method capabilities for Windows devices
titleSuffix: Microsoft Intune
description: Capabilities for each enrollment method for Windows devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/04/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# Intune enrollment method capabilities for Windows devices
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

There are several methods to enroll your workforce's devices in Intune. Each method has different best practices and capabilities, as shown in the tables below.

## Best practices by enrollment method
| **Best practices** | **[Azure AD joined](windows-enroll.md#enable-windows-automatic-enrollment)**|**[Azure AD joined with Autopilot (User driven mode)](../../autopilot/enrollment-autopilot.md)** |**[Azure AD joined with Autopilot (Self deploying mode)](../../autopilot/enrollment-autopilot.md)** |**[Bulk](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#personal-devices)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Co-management](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Commonly used in EDU|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Devices can be used as shared devices|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Personal devices must access company resources|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Self-servicing of apps|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|

## Capabilities by enrollment method

| **Capabilities** | **[Azure AD joined](windows-enroll.md#enable-windows-automatic-enrollment)**|**[Azure AD joined with Autopilot (User driven mode)](../../autopilot/enrollment-autopilot.md)** |**[Azure AD joined with Autopilot (Self deploying mode)](../../autopilot/enrollment-autopilot.md)** |**[Bulk](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#personal-devices)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Co-management](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Conditional Access                                      |![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)\*\*|![Check](./media/enrollment-method-capab/checkmark.png)\*\*|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|User gets associated with the device                    |![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|Requires Azure AD Premium                               |![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|Device can assess resources protected by CA             |![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|Users must not be admins on their devices               |![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Ability to configure the device setup experience        |![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Ability to enroll devices without user interaction      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|Ability to run PowerShell scripts                       |![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)\*| 
|Supports automatic enrollment after AD domain join      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|Supports automatic enrollment after Hybrid Azure AD join|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|
|Supports automatic enrollment after Azure AD join       |![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![Check](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\* Client apps workloads in Configuration Manager must be moved to Intune Pilot or Intune.

\** [Devices are blocked for Conditional Access with the exception of Windows 10 (version 1803 and later) and Windows 11.](device-enrollment-manager-enroll.md)  

## Next steps

[Set up enrollment for Windows](windows-enroll.md)
