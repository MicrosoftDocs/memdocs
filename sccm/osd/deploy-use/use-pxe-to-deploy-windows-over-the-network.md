---
title: Use PXE for OSD over the network
titleSuffix: Configuration Manager
description: Use PXE-initiated OS deployments to refresh a computer’s operating system or to install a new version of Windows on a new computer.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Use PXE to deploy Windows over the network with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Preboot execution environment (PXE)-initiated OS deployments in Configuration Manager let clients request and deploy operating systems over the network. In this deployment scenario, you send the OS image and the boot images to a PXE-enabled distribution point.

> [!NOTE]  
>  When you create an OS deployment that targets only x64 BIOS computers, both the x64 boot image and x86 boot image must be available on the distribution point.

You can use PXE-initiated OS deployments in the following scenarios:

-   [Refresh an existing computer with a new version of Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

-   [Install a new version of Windows on a new computer (bare metal)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

Complete the steps in one of the OS deployment scenarios, and then use the sections in this article to prepare for PXE-initiated deployments.



##  <a name="BKMK_Configure"></a> Configure at least one distribution point to accept PXE requests

To deploy operating systems to Configuration Manager clients that make PXE boot requests, you must configure one or more distribution points to accept PXE requests. Once you configure the distribution point, it responds to PXE boot requests and determines the appropriate deployment action to take. For more information, see [Install or modify a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

> [!NOTE]  
>  When configuring a single PXE enabled distribution point to support multiple subnets it is not supported to use DHCP options. Configure IP helpers on the routers to allow PXE requests to be forwarded to your PXE enabled distribution points.

## Prepare a PXE-enabled boot image

To use PXE to deploy an OS, you must have both x86 and x64 PXE-enabled boot images distributed to one or more PXE-enabled distribution points. Use the information to enable PXE on a boot image and distribute the boot image to distribution points:

-   To enable PXE on a boot image, select **Deploy this boot image from the PXE-enabled distribution point** from the **Data Source** tab in the boot image properties.

-   If you change the properties for the boot image, redistribute the boot image to distribution points. For more information, see [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Create an exclusion list for PXE deployments

When you deploy operating systems with PXE, you can create an exclusion list on each distribution point. Add the MAC addresses to the exclusion list of the computers you want the distribution point to ignore. Listed computers don't receive the deployment task sequences that Configuration Manager uses for PXE deployment.

#### To create the exclusion list

1.  Create a text file on the distribution point that is enabled for PXE. As an example, name this text file **pxeExceptions.txt**.  

2.  Use a plain text editor, such as Notepad, and add the MAC addresses of the computers to be ignored by the PXE-enabled distribution point. Separate the MAC address values by colons, and enter each address on a separate line. For example: `01:23:45:67:89:ab`  

3.  Save the text file on the PXE-enabled distribution point site system server. The text file may be saved to any location on the server.  

4.  Edit the registry of the PXE-enabled distribution point to create a **MACIgnoreListFile** registry key. Add the string value of the full path for the text file on the PXE-enabled distribution point site system server. Use the following registry path:  

     `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    >  If you use the Registry Editor incorrectly, you might cause serious problems that may require you to reinstall the operating system. Microsoft cannot guarantee that you can solve problems that result from using the Registry Editor incorrectly. Use the Registry Editor at your own risk.  

5. Restart the WDS service or PXE responder service after you make this registry change. You don't need to restart the server.<!--512129-->  



## Manage duplicate hardware identifiers

Configuration Manager may recognize multiple computers as the same device if they have duplicate SMBIOS attributes or you use a shared network adapter. Mitigate these issues by managing duplicate hardware identifiers in hierarchy settings. For more information, see [Manage duplicate hardware identifiers](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a>RamDisk TFTP block size and window size

You can customize the RamDisk TFTP block and window sizes for PXE-enabled distribution points. If you've customized your network, a large block or window size could cause the boot image download to fail with a time-out error. The RamDisk TFTP block and window size customizations allow you to optimize TFTP traffic when using PXE to meet your specific network requirements. To determine what configuration is most efficient, test the customized settings in your environment. For more information, see [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_RamDiskTFTP).



## Configure deployment settings

To use a PXE-initiated OS deployment, configure the deployment to make the OS available for PXE boot requests. Configure available operating systems on the **Deployment Settings** tab in the deployment properties. For the **Make available to the following** setting, select one of the following options:

-   Configuration Manager clients, media, and PXE

-   Only media and PXE

-   Only media and PXE (hidden)



##  <a name="BKMK_Deploy"></a> Deploy the task sequence

Deploy the OS to a target collection. For more information, see [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). When you deploy operating systems by using PXE, you can configure whether the deployment is required or available.

-   **Required deployment**: Required deployments use PXE without any user intervention. The user can't bypass the PXE boot. However, if the user cancels the PXE boot before the distribution point responds, the OS isn't deployed.

-   **Available deployment**: Available deployments require that the user is present at the destination computer. A user must press the **F12** key to continue the PXE boot process. If a user isn't present to press **F12**, the computer boots into the current OS, or from the next available boot device.

You can redeploy a required PXE deployment by clearing the status of the last PXE deployment assigned to a Configuration Manager collection or a computer. For more information on the **Clear Required PXE Deployments** action, see [Manage clients](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) or [Manage collections](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). This action resets the status of that deployment and reinstalls the most recent required deployments.

> [!IMPORTANT]  
> The PXE protocol isn't secure. Make sure that the PXE server and the PXE client are located on a physically secure network, such as in a data center to prevent unauthorized access to your site.



##  How is the boot image selected for clients booting with PXE?

When a client boots with PXE, Configuration Manager provides the client with a boot image to use. Configuration Manager uses a boot image with an exact architecture match. If a boot image with the exact architecture isn't available, Configuration Manager uses a boot image with a compatible architecture. 

The following list provides details about how a boot image is selected for clients booting with PXE:  

1. Configuration Manager looks in the site database for the system record that matches the MAC address or SMBIOS of the client that's trying to boot.  

    > [!NOTE]  
    > If a computer that's assigned to a site boots to PXE for a different site, the policies aren't visible for the computer. For example, if a client is already assigned to site A, the management point and distribution point for site B aren't able to access the policies from site A. The client doesn't successfully PXE boot.  

2. Configuration Manager looks for task sequences that are deployed to the system record found in step 1.  

3. In the list of task sequences found in step 2, Configuration Manager looks for a boot image that matches the architecture of the client that's trying to boot. If a boot image is found with the same architecture, that boot image is used.  

4. If a boot image isn't found with the same architecture, Configuration Manager looks for a boot image that's compatible with the architecture of the client. It looks in the list of task sequences found in step 2. For example, a 64-bit client is compatible with 32-bit and 64-bit boot images. A 32-bit client is compatible with only 32-bit boot images. An UEFI client is compatible with only 64-bit boot images.  
