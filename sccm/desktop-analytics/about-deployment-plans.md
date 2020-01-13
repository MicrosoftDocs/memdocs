---
title: Deployment plans in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about deployment plans in Desktop Analytics.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

By default, Desktop Analytics refreshes deployment plan data daily. Any changes you make within a deployment plan, such as assigning importance to an app or choosing a device to include in a pilot, takes up to 24 hours to process. To speed up this process, request an on-demand data refresh. For more information, see [Desktop Analytics FAQ](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

After connecting Desktop Analytics to Configuration Manager, select your collections in the deployment plans. This integration then lets you deploy Windows to a collection based on the Desktop Analytics data.



## Readiness rules

The following readiness rules are available in deployment plans:

- Whether your devices automatically receive drivers from Windows Update. If devices receive the driver updates from Windows Update, then any driver issues identified as part of readiness assessment are automatically marked as **Ready**.  

- Low install count threshold for your Windows apps. If an app is installed on a higher percentage of computers than this threshold, the deployment plan marks the app as **Noteworthy**. This tag means you can decide how important the app is to test during the pilot phase.  


## Plan assets

<!-- 4670224 -->

While the [Assets](/sccm/desktop-analytics/about-assets) area also shows devices and apps, the **Plan assets** area under a specific deployment plan includes additional information.

### Devices

See the **Windows upgrade decision** for each device in the deployment plan.

The Windows upgrade decision to **Replace device** can be because of one of the following reasons:

- It failed a Windows 10 required processor check. For more information, see [Minimum hardware requirements](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
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

- The inventory data for that device is incomplete and Desktop Analytics can't perform a full compatibility assestment.

### Apps

Set the **Upgrade decision** and the **Importance** for this app in this deployment plan. For more information, see [How to create deployment plans](/sccm/desktop-analytics/create-deployment-plans).

In the details of the app, you can also see the following information: Recommendations, Compatibility risk factors, and Microsoft known issues. Use this information to help set the **Upgrade decision**. For more information, see [Compatibility assessment](/sccm/desktop-analytics/compat-assessment).

The apps that Desktop Analytics shows as *noteworthy* are based on the low install count threshold for the readiness rules of the deployment plan. For more information, see [Readiness rules](/sccm/desktop-analytics/create-deployment-plans#readiness-rules).

   > [!Tip]
   > For more information about the "Not important" app category, see [Automatic upgrade decision of system and store apps](/sccm/desktop-analytics/about-assets#bkmk_plan-autoapp). <!-- 3587232 -->


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

- [Learn about Desktop Analytics assets](/sccm/desktop-analytics/about-assets): devices, drivers, and apps  

- [Learn about security and feature updates](/sccm/desktop-analytics/about-updates)  

- [Create a deployment plan](/sccm/desktop-analytics/create-deployment-plans)  
