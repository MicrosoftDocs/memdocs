---
title: Use PXE for OSD over the network
titleSuffix: Configuration Manager
description: Use PXE-initiated OS deployments to refresh a computer's operating system or to install a new version of Windows on a new computer.
ms.date: 07/15/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Use PXE to deploy Windows over the network with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Preboot execution environment (PXE)-initiated OS deployments in Configuration Manager let clients request and deploy operating systems over the network. For this deployment method, you send the OS image and the boot images to a PXE-enabled distribution point.

> [!NOTE]
> When you create an OS deployment that targets only x64 BIOS computers, both the x64 boot image and x86 boot image must be available on the distribution point.

You can use PXE-initiated OS deployments in the following scenarios:

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

Complete the steps in one of the OS deployment scenarios, and then use the sections in this article to prepare for PXE-initiated deployments.

> [!WARNING]
> If you use PXE deployments, and configure device hardware with the network adapter as the first boot device, these devices can automatically start an OS deployment task sequence without user interaction. [Deployment verification](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) doesn't manage this configuration. While this configuration may simplify the process and reduce user interaction, it puts the device at greater risk for accidental reimage.

Starting in version 2006, PXE-based task sequences can download cloud-based content. The PXE-enabled distribution point still requires the boot image, and the device needs an intranet connection to the management point. It can then get additional content from a content-enabled cloud management gateway (CMG).<!--6209223--> For more information, see [Bootable media support for cloud-based content](deploy-task-sequence-over-internet.md#bootable-media-support-for-cloud-based-content).

## <a name="BKMK_Configure"></a> Configure distribution points for PXE

To deploy operating systems to Configuration Manager clients that make PXE boot requests, configure one or more distribution points to accept PXE requests. Then the distribution point responds to PXE boot requests, and determines the appropriate deployment action. For more information, see [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

> [!NOTE]
> When you configure a single PXE-enabled distribution point to support multiple subnets, it's not supported to use DHCP options. To allow the network to forward client PXE requests to PXE-enabled distribution points, configure IP helpers on the routers.

When you enable a PXE responder on a distribution point without Windows Deployment Service, it can be on the same server as the DHCP service.<!--3734270, SCCMDocs-pr #3416--> Add the following settings to support this configuration:

- Set the DWord value **DoNotListenOnDhcpPort** to `1` in the following registry key: `HKLM\Software\Microsoft\SMS\DP`.
- Set DHCP option 60 to `PXEClient`.
- Restart the SCCMPXE and DHCP services on the server.

## Prepare a PXE-enabled boot image

To use PXE to deploy an OS, distribute both x86 and x64 PXE-enabled boot images to one or more PXE-enabled distribution points.

- To enable PXE on a boot image, select **Deploy this boot image from the PXE-enabled distribution point** from the **Data Source** tab in the boot image properties.

- When you change the properties for the boot image, update and redistribute the boot image to distribution points. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## Manage duplicate hardware identifiers

Configuration Manager may recognize multiple computers as the same device if they have duplicate SMBIOS attributes or you use a shared network adapter. Mitigate these issues by managing duplicate hardware identifiers in hierarchy settings. For more information, see [Manage duplicate hardware identifiers](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="BKMK_PXEExclusionList"></a> Create an exclusion list for PXE deployments

> [!NOTE]
> In some circumstances, the process to [Manage duplicate hardware identifiers](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) may be easier.<!-- SCCMDocs issue 802 -->
>
> The behaviors of each can cause different results in some scenarios. The exclusion list never boots a client with the listed MAC address, no matter what.
>
> The duplicate ID list doesn't use the MAC address to find the task sequence policy for a client. If it matches the SMBIOS ID, or if there's a task sequence policy for unknown machines, the client still boots.

When you deploy operating systems with PXE, you can create an exclusion list on each distribution point. Add the MAC addresses to the exclusion list of the computers you want the distribution point to ignore. Listed computers don't receive the deployment task sequences that Configuration Manager uses for PXE deployment.

1. Create a text file on the PXE-enabled distribution point. For example, name the file **pxeExceptions.txt**.

1. Use a plain text editor, such as Notepad, to edit the file. Add the MAC addresses of the computers that the PXE-enabled distribution point should ignore. Separate the MAC address values by colons, and enter each address on a separate line. For example: `01:23:45:67:89:ab`

1. Save the text file on the PXE-enabled distribution point. You can save it to any location on the server.

1. Edit the registry on the PXE-enabled distribution point. Browse to the following registry path: `HKLM\Software\Microsoft\SMS\DP`. Create a **MACIgnoreListFile** string value. Add the full path to the text file on the PXE-enabled distribution point.

    > [!WARNING]
    > If you use the Registry Editor incorrectly, you might cause serious problems that may require you to reinstall Windows. Microsoft can't guarantee that you can solve problems that result from using the Registry Editor incorrectly. Use the Registry Editor at your own risk.

1. After you make this registry change, restart the WDS service or PXE responder service. You don't need to restart the server.<!--512129-->

## <a name="BKMK_RamDiskTFTP"></a> RamDisk TFTP block size and window size

You can customize the RamDisk TFTP block and window sizes for PXE-enabled distribution points. If you've customized your network, a large block or window size could cause the boot image download to fail with a time-out error. The RamDisk TFTP block and window size customizations allow you to optimize TFTP traffic when using PXE to meet your specific network requirements. To determine what configuration is most efficient, test the customized settings in your environment. For more information, see [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points).

## Configure deployment settings

To use a PXE-initiated OS deployment, configure the deployment to make the OS available for PXE boot requests. Configure available operating systems on the **Deployment Settings** tab in the deployment properties. For the **Make available to the following** setting, select one of the following options:

- Configuration Manager clients, media, and PXE

- Only media and PXE

- Only media and PXE (hidden)

## Option 82 during PXE DHCP handshake

Configuration Manager supports option 82 during the PXE DHCP handshake with the PXE responder without WDS. If you require option 82, make sure to use the PXE responder without WDS. Configuration Manager doesn't support option 82 with WDS.

## <a name="BKMK_Deploy"></a> Deploy the task sequence

Deploy the OS to a target collection. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md). When you deploy operating systems by using PXE, you can configure whether the deployment is required or available.

- **Required deployment**: Required deployments use PXE without any user intervention. The user can't bypass the PXE boot. However, if the user cancels the PXE boot before the distribution point responds, the OS isn't deployed.

- **Available deployment**: Available deployments require that the user is present at the destination computer. A user must press the **F12** key to continue the PXE boot process. If a user isn't present to press **F12**, the computer boots into the current OS, or from the next available boot device.

You can redeploy a required PXE deployment by clearing the status of the last PXE deployment assigned to a Configuration Manager collection or a computer. For more information on the **Clear Required PXE Deployments** action, see [Manage clients](../../core/clients/manage/manage-clients.md#manage-clients-from-the-devices-node) or [Manage collections](../../core/clients/manage/collections/manage-collections.md). This action resets the status of that deployment and reinstalls the most recent required deployments.

> [!IMPORTANT]
> The PXE protocol isn't secure. Make sure that the PXE server and the PXE client are located on a physically secure network, such as in a data center, to prevent unauthorized access to your site.

## How the boot image is selected for PXE

When a client boots with PXE, Configuration Manager provides the client with a boot image to use. Configuration Manager uses a boot image with an exact architecture match. If a boot image with the exact architecture isn't available, Configuration Manager uses a boot image with a compatible architecture.

The following list provides details about how a boot image is selected for clients booting with PXE:  

1. Configuration Manager looks in the site database for the system record that matches the MAC address or SMBIOS of the client that's trying to boot.  

    > [!NOTE]  
    > If a computer that's assigned to a site boots to PXE for a different site, the policies aren't visible for the computer. For example, if a client is already assigned to site A, the management point and distribution point for site B aren't able to access the policies from site A. The client doesn't successfully PXE boot.  

2. Configuration Manager looks for task sequences that are deployed to the system record found in step 1.  

3. In the list of task sequences found in step 2, Configuration Manager looks for a boot image that matches the architecture of the client that's trying to boot. If a boot image is found with the same architecture, that boot image is used.  

    If it finds more than one boot image, it uses the *highest* or most recent task sequence deployment ID. In the case of a multi-site hierarchy, the *higher* letter site would take precedence in that string comparison. For example, if they're both matched otherwise, a year-old deployment from site ZZZ is selected over yesterday's deployment from site AAA.<!-- SCCMDocs issue 877 -->  

4. If a boot image isn't found with the same architecture, Configuration Manager looks for a boot image that's compatible with the architecture of the client. It looks in the list of task sequences found in step 2. For example, a 64-bit BIOS/MBR client is compatible with 32-bit and 64-bit boot images. A 32-bit BIOS/MBR client is compatible with only 32-bit boot images. UEFI clients are only compatible with matching architecture. A 64-bit UEFI client is compatible with only 64-bit boot images and a 32-bit UEFI client is compatible with only 32-bit boot images.

## Next steps

[User experiences for OS deployment](../understand/user-experience.md#pxe)
