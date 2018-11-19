--- 
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 11/16/2018
---

##  <a name="BKMK_OSImagesApplyUpdates"></a> Apply software updates to an image  

> [!Note]  
> This section applies to both **OS images** and **OS upgrade packages**. It uses the general term "image" to refer to the Windows image file (WIM). Both of these objects have a WIM, which contains Windows installation files. Software updates are applicable to these files in both objects. The behavior of this process is the same between both objects.  

Each month there are new software updates applicable to the image. Before you can apply software updates to it, you need the following prerequisites: 

- A software updates infrastructure  
- Successfully synchronized software updates  
- Downloaded the software updates to the content library on the site server  

For more information, see [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates).  

Apply applicable software updates to an image on a specified schedule. This process is sometimes called *offline servicing*. On this schedule, Configuration Manager applies the selected software updates to the image. It can then also redistribute the updated image to distribution points. 

The site database stores information about the image, including the software updates that were applied at the time of the import. Software updates that you apply to the image since it was initially added are also stored in the site database. When you start the wizard to apply software updates, it retrieves the list of applicable software updates that the site hasn't yet applied to the image. Configuration Manager copies the software updates that you select from the content library on the site server. It then applies the software updates to the image.  


### Servicing process  

1.  In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select either **Operating System Images** or **Operating System Upgrade Packages**.  

2.  Select the object to which to apply software updates.  

3.  On the ribbon, select **Schedule Updates** to start the wizard.  

4.  On the **Choose Updates** page, select the software updates to apply to the image. It may take some time for the list of updates to appear in the wizard. Use the **Filter** to search for strings in the metadata. Use the **System architecture** drop-down list to filter on **X86**, **X64**, or **All**. You can select one, many, or all updates in the list. When you're finished selecting updates, select **Next**.  

5.  On the **Set Schedule** page, specify the following settings, and then click **Next**.  

    a.  **Schedule**: Specify the schedule for when the site applies the software updates to the image.  

    b.  **Continue on error**:  Select this option to continue to apply software updates to the image even when there's an error.  

    c.  **Update distribution points with the image**: Select this option to update the image on distribution points after the site applies the software updates.  

6.  Complete the Schedule Updates Wizard.  

> [!NOTE]  
>  To minimize the payload size, the servicing of OS upgrade packages and OS images removes the older version.  


### Servicing operations

In the Configuration Manager console, in either the **OS Images** or **OS Upgrade Packages** node, add the following columns to the view:
- **Scheduled Updates Date**: This property shows the next schedule that you've defined.  
- **Scheduled Updates Status**: This property shows the status. For example, **Successful** or **In Process**.  

Select a specific image object, and then switch to the **Update Status** tab in the details pane. This tab shows the list of updates in the image. 

Select a specific image object, and select **Properties** in the ribbon. The **Installed Updates** tab shows the list of updates in the image. The **Servicing** tab is a read-only view of the current servicing schedule and the updates that you've scheduled to apply. 

When the status is **In Process**, you can select **Cancel Scheduled Updates** on the ribbon. This action cancels the active servicing process. 

To troubleshoot this process, view the **OfflineServicingMgr.log** and **dism.log** files on the site server. For more information, see [Log files](/sccm/core/plan-design/hierarchy/log-files).


### <a name="bkmk_servicing-drive"></a> Specify the drive for offline OS image servicing  
<!--1358924-->

Starting in version 1810, specify the drive that Configuration Manager uses during offline servicing of OS images. This process can consume a large amount of disk space with temporary files. This option gives you flexibility to select the drive to use. 

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. In the ribbon, click **Configure Site Components** and select **Operating System Deployment**.  

2. On the **Offline Servicing** tab, specify the option for **A local drive to be used by offline servicing of images**.  

By default, this setting is **Automatic**. With this value, Configuration Manager selects the drive on which it's installed. 

If you select a drive that doesn't exist on the site server, Configuration Manager behaves the same as if you select **Automatic**. 

During offline servicing, Configuration Manager stores temporary files in the folder, `<drive>:\ConfigMgr_OfflineImageServicing`. It also mounts the OS image in this folder. 

