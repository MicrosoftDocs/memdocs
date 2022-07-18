---
title: Deploy content
titleSuffix: Configuration Manager
description: After you install distribution points for Configuration Manager, here's how you can begin to deploy content to them.
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Deploy and manage content for Configuration Manager

*Applies to: Configuration Manager (current branch)*

After you install distribution points for Configuration Manager, you can begin to deploy content to them. Typically, content transfers to distribution points across the network, but other options to get content to the distribution points exists. After content transfers to a distribution point, you can update, redistribute, remove, and validate that content on distribution points.  

<a name="bkmk_types"></a>

There are many types of content. All of the actions in this article apply to the following objects in the **Software Library** workspace in the Configuration Manager console:

- **Applications**: Expand the **Application Management** node, select **Applications**, and then select the specific applications.

- **Packages**: Expand the **Application Management** node, select **Packages**, and then select the specific packages.

- **Software update deployment packages**: Expand the **Software Updates** node, select **Deployment Packages**, and then select the specific deployment packages.

- **Driver packages**: Expand the **Operating Systems** node, select **Driver Packages**, and then select the specific driver packages.

- **OS images**: Expand the **Operating Systems** node, select **Operating System Images**, and then select the specific OS images.

- **OS upgrade packages**: Expand the **Operating Systems** node, select **Operating System Upgrade Packages**, and then select the specific OS upgrade packages.

- **Boot Images**: Expand the **Operating Systems** node, select **Boot Images**, and then select the specific boot images.

- **Task Sequences**: Expand the **Operating Systems** node, select **Task Sequences**, and then select the specific task sequence. Although task sequences don't contain content, they have associated content references.

## <a name="bkmk_distribute"></a> Distribute content

Typically, you distribute content to distribution points so that it's available to clients. The exception to this behavior is when you use on-demand content distribution for a specific deployment. When you distribute content, Configuration Manager stores content files in a package, and then distributes the package to the distribution point. The content for the package is pulled from the site server's content library.

When you create a package that contains source files, the site on which you create it becomes the site owner for the content source. Configuration Manager copies the source files from the source file path that you specify for the object to the content library on the site server that owns it. Then Configuration Manager replicates the information to additional sites. For more information, see [The content library](../../../plan-design/hierarchy/the-content-library.md).

Use the following procedure to distribute content to distribution points.  

1. In the Configuration Manager console, go to the **Software Library** workspace.

1. Select one of the [content types](#bkmk_types) that you want to distribute.

1. On the **Home** tab of the ribbon, in the **Deployment** group, select **Distribute Content**.

1. On the **General** page of the Distribute Content Wizard, verify that the content listed is the content that you want to distribute. Then choose whether you want Configuration Manager to detect content dependencies that are associated with the selected content and add the dependencies to the distribution.

    > [!NOTE]
    > For applications, you can also configure the **Detect associated content dependencies and add them to this distribution** setting. Configuration Manager automatically configures this setting for task sequences.

1. On the **Content** tab, if displayed, verify that the content listed is the content that you want to distribute.

    > [!NOTE]
    > The **Content** page displays only when you select the **Detect associated content dependencies and add them to this distribution** setting on the **General** page of the wizard.

1. On the **Content Destination** page, select **Add**, choose one of the following options:

    - **Collections**: Choose **User Collections** or **Device Collections**, and then select the collection associated with one or more distribution point groups.

        > [!NOTE]
        > It only displays the collections that are associated with a distribution point group. For more information, see [Manage distribution point groups](install-and-configure-distribution-points.md#bkmk_manage).

    - **Distribution Point**: Choose an existing distribution point, and then select **OK**. It doesn't display distribution points that have previously received the content.

    - **Distribution Point Group**: Choose an existing distribution point group, and then select **OK**. It doesn't display distribution point groups that have previously received the content.

    When you finish adding content destinations, select **Next**.

1. On the **Summary** page, review the settings for the distribution before you continue. To distribute the content to the selected destinations, select **Next**.

1. The **Progress** page displays the progress of the distribution.

1. The **Confirmation** page displays whether the content was successfully assigned to the servers. To further monitor the content distribution, see [Monitor content you've distributed with Configuration Manager](monitor-content-you-have-distributed.md).

## <a name="bkmk_prestage"></a> Use prestaged content

Prestaged content is a compressed file that contains the content files and associated metadata for a content type. You can then manually import this content to another site server, a secondary site, or a distribution point.

- When you import the prestaged content file on a site server, it adds the content files to its content library. It then registers the content in the site server database.

- When you import the prestaged content file on a distribution point, the content files are added to the content library on the distribution point. It then sends a status message to the site server, which informs the site that the content is available on the distribution point.

### Limitations and considerations for prestaged content

- When the distribution point is located on the site server, don't enable the distribution point for prestaged content. Instead use the procedure in [How to prestage content on a distribution point on a site server](#bkmk_dpsiteserver).

- When the distribution point is configured as a pull-distribution point, don't enable the distribution point for prestaged content. The prestage content configuration for a distribution point overrides the pull-distribution point configuration. A pull-distribution point that you configure for prestaged content doesn't pull content from its source distribution point and doesn't receive content from the site server.

- Before you can prestage content to the distribution point, create the content library on the server. Distribute content over the network at least once to prepare the content library. Then you can prestage content.

- When you prestage content for an object with a long package source path, the Extract Content command-line tool might fail. A long package source path is more than 140 characters.

For more information about when to prestage content files, see [Manage network bandwidth for content management](../../../plan-design/hierarchy/manage-network-bandwidth.md).

### <a name="BKMK_CreatePrestagedContentFile"></a> Step 1: Create a prestaged content file

1. In the Configuration Manager console, go to the **Software Library** workspace.

1. Select one of the [content types](#bkmk_types) that you want to prestage.

1. On the **Home** tab of the ribbon, select **Create Prestage Content File**.

1. On the **General** page of the Create Prestaged Content File Wizard, select **Browse**. Choose the location for the prestaged content file, specify a name for the file, and then select **Save**. You use this prestaged content file on primary site servers, secondary site servers, or distribution points to import the content and metadata.

1. For applications, select **Export all dependencies** to have Configuration Manager detect and add the dependencies associated with the application to the prestaged content file. By default, this setting is selected.

1. In **Administrator comments**, enter optional comments about the prestaged content file.

1. On the **Content** page, verify that the content listed is the content that you want to add to the prestaged content file.

1. On the **Content Locations** page, specify the distribution points from which to retrieve the content for the prestaged content file. You can select more than one distribution point to retrieve the content. The distribution points are listed in the Content locations section. The **Content** column displays how many of the selected packages or applications are available on each distribution point.

    Configuration Manager starts with the first distribution point in the list to retrieve the selected content. It then moves down the list to retrieve the remaining content required for the prestaged content file. To change the priority order of the distribution points, select **Move Up** or **Move Down**.

    When the distribution points in the list don't contain all of the selected content, add distribution points to the list that contain the content. Otherwise, exit the wizard, distribute the content to at least one distribution point, and then restart the wizard.

1. On the **Summary** page, confirm the details. You can go back to previous pages and make changes. Select **Next** to create the prestaged content file.

1. The **Progress** page displays the content that it's adding to the prestaged content file.

1. On the **Completion** page, verify that it successfully created the prestaged content file, and then select **Close**.

### <a name="BKMK_AssignContentToDistributionPoint"></a> Step 2: Assign the content to distribution points

After you prestage the content file, assign the content to distribution points.

> [!NOTE]
> When you use a prestaged content file to recover the content library on a site server, and don't have to prestage the content files on a distribution point, you can skip this procedure.

Use the following procedure to assign the content in the prestaged content file to distribution points.

> [!IMPORTANT]
> Verify that the distribution points that you want to prestage are configured as prestaged distribution points, or that the content is distributed to the distribution points over the network.

1. In the Configuration Manager console, go to the  **Software Library** workspace.

1. Select the same [content type](#bkmk_types) that you selected when you [created the prestaged content file](#BKMK_CreatePrestagedContentFile).

1. On the **Home** tab, in the **Deployment** group, select **Distribute Content**.

1. On the **General** page of the Distribute Content Wizard, verify that the content listed is the content that you prestaged. Choose whether you want Configuration Manager to detect content dependencies that are associated with the selected content and add the dependencies to the distribution.

    > [!NOTE]
    > For applications, you can also configure the **Detect associated content dependencies and add them to this distribution** setting. Configuration Manager automatically configures this setting for task sequences.

1. On the **Content** page, if displayed, verify that the content listed is the content that you want to distribute.

    > [!NOTE]
    > The **Content** page displays only when the **Detect associated content dependencies and add them to this distribution** setting is selected on the **General** page of the wizard.

1. On the **Content Destination** page, select **Add**, and choose one of the following options that includes the distribution points to be prestaged:

    - **Collections**: Choose **User Collections** or **Device Collections**, then select the collection associated with one or more distribution point groups.

      > [!NOTE]
      > It only displays the collections that are associated with a distribution point group. For more information, see [Manage distribution point groups](install-and-configure-distribution-points.md#bkmk_manage).

    - **Distribution Point**: Select an existing distribution point, and then select **OK**. It doesn't display distribution points that already have the content.

    - **Distribution Point Group**: Select an existing distribution point group, and then select **OK**. It doesn't display distribution point groups that already have the content.

    When you finish adding content destinations, select **Next**.

1. On the **Summary** page, review the settings for the distribution before you continue. To distribute the content to the selected destinations, select **Next**.

1. The **Progress** page displays the progress of the distribution.

1. The **Confirmation** page displays whether the content was successfully assigned to the distribution points. To monitor the content distribution, see [Monitor content you've distributed](monitor-content-you-have-distributed.md).

### <a name="BKMK_ExportContentFromPrestagedContentFile"></a> Step 3: Extract the content from the prestaged content file

After you create the prestaged content file and assign the content to distribution points, extract the content files to the content library on the target server.

First, manually copy the prestaged content file to the target server. Use a portable drive like a USB drive, or media like a DVD. Have it available at the location of the server that requires the content.

Next, you use the Extract Content command-line tool to export the content files from the prestaged content file.

- When you run the tool, it creates a temporary file as it creates the content files. Then it copies the file to the destination folder, and deletes the temporary file. The server needs sufficient disk space for this temporary file.

- The tool creates the temporary file in the specified destination folder for the content files.

- The user that runs the tool must have **Administrator** rights on the server where you extract the content.

#### To extract the content files from the prestaged content file

1. Copy the prestaged content file to the server where you want to extract the content.

1. Copy **ExtractContent.exe** from the `\bin\x64` subfolder of the Configuration Manager site installation. Copy it to the same folder on the target server as the prestaged content file.

1. On the target server, open the command prompt. Navigate to the folder location of the prestaged content file and Extract Content tool.

    > [!NOTE]
    > You can extract one or more prestaged content files on a site server, secondary site server, or distribution point.

1. Use the following commands to import the content:

    - Single file: `extractcontent.exe /P:<PrestagedFileLocation>\<PrestagedFileName> /S`

    - All prestaged files in the specified folder: `extractcontent.exe /P:<PrestagedFileLocation> /S`

    For example, if `D:\PrestagedFiles\` is the prestaged file location, and `MyPrestagedFile.pkgx` is the prestaged file name:

    `extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S`

    The `/S` parameter extracts only content files that are newer than what's currently in the content library.

    When you extract the prestaged content file on a site server, the content files are added to its content library. The site then registers the content in the site server database. When you export the prestaged content file on a distribution point, it adds the content files to the content library on the distribution point. The distribution point sends a status message to the parent primary site server, which then registers the content in the site database.

> [!IMPORTANT]
> When you update content on the site to a new version, make sure to also update content for prestaged content files. For example:
>
> 1. You create a prestaged content file for version 1 of a package.
> 1. You update the source files for the package with version 2.
> 1. You extract the version 1 prestaged content file on a distribution point.
>
> In this example, Configuration Manager doesn't automatically distribute package version 2 to the distribution point. Create a new prestaged content file that contains the new file version. Then extract the content, update the distribution point to distribute the files that have changed, or redistribute all files in the package.

### <a name="bkmk_dpsiteserver"></a> How to prestaged content on a distribution point on a site server

When a distribution point is installed on a site server, use the following procedure to successfully prestage content. This process is different because the content files are already in the content library.

When the distribution point isn't enabled for prestaged content or when the distribution point isn't located on a site server, see the [Use Prestaged content](#bkmk_prestage) section.

1. Verify that the distribution point isn't enabled for prestaged content.

    1. In the Configuration Manager console, go to the **Administration** workspace.

    1. In the **Administration** workspace, select the **Distribution Points** node. Then select the distribution point that's on the site server.

    1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

    1. On the **General** tab, verify that the option to **Enable this distribution point for prestaged content** isn't selected.

1. [Create a prestaged content file](#BKMK_CreatePrestagedContentFile).

1. [Assign the content to the distribution point](#BKMK_AssignContentToDistributionPoint).

1. On the site server, [extract the content from the prestaged content file](#BKMK_ExportContentFromPrestagedContentFile).

    > [!NOTE]
    > When the distribution point is on a secondary site, wait for at least 10 minutes. Then in the Configuration Manager console, assign the content to the distribution point on the secondary site.

## <a name="bkmk_manage"></a> Manage distributed content

You have the following options for managing content:

- [Update content](#update-content)
- [Update content on schedule](#update-content-on-schedule)
- [Redistribute content](#redistribute-content)
- [Remove content](#remove-content)
- [Validate content](#validate-content)

### Update content

When you update the source file location for a deployment by adding new files or replace existing files with a newer version, update the content files on distribution points. Use the **Update Distribution Points** or **Update Content** actions.

- The site copies the content files from the original package source location to the content library on the site that owns the package content source.
- It increments the package version.
- Each instance of the content library on site servers and on distribution points updates with only the changed files.

> [!WARNING]
> The package version for applications is always **1**. When you update the content for an application deployment type, Configuration Manager creates a new content ID for the deployment type, and the package references the new content ID.

#### Process to update content on distribution points

1. In the Configuration Manager console, go to the **Software Library** workspace.

1. Select the [content type](#bkmk_types) that you want to update.

1. For most object types: On the **Home** tab of the ribbon, in the **Deployment** group, select **Update Distribution Points**. Then select **OK** to confirm that you want to update the content.

    To update content for applications: Select the **Deployment Types** tab in the details pane. Choose the deployment type. On the **Deployment Type** tab of the ribbon, select **Update Content**. Then select **OK** to confirm that you want to refresh the content.

    When you update content for boot images: The **Update Distribution Points** action opens the Manage Distribution Point Wizard. For more information, see [Update distribution points with the boot image](../../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

### Update content on schedule

<!-- SCCMDocs#2132 -->

You can create a schedule for when the site updates the content for the object. Use this option for an object whose content changes frequently.

1. In the Configuration Manager console, go to the **Software Library** workspace.

1. Select the [content type](#bkmk_types) that you want to update.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Data source** tab. Select the option to **Update distribution points on a schedule**.

1. Select **Schedule** and specify a custom schedule. You can also set a recurrence pattern.

If the source content hasn't changed, then this action doesn't do anything. To redistribute all content, use the [distribute](#bkmk_distribute) or [redistribute](#redistribute-content) actions.

### Redistribute content

You can redistribute a package to copy all of the content files in the package to distribution points or distribution point groups. This action overwrites the existing files.

Use this operation to repair content files in the package or resend the content when the initial distribution fails. You can redistribute a package from:

- Package properties
- Distribution point properties
- Distribution point group properties

#### Process to redistribute content from package properties

1. In the Configuration Manager console, go to the **Software Library** workspace.

1. Select the [content types](#bkmk_types) that you want to redistribute.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content Locations** tab. Select the distribution point or distribution point group to which you want to redistribute the content, and select **Redistribute**.

#### Process to redistribute content from distribution point properties

1. In the Configuration Manager console, go to the **Administration** workspace.

1. In the **Administration** workspace, select the **Distribution Points** node. Then select the distribution point to which you want to redistribute content.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content** tab. Select the content to redistribute, and select **Redistribute**.

#### Process to redistribute content from distribution point group properties

1. In the Configuration Manager console, go to the **Administration** workspace.

1. In the **Administration** workspace, select the **Distribution Point Groups** node. Then select the distribution point group to which you want to redistribute content.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content** tab. Select the content to redistribute, and select **Redistribute**.

    > [!IMPORTANT]
    > The site redistributes the content in the package to all of the distribution points in the group.

#### Use the SDK to force replication of content

You can use the **RetryContentReplication** WMI method from the Configuration Manager SDK to force distribution manager to copy content from the source location to the content library.

Only use this method to force replication when you need to redistribute content after there were issues with normal replication of content. You can typically confirm this state in the **Monitoring** node of the console.

For more information about this SDK option, see [RetryContentReplication method in class SMS_CM_UpdatePackages](../../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md).

### Remove content

When you no longer require content on your distribution points, you can remove it.

When the content is associated with another package that was distributed to the same distribution point, you can't remove the content.

#### Process to remove content from distribution points using object properties

1. In the Configuration Manager console, select the **Software Library** workspace.

1. Select the [content type](#bkmk_types) that you want to remove its content.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content Locations** tab. Select the distribution point or distribution point group from which you want to remove the content, select **Remove**, and then select **OK**.

#### Process to remove content using distribution point properties

1. In the Configuration Manager console, select the **Administration** workspace.

1. In the **Administration** workspace, select the **Distribution Points** node, and then select the distribution point from which you want to delete the content.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content** tab. Choose the content to remove, select **Remove**, and then select **OK**.

#### Process to remove content using distribution point group properties

1. In the Configuration Manager console, select the **Administration** workspace.

1. In the **Administration** workspace, select the **Distribution Point Groups** node. Then select the distribution point group from which you want to remove content.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content** tab. Choose the content to remove, select **Remove**, and then select **OK**.

### Validate content

The content validation process verifies the integrity of content files on distribution points. You enable content validation on a schedule, or you can manually start content validation from the properties of distribution points and packages.

When the content validation process starts, Configuration Manager verifies the content files on distribution points. If the file hash is unexpected for the files on the distribution point, Configuration Manager creates a status message that you can review in the **Monitoring** workspace.

For more information about configuring the content validation schedule, see [Distribution point configurations](install-and-configure-distribution-points.md#bkmk_configs).

#### Process to validate all content on a distribution point

1. In the Configuration Manager console, select the **Administration** workspace.

1. Select the **Distribution Points** node, and then select the distribution point from which you want to validate content.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content** tab. Select the package that you want to validate. Select **Validate**, and then select **OK**. The content validation process starts for the package on the distribution point.

1. To view the results of the content validation process, go to the **Monitoring** workspace. Expand **Distribution Status**, and select the **Content Status** node. This node displays the content for each type. For more information about monitoring content status, see [Monitor content you've distributed](monitor-content-you-have-distributed.md).

#### Process to validate content for a specific object

1. In the Configuration Manager console, select the **Software Library** workspace.

1. Select the [content type](#bkmk_types) that you want to validate.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Content Locations** tab. Select the distribution point or distribution point group on which to validate the content. Select **Validate**, and then select **OK**. The content validation process starts for the content on the selected distribution point or distribution point group.

1. To view the results of the content validation process, go to the **Monitoring** workspace. Expand **Distribution Status**, and select the **Content Status** node. It displays the content for each type. For more information about monitoring the content status, see [Monitor content you've distributed](monitor-content-you-have-distributed.md).
