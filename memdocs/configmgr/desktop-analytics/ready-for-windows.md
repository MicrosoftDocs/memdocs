---
title: Ready for Windows
titleSuffix: Configuration Manager
description: About the retirement of the Ready for Windows website
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.localizationpriority: medium
---

# Ready for modern desktop retirement FAQ

<!-- placeholder -->

## Ready for Windows adoption status

The Adoption Status is based on information from commercial devices that share data with Microsoft. The status is integrated with support statements from software vendors.

Desktop Analytics provides the adoption status for each version of an asset found in commercial devices. This status doesn't include data from consumer devices or devices that don't share data. The status may not be representative of the adoption rate across all Windows 10 devices.

The possible categories are:

- **Highly adopted**: At least 100,000 commercial Windows 10 devices have installed this app.

- **Adopted**: At least 10,000 commercial Windows 10 devices have installed this app.

- **Insufficient data**: Too few commercial Windows 10 devices are sharing information for this app for Microsoft to categorize its adoption.

- **Contact developer**: There may be compatibility issues with this version of the app. Microsoft recommends contacting the software provider to learn more.

- **Unknown**: There's no information available for this version of this application. Information may be available for other versions of the application.

## General

### What happened to the Ready for Windows website?

Many customers have challenges with getting and staying current with Windows 10 and Microsoft 365 Apps for enterprise. The primary challenge is testing applications, because this process is typically manual. It's time-consuming for IT administrators and application owners to continually analyze existing applications, and then remediate any issues that arise.

The *Ready for modern desktop* directory listed software solutions that are supported and in-use on commercial devices running Windows 10 and Microsoft 365 Apps for enterprise. The directory helps IT managers who are considering the latest versions of Windows 10 and Microsoft 365 for their deployments.

Feedback from IT managers is that they want these insights integrated with the tools they already use to plan their deployment plans. Use [Desktop Analytics](./overview.md) and [Microsoft 365 Apps readiness features](/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) in Configuration Manager to plan and manage your Windows 10 and Microsoft 365 Apps for enterprise upgrade projects. 

> [!Note]
> Starting on April 21, 2020, Office 365 ProPlus is being renamed to **Microsoft 365 Apps for enterprise**. For more information, see [Name change for Office 365 ProPlus](/deployoffice/name-change). You may still see references to the old name in the Configuration Manager console and supporting documentation while the console is being updated.

### What is Desktop Analytics?

[Desktop Analytics](./overview.md) is a cloud-based service that integrates with Configuration Manager. The service provides insight and intelligence for you to make more informed decisions about the update readiness of your Windows endpoints. It combines the data specific to your organization with aggregated insights from the millions of Windows devices connected to Microsoft's cloud services.

-    Get a comprehensive view into the endpoints, applications, and drivers under management in your organization.

-    Assess application and driver compatibility with the latest Windows feature updates. Receive mitigation recommendations for known issues, as well as advanced insights for line-of-business apps.

-    Use artificial intelligence (AI) from the Microsoft cloud to optimize the set of pilot devices that adequately represent your overall environment.

### Why should I use Desktop Analytics for my Windows deployment plans?

Desktop Analytics provides the following benefits:

-    **Device and software inventory**: Inventory of key factors such as apps and versions of Windows.

-    **Pilot identification**: Identification of the smallest set of devices that provide the widest coverage of factors. It focuses on the factors that are most important to a pilot of Windows upgrades and updates. Making sure the pilot is more successful allows you to continue more quickly and confidently to broad deployments in production.

-    **Issue identification**: Using aggregated market data along with data from your environment, the service predicts potential issues to getting and staying current with Windows. It then suggests potential mitigations.

-    **Configuration Manager integration**: It cloud-enables your existing on-premises infrastructure. Use this data and analysis to deploy and manage Windows on your devices.

### What does the *Ready for Windows* status mean in Desktop Analytics?

The **Adoption Status** is based on information from commercial devices that share data with Microsoft. The status is integrated with support statements from software vendors.

Desktop Analytics provides the adoption status for each version of an asset found in commercial devices. This status doesn't include data from consumer devices or devices that don't share data. The status may not be representative of the adoption rate across all Windows 10 devices.

For more information, see [Compatibility assessment](compat-assessment.md).

### What assets get the *Ready for Windows* status in Desktop Analytics? 

Assets have the *Ready for Windows* status in Desktop analytics if:

-    The software provider declares support for the solution.
-    Customers have deployed it on a significant number of commercial Windows 10 devices that are sharing information with Microsoft.
-    The asset is relevant to commercial users.

### What additional insights do I get in Desktop Analytics?

Desktop Analytics provides an inventory of the [devices and their installed apps](about-assets.md), as well as [advanced insights](compat-assessment.md#advanced-insights) for line-of-business apps. 

## Software providers

### Can I still list my software solution in Desktop Analytics?

Publish a support statement that your product works with 32-bit or 64-bit Windows 10 or Microsoft 365 Apps for enterprise. To showcase your solutions in Desktop Analytics, talk to your Microsoft contact.

### How can listing my solutions benefit me?

Thousands of IT administrators manage millions of devices with Configuration Manager and Desktop Analytics. They use these tools to confidently plan and upgrade their organizations to the latest version of Windows 10 and Microsoft 365 Apps for enterprise. They also use them to make purchase decisions for software solutions.

Microsoft integrates support statements from software vendors with the adoption information they receive from commercial devices. Organizations around the world then use this data in Desktop Analytics and Office readiness tools. 

If your support statements aren't correctly associated with assets, talk to your Microsoft contact.

### Can I see detailed performance metrics on my assets?

Evaluate the performance of your solutions with health and metrics reports through the developer center: 

- [Windows Store](/windows/uwp/publish/health-report)
- [Desktop](/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office Add-ins](/office/dev/store/update-unpublish-and-view-metrics) 

### How can I develop compatible assets for Windows 10 and Microsoft 365 Apps for enterprise?

Make sure your desktop applications are compatible now, and stay compatible with Windows 10 in the future. For more information, see [Application compatibility for developers](https://developer.microsoft.com/windows/desktop/app-compatibility).

If you develop solutions for Microsoft 365 Apps for enterprise, see [Development best practices for COM, VSTO, and VBA add-ins in Office](/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).