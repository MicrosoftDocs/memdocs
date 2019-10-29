---
title: Ready for Windows
titleSuffix: Configuration Manager
description: About the retirement of the Ready for Windows website
ms.date: 10/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# Ready for modern desktop retirement FAQ

<!-- placeholder -->

## General

### What happened to the Ready for Windows website?

Many customers have challenges with getting and staying current with Windows 10 and Office 365 ProPlus. The primary challenge is testing applications. This process is typically manual. It's time-consuming for IT administrators and application owners to continually analyze existing applications. Then remediate any issues that arise.

The Ready for modern desktop directory listed software solutions that are supported and in use on commercial devices running Windows 10 and Office 365 ProPlus to help IT managers who were considering the latest versions of Windows 10 and Office 365 for their deployments. 

IT managers have told us they want these insights integrated with the tools they already use to plan and execute their deployment plans. Use [Desktop Analytics](https://aka.ms/dadocs) and [Office 365 ProPlus readiness features](/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) in with Configuration Manager to plan and manage your Windows 10 and Office 365 ProPlus upgrades projects end-to-end. 

### What is Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) is a cloud-based service that integrates with Configuration Manager. The service provides insight and intelligence for you to make more informed decisions about the update readiness of your Windows endpoints. By combining the data specific to your organization with aggregated insights from the millions of Windows devices connected to Microsoft’s cloud services, you can do some remarkable things:

-	Get a comprehensive view into the endpoints, applications, and drivers under management in your ecosystem.
-	Assess application and driver compatibility with the latest Windows feature updates and receive mitigation recommendations for known issues, as well as advanced insights for line of business apps.
-	Optimize the set of pilot devices that adequately represents your overall estate using the power of artificial intelligence (AI) and the Microsoft cloud.

### Why should I use Desktop Analytics for my Windows deployment plans?

Desktop Analytics provides the following benefits:

-	**Device and software inventory**: Inventory of key factors such as apps and versions of Windows.
-	**Pilot identification**: Identification of the smallest set of devices that provide the widest coverage of factors. It focuses on the factors that are most important to a pilot of Windows upgrades and updates. Making sure the pilot is more successful allows you to proceed more quickly and confidently to broad deployments in production.
-	**Issue identification**: Using aggregated market data along with data from your environment, the service predicts potential issues to getting and staying current with Windows. It then suggests potential mitigations.
-	**Configuration Manager integration**: The service cloud-enables your existing on-premises infrastructure. Use this data and analysis to deploy and manage Windows on your devices.

### What do the Ready for Windows status in Desktop Analytics mean?

See the [Compatibility assestment](/sccm/desktop-analytics/compat-assessment#ready-for-windows) page.

The Adoption Status is based on information from commercial devices that share data with us integrated with support statements from software vendors 

We provide an Adoption Status for each version of an asset found in commercial devices. This does not include data from consumer devices or devices that do not share data, so the status may not be representative of the adoption rate across all Windows 10 devices. 
What assets will get Ready for Windows status in Desktop Analytics? 

Assets will have a Ready for Windows status in Desktop analytics if:

-	the software provider has declared support for the solution 
-	the solution has been deployed on a significant number of commercial Windows 10 devices that are sharing information with Microsoft 
-	the solution is generally relevant to commercial users 

### What Additional insights do I get in Desktop Analytics?

Desktop Analytics provides an inventory of the [Devices and their installed apps](/sccm/desktop-analytics/about-assets), as well as [advanced insights](/sccm/desktop-analytics/compat-assessment#advanced-insights) for line of business apps. 


## Software provider FAQ

### Can I still list my software solution in Desktop Analytics?

You must have a published support statement that states that your product works with 32-bit and/or 64-bit Windows 10, or Office 365 ProPlus. To showcase your solutions in Desktop Analytics, talk to your Microsoft contact. 

### How can listing my solutions benefit me?

Thousands of IT pros managing millions of devices use Configuration Manager and Desktop Analytics to confidently plan and upgrade their organizations to the latest version of Windows 10 and Office 365 ProPlus, as well as making software solutions purchase decisions.

Support statements from software vendors are integrated with the adoption information Microsoft receives from commercial devices, which is then used in Desktop Analytics and Office readiness tools currently by Fortune 500 companies around the world. 

If your support statements are not correctly associated with assets, talk to your Microsoft contact

### Can I see detailed metrics on how my assets are performing?

Evaluate how your solutions are performing with health and metrics reports through the developer center, for [Windows Store](/windows/uwp/publish/health-report), [Desktop](/windows/desktop/appxpkg/windows-desktop-application-program) and [Office Add-ins](/office/dev/store/update-unpublish-and-view-metrics) 

### How can I develop compatible assets for Windows 10 and Office 365 ProPlus?

Follow [these guidelines](/windows/desktop/app-compatibility), to ensure your desktop applications are compatible now and stay compatible with Windows 10 in the future.

Read [these guidelines](/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office), if you develop for Office 365 Plus.

