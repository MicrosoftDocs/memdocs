---
title: Microsoft Store apps
titleSuffix: Configuration Manager
description: Manage and deploy apps from the Microsoft Store for Business and Education with Configuration Manager.
ms.date: 12/01/2021
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Manage apps from the Microsoft Store for Business and Education with Configuration Manager

> [!IMPORTANT]
> Starting in November 2021, this feature of Configuration Manager is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 10884039 --> For more information, see [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-endpoint-manager-integration-with-the-microsoft-store/bc-p/3592470).

The [Microsoft Store for Business and Education](/microsoft-store/) is where you find and acquire Windows apps for your organization. When you connect the store to Configuration Manager, you then synchronize the list of apps you've acquired. View these apps in the Configuration Manager console, and deploy them like you deploy any other app.

## Online and offline apps

The Microsoft Store for Business and Education supports two types of app:

- **Online**: This license type requires users and devices to connect to the store to get an app and its license. Devices running Windows 10 or later should be Microsoft Entra joined or Microsoft Entra hybrid joined. They can also be [Microsoft Entra registered](/entra/identity/devices/concept-device-registration). <!-- MEMDocs#1587-->

- **Offline**: This type lets you cache apps and licenses to deploy directly within your on-premises network. Devices don't need to connect to the store or have a connection to the internet.

For more information, see the [Microsoft Store for Business and Education overview](/mem/configmgr/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

### Summary of capabilities

Configuration Manager supports managing Microsoft Store for Business and Education apps on devices running Windows 10 or later with the Configuration Manager client. Configuration Manager offers the following capabilities for online and offline apps:

|Capability|Offline apps|Online apps|
|------------|------------|------------|
|Synchronize app data to Configuration Manager<br>(synchronization occurs every 24 hours)|Yes|Yes|
|Create Configuration Manager applications from store apps|Yes|Yes|
|Support for free apps from the store|Yes|Yes|
|Support for paid apps from the store|No|Yes<sup>[Note 1](#bkmk_note1)</sup>|
|Support required deployments to user or device collections|Yes|Yes|
|Support available deployments to user or device collections|Yes|Yes|
|Support line-of-business apps from the store|Yes|Yes|
|Provision a store app for all users on a device<sup>[Note 2](#bkmk_note2)</sup><!--1358310-->|Yes|Yes|

#### <a name="bkmk_note1"></a> Note 1: Online licensed apps version requirement

To deploy online licensed apps to Windows devices with the Configuration Manager client, they need to be running a supported version of Windows 10 or later.

#### <a name="bkmk_note2"></a> Note 2: Provision Windows app packages for all users on a device

For more information, see [Create Windows applications](../get-started/creating-windows-applications.md#bkmk_provision).

### Deploying online apps using the Microsoft Store for Business and Education to devices that run the Configuration Manager client

Before deploying Microsoft Store for Business and Education apps to devices that run the full Configuration Manager client, consider the following points:

- For full functionality, devices need to be running a supported version of Windows 10 or later.

- Register or join devices to the same Microsoft Entra tenant where you registered the Microsoft Store for Business and Education as a management tool.

- When the local Administrator account signs in on the device, it can't access Microsoft Store for Business and Education apps.

- Devices need a live internet connection to the Microsoft Store for Business and Education. For more information including proxy configuration, see [Prerequisites](/mem/intune/apps/store-apps-microsoft).

## Set up synchronization

When you synchronize the list of Microsoft Store for Business and Education apps that your organization acquired, you see these apps in the Configuration Manager console.

Connect your Configuration Manager site to Microsoft Entra ID and the Microsoft Store for Business and Education. For more information and details of this process, see [Configure Azure services](../../core/servers/deploy/configure/azure-services-wizard.md). Create a connection to the **Microsoft Store for Business** service.

Make sure the service connection point and targeted devices can access the cloud service. For more information, see [Prerequisites for Microsoft Store for Business and Education - Proxy configuration](/mem/intune/apps/store-apps-microsoft).

### Supplemental information and configuration

On the **App** page of the Azure Services Wizard, first configure the **Azure environment** and **Web app**. Then read the **More Information** section at the bottom of the page. This information includes the following other actions in the Microsoft Store for Business and Education portal:

- Configure Configuration Manager as the store management tool. For more information, see [Configure management provider](/windows/client-management/azure-active-directory-integration-with-mdm).

- Enable support for offline licensed apps. For more information, see [Distribute offline apps](/microsoft-store/distribute-offline-apps).

- Acquire at least one app. For more information, see [Find and acquire apps](/microsoft-store/find-and-acquire-apps-overview).

On the **Configurations** page of the Azure Services Wizard, specify the following information:

- **Path to Microsoft Store for Business app content storage**: Specify a shared network path, including a folder. For example, `\\server\share\folder`. When the site server syncs with the store, it caches content in this location. When you create an application in Configuration Manager, the site server copies the app content from this local cache to the site's content library.

- **Selected languages**: Select the languages to sync from the store and display to users in Software Center. For example, if the user configures Windows for German, then Software Center shows German strings for the store app. This behavior requires that language to be synchronized, and to exist for the specific application.

- **Default language**: If the user's language is unavailable, select a default language to use.

> [!NOTE]
> Configuration Manager doesn't synchronize the app icon from the store. If you need an icon to display for this app in Software Center, manually add it in the app properties. For more information, see [Manually specify application information](create-applications.md#bkmk_manual-app).<!-- 2837053 -->

## Create and deploy the app

After synchronization, create and deploy the Microsoft Store for Business and Education apps similar to any other Configuration Manager application.

1. In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then select the **License Information for Store Apps** node.

1. Choose the app you want to deploy, then select **Create Application** in the ribbon.

The site creates a Configuration Manager application containing the Microsoft Store for Business and Education app.

Then deploy and monitor this application as you would any other Configuration Manager application. For more information, see the following articles:

- [Deploy applications](deploy-applications.md)
- [Monitor applications from the console](monitor-applications-from-the-console.md)

## Manage the app

In the **Software Library** workspace, expand **Application Management**, then select the **License Information for Store Apps** node.

For each store app you manage, view the following information about the app:

- App name
- App platform
- The number of licenses for the app that you own
- The number of available licenses

After deploying online apps, any updates to that app come directly from the Microsoft Store. Furthermore, Configuration Manager doesn't check version compliance of online apps, just that Windows reports the app as installed.

When deploying offline apps to Windows devices with the Configuration Manager client, don't allow users to update applications external to Configuration Manager deployments. Control of updates to offline apps is especially important in multi-user environments such as classrooms. One option to disable the Microsoft Store is by using [group policy](/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy).

After the Microsoft Store for Business and Education administrator acquires an offline app, don't publish the app to users via the store. This configuration makes sure that users can't install or update online. Users only receive offline app updates via Configuration Manager.

## Next steps

[Troubleshoot the Microsoft Store for Business and Education integration with Configuration Manager](/troubleshoot/mem/configmgr/troubleshoot-microsoft-store-for-business-integration)
