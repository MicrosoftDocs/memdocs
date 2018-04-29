---
title: Create an image for an OEM in factory or a local depot
titleSuffix: Configuration Manager
description: Use prestaged media deployments to reduce network traffic while you deploy an operating system to a computer that is not fully provisioned.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Create an image for an OEM in factory or a local depot with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Prestaged media deployments in System Center Configuration Manager let you deploy an operating system to a computer that is not fully provisioned. The prestaged media is a Windows Imaging Format (WIM) file that can be installed on a bare-metal computer by the manufacturer (OEM) or at an enterprise staging center that is not connected to the Configuration Manager environment. Later in the Configuration Manager environment, the computer starts by using the boot image provided by the media, a hash check is run on the prestaged media to make sure it is valid, and then the computer connects to the site management point for available task sequences that complete the download process.


This method of deployment can reduce network traffic because the boot image and operating system image are already on the destination computer. You can specify applications, packages, and driver packages to include in the pre-staged media. After the operating system is installed on the computer, the local task sequence cache is checked for applications, packages, or driver packages first, and if the content cannot be found or has been revised, the content is downloaded from a distribution point configured in the prestaged media and then installed.  

 You can use prestaged media in the following operating system deployment scenarios:  

-   [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)  

 Complete the steps in one of the operating system deployment scenarios and then use the following sections to prepare for and create the prestaged media.  

## Configure deployment settings  
 When you use prestaged media to start the operating system deployment process, you must configure the deployment to make the operating system available to media. You can configure this on the **Deployment Settings** page of the Deploy Software Wizard or the **Deployment Settings** tab in the properties for the deployment.  For the **Make available to the following** setting, configure one of the following:  

-   **Configuration Manager clients, media and PXE**  

-   **Only media and PXE**  

-   **Only media and PXE (hidden)**  

## Create the prestaged media  
 Create the prestaged media file to send to the OEM or your local depot. For more information, see [Create prestaged media with System Center Configuration Manager](create-prestaged-media.md).  

## Send the prestaged media file to the OEM or local depot  
 Send the media to the OEM or your local depot to prestage the computers. The prestaged media file is applied to a formatted hard disk on the computer.  

## Start the computer to install the operating system  
 The prestaged media file is applied to computers. When the computer is started for the first time, the operating system installation process starts.  
