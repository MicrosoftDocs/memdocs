---
author: BalaDelli
ms.author: baladell
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/10/2021
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

1.  In the Configuration Manager console, go to the **Software Library** workspace, and select the **Software Updates** node.  

2.  Choose the software update to download by using one of the following methods:  

    -   Select one or more software update groups from the **Software Update Groups** node. Then click **Download** in the ribbon.  

    -   Select one or more software updates from **All Software Updates** node. Then click **Download** in the ribbon.  

        > [!NOTE]  
        >  In the **All Software Updates** node, Configuration Manager displays only software updates with a **Critical** and **Security** classification that have been released in the last 30 days.  

        > [!TIP]  
        >  Click **Add Criteria** to filter the software updates that are displayed in the **All Software Updates** node. Save search criteria that you often use, and then manage saved searches on the **Search** tab.  


3.  On the **Deployment Package** page of the Download Software Updates Wizard, configure the following settings:  

    -  **Select deployment package**: Choose this setting to select an existing deployment package for the software updates that are in the deployment.  

        > [!NOTE]  
        >  Software updates that the site has already downloaded to the selected deployment package won't be downloaded again.  

    -  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. The package must have a unique name that briefly describes the package content. It's limited to 50 characters.  

        -   **Description**: Specify a description that provides information about the deployment package. The optional description is limited to 127 characters.    

        -   **Package source**: Specifies the location of the software update source files. Type a network path for the source location, for example, `\\server\sharename\path`, or click **Browse** to find the network location. Create the shared folder for the deployment package source files before you proceed to the next page.  

             - You can't use the specified location as the source of another software deployment package.  

             - You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. If you do, first copy the content from the original package source to the new package source location.  

             -  The computer account of the SMS Provider and the user that's running the wizard to download the software updates must both have **Write** permissions to the download location. Restrict access to the download location. This restriction reduces the risk of attackers tampering with the software update source files.  

        - **Enable binary differential replication**: Enable this setting to minimize network traffic between sites. Binary differential replication (BDR) only updates the content that has changed in the package, instead of updating the entire package contents. For more information, see [Binary differential replication](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  On the **Distribution Points** page, specify the distribution points or distribution point groups to host the software update files. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). This page is available only when you create a new software update deployment package.  

5.  The **Distribution Settings** page is available only when you create a new software update deployment package. Specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Deployment packages are sent in priority order: high, medium, or low. Packages with identical priorities are sent in the order in which they were created. If there's no backlog, the package processes immediately regardless of its priority. By default, the site sends packages with **Medium** priority.  

    -   **Enable for on-demand distribution**: Use this setting to enable on-demand content distribution to distribution points configured for this feature and in the client's current boundary group. When you enable this setting, the management point creates a trigger for the distribution manager to distribute the content to all such distribution points when a client requests the content for the package and the content isn't available. For more information, see [On-demand content distribution](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.   

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This option is the default.  

        For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  


6.  On the **Download Location** page, specify the location that Configuration Manager uses to download the software update source files. Use one of the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the internet. This option is the default.  

    -   **Download software updates from a location on my network**: Select this setting to download the software updates from a local directory or shared folder. This setting is useful when the computer that runs the wizard doesn't have internet access. Any computer with internet access can preliminarily download the software updates. Then store them in a location on the local network that's accessible from the computer that runs the wizard.  


7.  On the **Language Selection** page, select the languages for which the site downloads the selected software updates. The site only downloads these updates if they're available in the selected languages. Software updates that aren't language-specific are always downloaded. By default, the wizard selects the languages that you've configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that a software update doesn't support, the download fails for the update.  

8. On the **Summary** page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

9. On the **Completion** page, verify that the software updates were successfully downloaded, and then click **Close**.  
