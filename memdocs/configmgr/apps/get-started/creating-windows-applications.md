---
title: Create Windows applications
titleSuffix: Configuration Manager
description: Learn more information about creating and deploying Windows applications in Configuration Manager.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
author: baladelli
manager: apoorvseth
ms.author: baladell
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Create Windows applications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

In addition to the other Configuration Manager requirements and procedures for [creating an application](../deploy-use/create-applications.md), also take the following considerations into account when you create and deploy applications for Windows devices.  

## <a name="bkmk_general"></a> General considerations  

Configuration Manager supports the deployment of Windows app package (`.appx`) and app bundle (`.appxbundle`) formats.

When you create an application in the Configuration Manager console, select the application installation file **Type** as **Windows app package (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**. For more information on creating apps in general, see [Create applications](../deploy-use/create-applications.md). For more information on the MSIX format, see [Support for MSIX format](#bkmk_msix).

> [!Note]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.<!--SCCMDocs issue 646-->  

## <a name="bkmk_provision"></a> Provision Windows app packages for all users on a device
<!--1358310-->
Provision an application with a Windows app package for all users on the device. One common example of this scenario is provisioning an app from the Microsoft Store for Business and Education, like Minecraft: Education Edition, to all devices used by students in a school. Previously, Configuration Manager only supported installing these applications per user. After signing in to a new device, a student would have to wait to access an app. Now when the app is provisioned to the device for all users, they can be productive more quickly.

> [!Important]  
> Be careful with installing, provisioning, and updating different versions of the same Windows app package on a device, which may cause unexpected results. This behavior may occur when using Configuration Manager to provision the app, but then allowing users to update the app from the Microsoft Store. For more information, see the next step guidance when you [Manage apps from the Microsoft Store for Business](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

When deploying offline apps to Windows devices with the Configuration Manager client, don't allow users to update applications external to Configuration Manager deployments. Control of updates to offline apps is especially important in multi-user environments such as classrooms. For more information, see [Manage apps from the Microsoft Store for Business and Education with Configuration Manager](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).<!-- MEMDocs#316 -->

Configuration Manager supports app provisioning on all supported versions of Windows 10 and later.<!--SCCMDocs-pr issue 2762-->

To configure a Windows app deployment type for this feature, enable the option to **Provision this application for all users on the device**. For more information, see [Create applications](../deploy-use/create-applications.md).

> [!Note]  
> If you need to uninstall a provisioned application from devices to which users have already signed on, you need to create two uninstall deployments. Target the first uninstall deployment to a device collection that contains the devices. Target the second uninstall deployment to a user collection that contains the users who have already signed on to devices with the provisioned application. When uninstalling a provisioned app on a device, Windows currently doesn't uninstall that app for users as well.

## <a name="bkmk_msix"></a> Support for MSIX format
<!--1357427-->

Configuration Manager supports the Windows app package (`.msix`) and app bundle (`.msixbundle`) formats. Supported versions of Windows 10 and later support these formats.

- For an overview of MSIX, see [A closer look at MSIX](/archive/blogs/sgern/a-closer-look-at-msix).  

- For how to create a new MSIX app, see [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### Convert applications to MSIX
<!--3607729, fka 1359029-->

Convert your existing Windows Installer (.msi) applications to the MSIX format.

#### Prerequisites for MSIX

- A reference device running Windows 10 version 1809 or later  

- Sign in to Windows on this device as a user with local administrative rights  

- Install the following apps on this device:  

  - Configuration Manager console  

  - Install the [MSIX Packaging Tool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) from the Microsoft Store  

  - Install the [MSIX packaging tool driver](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

Don't install any other apps or services on this device. It's your reference system.

#### Process to convert applications to MSIX format

1. Elevate the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.  

2. Select an application that has a Windows Installer (`.msi`) deployment type.  

    > [!Note]  
    > You need to be able to access the application's source content from the reference device.  
    >
    > The application's name can't have any special characters. Configuration Manager uses the app name as the name of the output file.  
    >
    > Don't install this application on the reference device in advance.  

3. Select **Convert to .MSIX** in the ribbon.

When the wizard completes, the MSIX Packaging Tool creates an MSIX file in the location you specified in the wizard. During this process, Configuration Manager silently installs the application on the reference device.

If the process fails, the summary page points to the log file with more information. If there's an error about capturing user state, sign out of Windows. Signing in again may resolve this issue.

To use this MSIX app, you first need to digitally sign it so that clients trust it. For more information on this process, see the following articles:

- [MSIX - The MSIX Packaging Tool - signing the MSIX package](/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [How to sign an app package using SignTool](/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

After signing the app, create a new deployment type on the application in Configuration Manager. For more information, see [Create deployment types for the application](../deploy-use/create-applications.md#bkmk_create-dt).

## <a name="bkmk_tsdt"></a> Task sequence deployment type

<!--3555953-->

> [!Note]  
> In this version of Configuration Manager, the task sequence deployment type is a pre-release feature. To enable it, see [Pre-release features](../../core/servers/manage/pre-release-features.md).

You can install complex applications using task sequences via the application model. Add a task sequence deployment type to an app either to install or uninstall the app. This deployment type provides the following behaviors:

- Display the app task sequence with an icon in Software Center. An icon makes it easier for users to find and identify the app task sequence.

- Define additional metadata for the app task sequence, including localized information

- Starting in version 2010, deploy an app task sequence to a user collection<!--8018255-->

You can only add a non-OS deployment task sequence as a deployment type on an app. High-impact, OS deployment, or OS upgrade task sequences aren't supported. A user-targeted deployment still runs in the context of the local System account.

When you add this deployment type to an app, configure its properties on the **Task Sequence** page. For more information, see [Deployment type **Task Sequence** options](../deploy-use/create-applications.md#bkmk_dt-ts).

Starting in version 2006, use the following Windows PowerShell cmdlets to add and configure a task sequence deployment type:

- [Add-CMTaskSequenceDeploymentType](/powershell/module/configurationmanager/add-cmtasksequencedeploymenttype)
- [Set-CMTaskSequenceDeploymentType](/powershell/module/configurationmanager/set-cmtasksequencedeploymenttype)

> [!NOTE]
> Consider the following scenario:<!--10422235-->
>
> - An application has a task sequence deployment type.
> - It's deployed as available.
> - A device has maintenance windows defined.
> - A user on the device runs the deployment in Software Center outside of a maintenance window.
>
> Configuration Manager honors the user's intent to install the application, even though there's no available maintenance window. In version 2107 and earlier, when the task sequence ran, the **Restart Computer** step would fail because of the maintenance window.
>
> Starting in version 2111, this step now ignores maintenance windows only when the task sequence is run as an app deployment type.

### Prerequisites for a task sequence deployment type

Create a custom task sequence:

- Use only non-OS deployment steps, for example: **Install Package**, **Run Command Line**, or **Run PowerShell Script**. For more information including the full list of supported steps, see [Create a task sequence for non-OS deployments](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- On the task sequence properties, **User Notification** tab, don't select the option for a high-impact task sequence.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

When you create the application, to add a task sequence deployment type, your user account needs permission to read task sequences.<!-- 6348976 --> Use one of the following options to configure these permissions:

- Add the app administrator's user account to the built-in **Read-Only Analyst** role. This role allows them to view all Configuration Manager objects.

- Copy the built-in **Application Administrator** role to create a custom role. Add the **Read** permission on the **Task Sequence Package** object.

### Known issues for a task sequence deployment type

- Don't use the **Install Application** step in this task sequence. Use the [Install Package](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) step to install apps.

- In version 2006 and earlier, you can't yet deploy an app task sequence to a user collection. This issue was resolved in version 2010.

## <a name="bkmk_uwp"></a> Support for Universal Windows Platform (UWP) apps

Windows 10 or later devices don't require a sideloading key to install line-of-business apps. To enable sideloading on Windows, however, the registry key `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` must have a value of **1**.  

If you don't configure this registry key, Configuration Manager automatically sets this value to **1** the first time you deploy an app to the device. If you've set this value to **0**, Configuration Manager can't automatically change the value, and your line-of-business app deployment fails.  

Digitally sign UWP line-of-business apps. Use a code-signing certificate that's trusted on each device to which you deploy the app. Use certificates from your organization's PKI, or purchase a certificate from a third-party provider whose public root certificate is already trusted by Windows.  

To sign mobile app packages, use the following table to determine the type of code-signing certificate to use:

| Package  | Symantec  | Non-Symantec  |
|---------|---------|---------|
| Universal **.appx** packages on Windows 10 Mobile devices | Yes | Yes |
| **.xap** packages | Yes | No |
| **.appx** packages built for Windows Phone 8.1 to install on Windows 10 Mobile devices | Yes | No |

## <a name="bkmk_mdm-msi"></a> Deploy Windows Installer apps to MDM-enrolled Windows 10 devices  

The **Windows Installer through MDM (\*.msi)** deployment type lets you create and deploy Windows Installer-based apps to MDM-enrolled devices running Windows 10 or later.

When you use this deployment type, consider the following points:

- Only upload a single file with the MSI extension.  

- Configuration Manager uses the file's product code and product version for app detection.  

- Windows uses the app's default restart behavior. Configuration Manager doesn't control the app restart behavior.  

- Per-user MSI packages are installed for a single user.  

- Per-machine MSI packages are installed for all users of the device.  

- Configuration Manager supports app updates. The MSI product code of each version must be the same.
