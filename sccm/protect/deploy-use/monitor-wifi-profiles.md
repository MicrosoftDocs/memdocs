---
title: "How to monitor Wi-Fi profiles in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
caps.latest.revision: 4
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
# How to monitor Wi-Fi profiles in System Center Configuration Manager
After you have deployed System Center Configuration Manager Wi-Fi profiles to users in your hierarchy, you can use the following procedures to monitor the compliance status of the Wi-Fi profile:  
  
-   [How to View Compliance Results in the Configuration Manager Console](#BKMK_console)  
  
-   [How to View Compliance Results by Using Reports](#BKMK_Reports)  
  
##  <a name="BKMK_console"></a> How to View Compliance Results in the Configuration Manager Console  
 Use this procedure to view details about the compliance of deployed Wi-Fi profiles in the System Center Configuration Manager console.  
  
#### To view compliance results in the Configuration Manager console  
  
1.  In the System Center Configuration Manager console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, click **Deployments**.  
  
3.  In the **Deployments** list, select the Wi-Fi profile deployment for which you want to review compliance information.  
  
4.  You can review summary information about the compliance of the Wi-Fi profile deployment on the main page. To view more detailed information, select the Wi-Fi profile deployment, and then, on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  
  
     The **Deployment Status** page contains the following tabs:  
  
    -   **Compliant:** Displays the compliance of the Wi-Fi profile that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace, which contains all users that are compliant with this profile. The **Asset Details** pane displays the users that are compliant with the Wi-Fi profile. Double-click a user in the list to display additional information.  
  
        > [!IMPORTANT]  
        >  A Wi-Fi profile is not evaluated if it is not applicable on a client device; however, it is returned as compliant.  
  
    -   **Error:** Displays a list of all errors for the selected Wi-Fi profile deployment that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace, which contains all users that generated errors with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display additional information about the issue.  
  
    -   **Non-Compliant:** Displays a list of all noncompliant rules within the Wi-Fi profile that is based on the number of affected assets. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace, which contains all users that are not compliant with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display further information about the issue.  
  
    -   **Unknown:** Displays a list of all users that did not report compliance for the selected Wi-Fi profile deployment together with the current client status of the devices.  
  
5.  On the **Deployment Status** page, you can review detailed information about the compliance of the deployed Wi-Fi profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  
  
##  <a name="BKMK_Reports"></a> How to View Compliance Results by Using Reports  
 Compliance settings, which include Wi-Fi profiles in System Center Configuration Manager, also includes a number of built-in reports that let you monitor information about Wi-Fi profiles. These reports have the report category of **Compliance and Settings Management**.  
  
> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the compliance settings reports.  
  
 For more information about how to configure reporting in System Center Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## See Also  
 [Operations and maintenance for Wi-Fi Profiles in Configuration Manager](assetId:///7ca46f39-c1bd-4e05-aac9-cbea5dec7f78)