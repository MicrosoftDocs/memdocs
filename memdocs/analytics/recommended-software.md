---
title: Recommended software in Endpoint Analytics
titleSuffix: Configuration Manager
description: Get details about recommended software in Endpoint Analytics
ms.date: 06/25/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 5e54bd84-fb5b-4b03-8d49-b355cace9f60
author: mestew
ms.author: mstewart
manager: dougeby

---

# <a name="bkmk_rs"></a> Recommended software

> [!Important]  
> Endpoint Analytics computes the **Software adoption** score for all your Intune and co-managed devices, regardless of whether they've been configured with the [Intune data collection policy](settings.md#bkmk_profile) or not. For Configuration Manager-managed devices, scores are only computed for [enrolled devices](enroll-configmgr.md#bkmk_cm_enroll).

Certain software is known to improve the end-user experience, independent of lower-level health metrics. For example, Windows 10 has a much higher Net Promoter score than Windows 7. The **Software adoption** score is a number between 0 and 100. The score represents a weighted average of the percent of devices that have deployed various recommended software. The current weighting is higher for Windows than for the other metrics since users interact with them more often. The metrics are described below: 

[![Endpoint analytics Recommended software page](media/recommended-software.png)](media/recommended-software.png#lightbox)

## <a name="bkmk_win10"></a> Windows 10

Windows 10 provides a better user experience than older versions of Windows. For more information, see the [TEI whitepaper](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf).

This metric measures the percent of devices on Windows 10 versus an older version of Windows.

The recommended remediation action for moving devices from older versions of Windows is to create a deployment plan using [Desktop Analytics](../configmgr/desktop-analytics/overview.md).

## <a name="bkmk_ap"></a> Autopilot

Microsoft Autopilot provides a simpler initial provisioning experience for Windows 10 PCs than the native experience by reducing the number of screens in the Out Of Box Experience (OOBE) and providing defaults, to ensure the employees device is correctly provisioning from the factory or on reset.

This metric measures the percent of Windows 10 devices that are registered for Autopilot.

The recommended remediation action is to register existing devices in Autopilot using [Microsoft Intune](../intune/enrollment/enrollment-autopilot.md).

## <a name="bkmk_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) provides users with many productivity benefits including device-wide single sign-on to apps and services, Windows Hello sign-in, self-service BitLocker recovery, and corporate data roaming.

This metric measures the percent of devices enrolled in Azure AD.

Your Microsoft-Intune managed devices are already enrolled in Azure AD. The recommended remediation action for devices managed by Configuration Manager is to either [enroll them in Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) or [co-manage them](../configmgr/comanage/overview.md). Co-managing devices also improves your cloud management score.

## <a name="bkmk_intune"></a> Cloud management

Configuration Manager and Intune provide integrated cloud-powered management tools and unique co-management options to provision, deploy, manage, and secure endpoints and applications across an organization. With the power of cloud management, you can achieve several productivity benefits, including enabling access to corporate resources even when they're away from the corporate network, and eliminating the need for and performance overhead of Group Policy, resulting in a better end-user experience.

This metric measures the percent of PCs that have attached to the Microsoft 365 cloud to unlock additional capabilities. See how [Microsoft is enabling modern management for our employees](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

The recommended action for devices managed by Configuration Manager that aren't yet enrolled in Intune is to [co-manage them](../configmgr/comanage/overview.md) to unlock additional cloud-powered capabilities like conditional access.

## <a name="bkmk_np"></a> No commercial median

The built-in baseline of **Commercial median** doesn't currently have metrics for the subscores listed in the sections above.

## Next steps

Use [Proactive remediations](proactive-remediations.md) to help fix common support issues before end-users notice issues.