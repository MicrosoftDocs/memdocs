---
title: Compatibility assessment
titleSuffix: Configuration Manager
description: Learn about compatibility assessment for Windows apps and drivers in Desktop Analytics.
ms.date: 06/13/2019
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

# Compatibility assessment in Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

Upgrade assessments in Windows Analytics were generic, for example: Attention Needed or Fix available. It doesn't provide any visual indicator on how to prioritize apps or drivers with issues or upgrade insights. Desktop Analytics replaces this feature with **Compatibility Assessment**. Desktop Analytics shows the assessment for apps only in the deployment view for a pre-upgrade scenario. It categorizes the apps based on insights Microsoft gets from the machines included in a current deployment plan.

Desktop Analytics uses the following compatibility assessment categories:

- **Low**: The service found no signals to put this app at risk for a Windows upgrade. It's likely to work on the target OS as-is.  

- **Medium**: Analytics indicates that the application may have impaired functionality, although remediation is likely possible.  

- **High**: The application is almost certain to fail during or after upgrade. It may need a remediation.  

- **Unknown**: The app wasn't assessed. There are no other insights such as *MS Known Issues* or *Ready for Windows*.  


## Risk assessment engine

There are several sources that Desktop Analytics uses to generate the assessment rating.

### MS known issues

Desktop Analytics looks at the Microsoft app compatibility database for any known issues. It uses this database to determine any existing compatibility blocks for publicly available applications from Microsoft or other publishers. This check only applies to the target OS for the deployment plan you select.

### Ready for Windows

The [Ready for Windows](https://www.readyforwindows.com) app licationcatalog correlates the following data sources:

- Diagnostic data from other customers who report the same apps
- Additional checks from Microsoft like compatibility blocks on a device

The possible categories are:

- **Supported version available**: The software provider has declared support for one or more versions of this application on Windows 10.

- **Highly adopted**: At least 100,000 commercial Windows 10 devices have installed this app.  

- **Adopted**: At least 10,000 commercial Windows 10 devices have installed this app.  

- **Insufficient data**: Too few commercial Windows 10 devices are sharing information for this app for Microsoft to categorize its adoption.

- **Contact developer**: There may be compatibility issues with this version of the app. Microsoft recommends contacting the software provider to learn more. For more information, see [Ready for Windows](https://www.readyforwindows.com/).  

- **Unknown**: There's no Ready for Windows information available for this version of this application. Information may be available for other versions of the application at [Ready for Windows](https://www.readyforwindows.com/).  

### Adopted version available

There's another version of this app that's highly adopted by other customers. This signal uses data from Ready for Windows. If there are any upgrade blockers with your current version, consider deploying the alternative version instead.

### Driver dependency

The app is dependent on a driver. Desktop Analytics recommends the app for pilot testing. It should work fine for pilot, but you'll find any regressions. If you have any problems, contact the publisher to request a version that's compliant with Windows 10.


## Review applications

If Microsoft knows of issues with applications, Desktop Analytics lists and groups them by **Attention needed** or **Fix available**.

### Attention needed

For applications assessed as **Attention needed**, review the following table for details:

| Risk assessment | Action required? | Issue | What it means | Guidance |
|-----------------|------------------|-------|---------------|----------|
| Attention needed | No | Application is removed during upgrade | Windows detected compatibility issues. The application won't migrate to the new OS version. | No action is required for the upgrade to continue. |
| Attention needed | Yes | Blocking upgrade | Windows detected blocking issues, and can't remove the application during upgrade. It may not work on the new OS version. | Before upgrading, remove the application. Reinstall and test it on the new OS version. |
| Attention needed | No | Evaluate application on new OS | Windows will migrate the application, but it detected issues that may impact the app's performance on the new OS version. | No action is required for the upgrade to continue. Test the application on the new OS version. |
| Attention needed | No | Does not work with new OS, but won't block upgrade | The application isn't compatible with the new OS version, but won't block the upgrade. | No action is required for the upgrade to continue. Install a compatible version of the application on the new OS version. |
| Attention needed | Yes | Does not work with new OS, and will block upgrade | The application isn't compatible with the new OS version and will block the upgrade. | Remove the application before upgrading. A compatible version of the application may be available. |
| Attention needed | Yes | May block upgrade, test application | Windows detected issues that may interfere with the upgrade, but need further investigation. | Test the application's behavior during upgrade. If it blocks the upgrade, remove it before upgrading. Then reinstall it and test on the new OS version. |
| Attention needed | Maybe | Multiple | Multiple issues are affecting the application.| Select **Query** to see details about the issues detected by Windows. |

### Fix available

For applications assessed as **Fix available**, review the following table for details:

| Risk assessment | Action required? | Issue | What it means | Guidance |
|-----------------|------------------|-------|---------------|----------|
| Fix available | Yes | Blocking upgrade, update application to newest version | The existing version of the application isn't compatible with the new OS version and won't migrate. A compatible version of the application is available. | Update the application before upgrading. |
| Fix available| No | Reinstall application after upgrading | The application is compatible with the new OS version, but you need to reinstall it after you upgrade Windows. The upgrade process removes the application. | No action is required for the upgrade to continue. Reinstall the application on the new OS version. |
| Fix available| Yes | Blocking upgrade, but can be reinstalled after upgrading | The application is compatible with the new OS version, but won't migrate. | Remove the application before upgrading Windows. Reinstall it on the new OS version. |
| Fix available| Yes | Disk encryption blocking upgrade | The application's encryption features block the upgrade. | Disable the encryption feature before you upgrade Windows and enable it after the upgrade. |

## Review drivers

Desktop Analytics lists and groups by availability any drivers that won't migrate to the OS version.

See the following table for details on the availability categories:

| Driver availability | Action required? | What it means | Guidance |
|---------------------|------------------|---------------|----------|
| Available in-box | No, for awareness only | The currently installed version of an application or driver won't migrate to the new OS version. A compatible version is installed with the new OS version. | No action is required for the upgrade to continue. |
| Import from Windows Update | Yes | The currently installed version of a driver won't migrate to the new OS version. A compatible version is available from Windows Update. | If the computer automatically receives updates from Windows Update, no action is required. Otherwise, import a new driver from Windows Update after you upgrade Windows. |
| Available in-box and from Windows Update | Yes | The currently installed version of a driver won't migrate to the new OS version. Although a new driver is installed during upgrade, a newer version is available from Windows Update. | If the computer automatically receives updates from Windows Update, no action is required. Otherwise, import a new driver from Windows Update after you upgrade Windows. |
| Check with vendor | Yes | The driver won't migrate to the new OS version and Desktop Analytics can't locate a compatible version. | For a solution, check with the independent hardware vendor (IHV) who manufactures the driver, or the original equipment manufacturer (OEM) who provided the device. |


## See also

The FastTrack Center Benefit for Windows 10 provides access to **Desktop App Assure**. This benefit is a new service designed to address issues with Windows 10 and Office 365 ProPlus app compatibility. For more information, see [Desktop App Assure](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
