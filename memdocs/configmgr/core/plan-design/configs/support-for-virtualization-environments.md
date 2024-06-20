---
title: Support for virtualization
titleSuffix: Configuration Manager
description: The requirements for installing Configuration Manager client and site system roles in a virtualization environment.
ms.date: 08/02/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Support for virtualization environments with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports installing the client and site system roles on supported operating systems that run as a virtual machine (VM) in certain virtualization environments. This support exists even when the virtual host (virtualization environment) isn't supported as a client or site server.

For example, you use Microsoft Hyper-V Server 2016 to host a VM that runs Windows Server 2019. You can install the client or site system roles on the VM running Windows Server 2019. You can't install the client on the host running Microsoft Hyper-V Server 2016.

## Virtualization environments

- Windows Server 2022 (_starting in version 2107_)<!-- 10200029 -->
- Windows Server 2019
- Windows Server 2016 <sup>[Note 1](#bkmk_note1)</sup>
- Microsoft Hyper-V Server 2016 <sup>[Note 1](#bkmk_note1)</sup>
- Windows Server 2012 R2
- Microsoft Hyper-V Server 2012
- Windows Server 2012

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager doesn't support [nested virtualization](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), which is new with Windows Server 2016.

### Virtualization environment support

Each virtual computer needs the same or greater hardware and software requirements that you would use for a physical Configuration Manager computer.

To validate that Configuration Manager supports your virtualization environment, use the Server Virtualization Validation Program. It includes an online Virtualization Program Support Policy Wizard. For more information, see [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).

Configuration Manager can't manage VMs if they're offline. The Configuration Manager client on the host computer can't manage an offline VM image. For example, it can't install software updates or collect hardware inventory.

In general, Configuration Manager gives no special consideration to VMs. For example, if you stop a VM, and don't save its state, Configuration Manager might not determine if it has to reinstall a software update.

To help with Configuration Manager client performance in virtual environments that support multiple user sessions, it disables user policy by default. Starting in version 1910, you can enable user policy in this scenario. For more information, see [About client settings - Enable user policy for multiple user sessions](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="bkmk_Azure"></a> Microsoft Azure VMs

Configuration Manager can run on infrastructure as a service (IaaS) VMs in Azure just as it runs on-premises within your data center. Use Configuration Manager with Azure VMs in the following scenarios:

- **Scenario 1**: Run Configuration Manager on an Azure VM. Use it to manage clients on other Azure VMs.

- **Scenario 2**: Run Configuration Manager on an Azure VM. Use it to manage clients that aren't running on Azure.

- **Scenario 3**: Run different Configuration Manager site system roles on Azure VMs. Run other roles in your on-premises data center, properly connected to Azure.

> [!NOTE]
> These scenarios also apply to IaaS VMs on Azure Stack Hub.<!-- 10371381 -->

The same Configuration Manager requirements for networks, supported configurations, and hardware requirements also apply to Azure VMs.

For more information, see [Configuration Manager on Azure FAQ](../../understand/configuration-manager-on-azure.yml).

> [!IMPORTANT]
> Configuration Manager sites and clients that run on Azure VMs are subject to the same license requirements as on-premises installations.

## Azure Virtual Desktop

[Azure Virtual Desktop](/azure/virtual-desktop/) is a desktop and app virtualization service that runs on Microsoft Azure. Use Configuration Manager to manage these virtual devices running Windows in Azure. For more information, see [Supported operating systems for clients and devices](supported-operating-systems-for-clients-and-devices.md#azure-virtual-desktop).

## Next steps

[Manage Configuration Manager clients in a virtual desktop infrastructure (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)
