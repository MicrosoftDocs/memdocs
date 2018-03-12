---
titleSuffix: "Configuration Manager"
description: "Learn about the Management Insights functionality available in the Configuration Manager console."
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby

---
# Management Insights in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Management insights in System Center Configuration Manager provide information about the current state of your environment. The information is based on analysis of data from the site database. Insights help you to better understand your environment and take action based on the insight. <!--1353967-->

## Review Management Insights in the Configuration Manager console 

1. Open the Configuration Manager Console. 
2. Go to the **Administration** node and click on **Management Insights**.
3. Select **All Insights**
4. Double-click on the **Management Insight Group Name** you want to review. Alternatively, highlight it and click on **Show Insights** in the Ribbon. 
5. Four tabs are available for review along with prerequisites needed to run the rule. 
    - **All Rules**: Gives the complete list of rules for the management insight group chosen.
    - **Complete**:  Lists rules where no action is needed. 
    - **In Progress**: Shows rules where some, but not all, prerequisites are complete.
    - **Action Needed**: Rules needing actions taken are listed. Right-click and select **More Details** to retrieve specific items where action is needed. 
    - **Prerequisites**: If a rule needs items completed before they can be run, the required items will be listed here.  
    
    **All rules and prerequisites for the cloud services group**
    ![Management insights- All rules and prerequisites for cloud services group](./media/Management-insights-all-cloud-rules.png)

## Management insights reevaluation and logging
The management insight rules reevaluate their applicability on a weekly schedule. You can re-evaluate a rule on demand by right-clicking the rule and selecting **Re-evaluate**.

**Log File for management insight rules**: SMS_DataEngine.log
## Management insights groups and rules
Rules are organized into different management insight groups. When groups and rules are added, they'll be added to the following list:

**Applications**: Insights for your application management.

- **Applications without deployments** -Lists the applications in your environment that do not have active deployments. This rule helps you find and delete unused applications to simplify the list of applications displayed in the console. 

**Cloud Services**: Helps you integrate with many cloud services; enabling modern management of your devices. 
 - **Assess co-management readiness** -Helps you understand what steps are needed to enable co-management. This rule has prerequisites. 
 - **Enable your devices to be hybrid Azure Active Directory-joined** -Azure AD-joined devices allow users to sign in with their domain credentials while ensuring devices meet the organization's security and compliance standards. 
 - **Modernize your identity and access infrastructure** -Azure AD cloud service with integrated multi-factor authentication protects sensitive data and applications both on-premises and in the cloud. 
 - **Upgrade your clients to Windows 10, version 1709 or above** -Windows 10, version 1709 or above improves and modernizes the computing experience of your users. 


**Collections**: Insights that help simplify management by cleaning up and reconfiguring collections.
   - **Empty Collections** -Lists collections in your environment that have no members. 

**Simplified Management**: Insights that help you simplify the day-to-day management of your environment. 
   - **Outdated client versions** -Lists all clients whose versions are older than two years. 

**Software Center**: Insights for managing Software Center. 
   - **Direct users to Software Center instead of Application Catalog** -Check if users have installed or requested applications from the Application Catalog in the last 14 days. The primary functionality of Application Catalog is now included in Software Center. Support for the Application Catalog website ends with the first update released after June 1, 2018
   - **Use the new version of Software Center** -The previous version of Software Center is no longer supported. Set up clients to use the new Software Center by enabling the client setting **Computer Agent** >**Use new Software Center**.

**Windows 10**: Insights related to the deployment and servicing of Windows 10. The Windows 10 management insight group is available when more than half of clients are running Windows 7, Windows 8, or Windows 8.1.
   - **Configure Windows telemetry and commercial ID key** -To use data from Upgrade Readiness, devices must be configured with a Commercial ID key and have telemetry enabled. Windows 10 devices must be set to Enhanced (Limited) telemetry level or higher.
   - **Connect Configuration Manager to Upgrade Readiness** -Leverage Upgrade Readiness to expedite your Windows 10 deployments before Windows 7 goes out of support. **Configure Windows telemetry and commercial ID key** is a prerequisite.

     **Windows 10 management insights rules**
    ![Management insights- Rules for Windows 10](./media/Windows-10-insights-group.png)
    