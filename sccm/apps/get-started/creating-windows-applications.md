---
title: Create Windows applications
titleSuffix: Configuration Manager
description: Learn more information about creating and deploying Windows applications in Configuration Manager.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
---

# Create Windows applications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

In addition to the other Configuration Manager requirements and procedures for [creating an application](/sccm/apps/deploy-use/create-applications), also take the following considerations into account when you create and deploy applications for Windows devices.  



## <a name="bkmk_general"></a> General considerations  

Configuration Manager supports the deployment of Windows app package (.appx) and app bundle (.appxbundle) formats for Windows 8.1 and Windows 10 devices.

When you create an application in the Configuration Manager console, select the application installation file **Type** as **Windows app package (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**. For more information on creating apps in general, see [Create applications](/sccm/apps/deploy-use/create-applications). For more information on the MSIX format, see [Support for MSIX format](#bkmk_msix). 

> [!Note]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Provision Windows app packages for all users on a device
<!--1358310-->
Starting in version 1806, provision an application with a Windows app package for all users on the device. One common example of this scenario is provisioning an app from the Microsoft Store for Business and Education, like Minecraft: Education Edition, to all devices used by students in a school. Previously, Configuration Manager only supported installing these applications per user. After signing in to a new device, a student would have to wait to access an app. Now when the app is provisioned to the device for all users, they can be productive more quickly.

> [!Important]  
> Be careful with installing, provisioning, and updating different versions of the same Windows app package on a device, which may cause unexpected results. This behavior may occur when using Configuration Manager to provision the app, but then allowing users to update the app from the Microsoft Store. For more information, see the next step guidance when you [Manage apps from the Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

When provisioning an offline licensed app, Configuration Manager doesn't allow Windows to automatically update it from the Microsoft Store.  

Configuration Manager supports app provisioning on the following versions of Windows:<!--SCCMDocs-pr issue 2762-->
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later

To configure a Windows app deployment type for this feature, enable the option to **Provision this application for all users on the device**. For more information, see [Create applications](/sccm/apps/deploy-use/create-applications).


> [!Note]  
> If you need to uninstall a provisioned application from devices to which users have already signed on, you need to create two uninstall deployments. Target the first uninstall deployment to a device collection that contains the devices. Target the second uninstall deployment to a user collection that contains the users who have already signed on to devices with the provisioned application. When uninstalling a provisioned app on a device, Windows currently doesn't uninstall that app for users as well. 



## <a name="bkmk_msix"></a> Support for MSIX format
<!--1357427-->

Starting in version 1806, Configuration Manager supports the new Windows 10 app package (.msix) and app bundle (.msixbundle) formats. Windows 10 version 1809 or later support these new formats.  

- For an overview of MSIX, see [A closer look at MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- For how to create a new MSIX app, see [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  


### Convert applications to MSIX
<!--3607729, fka 1359029-->

Starting in version 1810, convert your existing Windows Installer (.msi) applications to the MSIX format. 

#### Prerequisites
- A reference device running Windows 10 version 1809 or later  

- Sign in to Windows on this device as a user with local administrative rights  

- Install the following apps on this device:  

    - Configuration Manager console  

    - Install the [MSIX Packaging Tool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) from the Microsoft Store  

    - Install the [MSIX packaging tool driver](https://docs.microsoft.com/windows/msix/packaging-tool/mpt-known-issues#msix-packaging-tool-driver-considerations)<!--SCCMDocs-pr issue #3091-->  

Don't install any other apps or services on this device. It's your reference system. 

#### Process to convert applications to MSIX format
1. Elevate the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.  

2. Select an application that has a Windows Installer (.msi) deployment type.  

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
- [MSIX – The MSIX Packaging Tool – signing the MSIX package](https://blogs.msdn.microsoft.com/sgern/2018/09/06/msix-the-msix-packaging-tool-signing-the-msix-package/)
- [How to sign an app package using SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

After signing the app, create a new deployment type on the application in Configuration Manager. For more information, see [Create deployment types for the application](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).




## <a name="bkmk_uwp"></a> Support for Universal Windows Platform (UWP) apps  

Windows 10 devices don't require a sideloading key to install line-of-business apps. To enable sideloading on Windows, however, the registry key `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` must have a value of **1**.  

If you don't configure this registry key, Configuration Manager automatically sets this value to **1** the first time you deploy an app to the device. If you've set this value to **0**, Configuration Manager can't automatically change the value, and your line-of-business app deployment fails.  

Digitally sign UWP line-of-business apps. Use a code-signing certificate that's trusted on each device to which you deploy the app. Use certificates from your organization's PKI, or purchase a certificate from a third-party provider whose public root certificate is already trusted by Windows.  

To sign mobile app packages, use the following table to determine the type of code-signing certificate to use:

| Package  | Symantec  | Non-Symantec  |
|---------|---------|---------|
| Universal **.appx** packages on Windows 10 Mobile devices | Yes | Yes |
| **.xap** packages | Yes | No | 
| **.appx** packages built for Windows Phone 8.1 to install on Windows 10 Mobile devices | Yes | No | 



## <a name="bkmk_mdm-msi"></a> Deploy Windows Installer apps to MDM-enrolled Windows 10 devices  

The **Windows Installer through MDM (\*.msi)** deployment type lets you create and deploy Windows Installer-based apps to MDM-enrolled devices running Windows 10.  

When you use this deployment type, consider the following points:    

-   Only upload a single file with the MSI extension.  

-   Configuration Manager uses the file's product code and product version for app detection.  

-   Windows uses the app's default restart behavior. Configuration Manager doesn't control the app restart behavior.  

-   Per-user MSI packages are installed for a single user.  

-   Per-machine MSI packages are installed for all users of the device.  

-   Configuration Manager supports app updates. The MSI product code of each version must be the same.  
