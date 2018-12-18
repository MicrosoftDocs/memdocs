---
title: Compatibility risk for Windows apps
titleSuffix: Configuration Manager
description: A how-to guide for determining compatibility risk for Windows apps in Desktop Analytics.
ms.date: 12/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
---

# How to determine compatibility risk for Windows apps in Desktop Analytics 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

"Upgrade Assessment" from Windows Analytic were generic (Attention Needed or Fix available) in nature and doesn't provide an IT admin a visual indicator on how to prioritize apps with issues or upgrade insights. In the new desktop analytics experience "Upgrade Assessment" is replaced with "Compatibility Risk". The app risk assessment will be shown for apps only in deployment view for a pre-upgrade scenario. Apps will be categorized into High/Medium/Low/Unknown based on insights we get from the machines included in a current deployment plan.

#### LOW
Analytics indicates no signals were found to put this app at an upgrade risk. It is likely to work on the target OS as-is.

#### MEDIUM
Analytics indicates that the application may have impaired functionality, although remediation is likely possible.

#### HIGH
Analytics indicates that the application is almost certain to fail during or after upgrade and the application may need a remediation.

#### Unknown
App(s) which was not assessed by App Health Analyzer and had no other insights from analytics such as "MS Known Issues" and "Ready for Windows" 



## Risk Assessment Engine

Current sources which are used for risk rating generation (H/M/L) are documented in this section
{diagram}

1. MS Known issues
To determine any existing compatibility blocks applicable for 1st & 3rd party apps, we look at compatibility database for any known issues for the target OS the deployment plan is set for.  

2. Ready for windows datastore
For apps RFW datastore not only checks for compatibility blocks on a device but also correlates data from other commercial entities reporting similar apps. So, if an app foo seems to be blocked on a specific device, we have seen instances where in general population (similar OS build/version) the app reported no issues (blocks/crashes) from those devices. 

3. App Health Analyzer signals for compatibility assessment
App Health Analyzer toolkit for Desktop analytics is built on core solutions & methodology which Microsoft has built to evaluate desktop apps for compatibility issues. It uses innovative techniques to focus your validation efforts for desktop apps including LOB's by providing risk rating along with remediations you can take. It also has great integration story with desktop analytics to help customers mitigate upgrade issues through actionable insights. You can download the Toolkit from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=57276). The most current version was released on Oct 31, 2018. We recommend that you always download and use the most current version.

#### Learn more about the toolkit from this link.
Here are the existing signals in the current version of the toolkit along with guidance's to help you with remediation/fixes for your compatibility issues.

| Signal | Guidance | 
|--------|----------|
| Adopted version available | There is an alternate version of this app which is highly adopted or adopted on other commercial devices according to Ready for Windows. You can consider deploying this version if there are any upgrade blockers. |
| 16 Bit | It is recommended to remove all 16-bit components from applications and replace with 32-bit or 64-bit equivalents, more Information. The other option is to enable NTVDM for support on Win 10. |
| Requires admin privileges | App is recommended for pilot testing to discover any regressions as it should work fine. If found affected, IT admin must allow the user of the application to have admin access. More information on how to fix app manifest for these privileges that require Administrator permissions. |
| Java Dependency | Many Java applications rely on a separately installed Java Runtime Environment (JRE). While older JRE versions may continue to work on Windows 10, Oracle only supports the latest JRE versions Oracle Support Statement. Although there is the option to continue running your application on older unsupported JREs, for security reasons it may be preferable to run on the latest supported JRE versions. Check that your application runs on the latest JRE versions. |
| Not-dpi Aware | App is recommended for pilot testing to discover any regressions as it should work fine. If found affected, manifest the application to avoid any issues when your app runs on advanced screen resolutions on Windows 10. |
| VB6 | App is recommended for pilot testing as VB6 applications are generally compatible. If the app regresses during pilot due to any additional dependencies or widgets, then used then they should be updated to VB .NET |
| OS version dependency | App is recommended for pilot testing to discover any regressions as it should work fine. If found affected, consider redeveloping the application to use Version Helpers API or manifest the application by targeting Windows 10. |
| Silverlight Framework | App is recommended for pilot testing to discover any regressions as it should work fine. However, it is recommended for out of browser apps not to use Silverlight technology. Microsoft has set the support end date of Silverlight 5 to be October 2021. Silverlight is no longer supported in Google Chrome as of September 2015, and in Firefox as of March 2017. There is no Silverlight plugin available for Microsoft Edge. |
| 1.0/1.1 .NET framework | .NET 1.0 is not supported on Win10, .NET 1.1 is also not compatible on Win10. If it is a third-party application, contact the vendor to request a Windows 10-compliant version. Otherwise, redevelop the application so that it uses a supported version of .NET Framework. |
| 2.0/3.0 .NET framework | .NET 2.0 and 3.5 frameworks are supported on 10 but are sometime needed to be enabled as Feature on Demand |
| UI Access | Set this flag in manifest to false, if you are not intending to use accessibility features in your app. Applications with UI access can bypass user interface control levels to drive input to higher privilege windows on the desktop. This setting should only be used for user interface Assistive Technology applications. |
| Driver Dependency | App is dependent on drivers, is recommended for pilot testing to discover any regressions as it should work fine. If found affected contact the vendor to request a Windows 10-compliant version. |



## App Confidence simulation for a sample population
Here is a sample case study to showcase how adopting App Health Analyzer in your windows migration workflow with Desktop analytics can help with reducing time and efforts with data driven app validation approach. This is before/after app confidence metrics for a sample commercial device which ran App Health Analyzer toolkit. Self-hosted devices which ran AHA (60 machines) & desktop apps on these devices including LOB (899).

{screenshot/diagram}

