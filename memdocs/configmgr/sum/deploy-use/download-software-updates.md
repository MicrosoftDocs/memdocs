---
title: Download software updates
titleSuffix: Configuration Manager
description: Use the Download Software Updates Wizard to download software updates and distribute them to distribution points so they are ready to deploy to clients.
ms.date: 03/20/2023
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
manager: apoorvseth
author: BalaDelli
ms.author: baladell
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---



# Download software updates  

*Applies to: Configuration Manager (current branch)*

There are several methods available to you for downloading software updates in Configuration Manager. When you create an automatic deployment rule (ADR) or manually deploy software updates, the software updates are downloaded to the content library on the site server. Then, the software updates are copied to the content library on the distribution points that are associated with the configured deployment package. If you want to download the software updates before you deploy them, you can use the Download Updates Wizard. Doing this will enable you to verify that the software updates are available on distribution points before you deploy the software updates to client computers.  

> [!NOTE]  
>  - Starting March 28, 2023, on-premises Windows 11, version 22H2 devices will receive quality updates via the Unified Update Platform (UUP). On-premises update management with Unified Update Platform (UUP) requires an additional 10 GB of space per Windows version and processor architecture for each version. For more information, see the [UUP considerations](/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#uup-considerations) section
>  - For information about monitoring content status, see the [Content status monitoring](../deploy-use/monitor-software-updates.md#BKMK_ContentStatus).  

Use the following procedure to download software updates by using the Download Software Updates Wizard.  

#### To download software updates  
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

<!---
1.  In the Configuration Manager console, navigate to **Software Library** > **Software Updates**.  

3.  Choose the software update to download by using one of the following methods:  

    -   Select one or more software update groups from **Software Update Groups**, and then, on the **Home** tab, in the **Update Group** group, click **Download**.  

    -   Select one or more software updates from **All Software Updates**, and then, on the **Home** tab, in the **Update** group, click **Download**.  

        > [!NOTE]  
        >  On the **All Software Updates** node, Configuration Manager displays only software updates with a **Critical** and **Security** classification that have been released in the last 30 days.  

        > [!TIP]  
        >  Click **Add Criteria** to filter the software updates that are displayed in the **All Software Updates** node, save search criteria that you often use, and then manage saved searches on the **Search** tab.  

         The **Download Software Updates Wizard** opens.  

4.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Choose this setting to select an existing deployment package for the software updates that are in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package will not be downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates that are in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. The package must have a unique name that briefly describes the package content.  It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files. Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

5.  On the **Distribution Points** page, specify the distribution points or distribution point groups that will host the software update files, and then click **Next**. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  The Distribution Points page is available only when you create a new software update deployment package.  

6.  On the **Distribution Settings** page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Deployment packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

7.  On the **Download Location** page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

8.  On the **Language Selection** page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

9. On the **Summary** page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

10. On the **Completion** page, verify that the software updates were successfully downloaded, and then click **Close**.  --->
