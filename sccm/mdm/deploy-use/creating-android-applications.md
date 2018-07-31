---
title: Create Android applications
titleSuffix: Configuration Manager
description: How to create and deploy applications for Android devices in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create Android applications in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A Configuration Manager application has one or more deployment types. Deployment types comprise the installation files and information required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

See [create an application](/sccm/apps/deploy-use/create-applications#bkmk_create) for the steps to create Configuration Manager applications and deployment types. 

Keep in mind the following considerations when you create and deploy applications for Android devices:  



## General considerations for Android apps

Configuration Manager supports the deployment of Android .apk packages. 

It supports the following deployment actions:

|Device type|Supported actions|
|-|-|
|Android|**Available**, **Required**: The user must consent to both installation and uninstallation.|
|Android for Work |**Available**, **Required** |



## Approve and deploy Android for Work apps

As a Configuration Manager administrator, you can also approve apps in the [Play for Work website](https://play.google.com/work). Then deploy those apps to managed Android for Work devices.

Follow these steps to approve apps in the Play for Work store, sync them to the Configuration Manager console, and deploy them to managed Android for Work devices. To deploy apps to users' work profiles, you need to approve the apps in Play for Work. Then sync the apps with the Configuration Manager console.

1. Open a browser and go to: https://play.google.com/work.  

2. Sign in by using the Google admin account that you bound to your Microsoft Intune tenant.  

3. Browse for apps you'd like to deploy in your environment. Choose **Approve** for each of them to make the app available for Android for Work.  

4. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Android for Work** node.  

5. Click **Sync** in the ribbon.  

6. Wait up to 10 minutes for apps to sync. Then go to the **Software Library** workspace, expand **Application Management**, and select the **License Information for Store Apps** node.  

7. Select an app synced from Play for Work, and then click **Create Application**.  

8. Complete the wizard.  

9. Go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Select an Android for Work app, and deploy as usual.  

To sync Play for Work apps with Configuration Manager, approve at least one app on the Play for Work website first.

Apps deployed as **Available** display in the work-badged Google Play app instead of the Company Portal. This lets you deploy apps from a trusted source. The work-badged Google Play app is a trusted source. You don't have to allow apps from untrusted sources.
