---
title: Apps for GCC High and DoD environments
titleSuffix: Microsoft Intune
description: Learn about apps involving GCC High and DoD environments using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 29329f86-1aa5-434f-9925-8dc28bf35348

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Deploying apps using Intune on the GCC High and DoD Environments 

Microsoft Intune can be used by tenant administrators to distribute apps to their workforce. The workforce is the company employee, the users of the apps. There are many types of apps that can be deployed from Intune on GCC High or DoD environments. If an administrator needs to upload and distribute a Windows app intended for a GCC High or DoD audience that is custom-made, created by third-party vendors, or as an offline app downloaded from the [Microsoft Store for Business](https://businessstore.microsoft.com/store), the admin can choose to distribute it as a [line-of-business app](apps-add.md#app-types-in-microsoft-intune).  

> [!NOTE]
> For commercial environments, a tenant admin can sync their Microsoft Store for Business (MSFB) with Intune, however for GCC High and DoD environments, this service is not available. Admins in this situation must deploy an app by uploading directly to Intune. To get the oflline version of the desired app, an actual commercial account will have to be used to log in to MSFB to download the package, and this is currently the only work-around for GCC high and DOD environments.

## Add line-of-business apps using Intune 

To add a line-of-business app intended for a GCC High or DoD environment using Intune, you can follow the [Windows LOB app](lob-apps-windows.md) instructions. You may choose to deploy the Company Portal first from the Microsoft Store for Business. If you choose to use the Company Portal, you can manually install and deploy the Company Portal. For more information, see [How to configure the Microsoft Intune Company Portal app](company-portal-app.md). 

## Distribute Offline Apps from the Store for Business using Intune  

If you need to [download an offline-licensed app](/microsoft-store/distribute-offline-apps#download-an-offline-licensed-app) from the Microsoft Store for Business, follow these steps to download the application: 

1. Sign in to the [Store for Business](https://businessstore.microsoft.com/).
2. Select **Manage** > **Settings**.
3. Under **Shopping Experience**, set **Show offline apps** to **On**.

When shopping for apps, if an offline version is available, you can choose to change the license type to offline. After getting the app, you can then manage it by selecting **Manage** > **Products & Services** in the [Store for Business](https://businessstore.microsoft.com/). Additionally, you can download the app and its dependencies. Then, you can deploy this downloaded app (and its dependencies) to users using Intune.  

## Syncing Intune to the Store for Business 

In a commercial (non-government) environment, an admin can sync Intune to the Microsoft Store for Business. This is not an available feature on the government environments. For details about differences between Intune in commercial environments and Intune for government environments, see [Enterprise Mobility + Security for US Government Service Description](/enterprise-mobility-security/solutions/ems-govt-service-description).  

To sync Intune to your Store for Business account, see [How to manage apps you purchased from the Microsoft Store for Business with Microsoft Intune](windows-store-for-business.md).  

## Compliance 

Review the privacy and compliance statements of apps and compare them to the compliance, security and privacy requirements of your organization when assessing the appropriate use of these services.   

## Next steps

To learn more about deploying and assigning apps, see [Assign apps to groups with Microsoft Intune](apps-deploy.md).

