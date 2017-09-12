---
title: Refresh an existing computer with a new version of Windows | Microsoft Docs
description: "You can use several methods in Configuration Manager to partition and format (wipe) an existing computer and install a new operating system on the computer."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
caps.latest.revision: 7
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Refresh an existing computer with a new version of Windows using System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic provides the general steps in System Center Configuration Manager to partition and format (wipe) an existing computer and install a new operating system on the computer. For this scenario, you can choose from many different deployment methods, such as PXE, bootable media, or Software Center. You can also  choose to install a state migration point to store settings and then restore them to the new operating system after it is installed. If you are unsure that this is the right operating system deployment scenario for you, see [Scenarios to deploy enterprise operating systems](scenarios-to-deploy-enterprise-operating-systems.md).  

 Use the following sections to refresh an existing computer with a new version of Windows.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Plan for and implement  infrastructure requirements**  

     There are several infrastructure requirements that must be in place before you can deploy operating systems, such as Windows ADK, User State Migration Tool (USMT), Windows Deployment Services (WDS), supported hard disk configurations, etc. For more information, see [Infrastructure requirements for operating system deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Install a state migration point (required only if you transfer settings)**  

     When you are going to capture settings from the existing computer, and then restore the settings to the new operating system, you must install a state migration point. For more information, see [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Configure  

1.  **Prepare a boot image**  

     Boot images start a computer in a Windows PE environment (a minimal operating system with limited components and services) that can then install a full Windows operating system on the computer.   When you deploy operating systems, you must select a boot image to use and distribute the image to a distribution point. Use the following to prepare the boot image:  

    -   To learn more about boot images, see [Manage boot images](../get-started/manage-boot-images.md).  

    -   For more information about how  to customize a boot image, see [Customize boot images](../get-started/customize-boot-images.md).  

    -   Distribute the boot image to distribution points. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Prepare an operating system image**  

     The operating system image contains the files necessary to install the operating system on the destination computer. Use the following to prepare the operating system image:  

    -   To learn more about how to create an operating system image, see  [Manage operating system images](../get-started/manage-operating-system-images.md).  

    -   Distribute the operating system image to distribution points. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Create a task sequence to deploy operating systems over the network**  

     Use a task sequence to automate the installation of the operating system over the network. Use the steps in [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md) to create the task sequence to deploy the operating system. Depending on the deployment method that you choose, there might be additional considerations for the task sequence.  

    > [!NOTE]  
    >  In this scenario, the task sequence formats and partitions the hard disks on the computer. To capture user settings, you must use the state migration point, and select **Save user settings and files on a State Migration Point** on the **State Migration** page of the Create Task Sequence wizard. If you save the user settings and files locally, they will be lost when the hard disk is formatted and Configuration Manager will be unable to restore the settings. For more information, see [Manage user state](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Deploy  

-   Use one of the following deployment methods to deploy the operating system:  

    -   [Use PXE to deploy Windows over the network](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Use multicast to deploy Windows over the network](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Create an image for an OEM in factory or a local depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Use bootable media to deploy Windows over the network](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md)  

## Monitor  

-   **Monitor the task sequence deployment**  

     To monitor the task sequence deployment  to install the operating system, see [Monitor operating system deployments](monitor-operating-system-deployments.md).  
