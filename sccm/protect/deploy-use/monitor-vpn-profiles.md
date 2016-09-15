---
title: "Monitor VPN profiles | System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0b91f15-7e42-44ba-9baf-c2cdb068554a
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
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
# How to monitor VPN profiles in System Center Configuration Manager
After you have deployed System Center Configuration Manager VPN profiles to devices in your hierarchy, you can use the following procedures to monitor the compliance status of the VPN profile:  
  
-   [How to View Compliance Results in the Configuration Manager Console](#BKMK_console)  
  
-   [How to View Compliance Results by Using Reports](#BKMK_Reports)  
  
##  <a name="BKMK_console"></a> How to View Compliance Results in the Configuration Manager Console  
 Use this procedure to view details about the compliance of deployed VPN profiles in the System Center Configuration Manager console.  
  
#### To view compliance results in the Configuration Manager console  
  
1.  In the System Center Configuration Manager console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, click **Deployments**.  
  
3.  In the **Deployments** list, select the VPN profile deployment for which you want to review compliance information.  
  
4.  You can review summary information about the compliance of the VPN profile deployment on the main page. To view more detailed information, select the VPN profile deployment, and then on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  
  
     The **Deployment Status** page contains the following tabs:  
  
    -   **Compliant:** Displays the compliance of the VPN profile that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace, which contains all users that are compliant with this profile. The **Asset Details** pane displays the users that are compliant with the VPN profile. Double-click a user in the list to display additional information.  
  
        > [!IMPORTANT]  
        >  A VPN profile is not evaluated if it is not applicable on a client device; however, it is returned as compliant.  
  
    -   **Error:** Displays a list of all errors for the selected VPN profile deployment that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace, which contains all users that generated errors with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display additional information about the issue.  
  
    -   **Non-Compliant:** Displays a list of all noncompliant rules within the VPN profile that are based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace, which contains all users that are not compliant with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display further information about the issue.  
  
    -   **Unknown:** Displays a list of all users that did not report compliance for the selected VPN profile deployment together with the current client status of the devices.  
  
5.  On the **Deployment Status** page, you can review detailed information about the compliance of the deployed VPN profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  
  
    > [!IMPORTANT]  
    >  For  devices running Windows 8.1 and later, you may obtain a compliance error stating that the  Check Point VPN deployment failed due to an issue with the fingerprint feature. This error can be safely ignored, as the fingerprint feature is specific to iOS, and the deployment will have succeeded.  
  
##  <a name="BKMK_Reports"></a> How to View Compliance Results by Using Reports  
 Compliance settings, which include VPN profiles in System Center Configuration Manager, also includes a number of built-in reports that let you monitor information about VPN profiles. These reports have the report category of **Compliance and Settings Management**.  
  
> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the compliance settings reports.  
  
 For more information about how to configure reporting in System Center Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## See Also  
 [Operations and maintenance for VPN profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20VPN%20profiles%20in%20System%20Center%20Configuration%20Manager.md)