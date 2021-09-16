---
title: Deployment plans in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about deployment plans in Desktop Analytics.
ms.date: 04/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# About deployment plans in Desktop Analytics

Desktop Analytics collects and analyzes device, application, and driver data in your organization. Based on this analysis and your input, you can use the service to create deployment plans for Windows 10. Deployment plans have the following features:  

- Automatically recommend which devices to include in pilots  

- Identify compatibility issues and suggest mitigations  

- Assess the health of the deployment before, during, and after updates  

- Track the progress of your deployment  

As part of your deployment plan, you do the following actions:  

- Define what versions of Windows 10 you want to deploy  

- Choose what groups of devices to which you want to deploy  

- Create readiness rules for the deployment  

- Define the importance of your apps  

- Choose pilot devices based on automatic recommendations  

- Decide how to fix issues with apps based on recommendations from Desktop Analytics  

By default, Desktop Analytics refreshes deployment plan data daily. Any changes you make within a deployment plan, such as assigning importance to an app or choosing a device to include in a pilot, takes up to 24 hours to process. To speed up this process, request an on-demand data refresh. For more information, see [Desktop Analytics FAQ](faq.yml#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal-).  

After connecting Desktop Analytics to Configuration Manager, select your collections in the deployment plans. This integration then lets you deploy Windows to a collection based on the Desktop Analytics data.

Deployment plans support targeting the three most recent Windows 10 versions. Desktop Analytics will add support for a new Windows 10 version within 45 days after it's available. At that time, the service will also drop the oldest version. You won't be able to use any deployment plans that target the oldest version. If you have any ongoing deployment plans that target the oldest supported version in Desktop Analytics, complete the deployment within 45 days after a new windows 10 version is available.

## Readiness rules

The following readiness rules are available in deployment plans:

- Whether your devices automatically receive drivers from Windows Update. If devices receive the driver updates from Windows Update, then any driver issues identified as part of readiness assessment are automatically marked as **Ready**.  

- Low install count threshold for your Windows apps. If an app is installed on a higher percentage of computers than this threshold, the deployment plan marks the app as **Noteworthy**. This tag means you can decide how important the app is to test during the pilot phase.  

## Plan assets

<!-- 4670224 -->

While the [Assets](about-assets.md) area also shows devices and apps, the **Plan assets** area under a specific deployment plan includes additional information.

### Devices

See the **Windows upgrade decision** for each device in the deployment plan.

The Windows upgrade decision to **Replace device** can be because of one of the following reasons:

- It failed a Windows 10 required processor check. For more information, see [Minimum hardware requirements](/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- It has a BIOS block
- It doesn't have enough memory
- A boot critical component on the system has a blocked driver
- The specific make and model can't upgrade
- There's a display-class component with a driver block that has all of the following attributes:
  - You don't override
  - There's no driver in the new OS version
  - It's not already on Windows Update
- There's another plug-and-play component on the system that blocks upgrade
- There's a wireless component that uses an XP-emulated driver
- A network component with an active connection will lose its driver. In other words, after upgrade it could lose network connectivity.

The Windows upgrade decision to **Re-install** indicates the upgrade will require a reinstall as opposed to an in-place upgrade.

A **Blocked** Windows upgrade decision can be caused by the following reasons:

- You set the upgrade decision of one or more assets to **Unable**.

- The inventory data for that device is incomplete and Desktop Analytics can't do a full compatibility assessment.

### Apps

Set the **Upgrade decision** and the **Importance** for this app in this deployment plan. For more information, see [How to create deployment plans](create-deployment-plans.md).

In the details of the app, you can also see the following information: Recommendations, Compatibility risk factors, and Microsoft known issues. Use this information to help set the **Upgrade decision**. For more information, see [Compatibility assessment](compat-assessment.md).

The apps that Desktop Analytics shows as *noteworthy* are based on the low install count threshold for the readiness rules of the deployment plan. For more information, see [Readiness rules](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > For more information about the "Not important" app category, see [Automatic upgrade decision of system and store apps](about-assets.md#automatic-upgrade-decision-of-system-and-store-apps). <!-- 3587232 -->

The **App versions details** setting is off by default, so this tab combines all versions of apps with the same name and publisher.<!-- 5542186 --> The default behavior helps reduce the total number of apps that you see, which helps reduce your efforts to annotate the apps. The count of apps in the **Noteworthy Apps** tile also reflects this setting. For example, instead of listing hundreds of instances of Microsoft Edge, there's one instance for all versions. You can make decisions once for all versions. If you need to make decisions about specific versions of an app, turn on this setting. You can also configure this setting when working at the global assets level. For more information, see [About assets - Apps](about-assets.md#apps).

When the **App versions details** setting is off, the app details pane shows the number of app versions and languages that it combines. If you save any changes to the app details, it applies to all versions. For example, set the **Upgrade Decision** or **Importance**. Some values will display "Multiple", which means there's not one consistent value across all versions. The service still makes compatibility risk assessments for each version. Turn on **App versions details** to see the compatibility risk assessment for a specific app version.

### Drivers

See the list of drivers included with this deployment plan. Set the **Upgrade decision**, review Microsoft's recommendation, and see compatibility risk factors.

## Importance

As part of the deployment plan, set the *importance* of the apps. Desktop Analytics detects these apps as installed on the target devices. This setting helps Desktop Analytics determine which devices it includes in the pilot phase of the deployment.

If an app is installed on less than 2% of the targeted devices, it's marked **Low install count**. Two percent is the default value. You can adjust the threshold in the readiness settings from 0% to 10%. Desktop Analytics automatically marks these apps as **Ready to upgrade**.  

For apps, choose an importance of **Critical**, **Important**, or **Not important**. If you mark one as critical or important, Desktop Analytics includes in the pilot deployment some devices with that app. The service includes in the pilot more instances of a critical app. If you mark an app as not important, Desktop Analytics automatically sets it to **Ready to upgrade**.

## Pilot devices

Desktop Analytics combines your importance information with the global pilot settings. It then creates a recommendation for which devices should be part of the pilot deployment. The recommended pilot deployment includes devices with different hardware configurations and one or more instances of all the critical and important apps. If an app is marked critical, the service recommends more devices with that app in the pilot.

## Deployment plans in Configuration Manager

After creating a deployment plan, use Configuration Manager to deploy the products. Once the deployment starts, Desktop Analytics monitors the deployment based on the settings in the plan.

## Next steps

- [Learn about Desktop Analytics assets](about-assets.md): devices, drivers, and apps

- [Learn about feature updates](about-updates.md)

- [Create a deployment plan](create-deployment-plans.md)
