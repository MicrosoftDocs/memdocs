---
title: Compatibility risk for Windows apps
titleSuffix: Configuration Manager
description: Learn about compatibility risk for Windows apps in Desktop Analytics.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
---

# Compatibility risk for Windows apps in Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

Upgrade assessments in Windows Analytics were generic, for example: Attention Needed or Fix available. It doesn't provide any visual indicator on how to prioritize apps with issues or upgrade insights. Desktop Analytics replaces this feature with **Compatibility Risk**. Desktop Analytics shows the app risk assessment for apps only in the deployment view for a pre-upgrade scenario. It categorizes the apps based on insights Microsoft gets from the machines included in a current deployment plan.

Desktop Analytics uses the following compatibility risk categories:

- **Low**: The service found no signals to put this app at risk for a Windows upgrade. It's likely to work on the target OS as-is.  

- **Medium**: Analytics indicates that the application may have impaired functionality, although remediation is likely possible.  

- **High**: The application is almost certain to fail during or after upgrade. It may need a remediation.  

- **Unknown**: The app wasn't assessed. There are no other insights such as *MS Known Issues* or *Ready for Windows*.  


## Risk assessment engine

There are several sources that Desktop Analytics uses to generate the risk rating.

### MS known issues

Desktop Analytics looks at the Microsoft app compatibility database for any known issues. It uses this database to determine any existing compatibility blocks for publicly available applications from Microsoft or other publishers. This check only applies to the target OS for the deployment plan you select.

### Ready for Windows

The [Ready for Windows](https://www.readyforwindows.com) app catalog correlates diagnostic data from other customers reporting the same apps with additional checks from Microsoft like compatibility blocks on a device.

The possible categories are:

- **Insufficient Data** means too few commercial Windows 10 devices are sharing information for this app for Microsoft to categorize its adoption.

- **Adopted** means the app has been installed on at least 10,000 commercial Windows 10 device.  

- **Highly Adopted** means the app has been installed on at least 100,000 commercial Windows 10 devices.  

- **Contact Developer** means there may be compatibility issues with this solution, and thus Microsoft recommends contacting the software provider to learn more.  

### Adopted version available

There's another version of this app that's highly adopted by other customers. This signal uses data from Ready for Windows. If there are any upgrade blockers with your current version, consider deploying the alternative version instead.

### Driver dependency

The app is dependent on a driver. Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. If you have any problems, contact the publisher to request a version that's compliant with Windows 10.


## See also

The FastTrack Center Benefit for Windows 10 provides access to **Desktop App Assure**. This benefit is a new service designed to address issues with Windows 10 and Office 365 ProPlus app compatibility. For more information, see [Desktop App Assure](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
