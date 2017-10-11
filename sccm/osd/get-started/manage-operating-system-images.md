---
title: Manage operating system images
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, learn about the methods that you can use to manage operating system images that are stored in Windows Imaging (WIM) files."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
caps.latest.revision: 17
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Manage operating system images with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Operating system images in Configuration Manager are stored in the Windows Imaging (WIM) file format and represent a compressed collection of reference files and folders that are required to successfully install and configure an operating system on a computer. For all operating system deployment scenarios, you must select an operating system image.   You can use the default operating system image or  build the operating system image from a reference computer that you configure. When you build the reference computer, you can add operating system files, drivers, support files, software updates, tools, and other software applications to the operating system before you capture it to create the image file. The following provides information about each method.  

 **Default image**  

 The default operating system image (install.wim) is included with the Windows operating system installation files. This image is a basic operating system image that contains a standard set of drivers. When you use the default operating system image, you can install apps and make other configurations after the operating system installs by using task sequence steps.  The default operating system image is located in <*operating system source path*>\Sources\install.wim.  

-   **Advantages**  

    -   The image size is smaller than a captured image.  

    -   Installing apps and configurations with task sequence steps  is more dynamic. For example, you can change the apps that will install and the configurations in the task sequence and not have to re-image the operating system.  

-   **Disadvantages**  

    -   Operating system installation can take more time because the app installation and other configurations occur after the operating system installation completes.  

 **Captured image**  

 To create a customized operating system image, you build a reference computer with the desired operating system, and install apps, configure settings, etc. Then, you capture the operating system image from the reference computer to create the WIM file. You can build the reference computer manually or use a task sequence to automate some or all of the build steps.   
For the steps to create a customized operating system image, see [Customize operating system images](customize-operating-system-images.md).  

-   **Advantages**  

    -   The installation can be faster than using the default image. For example, apps can be pre-installed with the captured operating system image and you won't need to install apps later by using task sequence steps.  

-   **Disadvantages**  

    -   Operating system installation can take more time because the app installation and other configurations occur after the operating system installation completes.  


##  <a name="BKMK_AddOSImages"></a> Add operating system images to Configuration Manager  
 Before you can use an operating system image, you must add the image to a Configuration Manager site. Use the following procedure to add an operating system image to a site.  

#### To add an operating system image to a site  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Operating System Images**.  

3.  On the **Home** tab, in the **Create** group, click **Add Operating System Image** to start the Add Operating System Image Wizard.  

4.  On the **Data Source** page, specify the network path to the operating system image. For example, specify **\\\server\path\OS.WIM**.  

5.  On the **General** page, specify the following information, and then click **Next**. This information is useful for identification purposes when you add multiple operating system images to the same site.  

    -   **Name**: Specify the name of the image. By default, the name of the image is taken from the WIM file.  

    -   **Version**: Specify the version of the image.  

    -   **Comment**: Specify a brief description of the image.  

6.  Complete the wizard.  

 You can now distribute the operating system image to distribution points.  

##  <a name="BKMK_DistributeBootImages"></a> Distribute operating system images to distribution points  
 Operating system images are distributed to distribution points in the same way as you distribute other content. In most cases, you must distribute the operating system image to at least one distribution point before you deploy the operating system. For the steps to distribute an operating system image, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSImagesApplyUpdates"></a> Apply software updates to an operating system image  
 Periodically, new software updates are released that are applicable to the operating system in your operating system image. Before you can apply software updates to an image you must have your software updates infrastructure in place, have successfully synchronized software updates, and downloaded the softare updates to the content library on the site server. For more information, see [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md).  

 You can apply applicable software updates to an image on a specified schedule. On the schedule that you specify, Configuration Manager applies the software updates that you select to the operating system image, and then optionally distributes the updated image to distribution points. Information about the operating system image is stored in the site database, including the software updates that were applied at the time of the import. Software updates that have been applied to the image since it was initially added are also stored in the site database. When you start the wizard to apply software updates to the operating system image, the wizard retrieves a list of applicable software updates that have not yet been applied to the image for you to select. Configuration Manager copies the software updates from the content library on the site server and applies the software updates to the operating system image.  

 Use the following procedure to apply software updates to an operating system image.  

#### To apply software updates to an operating system image  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Operating System Images**.  

3.  Select the operating system image to which to apply software updates.  

4.  On the **Home** tab, in the **Operating System Image** group, click **Schedule Updates** to start the wizard.  

5.  On the **Choose Updates** page, select the software updates to apply to the operating system image, and then click **Next**.  

6.  On the **Set Schedule** page, specify the following settings, and then click **Next**.  

    1.  **Schedule**: Specify the schedule for when the software updates are applied to the operating system image.  

    2.  **Continue on error**:  Select this option to continue to apply software updates to the image even when there is an error.  

    3.  **Distribute the image to distribution points**: Select this option to update the operating system image on distribution points after the software updates are applied.  

7.  On the **Summary** page, verify the information, and then click **Next**.  

8.  On the **Completion** page, verify that the software updates were successfully applied to the operating system image.  

##  <a name="BKMK_OSImageMulticast"></a> Prepare the operating system image for multicast deployments  
 Use multicast deployments to allow multiple computers to simultaneously download an operating system image. The image is multicast to clients by  the distribution point, rather than having the distribution point send a copy of the image to each client over a separate connection. When you choose the [Use multicast to deploy Windows over the network](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) operating system deployment method, you must configure the operating system image package to support multicast before you distribute the operating system image to a multicast-enabled distribution point. Use the following procedure to set the multicast options for an existing operating system image package.  

#### To modify an operating system image package to use multicast  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Operating System Images**.  

3.  Select the operating system image that you want to distribute to the multicast-enabled distribution point.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  Select the **Distribution Settings** tab, and configure the following options:  

    -   **Allow this package to be transferred via multicast (WinPE only)**: You must select this option for Configuration Manager to simultaneously deploy operating system images.  

    -   **Encrypt multicast packages**: Specify whether the image is encrypted before it is sent to the distribution point. Use this option if the package contains sensitive information. If the image is not encrypted, the contents of the package will be visible in clear text on the network and might be read by an unauthorized user.  

    -   **Transfer this package only via multicast**: Specify whether you want the distribution point to deploy the image only during a multicast session.  

         If you select **Transfer this package only via multicast**, you must also specify **Download content locally when needed by running task sequence** as the deployment option for the operating system image. You can specify the deployment options for the image when you deploy the operating system image, or you can specify them later by editing the properties of the deployment. The deployment options are on the **Distribution Points** tab of the **Properties** page of the deployment object.  

6.  Click **OK**.  
