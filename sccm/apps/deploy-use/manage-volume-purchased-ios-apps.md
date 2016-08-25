---
title: "Manage volume-purchased iOS apps with System Center Configuration Manager"
ms.custom: na
ms.date: 2016-08-14
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Manage volume-purchased iOS apps with System Center Configuration Manager

  
 The iOS app store give you the ability to purchase multiple licenses for an app you want to run in your company. This helps you reduce the administrative overhead of tracking multiple purchased copies of apps.  
  
 System Center Configuration Manager helps you deploy and manage iOS apps you purchased through the program by importing the license information from the app store and tracking how many of the licenses you have used.  
  
## Manage volume-purchased apps for iOS devices  
 You purchase multiple licenses for iOS apps through the Apple Volume Purchase Program (VPP). This involves setting up an Apple VPP account from the Apple web site and uploading the Apple VPP token into Configuration Manager which provides the following capabilities:  
  
-   Synchronize your volume purchase information with Configuration Manager.  
  
-   Apps you have purchased are displayed in the Configuration Manager console.  
  
-   You can deploy and monitor these apps and also track the number of licenses for each app that have been used.  
  
-   Configuration Manager can help you reclaim licenses when required by uninstalling volume-purchased apps you deployed to users.  
  
## Before you start  
 Before you begin, you'll need to get a VPP token from Apple, and upload this to Configuration Manager.  
  
> [!IMPORTANT]  
>  -   Currently, each organization can have only one VPP account and token.  
> -   Only the Apple Volume Purchase Program for Business is supported.  
> -   Once you associate an Apple VPP account to Intune, you cannot subsequently associate a different account. For this reason, it's very important that more than one person has the details of the account you use.  
> -   If you have previously used a VPP token with a different MDM product in your existing Apple VPP account, you must generate a new one to use with Configuration Manager.  
> -   Each token is valid for one year.  
> -   By default, Configuration Manager syncs with the Apple VPP service twice a day to ensure that your licenses are synchronized with Configuration Manager.  
>   
>      Only changes to your licenses are synchronized. However, once every 7 days, a full synchronization will be performed.  
>   
>      When you click **Sync** to perform a manual sync, this will always perform a full synchronization.  
> -   If you need to recover, or restore you Configuration Manager database, we recommend that you perform a manual sync afterwards to ensure that your synchronized license data is up to date.  
> -   While you can deploy iOS volume-purchased apps to user or device collections, VPP apps you deploy to a device without a user (for instance, a device you enrolled without user affinity using the Device Enrollment Program (DEP) or Apple Configurator) will not be installed.  
  
 Additionally, you must have imported a valid Apple Push Notification service (APNs) certificate from Apple to allow you to manage iOS devices, including app deployment. For more information, see [Set up iOS hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md).  
  
## Step 1 - To get and upload an Apple VPP token  
  
1.  In the Configuration Manager console, click **Administration**.  
  
2.  In the **Administration** workspace, expand **Cloud Services**, and then click **Apple Volume Purchase Program Tokens**.   
  
3.  On the **Home** tab, in the **Apple Volume Purchase Program Tokens** group, click **Add Apple Volume Purchase Program Token**.  
  
4.  On the **General** page of the **Add Apple Volume Purchase Program Token** wizard, configure the following:   
  
    -   **Name** - Enter a name for this token as it will be displayed in the Configuration Manager console.  
  
    -   **Token** - Click **Browse** and then select the VPP token you downloaded from the Apple web site.  
  
         Click the **See Apple VPP account** link, and if you haven't already, sign up for the business or education volume purchase program. Once you are signed up, download the Apple VPP token for your account.  
  
    -   **Description** - Optionally, enter a description that will help you identify this VPP token in the Configuration Manager console.  
  
    -   **Assigned categories to improve searching and filtering** - Optionally, you can assign categories to the VPP token to make it easier to search for in the Configuration Manager console.  
  
5.  Click **Next**, and then complete the wizard.  
  
 From the **Apple Volume Purchase Program Tokens** node, you can now view information about the Apple VPP token including when it was last updated, when it will expire, and when it was last synchronized. 
  
 You can fully synchronize the data held by Apple with Configuration Manager at any time by clicking **Sync** on the **Home** tab, in the **Sync** group.  
  
## Step 2 - Deploy a volume-purchased app  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **License Information for Store Apps**.  
  
3.  Choose the app you want to deploy, then, in the **Home** tab, in the **Create** group, click **Create Application**.
A Configuration Manager application is created containing the Windows Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.
  
    > [!IMPORTANT]  
    > You must choose a deployment purpose of **Required**. Available installations are not currently supported.
  
 When you deploy the app, a license is used by each user that installs the app.  
  
 To reclaim a license, you must change the deployment action to **Uninstall**. The license will be reclaimed once the app uninstalls.  
  
## Step 3 - Monitor iOS VPP apps  
 The **License Information for Store Apps** node of the **Software Library** workspace displays information about your volume purchased iOS apps including the total number of licenses you own for each app, and how many have been deployed. 
  
 You can also monitor the license usage of all VPP apps you have purchased by using the **Apple Volume Purchase Program apps for iOS with license counts** report.  
  
 This report displays the name of each application together with the total number of licenses you purchased, the number of licenses available and more.  
  
 For help with running Configuration Manager reports, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## See Also  
 [Manage and protect apps with System Center Configuration Manager](../Topic/Manage%20and%20protect%20apps%20with%20System%20Center%20Configuration%20Manager.md)