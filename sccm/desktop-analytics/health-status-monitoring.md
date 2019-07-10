---
title: Health status monitoring
titleSuffix: Configuration Manager
description: Learn about how health status monitoring works in Desktop Analytics.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Health status monitoring in Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

As you [deploy an update to production](/sccm/desktop-analytics/deploy-prod), use Desktop Analytics to help monitor the health state of your devices. This article explains in detail how health monitoring works.

For more information on how to use this feature, see [Monitor the health of updated devices](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Screenshot of the Monitor Health page of Desktop Analytics](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics only collects health data from devices that provide usage data it can use as a denominator. This means it doesn't include devices running Windows 7 and Windows 10 that aren't set to share diagnostic data at the Enhanced (Limited) level. If more than 10% of devices running Windows 10 are set to share diagnostic data at levels other than Enhanced (Limited), the **Monitor health** page displays a warning in the banner area.  

To view more information about a specific app, select it in the list.



## Apps

![Health status factors for an app in Desktop Analytics](media/monitor-health-status-factors.png)

Desktop Analytics monitors the following health status factors for apps:

- **% Devices with crashes**: For the last two weeks, the number of devices on which this particular app has crashed divided by the number of devices on which the app has been used. This view lets you see whether the app stability has increased or decreased on the new OS version. Desktop Analytics calculates this percentage for the following sets:  

    - **After update**: Devices that have updated to the target OS version specified in the deployment plan. To reduce the number of assets with insufficient data, Desktop Analytics collects this data for all of your updated devices. This set includes those devices not in the deployment plan.  

    - **Before update**: Devices that are on an OS version earlier than what's specified in the deployment plan. This list doesn't include devices running Windows 7.  

    - **Commercial avg**: The average (avg) crash rate across all commercial devices. This average is calculated across *all* versions of the app. If your version shows a crash rate above the commercial average, there may be a more stable version available.  

- **% Sessions with crashes**: Similar to the preceding, but counts the percentage of sessions with crashes in the last two weeks.  

To determine the health status of an app, Desktop Analytics requires data from at least 20 devices. Otherwise it reports **Insufficient data** for the app. The service calculates the health status based on the *session crash rate* from these devices. The device crash rate is provided for information only. It isn't used in the health status calculation.

At the bottom of the app details page, the following three tabs can help you troubleshoot:

- **Other versions**: A list of alternative versions of this app. For each version, it shows the relative changes to the crash rates within your organization and the commercial average. If you find a later version of the app with a lower crash rate, updating the app may help.  

    It also shows if the version has a **Ready for Windows** signal. For more information, see [Compatibility assessment](compat-assessment.md#driver-risk-assessment).  

- **Top issues**: A list of the most frequent failure IDs by instance count. A failure ID identifies the stack trace associated with the crash. You can use this ID when you call the app vendor for support.  

- **Recent crashes**:  A list of devices on which the app recently crashed. You can filter by failure ID and other criteria. Use this information to troubleshoot the issue by gathering logs or trying fixes on specific devices before trying a broader deployment.  

If you find a serious health regression that you're unable to fix, change the app's **Upgrade decision** to **Unable**. This action prevents future deployment of the update to devices with this asset.


## See also

- [Compatibility assessment in Desktop Analytics](/sccm/desktop-analytics/compat-assessment)  

- [How to deploy to production with Desktop Analytics](/sccm/desktop-analytics/deploy-prod)  
