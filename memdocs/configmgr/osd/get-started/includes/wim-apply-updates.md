---
author: banreet
ms.author: banreetkaur
ms.service: configuration-manager
ms.topic: include
ms.date: 08/10/2021
ms.localizationpriority: medium
---

## Apply software updates to an image

> [!NOTE]
> This section applies to both **OS images** and **OS upgrade packages**. It uses the general term "image" to refer to the Windows image file (WIM). Both of these objects have a WIM, which contains Windows installation files. Software updates are applicable to these files in both objects. The behavior of this process is the same between both objects.

Each month there are new software updates applicable to the image. Before you can apply software updates to it, you need the following prerequisites:

- A software updates infrastructure
- Successfully synchronized software updates
- Downloaded the software updates to the content library on the site server

For more information, see [Deploy software updates](../../../sum/deploy-use/deploy-software-updates.md).

Apply applicable software updates to an image on a specified schedule. This process is sometimes called *offline servicing*. On this schedule, Configuration Manager applies the selected software updates to the image. It can then also redistribute the updated image to distribution points.

> [!IMPORTANT]
> While you can select any software update that's applicable to the image based on version, DISM can only apply certain types of updates to the image. The **OfflineServicingMgr.log** file shows the following entry: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

The site database stores information about the image, including the software updates that were applied at the time of the import. Software updates that you apply to the image since it was initially added are also stored in the site database. When you start the wizard to apply software updates, it retrieves the list of applicable software updates that the site hasn't yet applied to the image. Configuration Manager copies the software updates that you select from the content library on the site server. It then applies the software updates to the image.

### Servicing process

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select either **Operating System Images** or **Operating System Upgrade Packages**.

1. Select the object to which to apply software updates.

1. On the ribbon, select **Schedule Updates** to start the wizard.

1. On the **Choose Updates** page, select the software updates to apply to the image. It may take some time for the list of updates to appear in the wizard. Use the **Filter** to search for strings in the metadata. Use the **System architecture** drop-down list to filter on **X86**, **X64**, or **All**. You can select one, many, or all updates in the list. When you're finished selecting updates, select **Next**.

1. On the **Set Schedule** page, specify the following settings, and then select **Next**.

    1. **Schedule**: Specify the schedule for when the site applies the software updates to the image.

    1. **Continue on error**: Select this option to continue to apply software updates to the image even when there's an error.

    1. **Update distribution points with the image**: Select this option to update the image on distribution points after the site applies the software updates.

1. Complete the Schedule Updates Wizard.

> [!NOTE]
> To minimize the payload size, the servicing of OS upgrade packages and OS images removes the older version.

### Servicing operations

In the Configuration Manager console, in either the **OS Images** or **OS Upgrade Packages** node, add the following columns to the view:

- **Scheduled Updates Date**: This property shows the next schedule that you've defined.
- **Scheduled Updates Status**: This property shows the status. For example, **Successful** or **In Process**.

Select a specific image object, and then switch to the **Update Status** tab in the details pane. This tab shows the list of updates in the image.

Select a specific image object, and select **Properties** in the ribbon. The **Installed Updates** tab shows the list of updates in the image. The **Servicing** tab is a read-only view of the current servicing schedule and the updates that you've scheduled to apply.

When the status is **In Process**, you can select **Cancel Scheduled Updates** on the ribbon. This action cancels the active servicing process.

To troubleshoot this process, view the **OfflineServicingMgr.log** and **dism.log** files on the site server. For more information, see [Log files](../../../core/plan-design/hierarchy/log-files.md).

### Specify the drive for offline OS image servicing

<!--1358924-->

You can specify the drive that Configuration Manager uses during offline servicing of OS images. This process can consume a large amount of disk space with temporary files. This option gives you flexibility to select the drive to use.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. In the ribbon, select **Configure Site Components** and then choose **Operating System Deployment**.

1. On the **Offline Servicing** tab, specify the option for **A local drive to be used by offline servicing of images**.

By default, this setting is **Automatic**. With this value, Configuration Manager selects the drive on which it's installed.

If you select a drive that doesn't exist on the site server, Configuration Manager behaves the same as if you select **Automatic**.

During offline servicing, Configuration Manager stores temporary files in the folder, `<drive>:\ConfigMgr_OfflineImageServicing`. It also mounts the OS image in this folder.

### Optimized image servicing

<!--3555951-->

When you apply software updates to an OS image, you can optimize the output by removing any superseded updates. The optimization to offline servicing only applies to images with a single index.

When you schedule the site to apply software updates to an OS image, it uses the Windows Deployment Image Servicing and Management (DISM) command-line tool. During the servicing process, this change introduces the following two additional steps:

- It runs DISM against the mounted offline image with the parameters `/Cleanup-Image /StartComponentCleanup /ResetBase`. If this command fails, the current servicing process fails. It doesn't commit any changes to the image.

- After Configuration Manager commits changes to the image and unmounts it from the file system, it exports the image to another file. This step uses the DISM parameter `/Export-Image`. It removes unneeded files from the image, which reduces the size.

Microsoft recommends that you regularly apply updates to your offline images. You don't have to use this option every time you service an image. When you do this process each month, this option provides you the greatest advantage by using it over time. For more information, see [Recommendations for Install Software Updates step](../../understand/install-software-updates.md#recommendations).

While this option helps reduce the overall size of the serviced image, it does take longer to complete the process. Use the wizard to schedule servicing during convenient times. It also requires additional storage on the site server. You can customize the site to use an alternate location. For more information, see [Specify the drive for offline OS image servicing](#specify-the-drive-for-offline-os-image-servicing).

#### Process to optimize image servicing

1. Start the [servicing process](#servicing-process).

1. On the **Set Schedule** page, select the option to **Remove superseded updates after the image is updated**. This option isn't automatically enabled. If the image has more than one index, you can't use this option.

1. To schedule image servicing, complete the wizard.

Validate and monitor the process using the **OfflineServicing.log**.
