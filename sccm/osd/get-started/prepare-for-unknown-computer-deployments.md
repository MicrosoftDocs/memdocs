---
title: Prepare for unknown computer deployments
titleSuffix: "Configuration Manager"
description: "Learn how to deploy operating systems to computers that are not managed by Configuration Manager in your System Center Configuration Manager environment."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Prepare for unknown computer deployments in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the information in this topic to deploy operating systems to unknown computers in your System Center Configuration Manager environment. An unknown computer is a computer that is not managed by Configuration Manager. This means that there is no record of these computers in the Configuration Manager database. Unknown computers include the following:  

-   A computer where the Configuration Manager client is not installed  

-   A computer that is not imported into Configuration Manager  

-   A computer that is not been discovered by Configuration Manager  

 You can deploy operating systems to unknown computers with the following deployment methods:  

-   [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

-   [Use bootable media to deploy an operating system](../deploy-use/create-bootable-media.md)  

-   [Use prestaged media to deploy an operating system](../deploy-use/create-prestaged-media.md)  

## Unknown computer deployment workflow  
 The following is the basic workflow to deploy an operating system to an unknown computer:  

-   Select an unknown computer object to use in the deployment. You can deploy the operating system to one of the unknown computer objects in the **All Unknown Computers** collection or you can add the objects in the **All Unknown Computer** collection to another collection. Configuration Manager provides two unknown computer objects in the **All Unknown Computers** collection. One object is for x86 computers and the other object is for x64 computers.  

    > [!NOTE]  
    >  The **x86 Unknown Computer** object is for computers that are only x86 capable. The **x64 Unknown Computer** object is for computers that are x86 and x64 capable. In other words, these objects describe the architecture of the destination computer. They do not describe the operating system that you want to deploy to the destination computer.  

-   Configure a PXE-enabled distribution point or create media to support unknown computer deployments.  

-   Deploy the task sequence to install the  operating system.  

## Unknown Computer Installation Process  
 When a computer is first started from PXE or from media, Configuration Manager checks to see if a record for that computer exists in the Configuration Manager database. If there is a record, Configuration Manager then checks to see if there are any task sequences deployed to the record. If there is not a record, Configuration Manager checks to see if there are any task sequences deployed to an unknown computer object. In either case, Configuration Manager then performs one of the following actions:  

-   If there is an available task sequence, Configuration Manager prompts the user to run the task sequence.  

-   If there is a required task sequence, Configuration Manager automatically runs the task sequence.  

-   If a task sequence is not deployed for the record, Configuration Manager generates an error that there is no deployed task sequence for the destination computer.  

 When an unknown computer is started, Configuration Manager recognizes the computer as an unprovisioned computer rather than an unknown computer. This means that the computer can now receive the task sequences that were deployed to the unknown computer object. The deployed task sequence then installs an operating system image that must include the Configuration Manager client.  

 After the Configuration Manager client is installed, a record for the computer is created and the computer is listed in the appropriate Configuration Manager collection. If the computer fails to install the operating system image or the Configuration Manager client, an "Unknown" record for the computer is created and the computer appears in the **All Systems** collection.  

> [!NOTE]  
>  During the installation of the operating system image, the task sequence can retrieve collection variables but not computer variables from this computer.  

##  <a name="BKMK_EnablingUnknown"></a> Enabling Unknown Computer Support  
 Use the following to enable unknown computer support when you deploy an operating system by using PXE, bootable media, and prestaged media.  

-   **PXE**  

     Select the **Enable unknown computer support** check box on the **PXE** tab for a distribution point that is enabled for PXE. For more information, see [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Bootable media**  

     Select the **Enable unknown computer support** check box on the **Security** page of the Create Task Sequence Media Wizard. For more information, see [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) and [Use PXE to deploy Windows over the network with System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Prestaged media**  

     Select the **Enable unknown computer support** check box on the **Security** page of the Create Task Sequence Media Wizard. For more information, see [Create prestaged media with System Center Configuration Manager](../deploy-use/create-prestaged-media.md).  
