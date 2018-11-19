---
title: Manage OS images
titleSuffix: Configuration Manager
description: Learn the methods to manage OS images stored in Windows image (WIM) files.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage OS images with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

OS images in Configuration Manager are stored in the Windows image (WIM) file format. These images are a compressed collection of reference files and folders use to install and configure a new OS on a computer. Many OS deployment scenarios require an OS image. 

You can use a [default OS image](#default-image), or build the OS image from a [reference computer](#bkmk_capture) that you configure. When you build the reference computer, you add OS files, drivers, support files, software updates, tools, and applications to the OS. Then you capture it to create the image file. 

### Default image

The Windows installation files include the default OS image. This image is a basic OS image that contains a standard set of drivers. When you use the default OS image, use task sequence steps to install apps and make other configurations after the OS installs on a device. Locate the default OS image in the Windows source files: `\Sources\install.wim`.  

#### Default image advantages

- The image size is smaller than a captured image.  

- Installing apps and configurations with task sequence steps is more dynamic. For example, change the configurations and apps that install in the task sequence, without having to reimage the device.  

#### Default image disadvantages

- OS installation can take more time. The application installation and other configurations occur after the OS installation completes.  


### <a name="bkmk_capture"></a> Captured image from a reference computer

To create a customized OS image, build a reference computer with the desired OS. Then install applications and configure settings. Capture the OS image from the reference computer to create the WIM file. Manually build the reference computer, or use a task sequence to automate some or all of the build steps. For more information, see [Customize OS images](/sccm/osd/get-started/customize-operating-system-images).  

#### Captured image advantages

- The installation can be faster than using the default image. For example, applications can be preinstalled with the captured OS image. Then you don't need to install those same applications later by using task sequence steps.  

#### Captured image disadvantages

- The image size is potentially larger than the default image.  

- Need to create a new image when you require updates for applications and tools.  



##  <a name="BKMK_AddOSImages"></a> Add an OS image  

Before you can use an OS image, add it to your Configuration Manager site. 

1.  In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Operating System Images** node.  

2.  On the **Home** tab of the ribbon, in the **Create** group, select **Add Operating System Image**. This action starts the Add Operating System Image Wizard.  

3.  On the **Data Source** page, specify the network **Path** to the OS image file. For example, `\\server\share\path\image.wim`.  

4.  On the **General** page, specify the following information. This information is useful for identification purposes when you have more than one OS image.  

    -   **Name**: A unique name for the image. By default, the name comes from the WIM file name.  

    -   **Version**: An optional version identifier. This property doesn't need to be the OS version of the image. It's often your organization's version for the package.   

    -   **Comment**: An optional brief description.  

5.  Complete the wizard.  


Next, distribute the OS image to distribution points.  



##  <a name="BKMK_DistributeBootImages"></a> Distribute content to distribution points  

Distribute OS images to distribution points the same as other content. Before you deploy the task sequence, distribute the OS image to at least one distribution point. For more information, see [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



##  <a name="BKMK_OSImageMulticast"></a> Prepare the OS image for multicast deployments  

Use multicast deployments to allow more than one computer to simultaneously download an OS image. The image is multicast to clients by the distribution point, rather than each client downloading a copy of the image from the distribution point over a separate connection. When you choose the OS deployment method to [Use multicast to deploy Windows over the network](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network), configure the OS image to support multicast. Then distribute the image to a multicast-enabled distribution point. 

1.  In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Operating System Images** node.  

2.  Select the OS image that you want to distribute to a multicast-enabled distribution point.  

3.  On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.  

4.  Switch to the **Distribution Settings** tab, and configure the following options:  

    -   **Allow this package to be transferred via multicast (WinPE only)**: Select this option for Configuration Manager to simultaneously deploy OS images using multicast.  

    -   **Encrypt multicast packages**: Specify whether the site encrypts the image before it's sent to the distribution point. If the image contains sensitive information, use this option. If the image isn't encrypted, its contents are visible in clear text on the network. Then an unauthorized user could intercept and view the image contents.  

    -   **Transfer this package only via multicast**: Specify whether you want the distribution point to deploy the image only during a multicast session.  

         If you select **Transfer this package only via multicast**, you must also specify the task sequence deployment option to **Download content locally when needed by the running task sequence**. For more information, see [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).   

5.  Select **OK** to save the settings and close the image properties.  
