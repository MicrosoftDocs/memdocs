---
title: "Manage Windows as a Service - Configuration Manager | Microsoft Docs"
description: "View the state of Windows as a Service using Configuration Manager, create servicing plans to form deployment rings, and view alerts when Windows 10 clients are near end of support."

ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
caps.latest.revision: 26
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Manage Windows as a service using System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


 In System Center Configuration Manager, you can view the state of Windows as a Service in your environment, create servicing plans to form deployment rings and ensure that Windows 10 current branch systems are kept up to date when new builds are released, and view alerts when Windows 10 clients are near end of support for their build of Current Branch (CB) or Current Branch for Business (CBB).  

 For more information about Windows 10 servicing options, see  [Windows 10 servicing options for updates and upgrades](https://technet.microsoft.com/library/mt598226\(v=vs.85\).aspx).  

 Use the following sections to manage Windows as a service.

##  <a name="BKMK_Prerequisites"></a> Prerequisites  
 To see data in the Windows 10 servicing dashboard, you must do the following:  

-   Windows 10 computers must use Configuration Manager software updates with  Windows Server Update Services (WSUS) for software update management. When computers use Windows Update for Business (or Windows Insiders) for software update management, the computer will not be evaluated in Windows 10 servicing plans. For more information, see [Integration with Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   WSUS 4.0 with the [hotfix 3095113](https://support.microsoft.com/kb/3095113) must be installed on your software update points and site servers. This adds the **Upgrades** software update classification. For more information, see [Prerequisites for software updates](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   WSUS 4.0 with the [hotfix 3159706](https://support.microsoft.com/kb/3159706) must be installed on your software update points and site servers to upgrade computers to the Windows 10 Anniversary Update, as well as for subsequence versions. There are manual steps described in the support article that you must take to install this hotfix. For more information, see the [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/).

-   Enable Heartbeat Discovery. The data displayed in the Windows 10 servicing dashboard is found by using discovery. For more information, see [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#bkmk_confighbdisc).  

     The following Windows 10 branch and build information is discovered and stored in the following attributes:  

    -   **Operating System Readiness Branch**: Specifies the operating system branch. For example, **0** = CB (no not defer upgrades), **1** = CBB (defer upgrades), **2** = Long Term Servicing Branch (LTSB)

    -   **Operating System Build**: Specified the operating system build. For example, **10.0.10240** (RTM) or **10.0.10586** (version 1511)  

-   The service connection point must be installed  and  configured for **Online, persistent connection** mode to see data on the Windows 10 servicing dashboard. When you are  in offline mode, you  will not  see data updates in the dashboard until you  get Configuration Manager servicing updates.   
     For more information, see [About the service connection point](../../core/servers/deploy/configure/about-the-service-connection-point.md).  


-   Internet Explorer 9 or later must be installed on the computer that runs the Configuration Manager console.  

-   Software updates must be configured and synchronized. You must select the **Upgrades** classification and synchronize software updates before any Windows 10 feature upgrades will be available in the Configuration Manager console. For more information, see [Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md).  

##  <a name="BKMK_ServicingDashboard"></a> Windows 10 servicing dashboard  
 The Windows 10 servicing dashboard provides you with information about Windows 10 computers in your environment, active servicing plans, compliance information, and so on. The data in the Windows 10 servicing dashboard is dependent on having the Service Connection Point installed. The dashboard has the following tiles:  

-   **Windows 10 Usage tile**:  Provides a breakdown of public builds of Windows 10. Windows Insiders builds are listed as **other** as well as any builds that are not yet known to your site. The service connection point will download metadata that informs it about the Windows builds, and then  this data is compared against discovery data.  

-   **Windows 10 Rings tile**:  Provides a breakdown of Windows 10 by branch and readiness state . The LTSB segment will be all LTSB versions (whereas the first tile breaks down the specific versions. For example, Windows 10 LTSB 2015. The **Release Ready** segment corresponds to CB, and the **Business ready** segment is CBB.  

-   **Create Service Plan tile**:   Provides a quick way to create a servicing plan. You specify the name, collection (only displays the top ten collections by size, smallest first), deployment package (only displays the top ten packages by most recently modified), and readiness state. Default values are used for the other settings. Click **Advanced Settings** to  start the Create Servicing Plan wizard where you can configure all of the service plan settings.  

-   **Expired tile**: Displays the percentage of devices that are on a build of Windows 10 that is past its end of life. Configuration Manager determines the percentage from the metadata that the  Service Connection Point downloads and  compares it  against discovery data. A build that is past its end of life is no longer receiving monthly cumulative updates, which includes security updates. The computers in this category should be upgraded to the next build version. Configuration Manager rounds up to the next whole number. For example, if you have 10,000 computers and only one on an expired build, the tile will display 1%.  

-   **Expire Soon tile**: Displays the percentage of computers that are on a build that is near end of life (within about four months), similar to the **Expired** tile. Configuration Manager rounds up to the next whole number.  

-   **Alerts tile**: Displays active alerts.  

-   **Service Plan Monitoring tile**: Display servicing plans that you have created and a chart of the compliance for each. This gives you a quick overview of the current state of the servicing plan deployments. If an earlier deployment ring meets your expectations for compliance, then you can select a later servicing plan (deploying ring) and click **Deploy Now** instead of waiting for the servicing plan rules to be triggered automatically.  

-   The **Windows 10 Builds tile**:  Display is a fixed image time line that provides you an overview of the Windows 10 builds that are currently released and gives you a general idea of when builds will transition into different states.  

> [!IMPORTANT]  
>  The information shown in the Windows 10 servicing dashboard (such as the support lifecycle for Windows 10  versions) is provided for your convenience and only for use internally within your company. You should not solely rely on this information to confirm update compliance. Be sure to verify the accuracy of the information provided to you.  

## Servicing plan workflow  
 Windows 10 servicing plans in Configuration Manager are much like automatic deployment rules for software updates. You create a servicing plan with the following criteria that Configuration Manager evaluates:  

-   **Upgrades classification**: Only updates that are in the **Upgrades** classification are evaluated.  

-   **Readiness state**: The readiness state defined in the servicing plan is compared with the readiness state for the upgrade. The metadata for the upgrade is retrieved when the service connection point checks for updates.  

-   **Time deferral**: The number of days that you specify for **How many days after Microsoft has published a new upgrade would you like to wait before deploying in your environment** in the servicing plan. Configuration Manager evaluates whether to include an upgrade in the deployment if the current date is after the release date plus the configured number of days.  

 When an upgrade meets the criteria, the servicing plan adds the upgrade to the deployment package, distributes the package to distribution points, and deploys the upgrade to the collection based on the settings that you configure in the servicing plan.  You can monitor the deployments in the Service Plan Monitoring tile on the Windows 10 Servicing Dashboard. For more information, see [Monitor software updates](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="BKMK_ServicingPlan"></a> Windows 10 servicing plan  
 As you deploy Windows 10 CB, you can create one or more servicing plans to define the deployment rings that you want in your environment, and then monitor them in the Windows 10 servicing dashboard.   
Servicing plans use only the **Upgrades** software updates classification, not cumulative updates for Windows 10. For those updates, you will still need to deploy by using the software updates workflow.  The end-user experience with a servicing plan is the same as it is with software updates, including the settings that you configure in the servicing plan.  

> [!NOTE]  
>  You can use a task sequence to deploy an upgrade for each Windows 10 build, but it requires more manual work. You would need to import the updated source files as an operating system upgrade package, and then create and deploy the task sequence to the appropriate set of computers. However, a task sequence provides additional customized options, such as the pre-deployment and post-deployment actions.  

 You can create a basic servicing plan from the Windows 10 servicing dashboard. After you specify the name,  collection (only displays the top ten collections by size, smallest first), deployment package (only displays the top ten packages by most recently modified), and readiness state, Configuration Manager creates the servicing plan with default values for the other settings. You can also start the Create Servicing Plan wizard to configure all of the settings. Use the following procedure to create a servicing plan by using the Create Servicing Plan wizard.  

> [!NOTE]  
>  Beginning in Configuration Manager version 1602, you can manage the behavior for high-risk deployments. A high-risk deployment is a deployment that is automatically installed and has the potential to cause unwanted results. For example, a task sequence that has a purpose of **Required** that deploys Windows 10 is considered a high-risk deployment. For more information, see [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### To create a Windows 10 servicing plan  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Windows 10 Servicing**, and then click **Servicing Plans**.  

3.  On the **Home** tab, in the **Create** group, click **Create Servicing Plan**. The Create Servicing Plan Wizard opens.  

4.  On the **General** page, configure the following settings:  

    -   **Name**: Specify the name for the servicing plan. The name must be unique, help to describe the objective of the rule, and identify it from others in the Configuration Manager site.  

    -   **Description**: Specify a description for the servicing plan. The description should provide an overview of the servicing plan and any other relevant information that helps to identify and differentiate the plan among others in the Configuration Manager site. The description field is optional, has a limit of 256 characters, and has a blank value by default.  

5.  On the Servicing Plan page, configure the following settings:  

    -   **Target Collection**: Specifies the target collection to be used for the servicing plan. Members of the collection receive the Windows 10 upgrades that are defined in the servicing plan.  

        > [!NOTE]  
        >  Beginning in Configuration Manager version 1602, when you deploy a high-risk deployment, such as servicing plan, the **Select Collection** window displays only the custom collections that meet the deployment verification settings that are configured in the site's properties.
        >    
        > High-risk deployments are always limited to custom collections, collections that you create, and the built-in **Unknown Computers** collection. When you create a high-risk deployment, you cannot select a built-in collection such as **All Systems**. Uncheck **Hide collections with a member count greater than the site's minimum size configuration** to see all custom collections that contain fewer clients than the configured maximum size. For more information, see [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >  
        > The deployment verification settings are based on the current membership of the collection. After you deploy the servicing plan, the collection membership is not reevaluated for the high-risk deployment settings.  
        >  
        > For example, let's say you set **Default size** to 100 and the **Maximum size** to 1000. When you create a high risk deployment, the **Select Collection** window will only display collections that contain less than 100 clients. If you clear the **Hide collections with a member count greater than the site's minimum size configuration** setting, the window will display collections that contain less than 1000 clients.  
        >
        > When you select a collection that contains a site role, the following applies:    
        >   
        >    - If the collection contains a site system server and in the deployment verification settings you configure to block collections with site system servers, then an error occurs and you cannot continue.    
        >    - If the collection contains a site system server and in the deployment verification settings you configure to warn you if collections that have site system servers, if the collection exceeds the default size value, or if the collection contains a server, then the Deploy Software Wizard will display a high risk warning. You must agree to create a high risk deployment and an audit status message is created.  

6.  On the Deployment Ring page, configure the following settings:  

    -   **Specify the Windows readiness state to which this servicing plan should apply**: Select one of the following:  

        -   **Release Ready (Current Branch)**: In the CB servicing model, feature updates are available as soon as Microsoft releases them.

        -   **Business Ready (Current Branch for Business)**: The CBB servicing branch is typically used for broad deployment. Windows 10 clients in the CBB servicing branch receive the same build of Windows 10 as those in the CB servicing branch, just at a later time.

        For more information about servicing branches and what options is best for you, see [Servicing branches](https://technet.microsoft.com/itpro/windows/manage/waas-overview#servicing-branches).

    -   **How many days after Microsoft has published a new upgrade would you like to wait before deploying in your environment**: Configuration Manager evaluates whether to include an upgrade in the deployment if the current date is after the release date plus the number of days that you configure for this setting.

    -   Prior to Configuration Manager version 1602, click **Preview** to view the Windows 10 updates associated with the readiness state.  

    For more information, see [Servicing branches](https://technet.microsoft.com/itpro/windows/manage/waas-overview#servicing-branches).
7.  Beginning in Configuration Manager version 1602, on the Upgrades page, configure the search criteria to filter the upgrades that will be added to the service plan. Only upgrades that meet the specified criteria will be added to the associated deployment.  

     Click **Preview** to view the upgrades that meet the specified criteria.  

8.  On the Deployment Schedule page, configure the following settings:  

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
            >  The actual installation deadline time is the displayed deadline time plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the updates in the deployment at the same time.  
            >   
            >  You can configure the **Computer Agent** client setting **Disable deadline randomization** to disable the installation randomization delay for required updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

9. On the User Experience page, configure the following settings:  

    -   **User notifications**: Specify whether to display notification of the updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers.  

    -   **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the update deployment. Specify whether to install the updates in the deployment. Also specify whether to perform a system restart after update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after updates are installed and a system restart is required to complete the installation.  

    -   **Write filter handling for Windows Embedded devices**: When you deploy updates to Windows Embedded devices that are write filter enabled, you can specify to install the update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

        > [!NOTE]  
        >  When you deploy an update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  

10. On the Deployment Package page, select an existing deployment package or configure the following settings to create a new deployment package:  

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

11. On the Distribution Points page, specify the distribution points or distribution point groups that will host the update files. For more information about distribution points, see [Configure a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).

    > [!NOTE]  
    >  This page is available only when you create a new software update deployment package.  

12. On the Download Location page, specify whether to download the update files from the Internet or from your local network. Configure the following settings:  

    -   **Download software updates from the Internet**: Select this setting to download the updates from a specified location on the Internet. This setting is enabled by default.  

    -   **Download software updates from a location on the local network**: Select this setting to download the updates from a local directory or shared folder. This setting is useful when the computer that runs the wizard does not have Internet access. Any computer with Internet access can preliminarily download the updates and store them in a location on the local network that is accessible from the computer that runs the wizard.  

13. On the Language Selection page, select the languages for which the selected updates are downloaded. The updates are downloaded only if they are available in the selected languages. Updates that are not language specific are always downloaded. By default, the wizard selects the languages that you have configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that are not supported by an update, the download will fail for the update.  

14. On the Summary page, review the settings and click **Next** to create the servicing plan.  

 After you have completed the wizard, the servicing plan will run. It will add the updates that meet the specified criteria to a software update group, download the updates to the content library on the site server, distribute the updates to the configured distribution points, and then deploy the software update group to clients in the target collection.  

##  <a name="BKMK_ModifyServicingPlan"></a> Modify a servicing plan  
After you create a basic servicing plan from the Windows 10 servicing dashboard or you need to change the settings for an existing servicing plan, you can go to properties for the servicing plan.

> [!NOTE]
> You can configure settings in the properties for the servicing plan that are not available in the wizard when you create the servicing plan. The wizard uses default settings for the settings for the following: download settings, deployment settings, and alerts.  

Use the following procedure to modify the properties of a servicing plan.  

#### To modify the properties of a servicing plan  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Windows 10 Servicing**,  click **Servicing Plans**, and then select the servicing plan that you want to modify.  

3.  On the **Home** tab, click **Properties** to open properties for the selected servicing plan.

    The following settings are available in the servicing plan properties that were not configured in the wizard:

    **Deployment Settings**: On the Deployment Settings tab, configure the following settings:  

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

    **Download Settings**: On the Download Settings tab, configure the following settings:  

    - Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  

    - Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  

    -   **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see  [Fundamental concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Specify whether to have clients download software updates from Microsoft Update if software updates are not available on distribution points.
        > [!IMPORTANT]
        > Do not use this setting for Windows 10 Servicing updates. Configuration Manager (at least through version 1610) will fail to download the Windows 10 Servicing updates from Microsoft Update.

    -   Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.   

    **Alerts**: On the Alerts tab, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment. You can configure alerts only when **Type of deployment** is set to **Required** on the Deployment Settings page.  

    > [!NOTE]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  
