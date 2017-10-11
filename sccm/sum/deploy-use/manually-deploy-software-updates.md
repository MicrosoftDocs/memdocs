---

title: Manually deploy software updates
titleSuffix: "Configuration Manager"
description: "To deploy updates manually, select updates from the Configuration Manager console and manually deploy them, or add updates to an update group and deploy the group."
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
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf

---

#  <a name="BKMK_ManualDeploy"></a> Manually deploy software updates  

*Applies to: System Center Configuration Manager (Current Branch)*

 A manual software update deployment is the process of selecting software updates from the Configuration Manager console and manually initiating the deployment process. Or, you can add selected software updates to an update group, and then manually deploy the update group. You will typically use manual deployment to get your client devices up-to-date with required software updates before you create ADRs that will manage ongoing monthly software update deployments. You will also use a manual method to deploy out-of-band software updates. If you need help to determine which deployment method is right for you, see [Deploy software updates](deploy-software-updates.md).

 The following sections provide the steps to manually deploy software updates.  

##  <a name="BKMK_1SearchCriteria"></a> Step 1: Specify search criteria for software updates  
 There are potentially thousands of software updates displayed in the Configuration Manager console. The first step in the workflow for manually deploying software updates is to identify the software updates that you want to deploy. For example, you could provide criteria that retrieves all software updates that are required on more than 50 client devices and that have a **Security** or **Critical** software update classification.  

> [!IMPORTANT]  
>  The maximum number of software updates that can be included in a single software update deployment is 1000.  

#### To specify search criteria for software updates  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **All Software Updates**. The synchronized software updates are displayed.  

    > [!NOTE]  
    >  On the **All Software Updates** node, Configuration Manager displays only software updates with a **Critical** and **Security** classification and have been released in the last 30 days.  

3.  In the search pane, filter to identify the software updates that you need by using one or both of the following steps:  

    -   In the search text box, type a search string that will filter the software updates. For example, type the article ID or bulletin ID for a specific software update, or enter a string that would appear in the title for several software updates.  

    -   Click **Add Criteria**, select the criteria that you want to use to filter software updates, click **Add**, and then provide the values for the criteria.  

4.  Click **Search** to filter the software updates.  

    > [!TIP]  
    >  You have the option to save the filter criteria on the **Search** tab and in the **Save** group.  

##  <a name="BKMK_2UpdateGroup"></a> Step 2: Create a software update group that contains the software updates  
 Software update groups provide an effective method for you to organize software updates in preparation for deployment. You can manually add software updates to a software update group or Configuration Manager can automatically add software updates to a new or existing software update group by using an ADR. Use the following procedures to manually add software updates to a new software update group.  

#### To manually add software updates to a new software update group  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, click **Software Updates**.  

3.  Select the software updates that are to be added to the new software update group.  

4.  On the **Home** tab, in the **Update** group, click **Create Software Update Group**.  

5.  Specify the name for the software update group and optionally provide a description. Use a name and description that provide enough information for you to determine what type of software updates are in the software update group. To proceed, click **Create**.  

6.  Click the **Software Update Groups** node to display the new software update group.  

7.  Select the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates that are included in the group.  

##  <a name="BKMK_3DownloadContent"></a> Step 3: Download the content for the software update group  
 Optionally, before you deploy the software updates, you can download the content for the software updates that are included in the software update group. You might choose to do this so you can verify that the content is available on the distribution points before you deploy the software updates. This will help you to avoid any unexpected issues with the content delivery. You can skip this step and the content will be downloaded and copied to the distribution points as part of the deployment process. Use the following procedure to download the content for software updates in the software update group.  



#### To download content for the software update group
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### To monitor content status
1. To monitor the content status for the software updates, click **Monitoring** in the Configuration Manager console.  

2. In the Monitoring workspace, expand **Distribution Status**, and then click **Content Status**.  

3. Select the software update package that you previously identified to download the software updates in the software update group.  

4. On the **Home** tab, in the **Content** group, click **View Status**.  

##  <a name="BKMK_4DeployUpdateGroup"></a> Step 4: Deploy the software update group  
 After you determine which software updates you intend to deploy and add these software updates to a software update group, you can manually deploy the software updates in the software update group. Use the following procedure to manually deploy the software updates in a software update group.  

#### To manually deploy the software updates in a software update group  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group that you intend to deploy.  

4.  On the **Home** tab, in the **Deployment** group, click **Deploy**. The **Deploy Software Updates Wizard** opens.  

5.  On the General page, configure the following settings:  

    -   **Name**: Specify the name for the deployment. The deployment must have a unique name that describes the purpose of the deployment, and differentiates it from other deployments in the Configuration Manager site. By default, Configuration Manager automatically provides a name for the deployment in the following format: **Microsoft Software Updates -** <*date*><*time*>  

    -   **Description**: Specify a description for the deployment. The description provides an overview of the deployment and any other relevant information that helps to identify and differentiate the deployment among others in Configuration Manager site. The description field is optional, has a limit of 256 characters, and has a blank value by default.  

    -   **Software Update/Software Update Group**: Verify that the displayed software update group, or software update, is correct.  

    -   **Select Deployment Template**: Specify whether to apply a previously saved deployment template. You can configure a deployment template to contain  multiple common software update deployment properties and then apply the template when you deploy subsequent software updates to ensure consistency across similar deployments and to save time.  

    -   **Collection**: Specify the collection for the deployment, as applicable. Members of the collection receive the software updates that are defined in the deployment.  

6.  On the Deployment Settings page, configure the following settings:  

    -   **Type of deployment**: Specify the deployment type for the software update deployment. Select **Required** to create a mandatory software update deployment in which the software updates are automatically installed on clients before a configured installation deadline. Select **Available** to create an optional software update deployment that is available for users to install from Software Center.  

        > [!IMPORTANT]  
        >  After you create the software update deployment, you cannot later change the type of deployment.  

        > [!NOTE]  
        >  A software update group deployed as **Required** will be downloaded in background and honor  BITS settings, if configured.  
        > However, software update groups deployed as **Available** will be downloaded in the foreground and will ignore BITS settings.  

    -   **Use Wake-on-LAN to wake up clients for required deployments**: Specify whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time will be awakened  so the software update installation can initiate. Clients that are in sleep mode that do not require any software updates in the deployment are not started. By default, this setting is not enabled and is available only when **Type of deployment** is set to **Required**.  

        > [!WARNING]  
        >  Before you can use this option, computers and networks must be configured for Wake On LAN.  

    -   **Detail level**: Specify the level of detail for the state messages that are reported by client computers.  

7.  On the Scheduling page, configure the following settings:  

    -   **Schedule evaluation**: Specify whether the available time and installation deadline times are evaluated according to UTC or the local time of the computer running the Configuration Manager console.  

        > [!NOTE]  
        >  When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.  

    -   **Software available time**: Select one of the following settings to specify when the software updates will be available to clients:  

        -   **As soon as possible**: Select this setting to make the software updates in the deployment available to clients as soon as possible. When the deployment is created, the client policy is updated, the clients are made aware of the deployment at their next client policy polling cycle, and then the software updates are available for installation.  

        -   **Specific time**: Select this setting to make the software updates in the deployment available to clients at a specific date and time. When the deployment is created, the client policy is updated and clients are made aware of the deployment at their next client policy polling cycle. However, the software updates in the deployment are not available for installation until after the specified date and time.  

    -   **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment.  

        > [!NOTE]  
        >  You can configure the installation deadline setting only when **Type of deployment** is set to **Required** on the Deployment Settings page.  

        -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  

        -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time.  

        > [!NOTE]  
        >  The actual installation deadline time is the specific time that you configure plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the software updates in the deployment at the same time.  
        >   
        >  You can configure the **Computer Agent** client setting, **Disable deadline randomization** to disable the installation randomization delay for the required software updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  On the User Experience page, configure the following settings:  

    -   **User notifications**: Specify whether to display notification of the software updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers. When **Type of deployment** is set to **Available** on the Deployment Settings page, you cannot select **Hide in Software Center and all notifications**.  

    -   **Deadline behavior**: *Available only when **Type of deployment** *is set to **Required** *on the Deployment Settings page.*   
    Specify the behavior that is to occur when the deadline is reached for the software update deployment. Specify whether to install the software updates in the deployment. Also specify whether to perform a system restart after software update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Device restart behavior**: *Available only when **Type of deployment** *is set to **Required** *on the Deployment Settings page.*    
    Specify whether to suppress a system restart on servers and workstations after software updates are installed and a system restart is required to complete the installation.  

        > [!IMPORTANT]  
        >  Suppressing system restarts can be useful in server environments or for cases in which you do not want the computers that are installing the software updates to restart by default. However, doing so can leave computers in an insecure state, whereas allowing a forced restart helps to ensure immediate completion of the software update installation.

    -   **Write filter handling for Windows Embedded devices**: When you deploy software updates to Windows Embedded devices that are write filter enabled, you can specify to install the software update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

        > [!NOTE]  
        >  When you deploy a software update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  

    - **Software updates deployment re-evaluation behavior upon restart**: Starting in Configuration Manager version 1606, select this setting to configure software updates deployments to have clients run a software updates compliance scan immediately after a client installs software updates and restarts. This enables the client to check for additional software updates that become applicable after the client restarts, and to then install them (and become compliant) during the same maintenance window.

9. On the Alerts page, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment. You can configure alerts only when **Type of deployment** is set to **Required** on the Deployment Settings page.  

    > [!NOTE]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  

10. On the Download Settings page, configure the following settings:  

    - Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  

    - Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  

    - **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see  [Fundamental concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates**: Select this setting to have clients that are connected to the intranet download software updates from Microsoft Update if software updates are not available on distribution points. Internet-based clients can always go to Microsoft Update for software updates content.

    - Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

    > [!NOTE]  
    >  Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you have configured the distribution point, the deployment package, and the settings on this page. For more information, see [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. If you have performed [Step 3: Download the content for the software update group](#BKMK_3DownloadContent), then the Deployment Package, Distribution Points, and Language Selection pages are not displayed, and you can skip to step 15 of the wizard.  

    > [!IMPORTANT]  
    >  Software updates that have been previously downloaded to the content library on the site server are not downloaded again. This is true even when you create a new deployment package for the software updates. If all software updates have already been previously downloaded, the wizard skips to the **Language Selection** page (step 15).  

12. On the Deployment Package page, select an existing deployment package or configure the following settings to specify a new deployment package:  

    1.  **Name**: Specify the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

    2.  **Description**: Specify a description that provides information about the deployment package. The description is limited to 127 characters.  

    3.  **Package source**: Specify the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

        > [!NOTE]  
        >  The deployment package source location that you specify cannot be used by another software deployment package.  

        > [!IMPORTANT]  
        >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

        > [!IMPORTANT]  
        >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

    4.  **Sending priority**: Specify the sending priority for the deployment package. Configuration Manager uses the sending priority for the deployment package when it sends the package to distribution points. Deployment packages are sent in priority order: High, Medium, or Low. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority.  

13. On the Distribution Points page, specify the distribution points or distribution point groups that will host the software update files. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. On the Download Location page, specify whether to download the software update files from the Internet or from your local network. Configure the following settings:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from a specified location on the Internet. This setting is enabled by default.  

    -   **Download software updates from a location on the local network**: Select this setting to download the software updates from a local folder or shared network folder. This setting is useful when the computer that runs the wizard does not have Internet access. The software updates can be preliminarily downloaded from any computer that has Internet access and stored in a location on the local network for subsequent access for installation.  

15. On the Language Selection page, select the languages for which the selected software updates are downloaded. The software updates are downloaded only if they are available in the selected languages. Software updates that are not language specific are always downloaded. By default, the wizard selects the languages that you have configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that are not supported by a software update, the download will fail for the software update.  

16. On the Summary page, review the settings. To save the settings to a deployment template, click **Save As Template**, enter a name and select the settings that you want to include in the template, and then click **Save**. To change a configured setting, click the associated wizard page and change the setting.  

    > [!WARNING]  
    >  The template name can consist of alphanumeric ASCII characters as well as **\\** (backslash) or **‘** (single quotation mark).  

17. Click **Next** to deploy the software update.  

 After you have completed the wizard, Configuration Manager downloads the software updates to the content library on the site server, distributes the software updates to the configured distribution points, and then deploys the software update group to clients in the target collection. For more information about the deployment process, see [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## Next steps
[Monitor software updates](monitor-software-updates.md)
