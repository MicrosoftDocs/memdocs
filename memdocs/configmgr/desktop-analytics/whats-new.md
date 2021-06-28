---
title: What's new in Desktop Analytics
titleSuffix: Configuration Manager
description: A summary of the new features in the latest monthly release of the Desktop Analytics cloud service.
ms.date: 07/07/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
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

## July 2021

### Support for the Windows diagnostic data processor configuration

<!-- 10220671 -->

Desktop Analytics now supports the new [Windows diagnostic data processor configuration](/windows/privacy/changes-to-windows-diagnostic-data-collection#new-windows-diagnostic-data-processor-configuration). This configuration provides you greater control of your Windows diagnostic data. Microsoft acts as a data processor, processing Windows diagnostic data for you as the controller. You'll continue to get insights to plan your deployments, and can fulfill [data subject requests](/windows/privacy/windows-10-and-privacy-compliance#3-the-process-for-exercising-data-subject-rights). These requests are typically to access or export Windows diagnostic data for a particular user's use of a device.

To take advantage of this change, make sure your environment is up to date:

- Use Configuration Manager version 2006 with [update rollup (4575789)](https://support.microsoft.com/topic/revised-update-rollup-for-microsoft-endpoint-configuration-manager-current-branch-version-2006-5861b9ee-9257-a15c-723e-c60110ce0c85) or a later version. Configuration Manager configures enrolled devices with policies for the Windows diagnostic data processor configuration. Update your site and clients to make sure they're using the latest configurations. Use Configuration Manager for the best experience with configuring and [enrolling devices into Desktop Analytics](enroll-devices.md#device-enrollment).

- The Windows diagnostic data processor configuration is supported on the following Windows 10 versions:
  - Pro, Education, and Enterprise editions
  - Version 1809 or later
  - July 2021 cumulative update or later

  > [!IMPORTANT]
  > Devices with an older OS version like Windows 7 will continue to show in Desktop Analytics until January 31, 2022. Use Desktop Analytics to update those devices to a supported version of Windows 10. After that date, only supported versions of Windows 10 will show in Desktop Analytics.

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

## What's new in Configuration Manager

The Desktop Analytics docs always refer to functionality in the latest version of Configuration Manager current branch. For more information on the latest changes in Configuration Manager, see [What's new in Configuration Manager incremental versions](../core/plan-design/changes/whats-new-incremental-versions.md).

## Deprecated features

When Microsoft plans to remove a significant feature of the Desktop Analytics service, that change will be announced in advance as a Configuration Manager deprecated feature. For more information, see [Deprecated features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
