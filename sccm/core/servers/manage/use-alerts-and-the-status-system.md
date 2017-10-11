---
title: "Alerts and the status system"
titleSuffix: "Configuration Manager"
description: "Configure alerts, and use the status system to remain informed about the state of your Configuration Manager deployment."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
caps.latest.revision: 10
author: Brendunsms.author: brendunsmanager: angrobe

---
# Use alerts and the status system for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Configure Alerts, and use the built-in Status System to remain informed about the state of your System Center Configuration Manager deployment.  


##  <a name="bkmk_Status"></a> Status system  
 All major site components generate status messages that provide feedback on site and hierarchy operations.    This information can keep you informed about the health of different site processes. You can tune the alert system to ignore noise for known problems while increasing early visibility for other issues which might need your attention.  

 By default, the Configuration Manager status system operates without configuration by using  settings that are suitable for most environments. However, you can configure the following:  

-   **Status Summarizers:** You can edit the status summarizers at each site to control the frequency of status messages that generate a status indicator change for the following four summarizers:  

    -   Application Deployment Summarizer  

    -   Application Statistics Summarizer  

    -   Component Status Summarizer  

    -   Site System Status Summarizer  

-   **Status Filter Rules:** You can create new status filter rules, modify the priority of rules, disable or enable rules, and delete unused rules at each site.  

    > [!NOTE]  
    >  Status filter rules do not support the use of environment variables to run external commands.  

-   **Status Reporting:** You can configure both server and client component reporting to modify how status messages are reported to the Configuration Manager status system, and specify where status messages are sent.  

    > [!WARNING]  
    >  Because the default reporting settings are appropriate for most environments, change them with caution. When you increase the level of status reporting by choosing to report all status details you can increase the amount of status messages to be processed which increases the processing load on the Configuration Manager site. If you decrease the level of status reporting you might limit the usefulness of the status summarizers.  

Because the status system maintains separate configurations for each site you must edit each site individually.  

###  <a name="bkmk_configstatus"></a> Procedures for configuring the status system  

##### To configure status summarizers  

1.  In the Configuration Manager console navigate to **Administration** > **Site Configuration** >**Sites**, and then select the site for which you want to configure the status system.  

2.  On the **Home** tab, in the **Settings** group, click **Status Summarizers**.  

3.  In the **Status Summarizers** dialog box, select the status summarizer that you want to configure, and then click **Edit** to open the properties for that summarizer. If you are editing the Application Deployment or Application Statistics summarizer, proceed with step 5. If you are editing the Component Status skip to step 6. If you are editing the Site System Status summarizer, skip to step 7.  

4.  Use the following steps after you open the property page for either the Application Deployment Summarizer or the Application Statistics Summarizer:  

    1.  On the **General** tab of the summarizers properties page configure the summarization intervals and then click **OK** to close the properties page.  

    2.  Click **OK** to close the **Status Summarizers** dialog box and complete this procedure.  

5.  Use the following steps after you open property pages for the Component Status Summarizer:  

    1.  On the **General** tab of the summarizers' properties page configure the replication and threshold period values.  

    2.  On the **Thresholds** tab, select the **Message type** you want to configure, and then click the name of a component in the **Thresholds** list.  

    3.  In the **Status Threshold Properties** dialog box, edit the warning and critical threshold values, and then click **OK**.  

    4.  Repeat steps 6.b and 6.c as needed and when you are finished, click **OK** to close the summarizer properties.  

    5.  Click **OK** to close the **Status Summarizers** dialog box and complete this procedure.  

6.  Use the following steps after you open the property pages for the Site System Status Summarizer:  

    1.  On the **General** tab of the summarizers' properties page configure the replication and schedule values.  

    2.  On the **Thresholds** tab, specify values for the **Default thresholds** to configure default thresholds for critical and warning status displays.  

    3.  To edit the values for specific **Storage objects**, select the object from the **Specific thresholds** list, and then click the **Properties** button to access and edit the storage objects warning and critical thresholds. Click **OK** to close the storage objects properties.  

    4.  To create a new storage object, click the **Create Object** button and specify the storage objects values. Click **OK** to close the objects properties.  

    5.  To delete a storage object, select the object and then click the **Delete** button.  

    6.  Repeat steps 7.b through 7.e as needed. When you are finished, click **OK** to close the summarizer properties.  

    7.  Click **OK** to close the **Status Summarizers** dialog box and complete this procedure.  

##### To create a status filter rule  

1.  In the Configuration Manager console navigate to **Administration** > **Site Configuration** >**Sites**, and then select the site where you want to configure the status system.  

2.  On the **Home** tab, in the **Settings** group, click **Status Filter Rules**. The **Status Filter Rules** dialog box opens.  

3.  Click **Create**.  

4.  In the **Create Status Filter Rule Wizard**, on the **General** page, specify a name for the new status filter rule and message-matching criteria for the rule, and then click **Next**.  

5.  On the **Actions** page, specify the actions to be taken when a status message matches the filter rule, and then click **Next**.  

6.  On the **Summary** page review the details for the new rule, and then complete the wizard.  

    > [!NOTE]  
    >  Configuration Manager only requires that the new status filter rule has a name. If the rule is created but you do not specify any criteria to process status messages, the status filter rule will have no effect. This behavior allows you to create and organize rules before you configure the status filter criteria for each rule.  

##### To modify or delete a status filter rule  

1.  In the Configuration Manager console navigate to **Administration** > **Site Configuration** >**Sites**, and then select the site where you want to configure the status system.  

2.  On the **Home** tab, in the **Settings** group, click **Status Filter Rules**.  

3.  In the **Status Filter Rules** dialog box, select the rule that you want to modify and then take one of the following actions:  

    -   Click **Increase Priority** or **Decrease Priority** to change the processing order of the status filter rule. Then select another action or go to step 8 of this procedure to complete this task.  

    -   Click **Disable** or **Enable** to change the status of the rule. After you change the status of the rule, select another action or go to step 8 of this procedure to complete this task.  

    -   Click **Delete** if you want do delete the status filter rule from this site, and then click **Yes** to confirm the action. After you delete a rule, select another action or go to step 8 of this procedure to complete this task.  

    -   Click **Edit** if you want to change the criteria for the status message rule, and continue to step 5 of this procedure.  

4.  On the **General** tab of the status filter rule properties dialog box, modify the rule and message-matching criteria.  

5.  On the **Actions** tab, modify the actions to be taken when a status message matches the filter rule.  

6.  Click **OK** to save the changes.  

7.  Click **OK** to close the **Status Filter Rules** dialog box.  

##### To configure status reporting  

1.  In the Configuration Manager console navigate to **Administration** > **Site Configuration** > **Sites**, and then select the site where you want to configure the status system.  

2.  On the **Home** tab, in the **Settings** group, click **Configure Site Components**, and select **Status Reporting**.  

3.  In the **Status Reporting Component Properties** dialog box, specify the server and client component status messages that you want to report or log:  

    1.  Configure **Report** to send status messages to the Configuration Manager status message system.  

    2.  Configure **Log** to write the type and severity of status messages to the Windows event log.  

4.  Click **OK**.  

###  <a name="BKMK_MonitorSystemStatus"></a> Monitor the status system of Configuration Manager  
 **System status** in Configuration Manager provides an overview of the general operations of sites and site server operations of your hierarchy. It can reveal operational problems for site system servers or components, and you can use the system status to review specific details for different Configuration Manager operations. You monitor system status from the **System Status** node of the **Monitoring** workspace in the Configuration Manager console.  

 Most Configuration Manager site system roles and components generate status messages. Status messages details are logged in each components operational log, but are also submitted to the site database where they are summarized and presented in a general rollup of each component or site systems health. These status message rollups provide information details for regular operations and warnings and error details. You can configure the thresholds at which warnings or errors are triggered and fine-tune the system to ensure rollup information ignores known issues that are not relevant to you while calling attention to actual problems on servers or for component operations that you might want to investigate.  

 System status is replicated to other sites in a hierarchy as site data, not global data. This means you can only see the status for the site to which your Configuration Manager console connects, and any child sites below that site. Therefore, consider connecting your Configuration Manager console to the top-level site of your hierarchy when you view system status.  

 Use the following table to identify the different system status views and when to use each one.  

|Node|More information|  
|----------|----------------------|  
|Site Status|Use this node to view a rollup of the status of each site system to review the health of each site system server. Site system health is determined by thresholds that you configure for each site in the **Site System Status Summarizer**.<br /><br /> You can view status messages for each site system, set thresholds for status messages, and manage the operation of the components on site systems by using the **Configuration Manager Service Manager**.|  
|Component Status|Use this node to view a rollup of the status of each Configuration Manager component to review the component's operational health. Component health is determined by thresholds that you configure for each site in the **Component Status Summarizer**.<br /><br /> You can view status messages for each component, set thresholds for status messages, and manage the operation of components by using the **Configuration Manager Service Manager**.|  
|Conflicting Records|Use this node to view status messages about clients that might have conflicting records.<br /><br /> Configuration Manager uses the hardware ID to attempt to identify clients that might be duplicates and alert you to the conflicting records. For example, if you have to reinstall a computer, the hardware ID would be the same, but the GUID that Configuration Manager uses might be changed.|  
|Status Message Queries|Use this node to query status messages for specific events and related details. You can use status message queries to find the status messages related to specific events.<br /><br /> You can often use status message queries to identify when a specific component, operation, or Configuration Manager object was modified, and the account that was used to make the modification. For example, you can run the built-in query for **Collections Created, Modified, or Deleted** to identify when a specific collection was created, and the user account used to create the collection.|  

####  <a name="bkmk_managestatus"></a> Manage site status and component status  
 Use the following information to manage the site status and component status:  

-   To configure thresholds for the status system, see [Procedures for configuring the status system](#bkmk_configstatus).  

-   To manage individual components in Configuration Manager, use the **Configuration Manager Service Manager**.  

####  <a name="bkmk_view"></a> View status messages  
 You can view the status messages for individual site system servers and components.  

 To view status messages in the Configuration Manager console, select a specific site system server or component, and then click **Show Messages**. When you view messages, you can select to view specific message types or messages from a specified period of time, and you can filter the results based on the status messages details.  

##  <a name="bkmk_Alerts"></a> Alerts  
 Configuration Manager alerts are generated by some operations when a specific condition occurs.  

-   Typically, alerts are generated when an error occurs that you must resolve  

-   Alerts might be generated to warn you that a condition exists so that you can continue to monitor the situation  

-   Some alerts you configure, such as alerts for Endpoint Protection and client status, while other alerts are configured automatically  

-   You can configure subscriptions to alerts which can then send details by email, increasing awareness of key issues  

 Use the following table to find information about how to configure alerts and alert subscriptions in Configuration Manager:  


|Action|More Information|  
|------------|----------------------|  
|Configure Endpoint Protection alerts for a collection|See **How to Configure Alerts for Endpoint Protection in Configuration Manager** in [Configuring Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)|  
|Configure client status alerts for a collection|See  [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).|  
|Manage Configuration Manager alerts|See the section [Management tasks for alerts](#BKMK_Manage) in this topic.|  
|Configure email subscriptions to alerts|See the section [Management tasks for alerts](#BKMK_Manage) in this topic..|  
|Monitor alerts|See the section [Monitor alerts](#BKMK_MonitorAlerts)|  

###  <a name="BKMK_Manage"></a> Management tasks for alerts  

##### To manage general alerts  

1.  In the Configuration Manager console navigate to **Monitoring** > **Alerts**, and then select a management task.  

  Use the following table for more information about the management tasks that might require some information before you select them.  

|Management task|Details|  
    |---------------------|-------------|  
    |**Configure**|Opens the *&lt;alert name*\>**Properties** dialog box where you can modify the name, severity, and thresholds for the selected alert. If you change the severity of the alert, this configuration affects how the alerts are displayed in the Configuration Manager console.|  
    |**Edit Comment**|Enter a comment for the selected alerts. These comments display with the alert in the Configuration Manager console.|  
    |**Postpone**|Suspends the monitoring of the alert until the specified date is reached. At that time, the state of the alert is updated.<br /><br /> You can only postpone an alert when it is enabled.|  
    |**Create subscription**|Opens the **New Subscription** dialog box where you can create an email subscription to the selected alert.|  

##### To configure Endpoint Protection alerts for a collection  

1.  pending  

##### To configure client status alerts for a collection  

1.  In the Configuration Manager console, click **Assets and Compliance** >   **Device Collections**.  

2.  In the **Device Collections** list, select the collection for which you want to configure alerts and then, in the **Home** tab, in the **Properties** group, click **Properties**.  

    > [!NOTE]  
    >  You cannot configure alerts for user collections.  

3.  On the **Alerts** tab of the *&lt;Collection Name*\>**Properties** dialog box, click **Add**.  

    > [!NOTE]  
    >  The **Alerts** tab is only visible if the security role you are associated with has permissions for alerts.  

4.  In the **Add New Collection Alerts** dialog box, choose the alerts that you want generated when client status thresholds fall below a specific value, then click **OK**.  

5.  In the **Conditions** list of the **Alerts** tab, select each client status alert and then specify the following information.  

    -   **Alert Name** - Accept the default name or enter a new name for the alert.  

    -   **Alert Severity** - From the drop-down list, choose the alert level that will be displayed in the Configuration Manager console.  

    -   **Raise alert** - Specify the threshold percentage for the alert.  

6.  Click **OK** to close the *&lt;Collection Name*\>**Properties** dialog box.  

##### To configure email notification for alerts  

1.  In the Configuration Manager console navigate to **Monitoring** > **Alerts** > **Subscriptions**.  

2.  On the **Home** tab, in the **Create** group, click **Configure Email Notification**.  

3.  In the **Email Notification Component Properties** dialog box, specify the following information:  

    -   **Enable email notification for alerts**: Select this check box to enable Configuration Manager to use an SMTP server to send email alerts.  

    -   **FQDN or IP Address of the SMTP server to send email alerts**: Enter the fully qualified domain name (FQDN) or IP address and the SMTP port for the email server that you want to use for these alerts.  

    -   **SMTP Server Connection Account**: Specify the authentication method for Configuration Manager to use to connect the email server.  

    -   **Sender address for email alerts**: Specify the email address from which alert emails are sent.  

    -   **Test SMTP Server**: Sends a test email to the email address specified in **Sender address for email alerts**.  

4.  Click **OK** to save the settings and to close the **Email Settings Component Properties** dialog box.  

##### To subscribe to email alerts  

1.  In the Configuration Manager console navigate to **Monitoring** > **Alerts**.  

2.  Select an alert and then, on the **Home** tab, in the **Subscription** group, click **Create subscription**.  

3.  In the **New Subscription** dialog box, specify the following information:  

    -   **Name**: Enter a name to identify the email subscription. You can use up to 255 characters.  

    -   **Email address**: Enter the email addresses that you want the alert sent to. You can separate multiple email addresses with a semicolon.  

    -   **Email language**: In the list, specify the language for the email.  

4.  Click **OK** to close the **New Subscription** dialog box and to create the email subscription.  

    > [!NOTE]  
    >  You can delete and edit subscriptions in the **Monitoring** workspace when you expand the **Alerts** node, and then click the **Subscriptions** node.  

###  <a name="BKMK_MonitorAlerts"></a> Monitor alerts  
 You can view alerts in the **Alerts** node of the **Monitoring** workspace. Alerts have one of the following alert states:  

-   **Never triggered**: The condition of the alert has not been met.  

-   **Active**: The condition of the alert is met.  

-   **Canceled**: The condition of an active alert is no longer met. This state indicates that the condition that caused the alert is now resolved.  

-   **Postponed**: An administrative user has configured Configuration Manager to evaluate the state of the alert at a later time.  

-   **Disabled**: The alert has been disabled by an administrative user. When an alert is in this state, Configuration Manager does not update the alert even if the state of the alert changes.  

 You can take one of the following actions when Configuration Manager generates an alert:  

-   Resolve the condition that caused the alert, for example, you resolve a network issue or a configuration issue that generated the alert. After Configuration Manager detects that the issue no longer exists, the alert state changes to **Cancel**.  

-   If the alert is a known issue, you can postpone the alert for a specific length of time. At that time, Configuration Manager updates the alert to its current state.  

     You can postpone an alert only when it is active.  

-   You can edit the **Comment** of an alert so that other administrative users can see that you are aware of the alert. For example, in the comment you can identify how to resolve the condition, provide information about the current status of the condition, or explain why you postponed the alert.  
