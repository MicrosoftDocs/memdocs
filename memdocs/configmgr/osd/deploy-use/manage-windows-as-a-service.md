---
title: Manage Windows as a Service
titleSuffix: Configuration Manager
description: View the state of Windows as a Service (WaaS) using Configuration Manager, create servicing plans to form deployment rings, and view alerts when Windows 10 clients are near end of support.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24 
author: mestew
ms.author: mstewart
manager: dougeby
---
# Manage Windows as a service using Configuration Manager

*Applies to: Configuration Manager (current branch)*

In Configuration Manager, you can view the state of Windows as a Service (WaaS) in your environment. Create servicing plans to form deployment rings, and ensure that Windows 10 systems are kept up-to-date when new builds are released. You can also view alerts when Windows 10 clients are near end of support for their Semi-Annual Channel build.

For more information about Windows 10 servicing options, see  [Overview of Windows as a Service](/windows/deployment/update/waas-overview#servicing-channels).

Use the following sections to manage Windows as a service.

## <a name="BKMK_Prerequisites"></a> Prerequisites

To see data in the Windows 10 servicing dashboard, you must do the following actions:

- Windows 10 computers must use Configuration Manager software updates with  Windows Server Update Services (WSUS) for software update management. When computers use Windows Update for Business (or Windows Insiders) for software update management, the computer isn't evaluated in Windows 10 servicing plans. For more information, see [Integration with Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Use a supported WSUS version:
  - WSUS 10.0.14393 (role in Windows Server 2016)
  - WSUS 10.0.17763 (role in Windows Server 2019) (Requires Configuration Manager 1810 or later)
  - WSUS 6.2 and 6.3 (role in Windows Server 2012 and Windows Server 2012 R2)
    - [KB 3095113 and KB 3159706 (or an equivalent update) must be installed](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) on WSUS 6.2 and 6.3.

- Enable Heartbeat Discovery. The data displayed in the Windows 10 servicing dashboard is found by using discovery. For more information, see [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    The following Windows 10 channel and build information is discovered and stored in the following attributes:  

    - **Operating System Readiness Branch**: Specifies the operating system channel. For example, **0** = Semi-Annual Channel - Targeted (don't defer updates), **1** = Semi-Annual Channel (defer updates), **2** = Long-Term Servicing Channel (LTSC)

    - **Operating System Build**: Specifies the operating system build. For example, **10.0.10240** (RTM) or **10.0.10586** (version 1511)

- The service connection point must be installed and configured for **Online, persistent connection** mode to see data on the Windows 10 servicing dashboard. When you are in offline mode, you don't see data updates in the dashboard until you get Configuration Manager servicing updates. For more information, see [About the service connection point](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- Internet Explorer 9 or later must be installed on the computer that runs the Configuration Manager console.

- Software updates must be configured and synchronized. Select the **Upgrades** classification and synchronize software updates before any Windows 10 feature upgrades are available in the Configuration Manager console. For more information, see [Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md).

- Starting in Configuration Manager version 1902, verify the **Specify thread priority for feature updates** [client setting](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) to ensure it's appropriate for your environment.

- Starting in Configuration Manager version 1906, verify the **Enable Dynamic Update for feature updates** [client setting](../../core/clients/deploy/about-client-settings.md#bkmk_du) to ensure it's appropriate for your environment. <!--4062619-->

## <a name="BKMK_ServicingDashboard"></a> Windows 10 servicing dashboard

The Windows 10 servicing dashboard provides you with information about Windows 10 computers in your environment, active servicing plans, compliance information, and so on. The data in the Windows 10 servicing dashboard is dependent on having the Service Connection Point installed. The dashboard has the following tiles:

- **Windows 10 Usage tile**: Provides a breakdown of public builds of Windows 10. Windows Insiders builds are listed as **other** as well as any builds that aren't yet known to your site. The service connection point downloads metadata that informs it about the Windows builds, and then this data is compared against discovery data.

- **Windows 10 Rings tile**: Provides a breakdown of Windows 10 by channel and readiness state. The LTSC segment includes all LTSC versions. The first tile breaks down the specific versions, for example, Windows 10 LTSC 2015.

- **Create Service Plan tile**: Provides a quick way to create a servicing plan. You specify the name, collection (only displays the top 10 collections by size, smallest first), deployment package (only displays the top 10 packages by most recently modified), and readiness state. Default values are used for the other settings. Click **Advanced Settings** to start the Create Servicing Plan wizard where you can configure all of the service plan settings.

- **Expired tile**: Displays the percentage of devices that are on a build of Windows 10 that is past its end of life. Configuration Manager determines the percentage from the metadata that the  Service Connection Point downloads and compares it against discovery data. A build that is past its end of life is no longer receiving monthly cumulative updates, which include security updates. The computers in this category should be upgraded to the next build version. Configuration Manager rounds up to the next whole number. For example, if you have 10,000 computers and only one on an expired build, the tile displays 1%.

- **Expire Soon tile**: Displays the percentage of computers that are on a build that is near end of life (within about four months), similar to the **Expired** tile. Configuration Manager rounds up to the next whole number.

- **Alerts tile**: Displays active alerts.

- **Service Plan Monitoring tile**: Display servicing plans that you've created and a chart of the compliance for each. This tile gives you a quick overview of the current state of the servicing plan deployments. If an earlier deployment ring meets your expectations for compliance, then you can select a later servicing plan (deploying ring) and click **Deploy Now** instead of waiting for the servicing plan rules to be triggered automatically.

- The **Windows 10 Builds tile**: Display is a fixed image time line that provides you an overview of the Windows 10 builds that are currently released and gives you a general idea of when builds transition into different states. This tile was removed starting in Configuration Manager version 1902 since more detailed information is offered in the [Product Lifecycle dashboard](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md). <!--3446861-->

> [!IMPORTANT]
> The information shown in the Windows 10 servicing dashboard (such as the support lifecycle for Windows 10  versions) is provided for your convenience and only for use internally within your company. You should not solely rely on this information to confirm update compliance. Be sure to verify the accuracy of the information provided to you.

## Drill through required updates
<!--4224414-->
*(Introduced in version 1906)*

You can drill through compliance statistics to see which devices require a specific Windows 10 feature update. To view the device list, you need permission to view updates and the collections the devices belong to. To drill down into the device list:

1. Go to **Software Library** > **Windows 10 Servicing** > **All Windows 10 Updates**.
1. Select any update that is required by at least one device.
1. Look at the **Summary** tab and find the pie chart under  **Statistics**.
1. Select the **View Required** hyperlink next to the pie chart to drill down into the device list.
1. This action takes you to a temporary node under **Devices** where you can see the devices requiring the update. You can also take actions for the node such as creating a new collection from the list.

## Servicing plan workflow

Windows 10 servicing plans in Configuration Manager are much like automatic deployment rules for software updates. You create a servicing plan with the following criteria that Configuration Manager evaluates:

- **Upgrades classification**: Only updates that are in the **Upgrades** classification are evaluated.

- **Readiness state**: The readiness state defined in the servicing plan is compared with the readiness state for the upgrade. The metadata for the upgrade is retrieved when the service connection point checks for updates.

- **Time deferral**: The number of days that you specify for **How many days after Microsoft has published a new upgrade would you like to wait before deploying in your environment** in the servicing plan. If the current date is after the release date plus the configured number of days, Configuration Manager evaluates whether to include an upgrade in the deployment.

  When an upgrade meets the criteria, the servicing plan adds the upgrade to the deployment package, distributes the package to distribution points, and deploys the upgrade to the collection based on the settings that you configure in the servicing plan. You can monitor the deployments in the Service Plan Monitoring tile on the Windows 10 Servicing Dashboard. For more information, see [Monitor software updates](../../sum/deploy-use/monitor-software-updates.md).

> [!NOTE]
> **Windows 10, version 1903 and later** was added to Microsoft Update as its own product rather than being part of the **Windows 10** product like earlier versions. This change caused you to do a number of manual steps to ensure that your clients see these updates. We've helped reduce the number of manual steps you have to take for the new product in Configuration Manager version 1906. For more information, see [Configuring products for versions of Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="BKMK_ServicingPlan"></a> Windows 10 servicing plan

As you deploy Windows 10 Semi-Annual Channel, you can create one or more servicing plans to define the deployment rings that you want in your environment, and then monitor them in the Windows 10 servicing dashboard. Servicing plans use only the **Upgrades** software updates classification, not cumulative updates for Windows 10. For those updates, you still need to deploy by using the software updates workflow. The end-user experience with a servicing plan is the same as it is with software updates, including the settings that you configure in the servicing plan.  

> [!NOTE]
> You can use a task sequence to deploy an upgrade for each Windows 10 build, but it requires more manual work. You would need to import the updated source files as an operating system upgrade package, and then create and deploy the task sequence to the appropriate set of computers. However, a task sequence provides additional customized options, such as the pre-deployment and post-deployment actions.

You can create a basic servicing plan from the Windows 10 servicing dashboard. After you specify the name, collection (only displays the top 10 collections by size, smallest first), deployment package (only displays the top 10 packages by most recently modified), and readiness state, Configuration Manager creates the servicing plan with default values for the other settings. You can also start the Create Servicing Plan wizard to configure all of the settings. Use the following procedure to create a servicing plan by using the Create Servicing Plan wizard.  

> [!NOTE]  
> You can manage the behavior for high-risk deployments. A high-risk deployment is a deployment that is automatically installed and has the potential to cause unwanted results. For example, a task sequence that has a purpose of **Required** that deploys Windows 10 is considered a high-risk deployment. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### To create a Windows 10 servicing plan

1. In the Configuration Manager console, click **Software Library**.

1. In the Software Library workspace, expand **Windows 10 Servicing**, and then click **Servicing Plans**.

1. On the **Home** tab, in the **Create** group, click **Create Servicing Plan**. The Create Servicing Plan Wizard opens.

1. On the **General** page, configure the following settings:

    - **Name**: Specify the name for the servicing plan. The name must be unique, help to describe the objective of the rule, and identify it from others in the Configuration Manager site.

    - **Description**: Specify a description for the servicing plan. The description should provide an overview of the servicing plan and any other relevant information that helps to identify and differentiate the plan among others in the Configuration Manager site. The description field is optional, has a limit of 256 characters, and has a blank value by default.

1. On the Servicing Plan page, specify the **Target Collection**. Members of the collection receive the Windows 10 upgrades that are defined in the servicing plan.

    - When you deploy a high-risk deployment, such as servicing plan, the **Select Collection** window displays only the custom collections that meet the deployment verification settings that are configured in the site's properties.

    - High-risk deployments are always limited to custom collections, collections that you create, and the built-in **Unknown Computers** collection. When you create a high-risk deployment, you can't select a built-in collection such as **All Systems**. Uncheck **Hide collections with a member count greater than the site's minimum size configuration** to see all custom collections that contain fewer clients than the configured maximum size. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - The deployment verification settings are based on the current membership of the collection. After you deploy the servicing plan, the collection membership isn't reevaluated for the high-risk deployment settings.

      - For example, let's say you set **Default size** to 100 and the **Maximum size** to 1000. When you create a high risk deployment, the **Select Collection** window will only display collections that contain fewer than 100 clients. If you clear the **Hide collections with a member count greater than the site's minimum size configuration** setting, the window will display collections that contain less than 1000 clients.  
      When you select a collection that contains a site role, the following criteria applies:
        - If the collection contains a site system server and in the deployment verification settings you configure to block collections with site system servers, then an error occurs and you can't continue.
        - If the collection contains a site system server and in the deployment verification settings you configure to warn you if collections that have site system servers, if the collection exceeds the default size value, or if the collection contains a server, then the Deploy Software Wizard will display a high risk warning. You must agree to create a high risk deployment and an audit status message is created.

1. On the Deployment Ring page, configure the following settings:

   - **Specify the Windows readiness state to which this servicing plan should apply**: Select one of the following options:

      - **Semi-Annual Channel (Targeted)**: In this servicing model, feature updates are available as soon as Microsoft releases them.

      - **Semi-Annual Channel**: This servicing channel is typically used for broad deployment. Windows 10 clients in the Semi-Annual Channel receive the same build of Windows 10 as those devices in the targeted channel, just at a later time.

        For more information about servicing channels and what options are best for you, see [Servicing channels](/windows/deployment/update/waas-overview#servicing-channels).

   - **How many days after Microsoft has published a new upgrade would you like to wait before deploying in your environment**: If the current date is after the release date plus the number of days that you configure for this setting, Configuration Manager evaluates whether to include an upgrade in the deployment.

1. On the Upgrades page, configure the search criteria to filter the upgrades that are added to the service plan. Only upgrades that meet the specified criteria are added to the associated deployment. The following property filters are available: <!--3098809, 3113836, 3204570 -->

   - **Architecture** (starting in version 1810)
   - **Language**
   - **Product Category** (starting in version 1810)
   - **Required**
      > [!IMPORTANT]
      > We recommend that as part of your search criteria, that you set the **Required** field with a value of **>=1**. Using this criteria ensures that only applicable updates are added to the service plan.
   - **Superseded** (starting in version 1810)
   - **Title**

    Click **Preview** to view the upgrades that meet the specified criteria.

1. On the Deployment Schedule page, configure the following settings:

   - **Schedule evaluation**: Specify whether Configuration Manager evaluates the available time and installation deadline times by using UTC or the local time of the computer that runs the Configuration Manager console.

       > [!NOTE]
       > When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.

   - **Software available time**: Select one of the following settings to specify when the software updates are available to clients:

        - **As soon as possible**: Select this setting to make the software updates that are included in the deployment available to the client computers as soon as possible. When you create the deployment with this setting selected, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become aware of the deployment and can obtain the updates that are available for installation.

        - **Specific time**: Select this setting to make the software updates that are included in the deployment available to the client computers at a specific date and time. When you create the deployment with this setting enabled, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become aware of the deployment. However, the software updates in the deployment aren't available for installation until after the configured date and time.

   - **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment:

        - **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.

        - **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time. Configuration Manager determines the deadline to install software updates by adding the configured **Specific time** interval to the **Software available time**.

           > [!NOTE]
           > The actual installation deadline time is the displayed deadline time plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the updates in the deployment at the same time.
           >
           > You can configure the **Computer Agent** client setting **Disable deadline randomization** to disable the installation randomization delay for required updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Delay enforcement of this deployment according to user preferences, up to the grace period defined on the client**: Select this option to honor the [**Grace period for enforcement after deployment deadline (hours)** client setting](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours).

1. On the User Experience page, configure the following settings:  

    - **User notifications**: Specify whether to display notification of the updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers.

    - **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the update deployment. Specify whether to install the updates in the deployment. Also specify whether to perform a system restart after update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

    - **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after updates are installed and a system restart is required to complete the installation.

    - **Write filter handling for Windows Embedded devices**: When you deploy updates to Windows Embedded devices that are write filter enabled, you can specify to install the update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.
        - When you deploy an update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.

    - **Software updates deployment re-evaluation behavior upon restart**: To force another update deployment evaluation cycle after restart, select the option **If any update in this deployment requires a system restart, run updates deployment evaluation cycle after restart**.

1. On the Deployment Package page, select an existing deployment package, no deployment package, or configure the following settings to create a new deployment package:

    1. **Name**: Specify the name of the deployment package. This name must be unique and describes the package content. It's limited to 50 characters.

    1. **Description**: Specify a description that provides information about the deployment package. The description is limited to 127 characters.

    1. **Package source**: Specifies the location of the software update source files. Type a network path for the source location, for example, **\\\server\\sharename\\path**, or click **Browse** to find the network location. Create the shared folder for the deployment package source files before you continue to the next page.
        - The deployment package source location that you specify cannot be used by another software deployment package.
        - The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location to reduce the risk of attackers tampering with the software update source files.
        - You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.

    1. **Sending priority**: Specify the sending priority for the deployment package. Configuration Manager uses the sending priority for the deployment package when it sends the package to distribution points. Deployment packages are sent in priority order: High, Medium or Low. Packages with identical priorities are sent in the order in which they were created. If there's no backlog, the package processes immediately regardless of its priority.

    1. **Enable binary differential replication**: Enable this option if you want to use binary differential replication.

1. On the Distribution Points page, specify the distribution points or distribution point groups that host the update files. For more information about distribution points, see [Configure a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > This page is available only when you create a new software update deployment package.  

1. On the Download Location page, specify whether to download the update files from the Internet or from your local network. Configure the following settings:

    - **Download software updates from the Internet**: Select this setting to download the updates from a specified location on the Internet. This setting is enabled by default.

    - **Download software updates from a location on the local network**: Select this setting to download the updates from a local directory or shared folder. This setting is useful when the computer that runs the wizard doesn't have Internet access. Any computer with Internet access can preliminarily download the updates and store them in a location on the local network that is accessible from the computer that runs the wizard.

1. On the Language Selection page, select the languages for which the selected updates are downloaded. The updates are downloaded only if they're available in the selected languages. Updates that aren't language-specific are always downloaded. By default, the wizard selects the languages that you've configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that are not supported by an update, the download fails for the update.

1. On the Summary page, review the settings and click **Next** to create the servicing plan.  

After you've completed the wizard, the servicing plan will run. It adds the updates that meet the specified criteria to a software update group, download the updates to the content library on the site server, distribute the updates to the configured distribution points, and then deploy the software update group to clients in the target collection.

## <a name="BKMK_ModifyServicingPlan"></a> Modify a servicing plan

After you create a basic servicing plan from the Windows 10 servicing dashboard or you need to change the settings for an existing servicing plan, you can go to properties for the servicing plan.

> [!NOTE]
> You can configure settings in the properties for the servicing plan that are not available in the wizard when you create the servicing plan. The wizard uses default settings for the settings for the following: download settings, deployment settings, and alerts.  

Use the following procedure to modify the properties of a servicing plan. 

### To modify the properties of a servicing plan

1. In the Configuration Manager console, click **Software Library**.

1. In the Software Library workspace, expand **Windows 10 Servicing**, click **Servicing Plans**, and then select the servicing plan that you want to modify.

1. On the **Home** tab, click **Properties** to open properties for the selected servicing plan.

    The following settings are available in the servicing plan properties that weren't configured in the wizard:

    **Deployment Settings**: On the Deployment Settings tab, configure the following settings:

    - **Use Wake-on-LAN to wake up clients for required deployments**: Specify whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time are awakened so the software update installation can initiate. Clients that are in sleep mode that don't require any software updates in the deployment aren't started. By default, this setting isn't enabled.

        > [!WARNING]
        > Before you can use this option, computers and networks must be configured for Wake On LAN.

    - **Detail level**: Specify the level of detail for the state messages that are reported by client computers.

    **Download Settings**: On the Download Settings tab, configure the following settings:

    - Specify whether the client downloads and installs the software updates when a client is connected to a slow network or is using a fallback content location.

    - Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates isn't available on a preferred distribution point.

    - **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see [Fundamental concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Specify whether to have clients download software updates from Microsoft Update if software updates aren't available on distribution points.
        > [!IMPORTANT]
        > Do not use this setting for Windows 10 Servicing updates. Configuration Manager (at least through version 1610) fails to download the Windows 10 Servicing updates from Microsoft Update.

    - Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.

    **Alerts**: On the Alerts tab, configure how Configuration Manager and System Center Operations Manager generate alerts for this deployment.
    - You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.

## Next steps

For more information, see [Fundamentals of Configuration Manager as a service and Windows as a service](../../core/understand/configuration-manager-and-windows-as-service.md).
