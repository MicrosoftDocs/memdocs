---
title: Work from anywhere (preview) report in Endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: The Work from anywhere (preview) report in Endpoint analytics provides insights to help your end users be productive from anywhere.
ms.date: 06/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2a77cfd2-7fa1-4b00-96b2-ff3baa7f5c77
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
---

# Work from anywhere (preview) report
<!--8668496-->
The ability for employees to work from anywhere productively is essential in today’s world. This report offers insights into how prepared your workforce is to be productive from anywhere. The **Work from anywhere** report is an evolution of the [Recommended software report](recommended-software.md). You may notice changes in your scores because the calculations are different in the **Work from anywhere** report.  From this report, you can review your scores and how they compare to the selected baseline. Learn how to improve your scores by reviewing the insights and recommendations for each of them.  

## <a name="bkmk_score"></a> Work from anywhere score

The **Work from anywhere score** is a number between 0 and 100. The score represents a weighted average of the percent of devices that have deployed the various insights for helping your end users be productive from anywhere. The score is computed for all Intune and Configuration Manager devices that have opted into [Endpoint analytics](overview.md).

The following metrics are weighted and used to compute the **Work from anywhere score**:

- [Windows 10](#bkmk_win10)
- [Cloud management](#bkmk_management)
- [Cloud identity](#bkmk_identity)
- [Cloud provisioning](#bkmk_provisioning)

:::image type="content" source="media/8668496-work-from-anywhere-score.png" alt-text="Screenshot of the Work from anywhere report showing the scores and metrics":::
## <a name="bkmk_win10"></a> Windows 10

Windows 10 provides a better user experience than older versions of Windows. The **Windows 10** metric measures the percent of devices on Windows 10. The recommended remediation actions vary depending on how the devices are managed. For Intune and co-managed devices, use Intune to [move devices to an updated version of Windows](../intune/protect/windows-10-feature-updates.md). For Configuration Manager devices, create a deployment plan using [Desktop Analytics](../configmgr/desktop-analytics/overview.md). Your score is based on if these remediation actions have been completed or not.

For information about the cost savings and benefits enabled by Windows 10, download the [TEI whitepaper](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RWCpaP).

> [!NOTE] 
> Currently, only devices that negatively impact your score are shown in the metric's device list.

:::image type="content" source="media/8668496-windows.png" alt-text="Screenshot of the Windows 10 fly out showing graph and insights":::

## <a name="bkmk_management"></a> Cloud management

Configuration Manager and Intune provide integrated cloud-powered management tools and unique co-management options to provision, deploy, manage, and secure endpoints and applications across an organization. With the power of cloud management, you can achieve several productivity benefits. Your end-users benefit when they can access corporate resources away from the corporate network. Eliminating the need for and performance overhead of Group Policy also results in a better end-user experience.

The **Cloud management** metric measures the percent of PCs that have attached to the Microsoft 365 cloud to unlock additional capabilities. There are multiple recommended actions for co-managed devices and their workloads, CMG, and tenant attached devices. See how [Microsoft is enabling modern management for our employees](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

> [!NOTE] 
> Currently, only devices that negatively impact your score are shown in the metric's device list.

Benefits of each cloud management types:

|[**Cloud management gateway (CMG)**](../configmgr/core/clients/manage/cmg/overview.md)|[**Tenant attach**](../configmgr/tenant-attach/device-sync-actions.md)|[**Co-management**](../configmgr/comanage/overview.md)|[**Intune**](../intune/fundamentals/what-is-intune.md)|
|---|---|---|---|
|No additional on-premises infrastructure investment required| View and take action on all PCs and mobile devices from a single console| Enhance Zero Trust with conditional access </br></br> Simplified PC and driver updating| All the benefits of **cloud management gateway**, **tenant attach**, and **co-management**.|
|Doesn't expose on-premises infrastructure to the internet| Gain insights into PC performance with [Endpoint analytics](overview.md)|Makes device provisioning easier with [Windows Autopilot](../configmgr/comanage/quickstart-autopilot.md)| Reduce in infrastructure with always up-to-date cloud-only infrastructure|
|Cloud virtual machines running the service are fully managed by Azure and require no maintenance| Protect PCs and servers with Microsoft Defender ATP| Gain additional remote actions with Intune </br> </br> Split PC management workloads between cloud and on-premises| |
| Easily set up and configured from the Configuration Manager console | Modernize your directory approach with Azure Active Directory| Consistent end-user experience for managing enrolled devices and installed apps| |

## <a name="bkmk_identity"></a> Cloud identity

Cloud identity provides users with many productivity benefits including device-wide single sign-on to apps and services, Windows Hello sign-in, self-service BitLocker recovery, and corporate data roaming. The **Cloud identity** metric measures the percent of devices enrolled in Azure Active Directory (AD) or hybrid Azure AD. Your Intune and co-managed devices are already enrolled in Azure AD. The recommended remediation action for devices managed by Configuration Manager is to [enroll them in hybrid Azure AD](/azure/active-directory/devices/hybrid-azuread-join-managed-domains).

> [!NOTE] 
> Currently, only devices that negatively impact your score are shown in the metric's device list.

:::image type="content" source="media/8668496-cloud-identity.png" alt-text="Screenshot of the Cloud identity fly out showing insights for the metric":::

## <a name="bkmk_provisioning"></a> Cloud provisioning

Cloud provisioning provides a simpler initial provisioning experience for Windows 10 PCs than the native experience. It reduces the number of screens in the Out Of Box Experience (OOBE) and provides defaults, to ensure the device is correctly provisioning from the factory or on reset. The **Cloud provisioning** metric measures the percentage of Windows 10 Intune devices that are both registered and have a deployment profile created for Autopilot. The recommended remediation actions are to register and create deployment profiles for existing devices in Windows Autopilot using Microsoft [Intune](../autopilot/enrollment-autopilot.md).

> [!NOTE] 
> - Currently, only devices that negatively impact your score are shown in the metric's device list.
> - You can export a device list as a `.csv` file from **Cloud provisioning** and use it to [Manually register devices with Windows Autopilot](../autopilot/add-devices.md#add-devices).

:::image type="content" source="media/8668496-cloud-provisioning.png" alt-text="Screenshot of the cloud provisioning tab showing the device list":::

## <a name="bkmk_np"></a> No commercial median

The built-in baseline of **Commercial median** doesn't currently have metrics for the subscore metrics listed in the sections above.

## Next steps

- View [Startup performance](startup-performance.md)
- Use [Proactive remediations](proactive-remediations.md) to help fix common support issues before end-users notice issues.
