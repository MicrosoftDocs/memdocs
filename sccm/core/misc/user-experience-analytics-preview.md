---
title: User experience analytics preview
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager technical preview branch version 1912.
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
---

# <a name="bkmk_uea"></a> User experience analytics private preview

> [!Note]  
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

## Overview

It's not uncommon for end users to experience long boot times or other disruptions. These disruptions can be due to a combination of:

- Legacy hardware
- Software configurations that aren't optimized for the end-user experience
- Issues caused by configuration changes and updates

These issues and other end-user experience problems persist because IT doesn't have much visibility into the end-user experience. Generally, the only visibility into these issues come from a slow costly support channel that doesn't usually provide clear information about what needs to be optimized. It's not only IT support bearing the cost of these problems. The time information workers spend dealing with issues is also costly. Performance, reliability, and support issues that reduce user productivity can have a large impact on an organization's bottom line as well.

**User experience analytics** aims to improve user productivity and reduce IT support costs by providing insights into the user experience. The insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing user impact of configuration changes.

This initial release, focuses on three things:

- [**Recommended software**](#bkmk_uea_rs): Recommendations for providing the best user experience
- [**Proactive remediation scripting**](#bkmk_uea_prs): Fix common support issues before end-users notice issues
- [**Start up performance**](#bkmk_uea_bp): Help IT get users from power-on to productivity quickly without lengthy boot and sign in delays

This release is just the beginning. We’ll be rapidly rolling out new insights for other key user-experiences soon after initial release.

## Getting started

This current private preview requires:
- Intune enrolled devices running Windows 10
- Startup performance insights are only available for devices running version 1903 or later of Windows 10.

Configuration Manager devices and Intune enrolled devices on prior versions of Windows 10 aren't currently supported for this private preview.

### Start gathering data

1. Go to `https://devicemanagement.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. Click **Start**. It may take up to 24 hours for startup performance data to populate from your Intune enrolled devices.

### Overview page

Once your data is ready, you'll notice some information on the **Overview** page, explained in more detail below:

- The **User experience score** is a 50/50 weighted average of the **Recommended software** and **Startup performance scores**. We’ll be expanding the set of subscores over time.

- You can compare your current score to other scores by setting a baseline.
  - As described in the [baseline](#bkmk_uea_baselines) section, there's a built-in baseline for *Commercial median* to see how you compare to a typical enterprise. You can create new baselines based on your current metrics so you can track progress or view regressions over time.
   - Baseline markers are shown for your overall score and subscores. If any of the scores have regressed by more than the configurable threshold from the selected baseline, the score is displayed in red and the top-level score is flagged as needing attention.
  - A status of **insufficient data** means you don’t have enough devices reporting to provide a meaningful score. We currently require at least five devices.

- **Filters** will enable you to view your score on a subset of devices or users. However, the filter functionality isn't enabled in this preview.

- **Insights and recommendations** is a prioritized list to improve your score. This list is filtered to the subnode's context when you navigate to **Best practices** or **Recommended software**.

![User experience analytics overview page](media/uea-overview-page.png)

## <a name="bkmk_uea_rs"></a> Recommended software

Certain software is known to improve the end-user experience, independent of lower-level health metrics. For example, Windows 10 has a much higher Net Promoter score than Windows 7. The **Software adoption** score is a number between 0 and 100 that represents a weighted average of the percent of devices that have deployed various recommended software. The current weighting is higher for Office 365 and Windows than for the other metrics since users interact with them more often. The metrics are described below: 

### <a name="bkmk_uea_win10"></a> Windows 10

Windows 10 provides a better user experience than older versions of Windows. This metric measures the percent of devices on Windows 10 versus an older version of Windows.

The recommended remediation action for moving devices from older versions of Windows is to create a deployment plan using [Desktop Analytics](/sccm/desktop-analytics/overview).

### <a name="bkmk_uea_opp"></a> Office 365

Office 365 provides a better user experience and improved collaboration compared to older versions of Office. This metric measures the percent of devices that have Office 365 installed vs an older version.

The recommended remediation action for moving devices from older versions of Office to Office 365 is upgrading it using either [Microsoft Intune](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Deploying-Office-365-ProPlus-with-Microsoft-Intune/ba-p/250292) or [Configuration Manager](https://docs.microsoft.com/deployoffice/deploy-office-365-proplus-with-configuration-manager).

### <a name="bkmk_uea_ap"></a> Autopilot

Autopilot provides a great experience for users to enroll new devices for enterprise management. This metric measures the percent of devices that are registered for Autopilot.

The recommended remediation action is to register existing devices in Autopilot using [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot). Autopilot provides a great user experience for:
- Reprovisioning if the device is ever reset.
- The initial provisioning experience for new devices pre-registered in Autopilot.

### <a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) provides users with single sign-on to the apps and services they need. This metric measures the percent of devices enrolled in Azure AD.

Your Microsoft-Intune managed devices are already enrolled in Azure AD. The recommended remediation action for devices managed by Configuration Manager is to either [enroll them in Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) or [co-manage them](/sccm/comanage/overview). Co-managing devices also improves your cloud management score.

### <a name="bkmk_uea_intune"></a> Cloud management

Microsoft Intune eliminates the need for and performance overhead of Group Policy, resulting in a better end-user experience. This metric measures the percent of PCs enrolled in Microsoft Intune.

The recommended remediation action for devices managed by Configuration Manager that aren't yet enrolled in Intune is to [co-manage them](/sccm/comanage/overview).

### <a name="bkmk_uea_np"></a> No commercial median

The built-in baseline of **Commercial median** doesn't currently have metrics for the subscores listed in the sections above.

## <a name="bkmk_uea_bp"></a> Startup performance




