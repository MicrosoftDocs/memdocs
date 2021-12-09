---
title: How to create deployment plans
titleSuffix: Configuration Manager
description: A how-to guide for creating deployment plans in Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# How to create deployment plans in Desktop Analytics

This article provides the steps for creating a deployment plan in Desktop Analytics. Before you start, first [learn about deployment plans](about-deployment-plans.md).

## Create a plan for Windows 10

Follow the steps in this section to use Desktop Analytics to create a plan for deploying Windows 10.

1. Open the [Desktop Analytics portal](https://aka.ms/desktopanalytics). Use credentials that have at least **Workspace Contributors** permissions.  

2. Select **Deployment Plans** in the Manage group.  

3. In the **Deployment Plans** pane, select **Create**.  

4. In the **Create deployment plan** pane, configure the following settings:  

    - **Name**: A unique name for the deployment plan  

    - **Products and versions**: Choose which Windows 10 version to deploy. Microsoft recommends creating deployment plans that use the most recent version.  

    - **Device groups**: Select one or more groups from the same hierarchy. These groups are [device collections](connect-configmgr.md#bkmk_Collections) synchronized from Configuration Manager.

        If you connect multiple Configuration Manager hierarchies to the same Desktop Analytics instance, a display name for the hierarchy prefixes the collection name in the global pilot configuration. This name is the **Display Name** property on the Desktop Analytics connection in the Configuration Manager console.<!-- 4814075 -->

        > [!NOTE]
        > Support for multiple hierarchies requires Configuration Manager version 1910 or later.
        >
        > If you select collections for multiple hierarchies, the portal displays a warning. You can't create the deployment plan with collections from multiple hierarchies.<!-- 4814075 -->

    - **Readiness rules**: These rules help to determine which devices qualify for upgrade. For more information, see [Readiness rules](#readiness-rules).  

    - **Completion date**: Choose the date by which Windows should be fully deployed to all the targeted devices.  

5. Select **Create**. The new plan appears in the list of deployment plans while its being processed. To expedite processing, request an on-demand data refresh. For more information, see [Desktop Analytics FAQ](faq.yml#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal-).  

6. Open the deployment plan by selecting its name.  

7. On the deployment plan menu, in the **Prepare** group, select **Identify importance**.  

    1. On the **Apps** tab, select to show only **Not Reviewed** assets.  

    2. Select each app, and then select **Edit**. You can select more than one app to edit at the same time.  

    3. Choose an importance level from the **Importance** list. If you want Desktop Analytics to validate the app during the pilot, select **Critical** or **Important**. It doesn't validate apps marked as **Not Important**. Assess its [compatibility](compat-assessment.md) and other plan insights when assigning importance levels.  

        When assigning importance levels, you can also choose the Upgrade decision.  

    4. Select **Save** when complete.  

8. On the deployment plan menu, in the **Prepare** group, select **Identify pilot**.  

    1. Review the recommended devices for the pilot.  

    2. Select each device, and select **Add to Pilot**. If you disagree with the recommendation, select **Replace**.  

        For more information on how Desktop Analytics makes these recommendations, select the information icon in the top right corner of the **Identify pilot** pane.

## Readiness rules

These rules help you determine which devices qualify for in-place upgrade. You can set these rules when you create the deployment plan, or edit them later.

To change the readiness rules:

1. In the Desktop Analytics portal, select the deployment plan.
1. Next to the name, select **Edit**.
1. Select **Readiness rules**.
1. Select **Windows OS**.
1. Make changes as necessary, and select **Save**.

For **Windows OS** upgrades, there are two rules available: Device drivers and Windows applications.

### Device drivers

Configure whether your devices get drivers from Windows Update. This value is **Off** by default. Enable this rule when you're using Windows Update for Business to manage updates including drivers. If you're using Configuration Manager to manage software updates, set this rule to **Off**.

### Windows applications

The apps that Desktop Analytics show as *noteworthy* are based on the low install count threshold. Set this threshold in the readiness rules for the deployment plan. By default, this threshold is **2.0%**. You can change the value from `0.0` to `10.0`.


## Next steps

Advance to the next article to deploy to pilot devices.
> [!div class="nextstepaction"]  
> [Deploy to pilot](deploy-pilot.md)  
