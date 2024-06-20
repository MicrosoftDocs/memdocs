---
title: Remote control prerequisites
titleSuffix: Configuration Manager
description: Get the prerequisites for remote control in Configuration Manager.
ms.date: 03/18/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Prerequisites for remote control in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Remote control in Configuration Manager has external dependencies and dependencies in the product.

## Dependencies external to Configuration Manager

To help improve performance, install the most up-to-date video driver on client devices.

You can't use Configuration Manager remote control to remotely administer client computers that run versions of the Configuration Manager client earlier than current branch.

> [!NOTE]
> No Windows services are required as an external dependency for remote control.

### Supported operating systems for the remote control viewer

The remote control viewer is supported on all operating systems that are supported for the Configuration Manager console. For information, see [Supported configurations for Configuration Manager consoles](../../../plan-design/configs/supported-operating-systems-consoles.md).

The following OS versions don't support the remote control viewer, but they do support the remote control client:

- Windows Embedded
- Windows Embedded for Point of Service (POS)
- Windows Fundamentals for Legacy PCs

## Configuration Manager dependencies

### Enable remote control

By default, remote control isn't enabled when you install Configuration Manager. For more information about how to enable and configure remote control, see [Configure remote control](configuring-remote-control.md).

### Reporting

Before you can run reports for remote control, install the reporting services point site system role. For more information, see [Introduction to reporting](../../../servers/manage/introduction-to-reporting.md).

### Security permissions

- To access collection resources and to start a remote control session from the Configuration Manager console, your account needs the **Read**, **Read Resource**, and **Remote Control** permissions for the **Collection** object.

- The **Remote Tools Operator** security role includes the permissions that are required to manage remote control in Configuration Manager.

- Permitted viewers must be given permission to use remote control by adding these users to the **Permitted viewers of Remote Control and Remote Assistance** list in the **Remote Tools** client settings.

For more information, see [Configure role-based administration](../../../servers/deploy/configure/configure-role-based-administration.md).

### Remote clients

Remote tools aren't supported for clients that are connected remotely. For example, you can't remote control a client that communicates with the site through a cloud management gateway (CMG). For more information about the network ports required for remote tools, see [Ports used in Configuration Manager](../../../plan-design/hierarchy/ports.md#BKMK_PortsConsole-Client).

> [!TIP]
> For tenant-attached devices, remote tools are available in the Microsoft Intune admin center. For more information, see [Support for remote tools](../cmg/supported-configurations.md#bkmk_note3).

## Next steps

[Configure remote control](configuring-remote-control.md)
