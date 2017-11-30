---
title: "Deploy content"
titleSuffix: "Configuration Manager"
description: "After you install distribution points for System Center Configuration Manager, here's how you can begin to deploy content to them."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
caps.latest.revision: 6
author: mstewartms.author: mstewartmanager: angrobe
---
# Deploy and manage content for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
After you install distribution points for System Center Configuration Manager, you can begin to deploy content to them. Typically, content transfers to distribution points across the network, but other options to get content to the distribution points exists. After content transfers to a distribution point, you can update, redistribute, remove, and validate that content on distribution points.  

##  <a name="bkmk_distribute"></a> Distribute content  
 Typically, you distribute content to distribution points so that it is available to client computers. (The exception to this is when you use on-demand content distribution for a specific deployment.)  When you distribute content,   Configuration Manager stores content files in a package, and then distributes the package to the distribution point. Types of content that you can distribute, include:  

-   Application deployment types  

-   Packages  

-   Deployment packages  

-   Driver packages  

-   Operating system images  

-   Operating system installers  

-   Boot images  

-   Task sequences  

When you create a package that contains source files, such as an application deployment type or deployment package, the site on which the package is created becomes the site owner for the package content source. Configuration Manager copies the source files from the source file path that you specify for the object to the content library on the site server that owns the package content source.  Then, Configuration Manager replicates the information to additional sites. (See [The content library](../../../../core/plan-design/hierarchy/the-content-library.md) for more information about this.)  

Use the following procedure to distribute content to distribution points.  

#### To distribute content on distribution points  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you want to distribute:  

    -   **Applications**: Expand **Application Management** > **Applications**, and then select the applications that you want to distribute.  

    -   **Packages**: Expand **Application Management** >  **Packages**, and then select the packages that you want to distribute.  

    -   **Deployment Packages**: Expand **Software Updates** >  **Deployment Packages**, and then select the deployment packages that you want to distribute.  

    -   **Driver Packages**: Expand **Operating Systems** >  **Driver Packages**, and then select the driver packages that you want to distribute.  

    -   **Operating System Images**: Expand **Operating Systems** >  **Operating System Images**, and then select the operating system images that you want to distribute.  

    -   **Operating System Installers**: Expand **Operating Systems** > **Operating System Installers**, and then select the operating system installers that you want to distribute.  

    -   **Boot Images**: Expand **Operating Systems** >  **Boot Images**, and then select the boot images that you want to distribute.  

    -   **Task Sequences**: Expand **Operating Systems** >  **Task Sequences**, and then select the task sequence that you want to distribute. Although task sequences do not contain content, they have associated content dependencies that are distributed.  

        > [!NOTE]  
        >  If you modify the task sequence, you must redistribute the content.  

3.  On the **Home** tab, in the **Deployment** group, click **Distribute Content**. The Distribute Content Wizard opens.  

4.  On the **General** page, verify that the content listed is the content that you want to distribute, choose whether you want Configuration Manager to detect content dependencies that are associated with the selected content and add the dependencies to the distribution, and then click **Next**.  

    > [!NOTE]  
    >  You have the option to configure the **Detect associated content dependencies and add them to this distribution** setting only for the application content type. Configuration Manager automatically configures this setting for task sequences, and it cannot be modified.  

5.  On the **Content** tab, if displayed, verify that the content listed is the content that you want to distribute, and then click **Next**.  

    > [!NOTE]  
    >  The **Content** page displays only when the **Detect associated content dependencies and add them to this distribution** setting is selected on the **General** page of the wizard.  

6.  On the **Content Destination** page, click **Add**, choose one of the following, and then follow the associated step:  

    -   **Collections**: Select **User Collections** or **Device Collections**, click the collection associated with one or more distribution point groups, and then click **OK**.  

        > [!NOTE]  
        >  Only the collections that are associated with a distribution point group are displayed. For more information about associating collections with distribution point groups, see [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) in the [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) topic.  

    -   **Distribution Point**: Select an existing distribution point, and then click **OK**. Distribution points that have previously received the content are not displayed.  

    -   **Distribution Point Group**: Select an existing distribution point group, and then click **OK**. Distribution point groups that have previously received the content are not displayed.  

    When you finish adding content destinations, click **Next**.  

7.  On the **Summary** page, review the settings for the distribution before you continue. To distribute the content to the selected destinations, click **Next**.  

8.  The **Progress** page displays the progress of the distribution.  

9. The **Confirmation** page displays whether the content was successfully assigned to the points. To monitor the content distribution, see  [Monitor content you have distributed with System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="bkmk_prestage"></a> Use Prestaged content  
 You can prestage content files for applications and package types:  

-   In the Configuration Manager console, you select the content that you need and then use the **Create Prestaged Content File Wizard** to create a compressed, prestaged content file that contains the files and associated metadata for the content that you selected.  

-   You can then manually import the content at a site server, secondary site, or distribution point.  

-   When you import the prestaged content file on a site server, the content files are added to the content library on the site server, and then registered in the site server database.  

-   When you import the prestaged content file on a distribution point, the content files are added to the content library on the distribution point, and a status message is sent to the site server that informs the site that the content is available on the distribution point.  

**Limitations and considerations for prestaged content:**  

-   **When the distribution point is located on the site server**, do not enable the distribution point for prestaged content. Instead, use the procedure in [How to prestage content on a distribution point on a site server](#bkmk_dpsiteserver).  

-   **When the distribution point is configured as a pull-distribution point**, do not enable the distribution point for prestaged content. The prestage content configuration for a distribution point overrides the pull-distribution point configuration. A pull-distribution point that is configured for prestaged content does not pull content from source distribution point and does not receive content from the site server.  

-   **The content library must be created on the distribution point before you can prestage content to the distribution point**. Distribute content over the network at least one time before you prestage content to the distribution point.  

-   **When you prestage content for a package with a long package source path** (for example, more than 140 characters), the Extract Content command-line tool might fail to successfully extract the content for that package to the content library.  

For information about when to prestage content files, see  *Prestaged content* in the [Manage network bandwidth for content management](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) topic.  

Use the following sections to prestage content.  

###  <a name="BKMK_CreatePrestagedContentFile"></a> Step 1: Create a Prestaged Content File  
 You can create a compressed, prestaged content file that contains the files and associated metadata for the content that you select in the Configuration Manager console. Use the following procedure to create a prestaged content file.  

##### To create a prestaged content file  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you want to prestage:  

    -   **Applications**: Expand **Application Management**, click **Applications**, and then select the applications that you want to prestage.  

    -   **Packages**: Expand **Application Management**, click **Packages**, and then select the packages that you want to prestage.  

    -   **Driver Packages**: Expand **Operating Systems**, click **Driver Packages**, and then select the driver packages that you want to prestage.  

    -   **Operating System Images**: Expand **Operating Systems**, click **Operating System Images**, and then select the operating system images that you want to prestage.  

    -   **Operating System Installers**: Expand **Operating Systems**, click **Operating System Installers**, and then select the operating system installers that you want to prestage.  

    -   **Boot Images**: Expand **Operating Systems**, click **Boot Images**, and then select the boot images that you want to prestage.  

    -   **Task Sequences**: Expand **Operating Systems**, click **Task Sequences**, and then select the task sequence that you want to prestage.  

3.  On the **Home** tab, in the **Deployment** group, click **Create Prestage Content File**. The Create Prestaged Content File Wizard opens.  

    > [!NOTE]  
    >  **For Applications:** On the **Home** tab, in the **Application** group, click **Create Prestaged Content File**.  
    >   
    >  **For Packages:** On the **Home** tab, in the &lt;*PackageName*> group, click **Create Prestaged Content File**.  

4.  On the **General** page, click **Browse**, choose the location for the prestaged content file, specify a name for the file, and then click **Save**. You use this prestaged content file on primary site servers, secondary site servers, or distribution points to import the content and metadata.  

5.  For applications, select **Export all dependencies** to have Configuration Manager detect and add the dependencies associated with the application to the prestaged content file. By default, this setting is selected.  

6.  In **Administrator comments**, enter optional comments about the prestaged content file, and then click **Next**.  

7.  On the **Content** page, verify that the content listed is the content that you want to add to the prestaged content file, and then click **Next**.  

8.  On the **Content Locations** page, specify the distribution points from which to retrieve the content files for the prestaged content file. You can select more than one distribution point to retrieve the content. The distribution points are listed in the Content locations section. The **Content** column displays how many of the selected packages or applications are available on each distribution point. Configuration Manager starts with the first distribution point in the list to retrieve the selected content, and then moves down the list in order to retrieve the remaining content required for the prestaged content file. Click **Move Up** or **Move Down** to change the priority order of the distribution points. When the distribution points in the list do not contain all of the selected content, you must add distribution points to the list that contain the content or exit the wizard, distribute the content to at least one distribution point, and then restart the wizard.  

9. On the **Summary** page, confirm the details. You can go back to previous pages and make changes. Click **Next** to create the prestaged content file.  

10. The **Progress** page displays the content that is being added to the prestaged content file.  

11. On the **Completion** page, verify that the prestaged content file was created successfully, and then click **Close**.  

###  <a name="BKMK_AssignContentToDistributionPoint"></a> Step 2: Assign the Content to Distribution Points  
 After you prestage the content file, assign the content to distribution points.  

> [!NOTE]  
>  When you use a prestaged content file to recover the content library on a site server, and do not have to prestage the content files on a distribution point, you can skip this procedure.  

 Use the following procedure to assign the content in the prestaged content file to distribution points.  

> [!IMPORTANT]  
>  Verify that the distribution points that you want to prestage are configure  as prestaged distribution points, or that the content is distributed to the distribution points by using the network.  

##### To assign the content to distribution points  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you selected when you created the prestaged content file:  

    -   **Applications**: Expand **Application Management**, click **Applications**, and then select the applications that you prestaged.  

    -   **Packages**: Expand **Application Management**, click **Packages**, and then select the packages that you prestaged.  

    -   **Deployment Packages**: Expand **Software Updates**, click **Deployment Packages**, and then select the deployment packages that you prestaged.  

    -   **Driver Packages**: Expand **Operating Systems**, click **Driver Packages**, and then select the driver packages that you prestaged.  

    -   **Operating System Images**: Expand **Operating Systems**, click **Operating System Images**, and then select the operating system images that you prestaged.  

    -   **Operating System Installers**: Expand **Operating Systems**, click **Operating System Installers**, and then select the operating system installers that you prestaged.  

    -   **Boot Images**: Expand **Operating Systems**, click **Boot Images**, and then select the boot images that you prestaged.  

3.  On the **Home** tab, in the **Deployment** group, click **Distribute Content**. The Distribute Content Wizard opens.  

4.  On the **General** page, verify that the content listed is the content that you prestaged, choose whether you want Configuration Manager to detect content dependencies that are associated with the selected content and add the dependencies to the distribution, and then click **Next**.  

    > [!NOTE]  
    >  You have the option to configure the **Detect associated content dependencies and add them to this distribution** setting only for the application content type. Configuration Manager automatically configures this setting for task sequences, and it cannot be modified.  

5.  On the **Content** page, if displayed, verify that the content listed is the content that you want to distribute, and then click **Next**.  

    > [!NOTE]  
    >  The **Content** page displays only when the **Detect associated content dependencies and add them to this distribution** setting is selected on the **General** page of the wizard.  

6.  On the **Content Destination** page, click **Add**, choose one of the following that includes the distribution points to be prestaged, and then follow the associated step:  

    -   **Collections**: Select **User Collections** or **Device Collections**, click the collection associated with one or more distribution point groups, and then click **OK**.  

        > [!NOTE]  
        >  Only the collections that are associated with a distribution point group are displayed.  For more information, see [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) in the [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) topic.  

    -   **Distribution Point**: Select an existing distribution point, and then click **OK**. Distribution points that have previously received the content are not displayed.  

    -   **Distribution Point Group**: Select an existing distribution point group, and then click **OK**. Distribution point groups that have previously received the content are not displayed.  

    When you finish adding content destinations, click **Next**.  

7.  On the **Summary** page, review the settings for the distribution before you continue. To distribute the content to the selected destinations, click **Next**.  

8.  The **Progress** page displays the progress of the distribution.  

9. The **Confirmation** page displays whether or not the content was successfully assigned to the distribution points. To monitor the content distribution, see [Monitor content you have distributed with System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="BKMK_ExportContentFromPrestagedContentFile"></a> Step 3: Extract the Content from the Prestaged Content File  
 After you create the prestaged content file and assign the content to distribution points, you can extract the content files to the content library on a site server or distribution point. Typically, you have copied the prestaged content file to a portable drive like a USB drive, or have burned content to media like a DVD, and have it available at the location of the site server or distribution point that requires the content.  

 Use the following procedure to manually export the content files from the prestaged content file by using the Extract Content command-line tool.  

> [!IMPORTANT]  
>  When you run the Extract Content command-line tool, the tool creates a temporary file as it creates the prestaged content file. Then, the file is copied to the destination folder and the temporary file is deleted. You must have sufficient disk space for this temporary file or the process fails. The temporary file is created in the following location:  
>   
>  -   The temporary file is created in same folder that you specify as the destination folder for the prestaged content file.  

> [!IMPORTANT]  
>  The user that runs the Extract Content command-line tool must have **Administrator** rights on the computer from which you are extracting the prestaged content.  

##### To extract the content files from the prestaged content file  

1.  Copy the prestaged content file to the computer from which you want to extract the content.  

2.  Copy the Extract Content command-line tool from &lt;*ConfigMgrInstallationPath*>\bin\\&lt;*platform*> to the computer from which you want to extract the prestaged content file.  

3.  Open the command prompt and navigate to the folder location of the prestaged content file and Extract Content tool.  

    > [!NOTE]  
    >  You can extract one or more prestaged content files on a site server, secondary site server, or distribution point.  

4.  Type **extractcontent /P:**&lt;*PrestagedFileLocation*>**\\**&lt;*PrestagedFileName*> **/S** to import a single file.  

     Type **extractcontent /P:**&lt;*PrestagedFileLocation*> **/S** to import all prestaged files in the specified folder.  

     For example, type **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** where `D:\PrestagedFiles\` is the PrestagedFileLocation, `MyPrestagedFile.pkgx` is the prestaged file name, and `/S` informs Configuration Manager to extract only content files that are newer than what is currently on the distribution point.  

     When you extract the prestaged content file on a site server, the content files are added to the content library on the site server, and then the content availability is registered in the site server database. When you export the prestaged content file on a distribution point, the content files are added to the content library on the distribution point, the distribution point sends a status message to the parent primary site server, and then the content availability is registered in the site database.  

    > [!IMPORTANT]  
    >  In the following scenario, you must update content that you extracted from a prestaged content file when the content is updated to a new version:  
    >   
    >  1.  You create a prestaged content file for version 1 of a package.  
    >  2.  You update the source files for the package with version 2.  
    >  3.  You extract the prestaged content file (version 1 of the package) on a distribution point.  
    >   
    > Configuration Manager does not automatically distribute package version 2 to the distribution point. You must create a new prestaged content file that contains the new file version and then extract the content, update the distribution point to distribute the files that have changed, or redistribute all files in the package.  

###  <a name="bkmk_dpsiteserver"></a> How to prestage content on a distribution point on a site server  
 When a distribution point is installed on a site server, you must use the following procedure to successfully prestage content. This is because  the content files are already in the content library.  

 When the distribution point is not enabled for prestage content or when the distribution point is not located on a site server, see the [Use Prestaged content](#bkmk_prestage) section in this topic.  

##### To prestage content on distribution points located on a site server  

1.  Use the following steps to verify that the distribution point is not enabled for prestaged content.  

    1.  In the Configuration Manager console, click **Administration**.  

    2.  In the **Administration** workspace, click **Distribution Points**, and then select the distribution point that is located on the site server.  

    3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

    4.  On the **General** tab, verify that the **Enable this distribution point for prestaged content** check box is not selected.  

2.  Create the prestaged content file by using the [Step 1: Create a Prestaged Content File](#BKMK_CreatePrestagedContentFile) section in this topic.  

3.  Assign the content to the distribution point by using the [Step 2: Assign the Content to Distribution Points](#BKMK_AssignContentToDistributionPoint) section in this topic.  

4.  On the site server, extract the content from the prestaged content file by using the [Step 3: Extract the Content from the Prestaged Content File](#BKMK_ExportContentFromPrestagedContentFile) section in this topic.  

    > [!NOTE]  
    >  When the distribution point is on a secondary site, wait for at least 10 minutes, and then by using a Configuration Manager console that is connected to the parent primary site, assign the content to the distribution point on the secondary site.  

##  <a name="bkmk_manage"></a> Manage the content you have distributed  
 You have the following options for managing content:  
 - [Update content](#update-content)
 - [Redistribute content](#redistribute-content)
 - [Remove content](#remove-content)
 - [validate content](#validate-content)

### Update content
When the source file location for a deployment is updated by adding new files or replace existing files with a newer version, you can update the content files on distribution points by using the **Update Distribution Points** or **Update Content** action:  
-   The content files are copied from the source file path to the content library on the site that owns the package content source  
-   The package version is incremented  
-   Each instance of the content library on site servers and on  distribution points updates with only the files that have changed  

> [!WARNING]  
>  The package version for applications is always 1. When you update the content for an application deployment type, Configuration Manager creates a new content ID for the deployment type, and the package references the new content ID.  

#### To update content on distribution points  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you want to distribute:  

    -   **Applications**: Expand **Application Management** > **Applications**, and then select the applications that you want to distribute. Click the **Deployment Types** tab, and then select the deployment type that you want to update.  

    -   **Packages**: Expand **Application Management** > **Packages**, and then select the packages that you want to update.  

    -   **Deployment Packages**: Expand **Software Updates** > **Deployment Packages**, and then select the deployment packages that you want to update.  

    -   **Driver Packages**: Expand **Operating Systems** > **Driver Packages**, and then select the driver packages that you want to update.  

    -   **Operating System Images**: Expand **Operating Systems** > **Operating System Images**, and then select the operating system images that you want to update.  

    -   **Operating System Installers**: Expand **Operating Systems** > **Operating System Installers**, and then select the operating system installers that you want to update.  

    -   **Boot Images**: Expand **Operating Systems** >  **Boot Images**, and then select the boot images that you want to update.  

3.  On the **Home** tab, in the **Deployment** group, click **Update Distribution Points**, and then click **OK** to confirm that you want to update the content.  

    > [!NOTE]  
    >  To update content for applications, click the **Deployment Types** tab, right-click the deployment type, click **Update Content**, and then click **OK** to confirm that you want to refresh the content.  

    > [!NOTE]  
    >  When you update content for boot images, the Manage Distribution Point Wizard opens. Review the information on the **Summary** page, and then complete the wizard to update the content.  

### Redistribute content
You can redistribute a package to copy all of the content files in the package to distribution points or distribution point groups and thereby overwrite the existing files.  

 Use this operation to repair content files in the package or resend the content when the initial distribution fails. You can redistribute a package from:  

-   Package properties  
-   Distribution point properties  
-   Distribution point group properties.  


#### To redistribute content from package properties  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you want to distribute:  

    -   **Applications**: Expand **Application Management** >  **Applications**, and then select the application that you want to redistribute.  

    -   **Packages**: Expand **Application Management** > **Packages**, and then select the package that you want to redistribute.  

    -   **Deployment Packages**: Expand **Software Updates** >  **Deployment Packages**, and then select the deployment package that you want to redistribute.  

    -   **Driver Packages**: Expand **Operating Systems** > **Driver Packages**, and then select the driver package that you want to redistribute.  

    -   **Operating System Images**: Expand **Operating Systems** > **Operating System Images**, and then select the operating system image that you want to redistribute.  

    -   **Operating System Installers**: Expand **Operating Systems** > **Operating System Installers**, and then select the operating system installer that you want to redistribute.  

    -   **Boot Images**: Expand **Operating Systems** >  **Boot Images**, and then select the boot image that you want to redistribute.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  Click the **Content Locations** tab, select the distribution point or distribution point group in which you want to redistribute the content, click **Redistribute**, and then click **OK**.  

#### To redistribute content from distribution point properties  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Distribution Points**, and then select the distribution point in which you want to redistribute content.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  Click the **Content** tab, select the content to redistribute, click **Redistribute**, and then click **OK**.  

#### To redistribute content from distribution point group properties  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Distribution Point Groups**, and then select the distribution point group in which you want to redistribute content.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  Click the **Content** tab, select the content to redistribute, click **Redistribute**, and then click **OK**.  

    > [!IMPORTANT]  
    >  The content in the package is redistributed to all of the distribution points in the distribution point group.  


#### Use the SDK to force replication of content
You can use the **RetryContentReplication** Windows Management Instrumentation (WMI) class method from the Configuration Manager SDK to force Distribution Manager to copy content from the source location to the content library.  

Only use this method to force replication when you must redistribute content after there were issues with normal replication of content (typically confirmed by use of the Monitoring node of the console).   

For more information about this SDK option, see [RetryContentReplication Method in Class SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) on MSDN.Microsoft.com.

### Remove content
When you no longer require content on your distribution points, you can remove the content files on the distribution point.  

-   Package properties  
-   Distribution point properties  
-   Distribution point group properties.  

However, when the content is associated with another package that was distributed to the same distribution point, you cannot remove the content.  

#### To remove package content files from distribution points  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you want to delete:  

    -   **Applications**: Expand **Application Management** > **Applications**, and then select the application that you want to remove.  

    -   **Packages**: Expand **Application Management** > **Packages**, and then select the package that you want to remove.  

    -   **Deployment Packages**: Expand **Software Updates** > **Deployment Packages**, and then select the deployment package that you want to remove.  

    -   **Driver Packages**: Expand **Operating Systems** > **Driver Packages**, and then select the driver package that you want to remove.  

    -   **Operating System Images**: Expand **Operating Systems** > **Operating System Images**, and then select the operating system image that you want to remove.  

    -   **Operating System Installers**: Expand **Operating Systems** > **Operating System Installers**, and then select the operating system installer that you want to remove.  

    -   **Boot Images**: Expand **Operating Systems** > **Boot Images**, and then select the boot image that you want to remove.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  Click the **Content Locations** tab, select the distribution point or distribution point group from which you want to remove the content, click **Remove**, and then click **OK**.  

#### To remove package content from distribution point properties  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Distribution Points**, and then select the distribution point in which you want to delete the content.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  Click the **Content** tab, select the content to remove, click **Remove**, and then click **OK**.  

#### To remove content from distribution point group properties  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Distribution Point Groups**, and then select the distribution point group in which you want to remove content.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  Click the **Content** tab, select the content to remove, click **Remove**, and then click **OK**.  


### Validate content
The content validation process verifies the integrity of content files on distribution points. You enable content validation on a schedule, or you can manually initiate content validation from the properties of distribution points and packages.  

 When the content validation process starts, Configuration Manager verifies the content files on distribution points, and if the file hash is unexpected for the files on the distribution point, Configuration Manager creates a status message that you can review in the **Monitoring** workspace.  

 For more information about configuring the content validation schedule, see [Distribution point configurations](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) in the [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) topic.  


#### To initiate content validation for all content on a distribution point  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Distribution Points**, and then select the distribution point in which you want to validate content.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  On the **Content** tab, select the package in which you want to validate the content, click **Validate**, click **OK**, and then click **OK**. The content validation process initiates for the package on the distribution point.  

5.  To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and click the **Content Status** node. The content for each package type (for example, Application, Software Update Package, and Boot Image) is displayed. For more information about monitoring content status, see [Monitor content you have distributed with System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### To initiate content validation for a package  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, select one of the following steps for the type of content that you want to validate:  

    -   **Applications**: Expand **Application Management** > **Applications**, and then select the application that you want to validate.  

    -   **Packages**: Expand **Application Management** > **Packages**, and then select the package that you want to validate.  

    -   **Deployment Packages**: Expand **Software Updates** > **Deployment Packages**, and then select the deployment package that you want to validate.  

    -   **Driver Packages**: Expand **Operating Systems** > **Driver Packages**, and then select the driver package that you want to validate.  

    -   **Operating System Images**: Expand **Operating Systems** > **Operating System Images**, and then select the operating system image that you want to validate.  

    -   **Operating System Installers**: Expand **Operating Systems** >  **Operating System Installers**, and then select the operating system installer that you want to validate.  

    -   **Boot Images**: Expand **Operating Systems** > **Boot Images**, and then select the boot image that you want to prestage.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  On the **Content Locations** tab, select the distribution point or distribution point group in which to validate the content, click **Validate**, click **OK**, and then click **OK**. The content validation process starts for the content on the selected distribution point or distribution point group.  

5.  To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and click the **Content Status** node. The content for each package type (for example, Application, Software Update Package, and Boot Image) is displayed. For more information about monitoring the content status, see [Monitor content you have distributed with System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
