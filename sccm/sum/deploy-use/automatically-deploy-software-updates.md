---
title: Automatically deploy software updates
description: "Automatically deploy software updates by adding new updates to an update group that's associated with an active deployment or by using ADRs."
keywords:
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
---

#  <a name="BKMK_AutoDeploy"></a> Automatically deploy software updates  

*Applies to: System Center Configuration Manager (Current Branch)*

 You can automatically deploy software updates by adding new software updates to an update group associated with an active deployment or you can use an automatic deployment rule (ADR). Typically, you will use ADRs to deploy monthly software updates (generally known as Patch Tuesday updates) and for managing definition updates. If you need help to determine which deployment method is right for you, see [Deploy software updates](deploy-software-updates.md)

##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
After you create and deploy a software update group, you can add software updates to the update group and they will be automatically deployed.  

> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  

Use the following procedure to add software updates to an existing update group.  

#### To add software updates to an existing software update group  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates**.  

2.  Select the software updates that are to be added to the new software update group.  

3.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  

4.  Select the software update group to which you want to add the software updates as members.  

5.  Click the **Software Update Groups** node to display the software update group.  

6.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Create an automatic deployment rule (ADR)  
You can automatically approve and deploy software updates by using an ADR. You can have the rule add software updates to a new software update group each time the rule runs or add software updates to an existing group. When a rule runs and adds software updates to an existing group, the rule removes all software updates from the group and then adds the software updates that meet the criteria that you define to the group. To run an ADR to find newly released software updates each day and deploy them to clients, for example, you must choose the option to create a new software update group instead of adding the software updates to an existing group.  

> [!WARNING]  
>  Before you create an ADR for the first time, verify that software updates synchronization has completed at the site. This is particularly important when you run Configuration Manager with a non-English language because software update classifications are displayed in English before the first synchronization, and then displayed in the localized language after software update synchronization completes. Rules that you create before you synchronize software updates might not work properly after synchronization because the text string might not match.  

 Use the following procedure to create an ADR.  

#### To create an ADR  

1.  In the Configuration Manager console, navigate to **Software Library** **Overview** > **Software Updates** > **Automatic Deployment Rules**.  

2.  On the **Home** tab, in the **Create** group, click **Create Automatic Deployment Rule**. The Create Automatic Deployment Rule Wizard opens.  

3.  On the **General** page, configure the following settings:  

    -   **Name**: Specify the name for the ADR. The name must be unique, help to describe the objective of the rule, and identify it from others in the Configuration Manager site.  

    -   **Description**: Specify a description for the ADR. The description should provide an overview of the deployment rule and any other relevant information that helps to identify and differentiate the rule among others in the Configuration Manager site. The description field is optional, has a limit of 256 characters, and has a blank value by default.  

    -   **Select Deployment Template**: Specify whether to apply a previously saved deployment template. You can configure a deployment template to contain multiple common software update deployment properties that can then be used when creating ADRs. These templates help to ensure consistency across similar deployments and to save time.  

         You can select from the built-in software update deployment templates from the Automatic Deployment Rule Wizard. The **Definition Updates** template provides common settings to use when you deploy definition software updates. The **Patch Tuesday** template provides common settings to use when you deploy software updates on a monthly cycle.  

    -   **Collection**: Specifies the target collection to be used for the deployment. Members of the collection receive the software updates that are defined in the deployment.  

    -   Decide whether to add software updates to a new or existing software update group. In most cases, you will probably choose to create a new software update group when the ADR is run. However, you might choose to use an existing group if the rule runs on a more aggressive schedule. For example, if you will run the rule daily for definition updates, then you could add the software updates to an existing software update group.  

    -   **Enable the deployment after this rule is run**: Specify whether to enable the software update deployment after the ADR runs. Regarding this specification, consider the following:  

        -   When you enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group, the software update content is downloaded as necessary, the content is copied to the specified distribution points, and the software updates are deployed to the clients in the target collection.  

        -   When you do not enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group and the software updates deployment policy is configured but the software updates are not downloaded or deployed to clients. This situation provides you time as needed to prepare to deploy the software updates, verify that the software updates that meet the criteria are adequate, and then enable the deployment at a later time.  

4.  On the Deployment Settings page, configure the following settings:  

    -   **Use Wake-on-LAN to wake up clients for required deployments**: Specifies whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time will be awakened so the software update installation can initiate. Clients that are in sleep mode that do not require any software updates in the deployment are not started. By default, this setting is not enabled.  

        > [!WARNING]  
        >  Before you can use this option, you must configure computers and networks for Wake On LAN.  

    -   **Detail level**: Specify the level of detail for the state messages that are reported by client computers.  

        > [!IMPORTANT]  
        >  When you deploy definition updates, set the detail level to **Error only** to have the client report a state message only when a definition update fails to be delivered to the client. Otherwise, the client will report a large number of state messages that might impact performance on the site server.  

    -   **License terms setting**: Specify whether to automatically deploy software updates with associated license terms. Some software updates include license terms, such as a service pack. When you automatically deploy software updates, the license terms are not displayed and there is not an option to accept the license terms. You can choose to automatically deploy all software updates regardless of an associated license terms or only deploy software updates that do not have associated license terms.  

        > [!NOTE]  
        >  To review the license terms for a software update, you can select the software update in the **All Software Updates** node of the **Software Library** workspace, and then on the **Home** tab, in the **Update** group, click **Review License**.  
        >   
        >  To find software updates with associated license terms, you can add the **License Terms** column to the results pane in the **All Software Updates** node, and then click the heading for the column to sort by the software updates with license terms.  

5.  On the Software Updates page, configure the criteria for the software updates that the ADR retrieves and adds to the software update group.  

    > [!IMPORTANT]  
    >  The limit for software updates in the ADR is 1000 software updates. To ensure that the criteria that you specify on this page retrieves less than 1000 software updates, consider setting the same criteria on the **All Software Updates** node in the **Software Library** workspace.  

    > [!NOTE]
    > Starting in Configuration Manager version 1610, you can filter on the content size for software updates in automatic deployment rules. For example, you can set the **Content Size (KB)** filter to **< 2048** to only download software updates that are smaller than 2MB. Using this filter prevents large software updates from automatically downloading to better support simplified Windows down-level servicing when network bandwidth is limited. For details, see [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

6.  On the Evaluation Schedule page, specify whether to enable the ADR to run on a schedule. When enabled, click **Customize** to set the recurring schedule.  

    > [!IMPORTANT]  
    >  The software update point synchronization schedule is displayed to help you determine the frequency of the evaluation schedule. You should never set the evaluation schedule with a frequency that exceeds the software updates synchronization schedule. The start time configuration for the schedule is based on the local time of the computer that runs the Configuration Manager console.  

    > [!NOTE]  
    >  To manually run the ADR, select the rule, and then click **Run Now** on the **Home** tab in the **Automatic Deployment Rule** group. Before you manually run the ADR, verify that software updates synchronization has been run since the last time you ran the rule.  

    > [!IMPORTANT]  
    >  The ADR evaluation can run as often as three times per day.  

7.  On the Deployment Schedule page, configure the following settings:  

    -   **Schedule evaluation**: Specify whether Configuration Manager evaluates the available time and installation deadline times by using UTC or the local time of the computer that runs the Configuration Manager console.  

        > [!NOTE]  
        >  When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.  

    -   **Software available time**: Select one of the following settings to specify when the software updates are available to clients:  

        -   **As soon as possible**: Select this setting to make the software updates that are included in the deployment available to the client computers as soon as possible. When you create the deployment with this setting selected, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become  aware of the deployment and can obtain the updates that are available for installation.  

        -   **Specific time**: Select this setting to make the software updates that are included in the deployment available to the client computers at a specific date and time. When you create the deployment with this setting enabled, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become aware of the deployment. However, the software updates in the deployment are not available for installation until after the configured date and time.  

    -   **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment:  

        -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  

        -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time. Configuration Manager determines the deadline to install software updates by adding the configured **Specific time** interval to the **Software available time**.  

        > [!NOTE]  
        >  The actual installation deadline time is the displayed deadline time plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the software updates in the deployment at the same time.  
        >   
        >  You can configure the **Computer Agent** client setting **Disable deadline randomization** to disable the installation randomization delay for required software updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. On the User Experience page, configure the following settings:  

    -   **User notifications**: Specify whether to display notification of the software updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers.  

    -   **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the software update deployment. Specify whether to install the software updates in the deployment. Also specify whether to perform a system restart after software update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after software updates are installed and a system restart is required to complete the installation.  

        > [!IMPORTANT]  
        >  Suppressing system restarts can be useful in server environments or in cases in which you do not want the computers that are installing the software updates to restart by default. However, doing so can leave computers in an insecure state, whereas allowing a forced restart helps to ensure immediate completion of the software update installation.  

    -   **Write filter handling for Windows Embedded devices**: When you deploy software updates to Windows Embedded devices that are write filter enabled, you can specify to install the software update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

        > [!NOTE]  
        >  When you deploy a software update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  

    - **Software updates deployment re-evaluation behavior upon restart**: Starting in Configuration Manager version 1606, select this setting to configure software updates deployments to have clients run a software updates compliance scan immediately after a client installs software updates and restarts. This enables the client to check for additional software updates that become applicable after the client restarts, and to then install them (and become compliant) during the same maintenance window.

9. On the Alerts page, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment.  

    > [!NOTE]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  

10. On the Download Settings page, configure the following settings:  

    - Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  

    - Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  

    - **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates**: Select this setting to have clients that are connected to the intranet download software updates from Microsoft Update if software updates are not available on distribution points. Internet-based clients can always go to Microsoft Update for software updates content.

    - Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

    > [!NOTE]  
    >  Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you have configured the distribution point, deployment package, and the settings on this page. For more information, see [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. On the Deployment Package page, select an existing deployment package or configure the following settings to create a new deployment package:  

    1.  **Name**: Specify the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

    2.  **Description**: Specify a description that provides information about the deployment package. The description is limited to 127 characters.  

    3.  **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

        > [!NOTE]  
        >  The deployment package source location that you specify cannot be used by another software deployment package.  

        > [!IMPORTANT]  
        >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

        > [!IMPORTANT]  
        >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

    4.  **Sending priority**: Specify the sending priority for the deployment package. Configuration Manager uses the sending priority for the deployment package when it sends the package to distribution points. Deployment packages are sent in priority order: High, Medium, or Low. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority.  

12. On the Distribution Points page, specify the distribution points or distribution point groups that will host the software update files. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  This page is available only when you create a new software update deployment package.  

13. On the Download Location page, specify whether to download the software update files from the Internet or from your local network. Configure the following settings:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from a specified location on the Internet. This setting is enabled by default.  

    -   **Download software updates from a location on the local network**: Select this setting to download the software updates from a local directory or shared folder. This setting is useful when the computer that runs the wizard does not have Internet access. Any computer with Internet access can preliminarily download the software updates and store them in a location on the local network that is accessible from the computer that runs the wizard.  

14. On the Language Selection page, select the languages for which the selected software updates are downloaded. The software updates are downloaded only if they are available in the selected languages. Software updates that are not language specific are always downloaded. By default, the wizard selects the languages that you have configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that are not supported by a software update, the download will fail for the software update.  

15. On the Summary page, review the settings. To save the settings to a deployment template, click **Save As Template**, enter a name and select the settings that you want to include in the template, and then click **Save**. To change a configured setting, click the associated wizard page and change the setting.  

    > [!NOTE]  
    >  The template name can consist of alphanumeric ASCII characters as well as **\\** (backslash) or **‘** (single quotation mark).  

16. Click **Next** to create the ADR.  

 After you have completed the wizard, the ADR will run. It will add the software updates that meet the specified criteria to a software update group, download the software updates to the content library on the site server, distribute the software updates to the configured distribution points, and then deploy the software update group to clients in the target collection.  

##  <a name="BKMK_AddDeploymentToADR"></a> Add a new deployment to an existing ADR  
 After you create an ADR, you can add additional deployments to the rule. This can help you manage the complexity of deploying different updates to different collections. Each new deployment has the full range of functionality and deployment monitoring experience.  

#### To add a new deployment to an existing ADR  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates** > **Automatic Deployment Rules**, and then select the desired rule.  

2.  On the **Home** tab, in the **Automatic Deployment Rule** group, click **Add Deployment**. The Add Deployment Wizard opens.  

3.  On the **Collection** page, configure the following settings:  

    -   **Collection**: Specifies the target collection to be used for the deployment. Members of the collection receive the software updates that are defined in the deployment.  

    -   **Enable the deployment after this rule is run**: Specify whether to enable the software update deployment after the ADR runs. Regarding this specification, consider the following:  

        -   When you enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group, the software update content is downloaded as necessary, the content is copied to the specified distribution points, and the software updates are deployed to the clients in the target collection.  

        -   When you do not enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group and the software updates deployment policy is configured but the software updates are not downloaded or deployed to clients. This situation provides you time as needed to prepare to deploy the software updates, verify that the software updates that meet the criteria are adequate, and then enable the deployment at a later time.  

4.  On the Deployment Settings page, configure the following settings:  

    -   **Use Wake-on-LAN to wake up clients for required deployments**: Specifies whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time will be awakened so the software update installation can initiate. Clients that are in sleep mode that do not require any software updates in the deployment are not started. By default, this setting is not enabled.  

        > [!WARNING]  
        >  Before you can use this option, you must configure computers and networks for Wake On LAN.  

    -   **Detail level**: Specify the level of detail for the state messages that are reported by client computers.  

        > [!IMPORTANT]  
        >  When you deploy definition updates, set the detail level to **Error only** to have the client report a state message only when a definition update fails to be delivered to the client. Otherwise, the client will report a large number of state messages that might impact performance on the site server.  

5.  On the Deployment Schedule page, configure the following settings:  

    -   **Schedule evaluation**: Specify whether Configuration Manager evaluates the available time and installation deadline times by using UTC or the local time of the computer that runs the Configuration Manager console.  

        > [!NOTE]  
        >  When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.  

    -   **Software available time**: Select one of the following settings to specify when the software updates are available to clients:  

        -   **As soon as possible**: Select this setting to make the software updates that are included in the deployment available to the client computers as soon as possible. When you create the deployment with this setting selected, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become  aware of the deployment and can obtain the updates that are available for installation.  

        -   **Specific time**: Select this setting to make the software updates that are included in the deployment available to the client computers at a specific date and time. When you create the deployment with this setting enabled, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become aware of the deployment. However, the software updates in the deployment are not available for installation until after the configured date and time.  

    -   **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment:  

        -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  

        -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time. Configuration Manager determines the deadline to install software updates by adding the configured **Specific time** interval to the **Software available time**.  

        > [!NOTE]  
        >  The actual installation deadline time is the displayed deadline time plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the software updates in the deployment at the same time.  
        >   
        >  You can configure the **Computer Agent** client setting **Disable deadline randomization** to disable the installation randomization delay for required software updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  On the User Experience page, configure the following settings:  

    -   **User notifications**: Specify whether to display notification of the software updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers.  

    -   **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the software update deployment. Specify whether to install the software updates in the deployment. Also specify whether to perform a system restart after software update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after software updates are installed and a system restart is required to complete the installation.  

        > [!IMPORTANT]  
        >  Suppressing system restarts can be useful in server environments or in cases in which you do not want the computers that are installing the software updates to restart by default. However, doing so can leave computers in an insecure state, whereas allowing a forced restart helps to ensure immediate completion of the software update installation.  

    -   **Write filter handling for Windows Embedded devices**: When you deploy software updates to Windows Embedded devices that are write filter enabled, you can specify to install the software update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

        > [!NOTE]  
        >  When you deploy a software update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  

7.  On the Alerts page, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment.  

    > [!WARNING]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  

8. On the Download Settings page, configure the following settings:  

    - Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  

    - Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  

    - **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates**: Select this setting to have clients that are connected to the intranet download software updates from Microsoft Update if software updates are not available on distribution points. Internet-based clients can always go to Microsoft Update for software updates content.

    - Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

    > [!NOTE]  
    > Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you have configured the distribution point, deployment package, and the settings on this page. For more information, see [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## Next steps
[Monitor software updates](monitor-software-updates.md)
