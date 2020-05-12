---
title: Install applications for a device
titleSuffix: Configuration Manager
description: Use Configuration Manager to immediately install an application to a device without a collection.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Install applications for a device

<!--4402180-->

Starting in version 1906, from the Configuration Manager console you can install applications to a device in real time. This feature can help reduce the need for separate collections for every application.

## Prerequisites

- Enable the [optional feature](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Approve application requests for users per device**.  

- [Deploy the application](deploy-applications.md) as *Available* to a device collection.  

    - On the **Deployment Settings** page of the deployment wizard, select the following option: **An administrator must approve a request for this application on the device**.  

        > [!Note]  
        > With these deployment settings, no policy is sent to the client. The app isn't shown as available in Software Center, and a user can't install the app with this deployment. After you use this action to install the app, the user can run it, and see its installation status in Software Center.

- Your user account needs the following permissions:

    - **Application**: Read, Approve

    - **Collection**: Read, Read Resource, Modify Resource, View Collected File

    For example, the **Application Administrator** built-in role has these permissions.

> [!TIP]
> In a hierarchy, wait for application and deployment information to replicate to the primary site to which the target client is assigned.<!-- SCCMDocs#2113 -->

## Process

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Devices** node. Select the target device, and then select the **Install application** action in the ribbon.

1. Select one or more applications from the list. The list only shows applications that you already deployed with the prerequisite settings.

This action triggers the installation of the selected pre-deployed applications on the device.

To see status of the approval request, in the **Software Library** workspace, expand **Application Management**, and select the **Application Requests** node.

Monitor the app installation the same as usual in the **Deployments** node of the **Monitoring** workspace.


## See also

[Approve applications](app-approval.md)
