---
title: Compatibility assessment
titleSuffix: Configuration Manager
description: Learn about compatibility assessment for Windows apps and drivers in Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# Compatibility assessment in Desktop Analytics

Upgrade assessments in previous solutions were generic, for example: Attention Needed or Fix available. It doesn't provide any visual indicator on how to prioritize apps or drivers with issues or upgrade insights. Desktop Analytics replaces this feature with **Compatibility Risk**. Desktop Analytics shows the assessment for apps only in the deployment view for a pre-upgrade scenario. It categorizes the apps based on insights Microsoft gets from the machines included in a current deployment plan.

Desktop Analytics uses the following compatibility assessment categories:

- **Low**: The service found no signals to put this app at risk for a Windows upgrade. It's likely to work on the target OS as-is.

- **Medium**: Analytics indicates that the application may have impaired functionality, although remediation is likely possible.

- **High**: The application is almost certain to fail during or after upgrade. It may need a remediation.

- **Unknown**: The app wasn't assessed. There are no other insights such as *MS Known Issues* or *Ready for Windows*.

In the list of app or driver assets in a deployment plan, you'll see this value for each asset in the **Compatibility Risk** column.

## App risk assessment

![Diagram of app risk assessment sources](media/app-risk-assessment-sources.png)

There are several sources that Desktop Analytics uses to generate the assessment rating for applications:

- [Microsoft known issues](#microsoft-known-issues)
- [Ready for Windows](#ready-for-windows)
- [Advanced insights](#advanced-insights)

You can find the assessment for each source on the app in Desktop Analytics. In the list of app assets in a deployment plan, select an individual app to open its properties flyout pane. You'll see an overall recommendation and assessment level. The **Compatibility risk factors** section shows the detail for these assessments.

> [!TIP]
> If the app details pane doesn't show the compatibility assessment, it may be because the **App Versions Details** setting is off. It's off by default, and combines all versions of apps with the same name and publisher. The service still makes compatibility risk assessments for each version. Turn on **App versions details** to see the compatibility risk assessment for a specific app version. For more information, see [Plan assets](about-deployment-plans.md#plan-assets).

## Microsoft known issues

Desktop Analytics looks at the Microsoft app compatibility database for any known issues. It uses this database to determine any existing compatibility blocks for publicly available applications from Microsoft or other publishers. This check only applies to the target OS for the deployment plan you select.

You'll see the following issues on the app properties pane as **MS known issues**:

### Asset is removed during upgrade

Windows detected compatibility issues with an application or driver. The asset won't migrate to the new OS version. No action is required for the upgrade to continue. Install a compatible version of the application or driver on the new OS version.

<!-- 3594545 -->
Windows can partially or fully remove these assets:

- Full removal: Windows setup completely removes the app or driver from the device during upgrade.
- Partial removal: Windows setup partially removes the app or driver from the device. You need to manually uninstall it after you upgrade Windows.

In both the cases, after you upgrade Windows, the user can't use the app or the hardware associated with the driver.

To see this recommendation in the Desktop Analytics portal:

1. In a deployment plan, select **Prepare pilot**.
1. Select the **Apps** tab.
1. Select an app, and then view the compatibility risk factors and recommendations in the side pane.

:::image type="content" source="media/3594545-app-removed.png" alt-text="Screenshot of asset recommendation in Desktop Analytics portal" lightbox="media/3594545-app-removed.png":::

### Blocking upgrade

Windows detected blocking issues, and can't remove the application during upgrade. It may not work on the new OS version. Before upgrading, remove the application. Reinstall and test it on the new OS version.

### Blocking upgrade, but can be reinstalled after upgrading

The application is compatible with the new OS version, but won't migrate. Remove the application before upgrading Windows. Reinstall it on the new OS version.

### Blocking upgrade, update application to newest version

The existing version of the application isn't compatible with the new OS version and won't migrate. A compatible version of the application is available. Update the application before upgrading.

### Disk encryption blocking upgrade

The application's encryption features block the upgrade. Disable the encryption feature before you upgrade Windows and enable it after the upgrade.

### Does not work with new OS, but won't block upgrade

The application isn't compatible with the new OS version, but won't block the upgrade. No action is required for the upgrade to continue. Install a compatible version of the application on the new OS version.

### Does not work with new OS, and will block upgrade

The application isn't compatible with the new OS version and will block the upgrade. Remove the application before upgrading. A compatible version of the application may be available.

### Evaluate application on new OS

Windows will migrate the application, but it detected issues that may impact the app's performance on the new OS version. No action is required for the upgrade to continue. Test the application on the new OS version.

### May block upgrade, test application

Windows detected issues that may interfere with the upgrade, but need further investigation. Test the application's behavior during upgrade. If it blocks the upgrade, remove it before upgrading. Then reinstall it and test on the new OS version.

### Multiple

Multiple issues affect the application. Select **Query** to see details about the issues detected by Windows.

### Reinstall application after upgrading

The application is compatible with the new OS version, but you need to reinstall it after you upgrade Windows. The upgrade process removes the application. No action is required for the upgrade to continue. Reinstall the application on the new OS version.

### Safeguards

<!-- 5746559 -->

Windows compatibility data classifies some apps and drivers with a *safeguard*, which may cause the update to Windows 10 to fail or roll back. Windows may also upgrade, but it removes the app or driver. Desktop Analytics can now help you to identify these safeguards in advance, so that you can remediate the asset before you deploy the update.

1. In the Desktop Analytics portal, select a deployment plan.

1. Select **Plan assets** in the menu, and switch to the **Apps** tab.

1. Filter the name column to show items with values that contain the word `Safeguard`. Select the result to see more information.

    > [!NOTE]
    > This entry isn't a real app that's installed on your devices. It's a placeholder to help identify apps or drivers in your environment with the safeguard compatibility tag.

1. In the recommendation section, select the link to *Learn more*. This link opens the Windows website with the current list of apps or drivers with the safeguard tag.

1. Compare the current published list against the list of assets in your environment. Remediate any potentially problematic apps or drivers by updating to a compatible version.

:::image type="content" source="media/5746559-safeguards.png" alt-text="Screenshot of the Safeguard app in Desktop Analytics" lightbox="media/5746559-safeguards.png":::

## Ready for Windows

The Adoption Status is based on information from commercial devices that share data with Microsoft. The status is integrated with support statements from software vendors.

Desktop Analytics provides the adoption status for each version of an asset found in commercial devices. This status doesn't include data from consumer devices or devices that don't share data. The status may not be representative of the adoption rate across all Windows 10 devices.

The possible categories are:

- **Highly adopted**: At least 100,000 commercial Windows 10 devices have installed this app.

- **Adopted**: At least 10,000 commercial Windows 10 devices have installed this app.

- **Insufficient data**: Too few commercial Windows 10 devices are sharing information for this app for Microsoft to categorize its adoption.

- **Contact developer**: There may be compatibility issues with this version of the app. Microsoft recommends contacting the software provider to learn more.

- **Unknown**: There's no information available for this version of this application. Information may be available for other versions of the application.

### Support statement

If the software provider supports one or more versions of this application on Windows 10, you'll see this statement on the app properties pane. In the Compatibility risk factors section, look at the **Support statement**.

## Advanced insights

Desktop Analytics can also detect issues using the following additional insights:

### Adopted version available

There's another version of this app that's highly adopted by other customers. This signal uses adoption data from the Windows ecosystem. If there are any upgrade blockers with your current version, consider deploying the alternative version instead. To find alternate application adopted versions, see application health under "Prepare Production".

### Driver dependency

The app is dependent on a driver. Desktop Analytics recommends the app for pilot testing to discover any regressions. If you have any problems, contact the publisher to request a version that's compliant with Windows 10.

### Additional insights

<!-- 4021225 -->
When you update the Configuration Manager site and clients to version 1906, clients also report these additional insights, when diagnostic data level is set to Enhanced Limited:

> [!Important]  
> To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. This scenario isn't functional until the client version is also the latest.

#### 16-bit apps

Remove all 16-bit components from applications, and replace with 32-bit or 64-bit equivalents. For more information, see [The Windows Vista and Windows Server 2008 Developer Story: Application Compatibility Cookbook](/previous-versions/aa480152\(v=msdn.10\)).

The other option is to enable NT Virtual DOS Machine (NTVDM) for support on Windows 10.

#### Requires admin privileges

The app requires the user to have administrative access to the device. Use an app manifest for these apps that require administrator permissions. For more information, see [Create and embed an application manifest](/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics recommends the app for pilot testing to discover any regressions.

#### Java dependency

Many Java applications rely on a separately installed Java Runtime Environment (JRE). While older JRE versions may continue to work on Windows 10, Oracle only supports the latest JRE versions. Using an older unsupported JRE may have security vulnerabilities. Check that your application runs on the latest JRE versions.

#### Not-DPI aware

The app may have display issues with advanced screen resolutions on Windows 10. Use an app manifest to avoid any issues with high DPI resolutions. For more information, see [Application manifests](/windows/desktop/SbsCs/application-manifests).

Desktop Analytics recommends the app for pilot testing to discover any regressions.

#### Silverlight framework

Microsoft recommends that non-browser-based apps don't use Silverlight. The support end date for Silverlight 5 is October 2021.

Most current web browsers don't support Silverlight.

| Browser | Support |
|---------|---------|
| Google Chrome | End of support: September 2015 |
| Firefox | End of support: March 2017 |
| Microsoft Edge | No plugin available |

Desktop Analytics recommends the app for pilot testing to discover any regressions.

#### .NET Framework 1.0/1.1

The .NET Framework version 1.0 isn't supported on Windows 10. Version 1.1 isn't compatible on Windows 10. If the app is from a third-party publisher, contact the vendor to request a version that's compliant with Windows 10. Otherwise, redevelop the application to use a supported version of .NET.

#### .NET Framework 2.0/3.0

.NET 2.0 and 3.5 frameworks are supported on Windows 10. You may need to enable the Windows feature. For more information, see [Install the .NET Framework 3.5 on Windows 10](/dotnet/framework/install/dotnet-35-windows-10).

#### UI access

Applications with UI access can bypass user interface control levels to drive input to higher privilege windows on the desktop. Only use this setting for user interface assistive technology applications.

If you're not using accessibility features in your app, set the UI access flag in the app manifest to false. For more information, see [Create and embed an application manifest](/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics recommends the app for pilot testing to discover any regressions.

## Driver risk assessment

Desktop Analytics also lists and groups by availability any drivers that won't migrate to the OS version.

You can find the assessment on the driver in Desktop Analytics. In the list of driver assets in a deployment plan, select an individual driver to open its properties flyout pane. You'll see an overall recommendation and assessment level. The **Compatibility risk factors** section shows the detail for these assessments.

| Driver availability | Action required? | What it means | Guidance |
|---------------------|------------------|---------------|----------|
| Available in-box | No, for awareness only | The currently installed version of an application or driver won't migrate to the new OS version. A compatible version is installed with the new OS version. | No action is required for the upgrade to continue. |
| Import from Windows Update | Yes | The currently installed version of a driver won't migrate to the new OS version. A compatible version is available from Windows Update. | If the computer automatically receives updates from Windows Update, no action is required. Otherwise, import a new driver from Windows Update after you upgrade Windows. |
| Available in-box and from Windows Update | Yes | The currently installed version of a driver won't migrate to the new OS version. Although a new driver is installed during upgrade, a newer version is available from Windows Update. | If the computer automatically receives updates from Windows Update, no action is required. Otherwise, import a new driver from Windows Update after you upgrade Windows. |
| Check with vendor | Yes | The driver won't migrate to the new OS version and Desktop Analytics can't locate a compatible version. | For a solution, check with the independent hardware vendor (IHV) who manufactures the driver, or the original equipment manufacturer (OEM) who provided the device. |

## See also

The FastTrack Center Benefit for Windows 10 provides access to **Desktop App Assure**. This benefit is a new service designed to address issues with Windows 10 and Microsoft 365 Apps for enterprise compatibility. For more information, see [Desktop App Assure](/fasttrack/win-10-app-assure).