---
title: Monitor certificate profiles
titleSuffix: Configuration Manager
description: Learn how to monitor the compliance status of Configuration Manager certificate profiles.
ms.date: 03/29/2022
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# How to monitor certificate profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in version 2203, this company resource access feature is no longer supported.<!-- 9315387 --> For more information, see [Frequently asked questions about resource access deprecation](../plan-design/resource-access-deprecation-faq.yml).

##  View Compliance Results in the Configuration Manager Console  

To monitor SCEP certificate compliance  do not use the console, rather, use [reports](#view-compliance-results-by-using-reports). 

1. In the Configuration Manager console, choose **Monitoring**>  **Deployments**.  

2. Select the certificate profile deployment of interest.  

3. Review summary certificate compliance information on the main page. For more detailed information, select the certificate profile, and then on the **Home** tab, in the **Deployment** group, choose **View Status** to open the **Deployment Status** page.  

    The **Deployment Status** page contains the following tabs:  

   -   **Compliant**: Displays the compliance of the certificate profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace. This node contains all users that are compliant with the certificate profile. The **Asset Details** pane also displays the users that are compliant with this profile. Double-click a user in the list for more information.  

       > [!IMPORTANT]  
       >  A certificate profile is not evaluated if it is not applicable on a client device. However, it is returned as compliant.  

   -   **Error**: Displays a list of all errors for the selected certificate profile deployment based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all users that generated errors with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display for more information.  

   -   **Non-Compliant**: Displays a list of all noncompliant rules within the certificate profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all users that are not compliant with this profile. When you select a user, the **Asset Details** pane displays the users that are affected by the selected issue. Double-click a user in the list to display further information about the issue.  

   -   **Unknown**: Displays a list of all users that did not report compliance for the selected certificate profile deployment together with the current client status of the devices.  

4. On the **Deployment Status** page, review detailed information about the compliance of the deployed certificate profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  

    The enrollment status of the certificate is displayed as a number. Use the following table to understand what each number means:  


   | Enrollment status |                                                                                                                   Description                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         The enrollment succeeded, and the certificate has been issued.                                                                                          |
   |    0x00000002     |                                                                    The request has been submitted and the enrollment is pending, or the request has been issued out of band.                                                                    |
   |    0x00000004     |                                                                                                          Enrollment must be deferred.                                                                                                           |
   |    0x00000010     |                                                                                                               An error occurred.                                                                                                                |
   |    0x00000020     |                                                                                                        The enrollment status is unknown.                                                                                                        |
   |    0x00000040     | The status information has been skipped. This can occur if a  HYPERLINK "<https://msdn.microsoft.com/windows/ms721572>" \l "_security_certification_authority_gly" certification authority is not valid or has not been selected for monitoring. |
   |    0x00000100     |                                                                                                           Enrollment has been denied.                                                                                                           |

##  View Compliance Results by Using Reports

Compliance settings in Configuration Manager include built-in reports that you can use to monitor information about certificate profiles. These reports have the report category of **Compliance and Settings Management**.  

> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the reports for compliance settings.  

To monitor SCEP certificate compliance  use these  certificate reports under the report node **Company Resource Access**:  

-   Certificate issuance history  
-   List of assets with certificates nearing expiry  
-   List of assets by certificate issuance status  



 For more information about how to configure reporting in Configuration Manager, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).  
