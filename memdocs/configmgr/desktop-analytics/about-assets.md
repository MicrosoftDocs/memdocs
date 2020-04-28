---
title: Assets in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about devices, drivers, and apps in Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

Configure the **Importance** of apps by setting one of the following categories:

- Critical
- Important
- Ignore
- Not reviewed
- Not important<!-- 3587232 -->

Select the app from the list, and select **Edit**. This action displays details for the app. Select the **Importance** drop-down menu and set a value. You can also assign an **Owner**. If you make any changes, select **Save**.

### <a name="bkmk_plan-autoapp" /> Automatic upgrade decision of system and store apps

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

In a deployment plan, you can also set the **Upgrade decision**. For more information, see [Plan assets](about-deployment-plans.md#plan-assets)

### Usage

<!-- 5533890 -->

- **Total installs**: This value is the number of installs of the selected app on all Desktop Analytics-enrolled devices.

- **Install percentage**: This value is the install percentage of the selected app against total Desktop Analytics-enrolled devices.

- **Devices launched this app in the last 30 days**: This value is the count of devices where a user launched the selected app. It only includes devices that reported usage in the past 30 days. This count is across all your devices enrolled with Desktop Analytics running on any version of Windows 10. It's possible that this count can vary for a deployment plan.

## Next steps

- [Learn about Desktop Analytics deployment plans](about-deployment-plans.md)  

- [Learn about security and feature updates](about-updates.md)  

- [Compatibility assessment in Desktop Analytics](compat-assessment.md)  
