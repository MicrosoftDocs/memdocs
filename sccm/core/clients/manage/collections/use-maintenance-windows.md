---
title: "Use maintenance windows"
titleSuffix: "Configuration Manager"
description: "Use collections and maintenance windows to effectively manage clients in System Center Configuration Manager."
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to use maintenance windows in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Maintenance windows enable you to define a time when Configuration Manager operations can be carried out on a device collection. You use maintenance windows to help ensure that client configuration changes occur during periods that don't affect productivity. Starting in Configuration Manager version 1810, your users can see when their next maintenance window is from the **Installation status** tab in the **Software Center**. <!--1358131-->

 The following operations support maintenance windows:  

-   Software deployments  

-   Software update deployments  

-   Compliance settings deployment and evaluation  

-   Operating system deployments  

-   Task sequence deployments  

 Configure maintenance windows with a start date, a start and finish time, and a recurrence pattern. The maximum duration of a window has to be less than 24 hours. By default, computer restarts caused by a deployment aren't allowed outside of a maintenance window, but you can override the default. Maintenance windows affect only the time when the deployment program runs; applications configured to download and run locally can download content outside of the window.  

 When a client computer is a member of a device collection that has a maintenance window, a deployment program runs only if the maximum allowed run time doesn't exceed the duration configured for the window. If the program fails to run, an alert is generated and the deployment is rerun during the next scheduled maintenance window that has available time.  

## Using multiple maintenance windows  
 When a client computer is a member of multiple device collections that have maintenance windows, these rules apply:  

-   If the maintenance windows don't overlap, they're treated as two independent maintenance windows.  

-   If the maintenance windows overlap, they're treated as a single maintenance window encompassing the time period covered by both maintenance windows. For example, if two windows, each an hour in duration overlap by 30 minutes, the effective duration of the maintenance window would be 90 minutes.  

 When a user initiates an application installation from Software Center, the application is installed immediately, regardless of any maintenance windows.  

 If an application deployment with a purpose of **Required** reaches its installation deadline during the nonbusiness hours configured by a user in Software Center, the application will be installed. 

### How to configure maintenance windows  

1.  In the Configuration Manager console, choose **Assets and Compliance**>  **Device Collections**.  

3.  In the **Device Collections** list, select a collection. You can't create maintenance windows for the **All Systems** collection.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Maintenance Windows** tab of the **&lt;collection name\> Properties** dialog box, choose the **New** icon.  

6.  Complete the **&lt;new\> Schedule** dialog.  

7.  Make a selection from the **Apply this schedule to** drop-down list.  

8.  Choose **OK** and then close the **&lt;collection name\> Properties** dialog box.  
