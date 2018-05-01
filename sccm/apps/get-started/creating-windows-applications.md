---
title: "Create Windows applications"
titleSuffix: "Configuration Manager"
description: "See which considerations you must take into account when you create and deploy applications for Windows devices."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Create Windows applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In addition to the other System Center Configuration Manager requirements and procedures for creating an application, you must also take the following considerations into account when you create and deploy applications for Windows devices.  

## General considerations  
 Configuration Manager supports deploying the following app file types:  

|Device type|Supported file types|  
|-----------------|---------------------|  
|Windows RT and Windows RT 8.1|*.appx, \*.appxbundle|  
|Windows 8.1 and later enrolled as a mobile device|*.appx, \*.appxbundle|  

 The following deployment actions are supported:  

|Device type|Supported actions|  
|-----------------|-----------------------|  
|Windows 8.1 and later|available, required, uninstall|  
|Windows RT|available, required, uninstall|  

## Support for Universal Windows Platform (UWP) apps  
 Windows 10 devices do not require a sideloading key to install line-of-business apps. For sideloading to be enabled, however, the registry key **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** must have a value of 1.  

 If this registry key is not configured, Configuration Manager automatically sets this value to **1** the first time you deploy an app to the device. If you have set this value to **0**, Configuration Manager cannot automatically change the value, and the deployment of line-of-business apps fails.  

 Universal Windows Platform line-of-business apps must be signed with a code-signing certificate that is trusted on each device to which the app is deployed. You can use certificates from an in-house PKI infrastructure, or a certificate from a third-party public root certificate installed on the device.  

 On Windows 10 Mobile devices, you can use a non-Symantec code signing certificate to sign universal **.appx** apps. For **.xap** apps, and also **.appx** packages built for Windows Phone 8.1 that you want to install on Windows 10 Mobile devices, you must use a Symantec code-signing certificate.  

## Deploy Windows Installer apps to enrolled Windows 10 PCs  
 The **Windows Installer through MDM (\*.msi)** installer type lets you create and deploy Windows Installer-based apps to enrolled PCs that run Windows 10.  

 The following considerations apply when you use this installer type:  

-   You can only upload a single file with the extension .msi.  

-   The file's product code and product version are used for app detection.  

-   The default restart behavior of the app is used. Configuration Manager does not control this.  

-   Per user MSI packages are installed for a single user.  

-   Per machine MSI packages are installed for all users on the device.  

-   App updates are supported when the MSI product code of each version is the same.  
