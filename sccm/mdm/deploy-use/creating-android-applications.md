---
title: "Create Android applications | Microsoft Docs"
description: "See which considerations you must take into account when you create and deploy applications for Android devices."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
---
# Create Android applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A System Center Configuration Manager application has one or more deployment types that comprise the installation files and information that are required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

 You can create applications by using the following methods:  

-   Automatically create the application and deployment types by reading the application installation files.  
-   Manually create the application and then add deployment types later.  
-   Import an application from a file.  

See [Start the create application wizard](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) for the steps required to create Configuration Manager applications and deployment types. Also, keep the following considerations in mind when you create and deploy applications for Android devices.  

## General considerations for Android apps

Configuration Manager supports the deployment of the following app types for Android:

|Device type|Supported files|
|-|-|
|Android|.apk|

The following deployment actions are supported:

|Device type|Supported actions|
|-|-|
|Android|**Available**, **Required** The user must consent to both installation and uninstallation.|
|Android for Work | **Required** |

## Approve and deploy Android for Work apps
As a Configuration Manager admin, you can also approve and deploy apps in the [Play for Work website](https://play.google.com/work), and deploy those apps to managed Android for Work devices.

Follow these steps to approve apps in the Play for Work store, sync them to the Configuration Manager console, and deploy them to managed Android for Work devices. To deploy apps to users' work profiles, you'll need to approve the apps in Play for Work, and then sync the apps with the Configuration Manager console.

1. Open a browser and go to: https://play.google.com/work.
2. Sign in by using the Google admin account that you bound to your Intune tenant.
3. Browse for apps you'd like to deploy in your environment, and choose **Approve** for each of them to make the app available for Android for Work.
4. In the Configuration Manager console, go to **Administrator** > **Overview** > **Cloud Services** > **Android for Work** and choose **Sync**.
5. Wait up to 10 minutes for apps to sync, and then go to **Software Library** > **Overview** > **Application Management** > **License Information for Store Apps**.
6. Choose an app synced from Play for Work and then choose **Create Application**.
7. Finish the wizard and choose **Close**.
8. Go to **Software Library** > **Overview** > **Application Management** > **Applications**, choose an Android for Work app, and deploy as usual.

To sync Play for Work apps with Configuration Manager, you must approve at least one app on the Play for Work website first.
