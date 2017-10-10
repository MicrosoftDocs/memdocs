---
title: "Configure client status"
titleSuffix: "Configuration Manager"
description: "Select client status settings in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to configure client status in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you can monitor System Center Configuration Manager client status and remediate problems that are found, you must configure your site to specify the parameters that are used to mark clients as inactive and configure options to alert you if client activity falls below a specified threshold. You can also disable computers from automatically remediating any problems that client status finds.  

##  <a name="BKMK_1"></a> To Configure Client Status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, click **Client Status**, then, in the **Home** tab, in the **Client Status** group, click **Client Status Settings**.  

3.  In the **Client Status Settings Properties** dialog box, specify the following values to determine client activity:  

    > [!NOTE]  
    >  If none of the settings are met, the client will be marked as inactive.  

    -   **Client policy requests during the following days:** Specify the number of days since a client requested policy. The default value is **7** days.  

    -   **Heartbeat discovery during the following days:** Specify the number of days since the client computer sent a heartbeat discovery record to the site database. The default value is **7** days.  

    -   **Hardware inventory during the following days:** Specify the number of days since the client computer has sent a hardware inventory record to the site database. The default value is **7** days.  

    -   **Software inventory during the following days:** Specify the number of days since the client computer has sent a software inventory record to the site database. The default value is **7** days.  

    -   **Status messages during the following days:** Specify the number of days since the client computer has sent status messages to the site database. The default value is **7** days.  

4.  In the **Client Status Settings Properties** dialog box, specify the following value to determine how long client status history data is retained:  

    -   **Retain client status history for the following number of days:** Specify how long you want the client status history to remain in the site database. The default value is **31** days.  

5.  Click **OK** to save the properties and to close the **Client Status Settings Properties** dialog box.  

##  <a name="BKMK_Schedule"></a> To Configure the Schedule for Client Status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, click **Client Status**, then, in the **Home** tab, in the **Client Status** group, click **Schedule Client Status Update**.  

3.  In the **Schedule Client Status Update** dialog box, configure the interval at which you want client status to update and then click OK.  

    > [!NOTE]  
    >  When you change the schedule for client status updates, the update will not take effect until the next scheduled client status update (for the previously configured schedule).  

##  <a name="BKMK_2"></a> To Configure Alerts for Client Status  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**.  

3.  In the **Device Collections** list, select the collection for which you want to configure alerts and then, in the **Home** tab, in the **Properties** group, click **Properties**.  

    > [!NOTE]  
    >  You cannot configure alerts for user collections.  

4.  On the **Alerts** tab of the *&lt;collection Name\>***Properties** dialog box, click **Add**.  

    > [!NOTE]  
    >  The **Alerts** tab is only visible if the security role you are associated with has permissions for alerts.  

5.  In the **Add New Collection Alerts** dialog box, choose the alerts that you want generated when client status thresholds fall below a specific value, then click **OK**.  

6.  In the **Conditions** list of the **Alerts** tab, select each client status alert and then specify the following information.  

    -   **Alert Name** - Accept the default name or enter a new name for the alert.  

    -   **Alert Severity** - From the drop-down list, choose the alert level that will be displayed in the Configuration Manager console.  

    -   **Raise alert** - Specify the threshold percentage for the alert.  

7.  Click **OK** to close the *&lt;collection Name\>***Properties** dialog box.  

##  <a name="BKMK_3"></a> To Exclude Computers from Automatic Remediation  

1.  Open the registry editor on the client computer for which you want to disable automatic remediation.  

    > [!WARNING]  
    >  If you use the Registry Editor incorrectly, you might cause serious problems that could require you to reinstall your operating system. Microsoft cannot guarantee that you can solve problems that result from using the Registry Editor incorrectly. Use the Registry Editor at your own risk.  

2.  Navigate to **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3.  Enter one of the following values for this registry key:  

    -   **True** - The client computer will not automatically remediate any problems that are found. However, you will still be alerted in the **Monitoring** workspace about any problems with this client.  

    -   **False** - The client computer will automatically remediate problems when they are found and you will be alerted in the **Monitoring** workspace. This is the default setting.  

4.  Close the registry editor.  

 You can also install clients using the CCMSetup **NotifyOnly** installation property to exclude them from automatic remediation. For more information about this client installation property, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  
