---
title: Monitor Email, Wi-Fi and VPN profiles
titleSuffix: Configuration Manager
description: Learn how to monitor the compliance status of email, Wi-Fi, and VPN profiles in Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Monitor Email, Wi-Fi and VPN profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, this company resource access feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 9315387 --> Use Microsoft Intune to [deploy resource access profiles](../../../intune/configuration/device-profiles.md).

After you have deployed Configuration Manager Email, Wi-Fi or VPN profiles to users in your hierarchy, you can use the following procedures to monitor the compliance status of the profile:  

-   [How to View Compliance Results in the Configuration Manager Console](#BKMK_console)  

-   [How to View Compliance Results by Using Reports](#BKMK_Reports)  

##  <a name="BKMK_console"></a> How to View Compliance Results in the Configuration Manager Console  
 Use this procedure to view details about the compliance of deployed profiles in the Configuration Manager console.  

#### To view compliance results in the Configuration Manager console  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, click **Deployments**.  

3.  In the **Deployments** list, select the  profile deployment for which you want to review compliance information.  

4.  You can review summary information about the compliance of the profile deployment on the main page. To view more detailed information, select the profile deployment, and then, on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  

     The **Deployment Status** page contains the following tabs:  

    -   **Compliant:** Displays the compliance of the profile that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace, which contains all users that are compliant with this profile. The **Asset Details** pane displays the users that are compliant with the profile. Double-click a user in the list to display additional information.  

        > [!IMPORTANT]  
        >  A profile is not evaluated if it is not applicable on a client device; however, it is returned as compliant.  

    -   **Error:** Displays a list of all errors for the selected profile deployment that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace, which contains all users that generated errors with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display additional information about the issue.  

    -   **Non-Compliant:** Displays a list of all noncompliant rules within the profile that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace, which contains all users that are not compliant with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display further information about the issue.  

    -   **Unknown:** Displays a list of all users that did not report compliance for the selected profile deployment together with the current client status of the devices.  

5.  On the **Deployment Status** page, you can review detailed information about the compliance of the deployed profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  

##  <a name="BKMK_Reports"></a> How to View Compliance Results by Using Reports  
 Compliance settings, which include profiles in Configuration Manager, also includes a number of built-in reports that let you monitor information about profiles. These reports have the report category of **Compliance and Settings Management**.  

> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the compliance settings reports.  

 For more information about how to configure reporting in Configuration Manager, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).  
