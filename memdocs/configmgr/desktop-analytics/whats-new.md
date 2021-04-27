---
title: What's new in Desktop Analytics
titleSuffix: Configuration Manager
description: A summary of the new features in the latest monthly release of the Desktop Analytics cloud service.
ms.date: 01/04/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
---

# What's new in Desktop Analytics

Learn what's new each month in Desktop Analytics.

> [!TIP]
> Each monthly update may take up to three days to rollout. Some features may roll out over several weeks and might not be available to all customers in the first week.

To get notified when this page is updated, copy and paste the following URL into your RSS feed reader: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## January 2021

### Change to required permissions for administrator role

<!-- 9049337 -->

By the end of March 2021, the [Desktop Analytics Administrator](/azure/active-directory/roles/permissions-reference#desktop-analytics-administrator-permissions) role in Azure Active Directory will no longer require the following permissions:

- `microsoft.office365.webPortal/allEntities/basic/read`
- `microsoft.office365.serviceHealth/allEntities/allTasks`
- `microsoft.office365.supportTickets/allEntities/allTasks`

These permissions aren't currently used by this role.

There's no action required at this time, this notice is a deprecation announcement.

## December 2020

### Security updates are deprecated in Desktop Analytics

<!-- 8099536 -->

In the Desktop Analytics portal, the **Security updates** tile on the home page and the **Security updates** page are deprecated. They'll be retired in March 2021. To monitor your devices' Windows updates and Microsoft Defender status, use [Update Compliance](/windows/deployment/update/update-compliance-get-started).

### Windows 10, version 20H2, now available in Desktop Analytics

<!-- 8630465 -->

In the Desktop Analytics portal, when you monitor feature updates, you'll now see Windows 10, version 20H2. When you create a deployment plan, you can select Windows 10, version 20H2, as the target version.

For more information, see the FAQ [Why aren't new Windows releases available immediately in Desktop Analytics?](faq.yml#why-aren-t-new-windows-releases-available-immediately-in-desktop-analytics-)

## August 2020

### Apps deployed from Configuration Manager are important by default

<!-- 4859763 -->

The **Importance** configuration of an app is essential for Desktop Analytics to determine the devices to include for pilot deployments. An administrator needed to manually configure the importance for all apps in Desktop Analytics. Only once you validate the pilot can you continue with a production deployment.

Now for any app that you deploy with Configuration Manager, Desktop Analytics automatically configures it as important by default. This behavior lets you configure the apps in your environment more quickly, to progress faster towards a production deployment.

For more information, see [Assets - Apps](about-assets.md#apps).

<!-- 6049643 -->

### Improved processing of diagnostic data during snapshot generation

Microsoft improved how they collect and process Windows diagnostic data from devices enrolled in Desktop Analytics. These improvements increase the reliability of the daily snapshot generation, and prepares for new features in development. As a result of this work, Microsoft temporarily disabled the count of **Devices launched this app in the last 30 days** in deployment plans. For more information, see [Assets - Apps](about-assets.md#usage).

## July 2020

### Windows 10, version 2004, now available in Desktop Analytics

<!-- 7370207 -->

In the Desktop Analytics portal, when you monitor feature updates, you'll now see Windows 10, version 2004. When you create a deployment plan, you can select Windows 10, version 2004, as the target version.

### Improved support for viewing the portal from any device

<!-- 6270240 -->

You can now view the Desktop Analytics portal in the Microsoft Endpoint Manager admin center from a variety of device types. It now meets the Web Content Accessibility Guidelines (WCAG) 2.1 for a display resolution as low as 320 x 256 pixels. For example, the following image is of the portal from an Apple iPhone 8:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="Desktop Analytics portal on an iPhone 8":::

### Notifications for service-impacting events

<!-- 4982509 -->

The Desktop Analytics portal now can display notification banners. These notifications allow Microsoft to communicate with you about important events and issues. For example, known issues with the service, data latency, or new prerequisites. For more information, see [Service notifications](troubleshooting.md#service-notifications).

## June 2020

### Improvement to prerequisites

Desktop Analytics no longer requires that you deploy a Microsoft 365 service in your Azure Active Directory (Azure AD) tenant. The **Office 365 client admin** app in Azure AD is now the **Desktop Analytics** app, to enable Configuration Manager retrieval of information and status from the service.

## May 2020

### Reduce the number of apps for review

<!-- 5542186 -->

To help consolidate and reduce the number of apps shown on the assets page in the portal, it now combines all versions of apps with the same name and publisher. The count of apps in the **Noteworthy Apps** tile reflects this setting. For example, instead of listing hundreds of instances of Microsoft Edge, there's one instance for all versions. You can make decisions once for all versions. If you need to make decisions about specific versions of an app, this behavior is configurable.

For more information, see [About assets - Apps](about-assets.md#apps).

## March 2020

### Support for multiple hierarchies

<!-- 4814075, 6079184 -->

You can now connect multiple Configuration Manager hierarchies to a single Azure Active Directory tenant with a single Commercial ID for Desktop Analytics. The portal categorizes devices from different hierarchies, and improves the experiences for global pilots and deployment plans.

- When you configure your global pilot, if you include collections that contain more than 20% of your total enrolled devices, the portal displays a warning.
- When you create a deployment plan, if you select collections for multiple hierarchies, the portal displays a warning.

> [!NOTE]
> Support for multiple hierarchies requires Configuration Manager version 1910 or later.

For more information, see the following articles:

- [Global pilot](deploy-pilot.md#bkmk_GlobalPilot)
- [How to create deployment plans](create-deployment-plans.md)

### Identify compatibility safeguards

<!-- 5746559 -->

Windows compatibility data classifies some apps and drivers with a *safeguard*, which may cause the update to Windows 10 to fail or rollback. Desktop Analytics can now help you to identify these safeguards in advance, so that you can remediate the asset before you deploy the update. For more information, see [Compatibility assessment - Safeguards](compat-assessment.md#safeguards).

## January 2020

### Additional app usage detail

<!-- 5533890 -->

When you select an app to see more information, the details pane now includes additional usage information. You can use this data to help understand the breadth of install for an app, as well as devices on which users regularly use the app. For more information, see [About assets - App usage](about-assets.md#usage).

### Provide feedback on Desktop Analytics

<!-- 5451636 -->

To share your feedback about Desktop Analytics, select the **Send a Smile** icon at the top of the portal on the right side. For more information, see [Share product feedback](get-support.md#bkmk_feedback).

## October 2019

### Improvements to compatibility recommendations

<!-- 3594545 -->

Desktop Analytics now provides additional detail when it detects that the Windows upgrade will completely or partially remove an application or driver. For more information, see [Compatibility assessment](compat-assessment.md#asset-is-removed-during-upgrade).

### Migrate from Windows Analytics to existing tenant

<!-- 5202803 -->

You can now migrate inputs from an existing Windows Analytics workspace after onboarding to Desktop Analytics.

## September 2019

### Migrate inputs from Windows Analytics

<!-- 4252663 -->

During onboarding, you can now migrate inputs from an existing Windows Analytics workspace.

### Offboard from Desktop Analytics

<!-- 4972396 -->

If you set up Desktop Analytics in your environment, but want to stop using the service, you can now close your account. If you change your mind in 90 days, you can reactivate the account. For more information, see [How to close your account](account-close.md).

## August 2019

### Reset your account

<!-- 3733897 -->

If you set up Desktop Analytics in your environment, but want to start over with onboarding and enrollment, you can now reset it. For more information on the process, see [Reset your account](account-reset.md).

### Automatic upgrade decision of system and store apps

<!-- 3587232 -->

To help reduce your efforts in annotating noteworthy apps, certain types of apps are automatically marked as *Not important*. The deployment plan upgrade decision for these apps is also marked as *Ready*. The following apps are compatible and should continue to work after you upgrade Windows:

- System apps and components published by Microsoft

- Apps managed and updated from the Microsoft Store

For more information, see [Automatic upgrade decision of system and store apps](about-assets.md#automatic-upgrade-decision-of-system-and-store-apps).

## What's new in Configuration Manager

The Desktop Analytics docs always refer to functionality in the latest version of Configuration Manager current branch. For more information on the latest changes in Configuration Manager, see [What's new in Configuration Manager incremental versions](../core/plan-design/changes/whats-new-incremental-versions.md).

## Deprecated features

When Microsoft plans to remove a significant feature of the Desktop Analytics service, that change will be announced in advance as a Configuration Manager deprecated feature. For more information, see [Deprecated features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
