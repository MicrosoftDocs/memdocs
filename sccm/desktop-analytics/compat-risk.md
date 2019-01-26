---
title: Compatibility risk for Windows apps
titleSuffix: Configuration Manager
description: Learn about compatibility risk for Windows apps in Desktop Analytics.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# Compatibility risk for Windows apps in Desktop Analytics 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

Upgrade assessments in Windows Analytics were generic, for example: Attention Needed or Fix available. It doesn't provide any visual indicator on how to prioritize apps with issues or upgrade insights. Desktop Analytics replaces this feature with **Compatibility Risk**. Desktop Analytics shows the app risk assessment for apps only in the deployment view for a pre-upgrade scenario. It categorizes the apps based on insights Microsoft gets from the machines included in a current deployment plan.

Desktop Analytics uses the following compatibility risk categories:

- **Low**: The service found no signals to put this app at risk for a Windows upgrade. It's likely to work on the target OS as-is.  

- **Medium**: Analytics indicates that the application may have impaired functionality, although remediation is likely possible.  

- **High**: The application is almost certain to fail during or after upgrade. It may need a remediation.  

- **Unknown**: The app wasn't assessed by App Health Analyzer. There are no other insights such as *MS Known Issues* or *Ready for Windows*.  



## Risk assessment engine

There are several sources that the App Health Analyzer uses to generate the risk rating.

![Diagram of App Health Analyzer risk assessment engine areas](media/aha-risk-assessment-engine.png)


### MS known issues

The App Health Analyzer looks at the Microsoft app compatibility database for any known issues. It uses this database to determine any existing compatibility blocks for publicly available applications from Microsoft or other publishers. This check only applies to the target OS for the deployment plan you select.


### Ready for Windows

The Ready for Windows datastore checks for compatibility blocks on a device. It also correlates data from other customers reporting similar apps. Microsoft uses data from other similar devices where this app reported no issues. 


### App Health Analyzer signals for compatibility assessment

Use the App Health Analyzer toolkit to collect additional signals for app compatibility. For more information, see [App Health Analyzer](/sccm/desktop-analytics/app-health-analyzer). 

The following signals are currently available:

#### Adopted version available
There's another version of this app that's highly adopted by other customers. This signal uses data from Ready for Windows. If there are any upgrade blockers with your current version, consider deploying the alternative version instead.

#### 16-bit
Remove all 16-bit components from applications, and replace with 32-bit or 64-bit equivalents. For more information, see [The Windows Vista and Windows Server 2008 Developer Story: Application Compatibility Cookbook](https://msdn.microsoft.com/library/aa480152.aspx). 

The other option is to enable NT Virtual DOS Machine (NTVDM) for support on Windows 10.

#### Requires admin privileges
The app requires the user to have administrative access to the device. Use an app manifest for these apps that require administrator permissions. For more information, see [Create and embed an application manifest](https://msdn.microsoft.com/library/bb756929.aspx).
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. 

#### Java dependency
Many Java applications rely on a separately installed Java Runtime Environment (JRE). While older JRE versions may continue to work on Windows 10, Oracle only supports the latest JRE versions. Using an older unsupported JRE may have security vulnerabilities. Check that your application runs on the latest JRE versions.

#### Not-DPI aware
The app may have display issues with advanced screen resolutions on Windows 10. Use an app manifest to avoid any issues with high DPI resolutions. For more information, see [Application manifests](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. 

#### Visual Basic version 6 (VB6)
Desktop Analytics recommends the app for pilot testing. VB6 applications are often compatible. If the app regresses during pilot because of any additional dependencies or widgets, then you should update the app to Visual Basic .NET 

#### OS version dependency
Consider redeveloping the application to use Version Helpers API, or manifest the application to target Windows 10.

Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. 

#### Silverlight framework
Microsoft recommends that non-browser-based apps don't use Silverlight. The support end date for Silverlight 5 is October 2021. 

Most current web browsers don't support Silverlight.

| Browser | Support |
|---------|---------|
| Google Chrome | End of support: September 2015 |
| Firefox | End of support: March 2017 |
| Microsoft Edge | No plugin available |

Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. 

#### .NET framework 1.0/1.1 
The .NET framework version 1.0 isn't supported on Windows 10. Version 1.1 isn't compatible on Windows 10. If the app is from a third-party publisher, contact the vendor to request a version that's compliant with Windows 10. Otherwise, redevelop the application to use a supported version of .NET.

#### .NET framework 2.0/3.0 
.NET 2.0 and 3.5 frameworks are supported on Windows 10. You may need to enable the Windows feature. For more information, see [Install the .NET Framework 3.5 on Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### UI access
Applications with UI access can bypass user interface control levels to drive input to higher privilege windows on the desktop. Only use this setting for user interface assistive technology applications.

If you're not using accessibility features in your app, set the UI access flag in the app manifest to false. For more information, see [Create and embed an application manifest](https://msdn.microsoft.com/library/bb756929.aspx).

#### Driver dependency
The app is dependent on a driver. Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. If you have any problems, contact the publisher to request a version that's compliant with Windows 10.



## App confidence simulation for a sample population

The following charts are from a sample case study. This data highlights the use of the App Health Analyzer with Desktop Analytics to take a data-driven approach to app validation. This approach can help reduce the time and effort in testing your applications during your Windows 10 upgrade.

This data shows the confidence metrics for 60 devices with 899 applications, including line-of-business apps.

![Before and after charts showing app confidence](media/aha-app-confidence-simulation.png)
