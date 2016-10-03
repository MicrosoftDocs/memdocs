---
title: "Monitor certificate profiles | System Center Configuration Manager"
ms.custom: na
ms.date: 01/15/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigmanms.author: nbigmanmanager: angrobe

---
# How to monitor certificate profiles in System Center Configuration Manager

After you deploy System Center Configuration Manager certificate profiles to users in your hierarchy, you can use the following procedures to monitor the compliance status of the certificate profile:  
  
-   [How to View Compliance Results in the Configuration Manager Console](#BKMK_console)  
  
-   [How to View Compliance Results by Using Reports](#BKMK_Reports)  
  
##  <a name="BKMK_console"></a> How to View Compliance Results in the Configuration Manager Console  
 Use this procedure to view details about the compliance of deployed certificate profiles in the System Center Configuration Manager console.  
  
> [!NOTE]  
>  To monitor SCEP certificate compliance  do not use the Configuration Manager console, rather, use reports as described in [How to View Compliance Results by Using Reports](#BKMK_Reports). Specifically, use these  certificate reports under the report node **Company Resource Access**:  
>   
>  -   Certificate issuance history  
> -   List of assets with certificates nearing expiry  
> -   List of assets by certificate issuance status  
  
#### To view compliance results in the Configuration Manager console  
  
1.  In the System Center Configuration Manager console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, click **Deployments**.  
  
3.  In the **Deployments** list, select the certificate profile deployment for which you want to review compliance information.  
  
4.  You can review summary information about the compliance of the certificate profile on the main page. To view more detailed information, select the certificate profile, and then on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  
  
     The **Deployment Status** page contains the following tabs:  
  
    -   **Compliant**: Displays the compliance of the certificate profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace. This node contains all users that are compliant with the certificate profile. The **Asset Details** pane also displays the users that are compliant with this profile. Double-click a user in the list to display additional information.  
  
        > [!IMPORTANT]  
        >  A certificate profile is not evaluated if it is not applicable on a client device. However, it is returned as compliant.  
  
    -   **Error**: Displays a list of all errors for the selected certificate profile deployment based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all users that generated errors with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display additional information about the issue.  
  
    -   **Non-Compliant**: Displays a list of all noncompliant rules within the certificate profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all users that are not compliant with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display further information about the issue.  
  
    -   **Unknown**: Displays a list of all users that did not report compliance for the selected certificate profile deployment together with the current client status of the devices.  
  
5.  On the **Deployment Status** page, you can review detailed information about the compliance of the deployed certificate profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  
  
     The enrollment status of the certificate is displayed as a number. Use the following table to understand what each number means:  
  
    |Enrollment status|Description|  
    |-----------------------|-----------------|  
    |0x00000001|The enrollment succeeded, and the certificate has been issued.|  
    |0x00000002|The request has been submitted and the enrollment is pending, or the request has been issued out of band.|  
    |0x00000004|Enrollment must be deferred.|  
    |0x00000010|An error occurred.|  
    |0x00000020|The enrollment status is unknown.|  
    |0x00000040|The status information has been skipped. This can occur if a  HYPERLINK "http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly" certification authority is not valid or has not been selected for monitoring.|  
    |0x00000100|Enrollment has been denied.|  
  
##  <a name="BKMK_Reports"></a> How to View Compliance Results by Using Reports  
 Compliance settings in System Center Configuration Manager include built-in reports that you can use to monitor information about certificate profiles. These reports have the report category of **Compliance and Settings Management**.  
  
> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the reports for compliance settings.  
  
 For more information about how to configure reporting in System Center Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
### See also  

 [Operations and maintenance for certificate profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md)

