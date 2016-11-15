---
title: "Manage apps from the Windows Store for Business | Microsoft Docs"
description: "Manage and deploy apps from the Windows Store for Business by using System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsftms.author: robstackmanager: angrobe
---
# Manage apps from the Windows Store for Business with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
The [Windows Store for Business](https://www.microsoft.com/business-store) is where you can find and purchase Windows apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can synchronize the list of apps you've purchased with Configuration Manager, view these in the Configuration Manager console, and deploy them like you would any other app.


## Online and offline apps

The Windows Store for Business supports two types of app:

- **Online** - This license type requires users and devices to connect to the store to get an app and its license. Windows 10 devices must be Azure Active Directory domain-joined.
- **Offline** - Organizations can cache apps and licenses to deploy directly within their on-premises network, without connecting to the store or having a connection to the Internet.

[Read more](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview) about the Windows Store for Business.

Configuration Manager supports managing Windows Store for Business apps on both Windows 10 devices running the Configuration Manager client, and also Windows 10 devices that are enrolled with Microsoft Intune (known as a hybrid configuration). Configuration Manager offers the following capabilities for online and offline apps.

> [!IMPORTANT]
> To use this capability, Windows 10 devices must be running the November 2015 (1511) release or later.

|Capability|Offline apps|Online apps|
|------------|------------|------------|
|Synchronize app data to Configuration Manager<br>(synchronization occurs every 24 hours)|Yes|Yes|
|Create Configuration Manager applications from store apps|Yes|Yes|
|Support for free apps from the store|Yes|Yes|
|Support for paid apps from the store|No|No|
|Support required deployments to user or device collections|Yes|Yes<sup>1</sup>|
|Support available deployments to user or device collections|Yes<sup>3</sup>|No<sup>2</sup>|

<sup>1</sup>Supports devices managed by Intune only. Although you are not blocked from creating an online application in the Configuration Manager console and deploying this to a device managed by the Configuration Manager client, this will not work. The end user will be directed to the relevant page in the app store from where they must install the app manually.

<sup>2</sup>Online apps can be deployed as available to user or device collections for devices managed by the Configuration Manager client only, but when the end user selects the app in Software Center, they will be taken to the Windows Store for Business, where they must install the app manually. Available deployments to devices enrolled with Microsoft Intune are not supported.

<sup>3</sup>Not supported for devices managed by Intune.

> [!IMPORTANT]
> In this release, if you have a Configuration Manager hierarchy containing a central administration site and at least one primary site, deployment of offline Windows Store for Business apps to devices managed by Intune will fail.


## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, click **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Click **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, click **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, then, in the **Home** tab, in the **Features** group, click **Turn on**.
3. Close, then re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**.

## Set up Windows Store for Business synchronization

**In Azure Active Directory, register Configuration Manager as a “Web Application and/or Web API” management tool. This will give you a client ID that you will need later.**
1. In the Active Directory node of [https://manage.windowsazure.com](https://manage.windowsazure.com), select your Azure Active Directory, then click **Applications** > **Add**.
2.  Click **Add an application my organization is developing**.
3.  Enter a name for the application, select **Web application** and/or **Web API**, then click the **Next** arrow.
4.  Enter the same URL for both the **Sign-on URL** and **App ID URI**. The URL can be anything and does not need to resolve to a real address. For example, you can enter *https://yourdomain/sccm*.
5.  Complete the wizard.

**In Azure Active Directory, create a client key for the registered management tool**
1.  Highlight the application you just created and click **Configure**.
2.  Under **Keys**, select a duration from the list, and then click **Save**. This will create a new client key. Do not navigate away from this page until you have successfully onboarded the Windows Store for Business to Configuration Manager.

**In the Windows Store for Business, configure Configuration Manager as the store management tool**
1.  Open [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) and sign-in if prompted.
2.  Accept the terms of use if requested.
3.  Under **Management Tools**, click **Add a management tool**.
4.  In **Search for the tool by name**, type the name of the application you created in AAD previously, then click **Add**.
5.  Click **Activate** next to the application you just imported.
6.  In the **Manage > Account Information** page, select **Show Offline-Licensed Apps** if you want to allow offline-licensed apps to be purchased.

**Add the store account to Configuration Manager**

1. Ensure you have purchased at least one app from the Windows Store for Business.In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, then click **Windows Store for Business**.
2.  On the **Home** tab, in the **Windows Store for Business** group, click **Add Windows Store for Business Account**.
3.  Add your tenant ID, client id, and client key from Azure Active Directory, then complete the wizard.
4. Once you are done, you will see the account you configured in the **Windows Store for Business** list in the Configuration Manager console.


## Create and deploy a Configuration Manager application from a Windows Store for Business app.
1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then click **License Information for Store Apps**.
2.  Choose the app you want to deploy, then, in the **Home** tab, in the **Create** group, click **Create Application**.
A Configuration Manager application is created containing the Windows Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.

> [!IMPORTANT]
> For devices enrolled with Intune, deployed apps are only available to the user who originally enrolled the device. No other users can access the app.

## Monitor Windows Store for Business Apps

In the **Software Library** workspace, expand **Application Management**, then click **License Information for Store Apps**.

For each store app you manage, you can view information about the app including its name, platform, then number of licenses for the app that you own, and the number of licenses you have available.
