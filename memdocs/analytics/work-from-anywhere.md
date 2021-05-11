---
title: Work from anywhere (preview) report in Endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: The Work from anywhere (preview) report in Endpoint analytics provides insights to help your end users be productive from anywhere.
ms.date: 05/14/2020
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

The ability for employees to work from anywhere productively is essential in today’s world. This report offers insights into how prepared your workforce is to be productive from anywhere. The **Work from anywhere** report is an evolution of the [Recommended software report](recommended-software.md). You may notice changes in your scores because the calculations are different in the **Work from anywhere** report.  From this report, you can review your scores and how they compare to the selected baseline. Learn how to improve your scores by reviewing the insights and recommendations for each of them.  

## <a name="bkmk_score"></a> Work from anywhere score

The **Work from anywhere score** is a number between 0 and 100. The score represents a weighted average of the percent of devices that have deployed the various insights for helping your end users be productive from anywhere. The score is computed for all Intune and Configuration Manager devices that have opted into [Endpoint analytics](overview.md).

The following metrics are weighted and used to compute the **Work from anywhere score**:

- [Windows 10](#windows-10)
- [Cloud management](#cloud-management)
- [Cloud identity](#cloud-identity)
- [Cloud provisioning](#cloud-provisioning)

## <a name="bkmk_win10"></a> Windows 10 metric

Windows 10 provides a better user experience than older versions of Windows. The **Windows 10** metric measures the percent of devices on Windows 10. The recommended remediation actions vary depending on how the devices are managed. For Intune and co-managed devices, use Intune to move devices to an updated version of Windows. For Configuration Manager devices, create a deployment plan using [Desktop Analytics](../configmgr/desktop-analytics/overview.md). Your score is based on if these remediation actions have been completed or not.

For information about the cost savings and benefits enabled by Windows 10, download the [TEI whitepaper](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RWCpaP).

## <a name="bkmk_management"></a> Cloud management metric

Configuration Manager and Intune provide integrated cloud-powered management tools and unique co-management options to provision, deploy, manage, and secure endpoints and applications across an organization. With the power of cloud management, you can achieve several productivity benefits. Your end-users benefit when they can access corporate resources away from the corporate network. Eliminating the need for and performance overhead of Group Policy also results in a better end-user experience.

The **Cloud management** metric measures the percent of PCs that have attached to the Microsoft 365 cloud to unlock additional capabilities. There are multiple recommended actions for co-managed devices and their workloads, CMG, and tenant attached devices. See how [Microsoft is enabling modern management for our employees](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

Benefits of each cloud management types:

|**Cloud management gateway (CMG)**|**Tenant attach**|**Co-management**|**Intune**|
|---|---|---|---|
|No additional on-premises infrastructure investment required| View and take action on all PCs and mobile devices from a single console| Enhance Zero Trust with conditional access| All the benefits of **cloud management gateway**, **tenant attach**, and **co-management**.|
|Doesn't expose on-premises infrastructure to the internet| Gain insights into PC performance with [Endpoint analytics](overview.md)|Makes device provisioning easier with [Windows Autopilot](../configmgr/comanage/quickstart-autopilot.md)| Reduce in infrastructure with always up-to-date cloud-only infrastructure|
|Cloud virtual machines running the service are fully managed by Azure and require no maintenance| Protect PCs and servers with Microsoft Defender ATP| Gain additional remote actions with Intune| |
| Easily set up and configured from the Configuration Manager console | Modernize your directory approach with Azure Active Directory| Split PC management workloads between cloud and on-premises| |
| | | Simplified PC and driver | |
| | | Consistent end-user experience for managing enrolled devices and installed apps| |

## <a name="bkmk_identity"></a> Cloud identity metric



## <a name="bkmk_mprovisioning"></a> Cloud provisioning metric
