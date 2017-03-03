---
title: "Manage apps from the Windows Store for Business | Microsoft Docs"
description: "Manage and deploy apps from the Windows Store for Business by using System Center Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
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
The [Windows Store for Business](https://www.microsoft.com/business-store) is where you can find and buy Windows apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can sync the list of apps you've bought with Configuration Manager, view them in the Configuration Manager console, and deploy them like you would any other app.


## Online and offline apps

The Windows Store for Business supports two types of app:

- **Online**--This license type requires users and devices to connect to the store to get an app and its license. Windows 10 devices must be Azure Active Directory domain-joined.
- **Offline**--Organizations can cache apps and licenses to deploy directly within their on-premises networks, without connecting to the store or having a connection to the Internet.

Read more about the [Windows Store for Business](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

Configuration Manager supports managing Windows Store for Business apps on Windows 10 devices running the Configuration Manager client and on Windows 10 devices that are enrolled with Microsoft Intune (hybrid configuration). Configuration Manager offers the following capabilities for online and offline apps.

> [!IMPORTANT]
> To use these capabilities, Windows 10 devices must be running the November 2015 (1511) release or later.

|Capability|Offline apps|Online apps|
|------------|------------|------------|
|Sync app data to Configuration Manager<br>(Synchronization occurs every 24 hours, or you can initiate an immediate synchronization,)|Yes|Yes|
|Create Configuration Manager applications from store apps|Yes|Yes|
|Support for free apps from the store|Yes|Yes<sup>1</sup>|
|Support for paid apps from the store|No|Yes<sup>1</sup>|
|Support required deployments to user or device collections|Yes|Yes<sup>1</sup>|
|Support available deployments to user or device collections|Yes<sup>2</sup>|No|

<sup>1</sup>Support is only for devices managed by Intune. You are not blocked from creating an online application in the Configuration Manager console and deploying this to a device managed by the Configuration Manager client, but the deployment will not work. Your users will be directed to the relevant page in the app store to install the app manually.

<sup>2</sup>Support is only for devices managed by the Configuration Manager client.

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## Set up Windows Store for Business synchronization

> [!IMPORTANT]
> When you set up a connection between Configuration Manager and the Windows Store for Business, you must provide a folder where app content synchronized from the store will be kept.
To ensure that this folder is secure and that its content can be deployed to devices, make sure the following permissions are in place:
-	The computer on which you install the service connection point site system role (the top-level site in the hierarchy) must have read and write permissions to the folder you specified when using the **Computer$** account.
-	The app author must have read permissions to the folder you specified.
-	The **Computer$** account of each computer that hosts an instance of the SMS Provider must be able to use the folder you specified.


In Azure Active Directory, register Configuration Manager as a Web Application or Web API management tool. This will give you a client ID that you will need later.
1. In the Active Directory node [https://manage.windowsazure.com](https://manage.windowsazure.com), select your Azure Active Directory, and then choose **Applications** > **Add**.
2.  Choose **Add an application my organization is developing**.
3.  Enter a name for the application, select **Web application** and/or **Web API**, and then choose **Next**.
4.  Enter the same URL for both the **Sign-on URL** and **App ID URI**. The URL can be anything and does not need to resolve to a real address. For example, you can enter *https://yourdomain/sccm*.
5.  Finish the wizard.

In Azure Active Directory, create a client key for the registered management tool.
1.  Highlight the application you just created and choose **Configure**.
2.  Under **Keys**, select a duration from the list, and then choose **Save**. This will create a new client key. Do not leave this page until you have successfully onboarded the Windows Store for Business to Configuration Manager.

In the Windows Store for Business, set up Configuration Manager as the store management tool.
1.  Open [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) and sign in if prompted.
2.  Accept the terms of use if requested.
3.  Under **Management Tools**, choose **Add a management tool**.
4.  In **Search for the tool by name**, type the name of the application you created in Azure Active Directory previously, then choose **Add**.
5.  Choose **Activate** next to the application you just imported.
6.  On the **Manage > Account Information** page, select **Show Offline-Licensed Apps** if you want to allow offline-licensed apps to be purchased.

> [!Note]
> If you are using more than one management tool to deploy Windows Store for Business apps, previously, you could only associate one of these with the Windows Store for Business. You can now associate multiple management tools with the store, for example, Intune and Configuration Manager.

Add the store account to Configuration Manager.

1. Ensure that you have bought at least one app from the Windows Store for Business. In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and then choose **Windows Store for Business**.
2.  On the **Home** tab, in the **Windows Store for Business** group, choose **Add Windows Store for Business Account**.
3.  Add your tenant ID, client id, and client secret key from Azure Active Directory, and then finish the wizard.
4. Once you're done, you will see the account you set up in the **Windows Store for Business** list in the Configuration Manager console.

Change the app languages that will be shown in the Application Catalog for users to download.

1.	In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Windows Store for Business**.
2.	Select your Windows Store for Business account, and then choose **Properties**.
3.	Select the **Language** tab.
4.	Add or remove the languages that will be shown in the Application Catalog. Select the default application catalog language that will be made available to users.

>[!IMPORTANT]
>In this release, if you change the languages that will be synchronized, you must restart the SMS Executive service on the site server before the language settings take effect.


Modify the client secret key from Azure Active Directory.

1.	In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Windows Store for Business**.
2.	Select your Windows Store for Business account, and then choose **Properties**.
3.	In the **Windows Store for Business Account Properties** dialog box, enter a new key in the **Client secret key** field, and then choose **Verify**. Once verified, choose **Apply**, and then close the dialog box.

## Sync apps from the store with Configuration Manager

Synchronization occurs every 24 hours, or you can initiate an immediate synchronization using this procedure:

1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Windows Store for Business**.
3.	On the **Home** tab, in the **Sync** group, choose **Sync Now**.
4.	The app you bought will appear in the **License Information for Store Apps** node of the **Application Management** workspace.


## Create and deploy a Configuration Manager application from a Windows Store for Business app

This procedure assumes you have acquired at least one free app, or bought at least one paid online licensed app from the Windows Store for Business.

1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, and then choose **License Information for Store Apps**.
2.  Choose the app you want to deploy, and then in the **Home** tab, in the **Create** group, choose **Create Application**.
A Configuration Manager application is created containing the Windows Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.

> [!IMPORTANT]
> For devices enrolled with Intune, deployed apps are only available to the user who originally enrolled the device. No other users can use the app.

## Monitor Windows Store for Business Apps

In the **Software Library** workspace, expand **Application Management**, and then choose **License Information for Store Apps**.

For each store app you manage, you can view information about the app including its name, platform, the number of licenses for the app that you own, and the number of licenses you have available.
