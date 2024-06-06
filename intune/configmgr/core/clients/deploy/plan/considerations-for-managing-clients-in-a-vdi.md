---
title: Manage VDI clients
titleSuffix: Configuration Manager
description: Manage Configuration Manager clients in a virtual desktop infrastructure (VDI).
ms.date: 08/11/2020
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Manage Configuration Manager clients in a virtual desktop infrastructure (VDI)

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports installing the Configuration Manager client on the following virtual desktop infrastructure (VDI) scenarios:

- **Personal virtual machines**: The virtual machine (VM) maintains user data and settings between sessions.

- **Remote Desktop Services sessions**: Host multiple, concurrent client sessions on a centralized server. Users connect to a session and run applications on that server.

- **Pooled virtual machines/Non-Persistent**: The VM doesn't persist between sessions. When a user closes a session, the virtual environment discards all data and settings. Pooled virtual machines are useful when you can't use Remote Desktop Services. For example, if a required application can't run on the Windows Server that hosts the client sessions.

- **Azure Virtual Desktop**: A desktop and app virtualization service that runs on Microsoft Azure. Starting in version 1906, use Configuration Manager to manage these virtual devices running Windows in Azure.

## Personal VMs

Configuration Manager treats personal VMs the same as a physical computer. You can preinstall the Configuration Manager client on the VM image or after you provision it.

For more information, see [Support for virtualization environments](../../../plan-design/configs/support-for-virtualization-environments.md).

## Remote Desktop Services

You don't install the Configuration Manager client for individual Remote Desktop sessions. Install it once on the server that hosts Remote Desktop Services. You can use all Configuration Manager client features on the Remote Desktop Services server.

For more information, see [Welcome to Remote Desktop Services](/windows-server/remote/remote-desktop-services/welcome-to-rds).

## Pooled VMs/Non-Persistent

When you decommission a pooled virtual machine, any changes made by Configuration Manager are lost.

Because the VM might only be operational for a short length of time, some Configuration Manager features may not return relevant data. For example, hardware inventory, software inventory, and software metering. Consider excluding pooled VM from inventory tasks.

## Azure Virtual Desktop

For more information, see [Supported operating systems for clients and devices](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#azure-virtual-desktop).

## Other considerations

Because virtualization supports running multiple Configuration Manager clients on the same physical computer, many client operations have a built-in randomized delay for scheduled actions. For example, hardware and software inventory, antimalware scans, software installations, and software update scans. This delay helps distribute the CPU processing and data transfer for a server that has multiple VMs that run the Configuration Manager client.

Except for Windows Embedded clients in servicing mode, Configuration Manager clients not in virtualized environments also use this randomized delay. This behavior helps avoid peaks in network bandwidth. It also reduces the CPU processing on site systems, such as the management point and site server. The delay interval varies according to the Configuration Manager capability. For example, see [About client settings - Disable deadline randomization](../about-client-settings.md#disable-deadline-randomization).

To help with Configuration Manager client performance in virtual environments that support multiple user sessions, it disables user policy by default. Starting in version 1910, you can enable user policy in this scenario. For more information, see [About client settings - Enable user policy for multiple user sessions](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).
