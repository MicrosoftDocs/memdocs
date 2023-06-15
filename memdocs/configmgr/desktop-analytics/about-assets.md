---
title: Assets in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about devices, drivers, and apps in Desktop Analytics.
ms.date: 12/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# Assets in Desktop Analytics

After devices report data to Desktop Analytics, it provides an inventory of the following assets:

- Devices
- Installed apps  

In the service portal, select **Assets** in the Desktop Analytics menu.

## Devices

The **Devices** tab displays key information about all devices in your organization that you enroll to Desktop Analytics. You can sort on any column or filter for particular values.

> [!NOTE]  
> If the dashboard isn't reporting the number of devices you expect to see for your environment, see [Desktop Analytics troubleshooting](troubleshooting.md).  

In a deployment plan, there's more detail about devices. For more information, see [Plan assets](about-deployment-plans.md#plan-assets)

## Apps

The **Apps** tab shows all installed apps that the service detects on your Windows devices.

**Noteworthy** apps are installed on more than 2% of enrolled devices.

> [!TIP]
> For a specific deployment plan, you can configure this value. In the properties of a deployment plan, in **Readiness rules**, specify the value to **Define a low install count threshold for your apps**.

The **App versions details** setting is off by default, so this tab combines all versions of apps with the same name and publisher.<!-- 5542186 --> The default behavior helps reduce the total number of apps that you see, which helps reduce your efforts to annotate the apps. The count of apps in the **Noteworthy Apps** tile also reflects this setting. For example, instead of listing hundreds of instances of Microsoft Edge, there's one instance for all versions. You can make decisions once for all versions. If you need to make decisions about specific versions of an app, turn on this setting. You can also configure this setting when working with a deployment plan. For more information, see [Plan assets](about-deployment-plans.md#plan-assets).

> [!TIP]
> To enable sort and filter on additional columns in the list, turn on **App versions details**.<!-- MEMDocs#1131 -->

Select the app from the list, and select **Edit**. This action displays details for the app. Select the **Importance** drop-down menu and set a value. You can also assign an **Owner**. If you make any changes, select **Save**.

Configure the **Importance** of apps by setting one of the following categories:

- Critical
- Important
- Ignore
- Not reviewed
- Not important<!-- 3587232 -->

> [!NOTE]
> If you deployed the app with Configuration Manager, Desktop Analytics automatically configures it as **important** by default. This behavior lets you configure the apps in your environment more quickly, to progress faster towards a production deployment.<!-- 4859763 -->

When the **App versions details** setting is off, the app details pane shows the number of app versions and languages that it combines. If you save any changes to the app details, it applies to all versions. For example, set the **Importance** or **Owner**. Some values will display "Multiple", which means there's not one consistent value across all versions.

### Automatic upgrade decision of system and store apps

<!-- 3587232 -->
Identifying **Importance** and **Upgrade Decision** is critical for all noteworthy apps in the Desktop Analytics workflow. To help reduce your efforts in annotating these apps, certain types of apps are automatically marked as *Not important*. The deployment plan upgrade decision for these apps is also marked as *Ready*. The following apps are compatible and should continue to work after you upgrade Windows:

- System apps and components published by Microsoft

- Apps managed and updated from the Microsoft Store

> [!TIP]
> Manage inputs for any app at a global level or per deployment plan.
>
> 1. In the Desktop Analytics portal, in the **Manage** menu, select **Assets**. Then select **Apps**.
>
> 2. Use the **Type** and **Category** columns to manage these app categories:
>
>    - For store apps, filter **Type** as **Modern**
>    - For system apps, filter **Category** as **Background process** or **Windows component**
>
> To filter on these attributes, first turn on **App versions details**.<!-- MEMDocs#1131 -->

In a deployment plan, you can also set the **Upgrade decision**. For more information, see [Plan assets](about-deployment-plans.md#plan-assets).

### Usage

<!-- 5533890 -->

- **Total installs**: This value is the number of installs of the selected app on all Desktop Analytics-enrolled devices.

- **Install percentage**: This value is the install percentage of the selected app against total Desktop Analytics-enrolled devices.

- **Devices launched this app in the last 30 days**: This value is the count of devices where a user launched the selected app. It only includes devices that reported usage in the past 30 days. This count is across all your devices enrolled with Desktop Analytics running on any version of Windows 10. It's possible that this count can vary for a deployment plan.

## Next steps

- [Learn about Desktop Analytics deployment plans](about-deployment-plans.md)  

- [Learn about feature updates](about-updates.md)  

- [Compatibility assessment in Desktop Analytics](compat-assessment.md)  
