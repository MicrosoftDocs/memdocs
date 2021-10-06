---
title: OSD infrastructure requirements
titleSuffix: Configuration Manager
description: Learn the external and product dependencies and requirements for OS deployment in Configuration Manager
ms.date: 09/08/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Infrastructure requirements for OS deployment in Configuration Manager

*Applies to: Configuration Manager (current branch)*

OS deployment in Configuration Manager has external dependencies as well as dependencies within the product. Use this article to help you prepare the infrastructure for OS deployment.

## Dependencies external to Configuration Manager

This section provides information about external tools, installation kits, and OS versions that are required to deploy operating systems in Configuration Manager.

### Windows ADK

The Windows Assessment and Deployment Kit (ADK) is a set of tools and documentation that support the configuration and deployment of Windows. Configuration Manager uses the Windows ADK to automate actions such as installing Windows, capturing images, and migrating user profiles and data.

For more information, see the following articles:

- [Support for the Windows ADK in Configuration Manager](../../core/plan-design/configs/support-for-windows-adk.md)

- [Download the Windows ADK](/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Make sure to download both the **Windows ADK** and the **Windows PE add-on for the ADK**.

- [Windows ADK scenarios for IT Pros](/windows/deployment/windows-adk-scenarios-for-it-pros)

#### Site systems

The Windows ADK is a prerequisite for the following site systems servers:

- The site server of the top-level site in the hierarchy

- The site server of each primary site in the hierarchy

- Every instance of the SMS Provider

> [!NOTE]
> Manually install the Windows ADK on each site server before you install the Configuration Manager site.

#### Windows ADK features

Install the following features of the Windows ADK:

- User State Migration Tool (USMT)

    > [!NOTE]
    > USMT isn't required on the SMS Provider.

- Windows Deployment Tools

- Windows Preinstallation Environment (Windows PE)

    > [!IMPORTANT]
    > Windows PE is a separate installer. Otherwise there's no functional difference from earlier versions of the Windows ADK.<!--SCCMDocs-pr issue 2908-->

For a list of the versions of the Windows ADK that you can use with different versions of Configuration Manager, see [Support for the Windows ADK](../../core/plan-design/configs/support-for-windows-adk.md).

### User State Migration Tool (USMT)

Configuration Manager uses a USMT package that includes the USMT source files to capture and restore the user state as part of your OS deployment. Configuration Manager setup at the top-level site automatically creates the USMT package. USMT captures user state from supported versions of Windows.

For more information, see the following articles:

- [Manage user state with Configuration Manager](../get-started/manage-user-state.md)

- [Common migration scenarios for USMT](/windows/deployment/usmt/usmt-common-migration-scenarios)

### Windows PE

Windows PE is used for boot images to start a computer. It's a Windows version with limited services that's used during the pre-installation and deployment of Windows. For more information about boot images, see [Manage boot images](../get-started/manage-boot-images.md).

### Windows Server Update Services (WSUS)

WSUS is required for the software update point, which is required to install software updates during OS deployment. For more information, see [Install a configure a software update point](../../sum/get-started/install-a-software-update-point.md).

### Internet Information Services (IIS) on the site system servers

IIS is required for the distribution point, state migration point, and management point. For more information, see [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).

### Windows Deployment Services (WDS)

You can use WDS for PXE deployments, or you can enable PXE on a distribution point without WDS. For more information, see [PXE provider options](#pxe-provider-options).

### Dynamic Host Configuration Protocol (DHCP)

DHCP is required for PXE deployments. You must have a functioning DHCP server with an active host to deploy operating systems by using PXE. For more information about PXE deployments, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### Windows device drivers

Windows device drivers can be used when you install the OS on the destination computer. They're also used when you run Windows PE in a boot image. For more information, see [Manage drivers](../get-started/manage-drivers.md).

## Configuration Manager dependencies

This section provides information about Configuration Manager OS deployment prerequisites.

### OS image

OS images in Configuration Manager are stored in the Windows Imaging (WIM) file format. They represent a compressed collection of reference files and folders. These images are required to successfully install and configure an OS on a computer. For more information, see [Manage OS images](../get-started/manage-operating-system-images.md).

### Driver catalog

To deploy a device driver, import the device driver, enable it, and make it available on a distribution point that the Configuration Manager client can access. For more information about the driver catalog, see [Manage drivers](../get-started/manage-drivers.md).

### Management point

Management points transfer information between clients and the Configuration Manager site. The client uses a management point to run the task sequence to complete the OS deployment. For more information about task sequences, see [Planning considerations for automating tasks](planning-considerations-for-automating-tasks.md).

### Distribution point

Distribution points are used in most deployments to store the data that's used to deploy an OS, such as the image or driver packages. Task sequences typically retrieve data from a distribution point to deploy the OS. For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

### PXE-enabled distribution point

To deploy PXE-initiated deployments, configure a distribution point to accept PXE requests from clients. For more information, see [Configure a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

### Multicast-enabled distribution point

To optimize your OS deployments by using multicast, configure a distribution point to support multicast. For more information, see [Configure a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

### State migration point

When you capture and restore user state data for side-by-side and refresh deployments, configure a state migration point to store the user state data on another computer.

For more about how to configure the state migration point, see [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#state-migration-point).

For more information about how to capture and restore user state, see [Manage user state](../get-started/manage-user-state.md).

### Reporting services point

To use Configuration Manager reports for OS deployments, install and configure a reporting point. For more information, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).

### Security permissions for OS deployments

The **Operating System Deployment Manager** security role is a built-in role that you can't change. However, you can copy the role, make changes, and then save these changes as a new custom security role. Here are some of the permissions that apply directly to OS deployments:

- **Boot Image Package**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope

- **Device Drivers**: Create, Delete, Modify, Modify Folder, Modify Report, Move Object, Read, Run Report

- **Driver Package**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope

- **Operating System Image**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope

- **Operating System Upgrade Package**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope

- **Task Sequence Package**: Create, Create Task Sequence Media, Delete, Modify, Modify Folder, Modify Report, Move Object, Read, Run Report, Set Security Scope

For more information, see [Create custom security roles](../../core/servers/deploy/configure/configure-role-based-administration.md#create-custom-security-roles).

### Security scopes for OS deployments

Use security scopes to provide administrative users with access to the securable objects used in OS deployments, such as OS and boot images, driver packages, and task sequence packages. For more information, see [Security scopes](../../core/understand/fundamentals-of-role-based-administration.md#security-scopes).

## PXE provider options

You can use Windows Deployment Services (WDS) on the same server as the distribution points that you configure to support PXE or multicast. WDS is included in the server OS. With this configuration, WDS is the service that performs the PXE boot. When the distribution point is installed and enabled for PXE, Configuration Manager installs a provider into WDS that uses the WDS PXE boot functions.

You can also enable PXE on a distribution point without WDS. For more information, see the **Enable a PXE responder without Windows Deployment Service** option in [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

### WDS requirements

- The WDS installation on the server requires that the administrator is a member of the local Administrators group.

- The WDS server must be either a member of an Active Directory domain or a domain controller for an Active Directory domain. All Windows domain and forest configurations support WDS.

- If the provider is installed on a remote server, install WDS on the site server and the remote provider.

> [!NOTE]
> If the server requires a restart, the installation of WDS might fail.

### Considerations when you have WDS and DHCP on the same server

If you plan to co-host the distribution point on a server running DHCP, consider the following configuration issues:

- You need a functioning DHCP server with an active scope. WDS uses PXE, which requires a DHCP server.

- A DNS server is required to run WDS.

- The following UDP ports must be open on the WDS server:

  - Port 67 (DHCP)

  - Port 69 (TFTP)

  - Port 4011 (PXE)

    > [!NOTE]
    > If DHCP authorization is required on the server, you need DHCP client port 68 to be open on the server.

- DHCP and WDS both require port number 67. If you co-host WDS and DHCP, you can move DHCP or the distribution point that's configured for PXE to a separate server. Or, you can use the following procedure to configure the WDS server to listen on a different port.

#### How to configure the WDS server to listen on a different port

1. Modify the following registry key:

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`

1. Set the registry value **UseDHCPPorts** to `0`.

1. For the new configuration to take effect, run the following command on the server:

    `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`

> [!NOTE]
> When you enable a PXE responder on a distribution point without WDS, it can be on the same server as the DHCP service. For more information, see [Configure at least one distribution point to accept PXE requests](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).

## Supported operating systems

All Windows operating systems listed as supported clients in [Supported operating systems for clients and devices](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) are supported for OS deployment.

## Supported disk configurations

Configuration Manager supports capturing an OS image only from computers that are configured with simple volumes. The following table lists the hard disk configurations that Configuration Manager OS deployment supports on reference and destination computers:

|Reference computer hard disk configuration|Destination computer hard disk configuration|
|------------------------------------------|--------------------------------------------|
|Basic disk|Basic disk|
|Simple volume on a dynamic disk|Simple volume on a dynamic disk|

Configuration Manager doesn't support the following hard disk configurations:

- Spanned volumes

- Striped volumes (RAID 0)

- Mirrored volumes (RAID 1)

- Parity volumes (RAID 5)

If the reference disk has a basic disk, you can't capture and apply the image to a destination computer with a dynamic disk.

## Next steps

- [Prepare site system roles for OS deployments](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Prepare for OS deployment](../get-started/prepare-for-operating-system-deployment.md)
