---
title: How to create deployment plans
titleSuffix: Configuration Manager
description: A how-to guide for creating deployment plans in Desktop Analytics.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# How to create deployment plans in Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

This article provides the steps for creating a deployment plan in Desktop Analytics. Before you start, first [learn about deployment plans](/sccm/desktop-analytics/about-deployment-plans).

Follow the steps in this article to use Desktop Analytics to create a plan for deploying Windows 10.

1. Open the [Desktop Analytics portal](https://aka.ms/m365aprod). Use credentials that have at least **Workspace Contributors** permissions.  

2. Select **Deployment Plans** in the Manage group.  

3. In the **Deployment Plans** pane, select **Create**.  

4. In the **Create deployment plan** pane, configure the following settings:  

    - **Name**: A unique name for the deployment plan  

    - **Products and versions**: Choose which Windows 10 version to deploy. Microsoft recommends creating deployment plans that use the most recent version.  

    - **Device groups**: Select one or more groups, and then select **Set as Target Groups**. Groups with **SCCM** as the source are collections synchronized from Configuration Manager.  

    - **Readiness rules**: These rules help to determine which devices qualify for upgrade.  

    - **Completion date**: Choose the date by which Windows should be fully deployed to all the targeted devices.  

5. Select **Create**. The new plan appears in the list of deployment plans while its being processed. Processing can take up to 48 hours before you can proceed to the next step.  

6. Open the deployment plan by selecting its name.  

7. On the deployment plan menu, in the **Prepare** group, select **Identify importance**.  

    1. On the **Apps** tab, select to show only **Not Reviewed** assets.  

    2. Select each app, and then select **Edit**. You can select more than one app to edit at the same time.  

    3. Choose an importance level from the **Importance** list. If you want Desktop Analytics to validate the app during the pilot, select **Critical** or **Important**. It doesn't validate apps marked as **Not Important**. Consider the [compatibility risk](/sccm/desktop-analytics/compat-risk) and other plan insights when assigning importance levels.  

        When assigning importance levels, you can also choose the Upgrade decision.  

    4. Select **Save** when complete.  

8. On the deployment plan menu, in the **Prepare** group, select **Identify pilot**.  

    1. Review the recommended devices for the pilot.  

    2. Select each device, and select **Add to Pilot**. If you disagree with the recommendation, select **Replace**.  

        For more information on how Desktop Analytics makes these recommendations, select the information icon in the top right corner of the **Identify pilot** pane.



### Next steps

Advance to the next article to deploy to pilot devices.
> [!div class="nextstepaction"]  
> [Deploy to pilot](/sccm/desktop-analytics/deploy-pilot)  
