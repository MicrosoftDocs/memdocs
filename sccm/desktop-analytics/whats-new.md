---
title: What's new in Desktop Analytics
titleSuffix: Configuration Manager
description: A summary of the new features in the latest monthly release of the Desktop Analytics cloud service.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# What's new in Desktop Analytics

Learn what's new each month in Desktop Analytics.

> [!TIP]
> Each monthly update may take up to three days to rollout. Some features may roll out over several weeks and might not be available to all customers in the first week.

To get notified when this page is updated, copy and paste the following URL into your RSS feed reader: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## March 2020

### Support for multiple hierarchies

<!-- 4814075, 6079184 -->

You can now connect multiple Configuration Manager hierarchies to a single Azure Active Directory tenant with a single Commercial ID for Desktop Analytics. The portal categorizes devices from different hierarchies, and improves the experiences for global pilots and deployment plans.

- When you configure your global pilot, if you include collections that contain more than 20% of your total enrolled devices, the portal displays a warning.
- When you create a deployment plan, if you select collections for multiple hierarchies, the portal displays a warning.

For more information, see the following articles:

- [Global pilot](/configmgr/desktop-analytics/deploy-pilot#bkmk_GlobalPilot)
- [How to create deployment plans](/configmgr/desktop-analytics/create-deployment-plans)

## January 2020

### Additional app usage detail

<!-- 5533890 -->

When you select an app to see more information, the details pane now includes additional usage information. You can use this data to help understand the breadth of install for an app, as well as devices on which users regularly use the app. For more information, see [About assets - App usage](/configmgr/desktop-analytics/about-assets#usage).

### Provide feedback on Desktop Analytics

<!-- 5451636 -->

To share your feedback about Desktop Analytics, select the **Send a Smile** icon at the top of the portal on the right side. For more information, see [Share product feedback](/configmgr/desktop-analytics/get-support#bkmk_feedback).

## October 2019

### Improvements to compatibility recommendations

<!-- 3594545 -->

Desktop Analytics now provides additional detail when it detects that the Windows upgrade will completely or partially remove an application or driver. For more information, see [Compatibility assessment](/sccm/desktop-analytics/compat-assessment#asset-is-removed-during-upgrade).

### Migrate from Windows Analytics to existing tenant

<!-- 5202803 -->

You can now migrate inputs from an existing Windows Analytics workspace after onboarding to Desktop Analytics.

## September 2019

### Migrate inputs from Windows Analytics

<!-- 4252663 -->

During onboarding, you can now migrate inputs from an existing Windows Analytics workspace.

### Offboard from Desktop Analytics

<!-- 4972396 -->

If you set up Desktop Analytics in your environment, but want to stop using the service, you can now close your account. If you change your mind in 90 days, you can reactivate the account. For more information, see [How to close your account](/sccm/desktop-analytics/account-close).

## August 2019

### Reset your account

<!-- 3733897 -->

If you set up Desktop Analytics in your environment, but want to start over with onboarding and enrollment, you can now reset it. For more information on the process, see [Reset your account](/sccm/desktop-analytics/account-reset).

### Automatic upgrade decision of system and store apps

<!-- 3587232 -->

To help reduce your efforts in annotating noteworthy apps, certain types of apps are automatically marked as *Not important*. The deployment plan upgrade decision for these apps is also marked as *Ready*. The following apps are compatible and should continue to work after you upgrade Windows:

- System apps and components published by Microsoft

- Apps managed and updated from the Microsoft Store

For more information, see [Automatic upgrade decision of system and store apps](/sccm/desktop-analytics/about-assets#bkmk_plan-autoapp).

## What's new in Configuration Manager

The Desktop Analytics docs always refer to functionality in the latest version of Configuration Manager current branch. For more information on the latest changes in Configuration Manager, see the following articles:

<!-- - [What's new in version 1910](/sccm/core/plan-design/changes/whats-new-in-version-1910#bkmk_da) -->

- [What's new in version 1906](/sccm/core/plan-design/changes/whats-new-in-version-1906#bkmk_da)
