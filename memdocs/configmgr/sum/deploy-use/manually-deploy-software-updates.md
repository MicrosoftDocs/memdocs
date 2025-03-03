---
title: Manually deploy software updates
titleSuffix: Configuration Manager
description: Manually create software deployments to get your clients up-to-date with required software updates, or to deploy out-of-band updates.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 04/08/2022
ms.topic: install-set-up-deploy
ms.service: configuration-manager
ms.subservice: software-updates
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manually deploy software updates  

*Applies to: Configuration Manager (current branch)*

A manual software update deployment is the process of selecting software updates from the Configuration Manager console and manually starting the deployment process. Or add selected software updates to an update group, and then manually deploy the update group. You typically use manual deployments to get your clients up-to-date with required software updates. You then use automatic deployment rules (ADR) to manage ongoing monthly software update deployments. Also use this manual method to deploy out-of-band software updates. For more information on which deployment method is right for you, see [Deploy software updates](deploy-software-updates.md).



##  <a name="BKMK_1SearchCriteria"></a> Step 1: Specify search criteria for software updates  

Depending upon the combinations of products and classifications that your site synchronizes, there are potentially thousands of software updates displayed in the Configuration Manager console. The first step in the workflow for manually deploying software updates is to identify the software updates that you want to deploy. For example, show all software updates required on more than 50 client devices with a **Security** or **Critical** classification.  

> [!IMPORTANT]  
>  A single software update deployment has a limit of 1000 software updates.  

### Process to specify search criteria for software updates  

1.  In the Configuration Manager console, go to the **Software Library** workspace, expand **Software Updates**, and click **All Software Updates**. This node displays all synchronized software updates.  

    > [!NOTE]  
    >  The **All Software Updates** node only displays software updates with a **Critical** and **Security** classification that have been released in the last 30 days.  

2.  In the search pane, filter to identify the software updates that you need. Use one or both of the following options:  

    -   In the search text box, type a search string that filters the software updates. For example, type the article or bulletin ID for a specific software update. Or enter a string that appears in the title of several software updates.  

    -   Click **Add Criteria**, and select the criteria to filter software updates. Click **Add**, and then provide the values for the criteria.  

3.  Click **Search** to filter the software updates.  

    > [!TIP]  
    >  Save frequently used filter criteria. On the ribbon, click the option to **Save Current Search**. Retrieve previous searches by clicking on **Saved Searches**.   



##  <a name="BKMK_2UpdateGroup"></a> Step 2: Create a software update group that contains the software updates   

Software update groups let you organize software updates in preparation for deployment. Use the following procedure to manually add software updates to a new software update group.  

### Process to manually add software updates to a new software update group  

1.  In the Configuration Manager console, go to the **Software Library** workspace, and select **Software Updates**. Select the desired software updates.  

2.  Click **Create Software Update Group** in the ribbon.  

3.  Specify the name for the software update group and optionally provide a description. Use a name and description that provide enough information for you to determine what type of updates are in the software update group. Click **Create**.  

4.  Select the **Software Update Groups** node, and select the new software update group. To display the list of updates in the group, click **Show Members** in the ribbon.  



##  <a name="BKMK_3DownloadContent"></a> Step 3: Download the content for the software update group  

Before you deploy the software updates, download the content for the software updates in the software update group. This step lets you verify that the content is available on distribution points before you deploy the software updates. It also helps you avoid any unexpected issues with content distribution. If you skip this step, as part of the deployment process the site downloads the content and distributes to the distribution points. Use the following procedure to download the content for software updates in the software update group.  


### Process to download content for the software update group
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### Process to monitor content status
1. To monitor the content status for the software updates, go to the **Monitoring** workspace in the Configuration Manager console. Expand **Distribution Status**, and then select the **Content Status** node.  

2. Select the software update package that you previously identified to download the software updates in the software update group.  

3. Click **View Status** in the ribbon.  



##  <a name="BKMK_4DeployUpdateGroup"></a> Step 4: Deploy the software update group  

After you determine the updates you want to deploy, and add them to a software update group, manually deploy the software update group.  

### Process to manually deploy the software updates in a software update group  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Software Updates**, and select the **Software Update Groups** node.  

2. Select the software update group that you want to deploy. Click **Deploy** in the ribbon.   

3. On the **General** page of the Deploy Software Updates Wizard, configure the following settings:  

   -   **Name**: Specify the name for the deployment. The deployment must have a unique name that describes its purpose, and differentiates it from other deployments in the site. This name field has a limit of 256 characters. By default, Configuration Manager automatically provides a name for the deployment in the following format: `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Description**: Specify a description for the deployment. The description is optional, but provides an overview of the deployment. Include any other relevant information that helps to identify and differentiate it among others in the site. The description field has a limit of 256 characters, and has a blank value by default.  

   -   **Software Update/Software Update Group**: Verify that the displayed software update group or software update is correct.  

   -   **Select Deployment Template**: Specify whether to apply a previously saved deployment template. Configure a deployment template to save common software update deployment properties. Then apply the template when you deploy software updates in the future. These templates save time and help to ensure consistency across similar deployments.  

   -   **Collection**: Specify the collection for the deployment. Devices in the collection receive the software updates in this deployment.  

4. On the **Deployment Settings** page, configure the following settings:  

   -   **Type of deployment**: Specify the deployment type for the software update deployment.  

       > [!IMPORTANT]  
       >  After you create the software update deployment, you can't change the type of deployment.  

        - Select **Required** to create a mandatory software update deployment. The software updates are automatically installed on clients before the installation deadline you configure. When you deploy a software update group as **Required**, clients download the content in background and honor BITS settings, if configured.

        - Select **Available** to create an optional software update deployment. This deployment is available for users to install from Software Center. For software update groups deployed as **Available**, clients download the content in the foreground and ignore BITS settings.

       > [!NOTE]  
       > Starting in Configuration Manager version 2203, you can select the **Pre-download content for this deployment** setting for **Available** deployments. This setting reduces installation wait times for clients since installation notifications won't be visible in Software Center until the content has fully downloaded. <!--4497776-->
       > - If an update is in multiple deployments for a client and the **Pre-download content for this deployment** setting is enabled for a least one of the deployments, then the content will pre-download.
       > - If you edit an existing deployment to use the **Pre-download content for this deployment** setting, the content will only pre-download if the software update is not yet available on the client.

   -   **Use Wake-on-LAN to wake up clients for required deployments**: Specifies whether to enable Wake On LAN at the deadline. Wake On LAN sends wake-up packets to computers that require one or more software updates in the deployment. The site wakes up any computers that are in sleep mode at the installation deadline time so the installation can initiate. Clients that are in sleep mode that don't require any software updates in the deployment aren't started. By default, this setting isn't enabled. It's only available for **Required** deployments. Before using this option, configure computers and networks for Wake On LAN. For more information, see [How to configure Wake On LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Detail level**: Specify the level of detail for the state messages that clients report to the site.  

5. On the **Scheduling** page, configure the following settings:  

   -   **Schedule evaluation**: Specify the time that Configuration Manager evaluates the available time and installation deadline times. Choose to use Coordinated Universal Time (UTC) or the local time of the computer that runs the Configuration Manager console.  

       - When you select **Client local time** here, and then select **As soon as possible** for the **Software available time**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available. This behavior is the same with the **Installation deadline** and the time when updates are installed on a client. If the client is in a different time zone, these actions occur when the client's time reaches the evaluation time.  

   -   **Software available time**: Select one of the following settings to specify when the software updates are available to clients:  

       -   **As soon as possible**: Makes the software updates in the deployment available to clients as soon as possible. When you create the deployment with this setting selected, Configuration Manager updates the client policy. At the next client policy polling cycle, clients become aware of the deployment and the software updates are available for installation.  

       -   **Specific time**: Makes software updates included in the deployment available to clients at a specific date and time. When you create the deployment with this setting enabled, Configuration Manager updates the client policy. At the next client policy polling cycle, clients become aware of the deployment. However, the software updates in the deployment aren't available for installation until after the configured date and time.  

   -   **Installation deadline**: These options are only available for **Required** deployments. Select one of the following settings to specify the installation deadline for the software updates in the deployment  

       -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  

       -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time.  

           - The actual installation deadline time is the displayed deadline time plus a random amount of time up to two hours. The randomization reduces the potential impact of clients in the collection installing updates in the deployment at the same time.   

           - To disable the installation randomization delay for required software updates, configure the client setting to **Disable deadline randomization** in the **Computer Agent** group. For more information, see [Computer Agent client settings](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**: Enable this setting to give users more time to install required software updates beyond the deadline.  

       - This behavior is typically required when a computer is turned off for long time, and needs to install many software updates or applications. For example, when a user returns from vacation, they have to wait for a long time as the client installs overdue deployments.  

       - Configure this grace period with the property **Grace period for enforcement after deployment deadline (hours)** in client settings. For more information, see the [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) section. The enforcement grace period applies to all deployments with this option enabled and targeted to devices to which you also deployed the client setting.  

       - After the deadline, the client installs the software updates in the first non-business window, which the user configured, up to this grace period. However, the user can still open Software Center and install the software updates at any time. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments.  

6. On the **User Experience** page, configure the following settings:  

   -   **User notifications**: Specify whether to display notification in Software Center at the configured **Software available time**. This setting also controls whether to notify users on the client computers. For **Available** deployments, you can't select the option to **Hide in Software Center and all notifications**.  

   -   **Deadline behavior**: This setting is only configurable for **Required** deployments. Specify the behaviors when the software update deployment reaches the deadline outside of any defined maintenance windows. The options include whether to install the software updates, and whether to perform a system restart after installation. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md). 
  
       > [!Note]
       > This applies only when the maintenance window is configured for the client device. If no maintenance window is defined on the device, the update of the installation and restart will always happen after the deadline.

   -   **Device restart behavior**: This setting is only configurable for **Required** deployments. Specify whether to suppress a system restart on servers and workstations if a restart is required to complete update installation.  

       > [!WARNING]  
       >  Suppressing system restarts can be useful in server environments, or when you don't want the target computers to restart by default. However, doing so can leave computers in an insecure state. Allowing a forced restart helps to ensure immediate completion of the software update installation.  

   -   **Write filter handling for Windows Embedded devices**: This setting controls the installation behavior on Windows Embedded devices that are enabled with a write filter. Choose the option to commit changes at the installation deadline or during a maintenance window. When you select this option, a restart is required and the changes persist on the device. Otherwise, the update is installed, applied to the temporary overlay, and committed later.  

       -  When you deploy a software update to a Windows Embedded device, make sure the device is a member of a collection that has a configured maintenance window.  

   - **Software updates deployment re-evaluation behavior upon restart**: Select this setting to configure software updates deployments to have clients run a software updates compliance scan immediately after a client installs software updates and restarts. This setting enables the client to check for additional updates that become applicable after the client restarts, then installs them during the same maintenance window.  

7. On the **Alerts** page, configure how Configuration Manager generates alerts for this deployment. Review recent software updates alerts from Configuration Manager in the **Software Updates** node of the **Software Library** workspace. If you're also using System Center Operations Manager, configure its alerts as well. Only configure alerts for **Required** deployments.  

8. On the **Download Settings** page, configure the following settings:  

    > [!NOTE]  
    >  Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you've configured the distribution point, the deployment package, and the settings on this page.  

    - Specify if clients should download and install the updates when they use a distribution point from a neighbor or the default site boundary groups.  

    - Specify if clients should download and install the updates from a distribution point in the site default boundary group, when the content for the software updates isn't available from a distribution point in the current or neighbor boundary groups.  

    - **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information, see [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Starting in version 1802, BranchCache is always enabled on clients. This setting is removed, as clients use BranchCache if the distribution point supports it.  

    - **If software updates are not available on distribution point in current, neighbor or site boundary groups, download content from Microsoft Updates**: Select this setting to have intranet-connected clients download software updates from Microsoft Update if updates aren't available on distribution points. Internet-based clients always go to Microsoft Update for software updates content.

    - Specify whether to allow clients to download after an installation deadline when they use metered internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you're on a metered connection.  

9. On the **Deployment Package** page, select one of the following options:  

    > [!Note]  
    > If you already performed [Step 3: Download the content for the software update group](#BKMK_3DownloadContent), then the wizard doesn't display the **Deployment Package**, **Distribution Points**, and **Language Selection** pages. Skip to the [Summary](#bkmk_summary) page of the wizard.  
    > 
    >  Software updates that have been previously downloaded to the content library on the site server aren't downloaded again. This behavior is true even when you create a new deployment package for the software updates. If all software updates have already been downloaded, the wizard skips to the [Summary](#bkmk_summary) page.  

    - **Select a deployment package**: Add these updates to an existing deployment package.  

    - **Create a new deployment package**: Add these updates to a new deployment package. Configure the following additional settings:  

        -  **Name**: Specify the name of the deployment package. Use a unique name that describes the package content. It's limited to 50 characters.  

        -  **Description**: Specify a description that provides information about the deployment package. The optional description is limited to 127 characters.  

        -  **Package source**: Specify the location of the software update source files. Type a network path for the source location, for example, `\\server\sharename\path`, or click **Browse** to find the network location. Create the shared folder for the deployment package source files before you continue to the next page.  

            - You can't use the specified location as the source of another software deployment package.  

            - You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. If you do, first copy the content from the original package source to the new package source location.  

            -  The computer account of the SMS Provider and the user that's running the wizard to download the software updates must both have **Write** permissions to the download location. Restrict access to the download location. This restriction reduces the risk of attackers tampering with the software update source files.  

        -  **Sending priority**: Specify the sending priority for the deployment package. Configuration Manager uses this priority when it sends the package to distribution points. Deployment packages are sent in priority order: high, medium, or low. Packages with identical priorities are sent in the order in which they were created. If there's no backlog, the package processes immediately regardless of its priority.  

        - **Enable binary differential replication**: Enable this setting to minimize network traffic between sites. Binary differential replication (BDR) only updates the content that has changed in the package, instead of updating the entire package contents. For more information, see [Binary differential replication](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **No deployment package**: Starting in version 1806, deploy software updates to devices without first downloading and distributing content to distribution points. This setting is beneficial when dealing with extremely large update content. Also use it when you always want clients to get content from the Microsoft Update cloud service. Clients in this scenario can also download content from peers that already have the necessary content. The Configuration Manager client continues to manage the content download, thus can utilize the Configuration Manager peer cache feature, or other technologies such as Delivery Optimization. This feature supports any update type supported by Configuration Manager software updates management, including Windows and Office updates.<!--1357933-->  

10. On the **Distribution Points** page, specify the distribution points or distribution point groups to host the software update files. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > If you already performed [Step 3: Download the content for the software update group](#BKMK_3DownloadContent), then the wizard doesn't display the **Deployment Package**, **Distribution Points**, and **Language Selection** pages. Skip to the [Summary](#bkmk_summary) page of the wizard.  

11. On the **Download Location** page, specify whether to download the software update files from the internet or from your local network. Configure the following settings:  

    -   **Download software updates from the internet**: Select this setting to download the software updates from a specified location on the internet. This setting is enabled by default.  

    -   **Download software updates from a location on the local network**: Select this setting to download the software updates from a local directory or shared folder. This setting is useful when the computer that runs the wizard doesn't have internet access. Any computer with internet access can preliminarily download the software updates. Then store them in a location on the local network that's accessible from the computer that runs the wizard.  

12. On the **Language Selection** page, select the languages for which the site downloads the selected software updates. The site only downloads these updates if they're available in the selected languages. Software updates that aren't language-specific are always downloaded. By default, the wizard selects the languages that you've configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that a software update doesn't support, the download fails for the update.  

    > [!Note]  
    > If you already performed [Step 3: Download the content for the software update group](#BKMK_3DownloadContent), then the wizard doesn't display the **Deployment Package**, **Distribution Points**, and **Language Selection** pages. Skip to the [Summary](#bkmk_summary) page of the wizard.  

13. <a name="bkmk_summary"></a> On the **Summary** page, review the settings. To save the settings to a deployment template, click **Save As Template**. Enter a name and select the settings you want to include in the template, then click **Save**. To change a configured setting, click the associated wizard page and change the setting.  

    -  The template name can consist of alphanumeric ASCII characters as well as `\` (backslash) or `'` (single quotation mark).  

14. Click **Next** to deploy the software update.  

    After you complete the wizard, Configuration Manager downloads the software updates to the content library on the site server. It then distributes the content to the configured distribution points, and deploys the software update group to clients in the target collection. For more information about the deployment process, see [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## Next steps
[Monitor software updates](monitor-software-updates.md)
