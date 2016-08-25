---
title: "How to create remote connection profiles in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
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
# How to create remote connection profiles in System Center Configuration Manager
Use the following required steps to create a remote connection profile by using the System Center Configuration Manager**Create Remote Connection Profile Wizard**.  
  
 Before you use this procedure, ensure you have read the introductory information and prerequisites in [Working with remote connection profiles in System Center Configuration Manager](../../compliance/plan-design/working-with-remote-connection-profiles.md).  
  
## Create and deploy a remote connection profile  
  
#### To create a remote connection profile  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then click **Remote Connection Profiles**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Remote Connection Profile**.  
  
4.  On the **General** page of the **Create Remote Connection Profile Wizard**, specify a name and optional description for the profile using a maximum of 256 characters for each.  
  
5.  On the **Profile** settings page of the wizard, specify the following settings for the remote connection profile:  
  
    -   **Full name and port of the Remote Desktop Gateway server (optional)** - Specify the name of the Remote Desktop Gateway Server to be used for connections.  
  
        > [!NOTE]  
        >  Configuration Manager does not support an internationalized domain name to be used to specify a server in this box.  
        >   
        >  The server name must be no longer than 256 characters and can contain uppercase characters, lowercase characters, numeric characters, and the **–** and **_** characters, which are separated by periods.  
  
    -   **Allow connections only from computers that run Remote Desktop with Network Level Authentication**  
  
6.  Select **Enabled** or **Disabled** for each of the following connection settings:  
  
    -   **Allow remote connections to work computers**  
  
    -   **Allow all primary users of the work computer to remotely connect**  
  
    -   **Allow Windows Firewall exception for connections on Windows domains and on private networks**  
  
    > [!IMPORTANT]  
    >  All three settings must be the same before you can proceed past this page of the wizard.  
  
7.  On the **Summary** page of the wizard, review the actions to be taken, and then complete the wizard.  
  
 The new remote connection profile is displayed in the **Remote Connection Profiles** node in the **Assets and Compliance** workspace.  
  
#### To deploy a remote connection profile  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then click Remote Connection Profiles.  
  
3.  In the **Remote Connection Profiles** list, select the remote connection profile that you want to deploy, and then, in the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
4.  In the **Deploy Remote Connection Profile** dialog box, specify the following information:  
  
    -   **Collection** - Click **Browse** to select the device collection where you want to deploy the remote connection profile.  
  
    -   **Remediate noncompliant rules when supported** - Enable this option to automatically remediate the remote connection profile when it is found to be noncompliant on a device, for example, when it is not present.  
  
    -   **Allow remediation outside the maintenance window** - If a maintenance window has been configured for the collection to which you deploy the remote connection profile, enable this option to let Configuration Manager remediate the remote connection profile outside the maintenance window. For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  
  
    -   **Generate an alert** - Enable this option to configure an alert that is generated if the remote connection profile compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.  
  
    -   **Specify the compliance evaluation schedule for this configuration baseline** - Specify the schedule by which the deployed remote connection profile is evaluated on devices. You can specify either a simple or a custom schedule.  
  
    > [!TIP]  
    >  If a device leaves a collection to which a remote connection profile has been deployed, the remote connection profile settings are disabled on the device. However, for this process to occur correctly, you must have already deployed at least one configuration item or configuration baseline that contains a configuration item from your site.  
    >   
    >  The profile is evaluated by devices when the user logs on.  
    >   
    >  If two remote connection profiles are deployed to the same device collection, where in one profile **Remediate noncompliant rules when supported** is checked and in the other profile, the same option is not checked, and the two remote connection profiles contain different connection settings, then the profile in which the option is not checked might override the settings in the other profile. This type of remote connection profile deployment is not supported by Configuration Manager.  
  
5.  Click **OK** to close the **Deploy Remote Connection Profile** dialog box and to create the deployment.  
  
## Monitor a remote connection profile  
  
### View compliance results in the Configuration Manager console  
  
1.  In the Configuration Manager console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, click **Deployments**.  
  
3.  In the **Deployments** list, select the remote connection profile deployment for which you want to review compliance information.  
  
4.  You can review summary information about the compliance of the remote connection profile deployment on the main page. To view more detailed information, select the remote connection profile deployment, and then on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  
  
     The **Deployment Status** page contains the following tabs:  
  
    -   **Compliant:** Displays the compliance of the remote connection profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace. This node contains all devices that are compliant with the remote connection profile. The **Asset Details** pane also displays the devices that are compliant with this profile. Double-click a device in the list to display additional information.  
  
        > [!IMPORTANT]  
        >  A remote connection profile is not evaluated if it is not applicable on a client device. However, it is returned as compliant.  
  
    -   **Error:** Displays a list of all errors for the selected remote connection profile deployment based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all devices that generated errors with this profile. When you select a device, the **Asset Details** pane displays the devices that the selected issue affects. Double-click a device in the list to display additional information about the issue.  
  
    -   **Non-Compliant:** Displays a list of all noncompliant rules within the remote connection profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all devices that are not compliant with this profile. When you select a device, the **Asset Details** pane displays the devices that the selected issue affects. Double-click a device in the list to display additional information about the issue.  
  
    -   **Unknown:** Displays a list of all devices that did not report compliance for the selected remote connection profile deployment, together with the current client status of the devices.  
  
5.  On the **Deployment Status** page, you can review detailed information about the compliance of the deployed remote connection profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  
  
### View compliance results with reports  
 Configuration Manager includes built-in reports that you can use to monitor information about remote connection profiles. These reports have the report category of **Compliance and Settings Management**.  
  
> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the reports for compliance settings.  
  
 For more information about how to configure reporting in Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## See Also  
 [Compliance settings technical reference for System Center Configuration Manager](../../compliance/deploy-use/compliance-settings-technical-reference.md)