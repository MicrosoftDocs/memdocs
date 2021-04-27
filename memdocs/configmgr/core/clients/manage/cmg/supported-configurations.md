---
title: Supported configurations for CMG
titleSuffix: Configuration Manager
description: A list of the features and configurations that the Configuration Manager cloud management gateway supports.
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
ms.assetid: 10f4c4e8-84ac-48ae-9fdc-195f3bdfcd0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Supported configurations for cloud management gateway

*Applies to: Configuration Manager (current branch)*

Use this article as a reference for the features and configurations that are supported by the Configuration Manager cloud management gateway (CMG).

## Specifications

- All Windows versions listed in [Supported operating systems for clients and devices](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) are supported for CMG.

- CMG only supports the management point and software update point roles.

- CMG doesn't support clients that only communicate with IPv6 addresses.<!--495606-->

- Software update points using a network load balancer don't work with CMG. <!--505311-->

- CMG deployments with the **cloud service (classic)** method don't support subscriptions for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [Azure services available in the Azure CSP program](/partner-center/azure-plan-available). In version 2006 and earlier, this deployment method is the only option.

  Starting in version 2010, customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure.<!--3601040--> For more information, see [Topology design: Virtual machine scale sets](plan-cloud-management-gateway.md#virtual-machine-scale-sets).

## Support for Configuration Manager features

The following table lists CMG support for Configuration Manager features:

| Feature | Support |
|---------|---------|
| Software updates | ![Supported](media/green_check.png) |
| Endpoint protection | ![Supported](media/green_check.png) <sup>[Note&nbsp;1](#bkmk_note1)</sup> |
| Hardware and software inventory | ![Supported](media/green_check.png) |
| Client status and notifications | ![Supported](media/green_check.png) |
| Run scripts | ![Supported](media/green_check.png) |
| CMPivot | ![Supported](media/green_check.png) |
| Compliance settings | ![Supported](media/green_check.png) |
| Automatic client upgrade | ![Supported](media/green_check.png) |
| Client install<br>(with [Azure AD integration](../../deploy/deploy-clients-cmg-azure.md)) | ![Supported](media/green_check.png) |
| Client install<br>(with [token authentication](../../deploy/deploy-clients-cmg-token.md)) | ![Supported](media/green_check.png) (2002) |
| Software distribution (device-targeted) | ![Supported](media/green_check.png) |
| Software distribution (user-targeted, required)<br>(with Azure AD integration) | ![Supported](media/green_check.png) |
| Software distribution (user-targeted, available)<br>([all requirements](../../../../apps/plan-design/prerequisites-deploy-user-available-apps.md)) | ![Supported](media/green_check.png) |
| BitLocker Management | ![Supported](media/green_check.png) (2010) |
| Windows 10 [in-place upgrade task sequence](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) <sup>[Note&nbsp;2](#bkmk_note2)</sup> | ![Supported](media/green_check.png) |
| Task sequence without a boot image, deployed with the option to **Download all content locally before starting task sequence** <sup>[Note&nbsp;2](#bkmk_note2)</sup> | ![Supported](media/green_check.png) |
| Task sequence without a boot image, deployed with [either download option](../../../../osd/deploy-use/deploy-task-sequence-over-internet.md#deploy-windows-10-in-place-upgrade-via-cmg) <sup>[Note&nbsp;2](#bkmk_note2)</sup> | ![Supported](media/green_check.png) (1910) |
| Task sequence with a boot image, started from Software Center <sup>[Note&nbsp;2](#bkmk_note2)</sup> | ![Supported](media/green_check.png) (2006) |
| Task sequence with a boot image, started from bootable media <sup>[Note&nbsp;2](#bkmk_note2)</sup> | ![Supported](media/green_check.png) (2010) |
| Any other task sequence scenario <sup>[Note&nbsp;2](#bkmk_note2)</sup> | ![Not supported](media/Red_X.png) |
| Client push | ![Not supported](media/Red_X.png) |
| Automatic site assignment | ![Not supported](media/Red_X.png) |
| Software approval requests | ![Not supported](media/Red_X.png) |
| Configuration Manager console | ![Not supported](media/Red_X.png) |
| Remote tools | ![Not supported](media/Red_X.png) |
| Reporting website | ![Not supported](media/Red_X.png) |
| Wake on LAN | ![Not supported](media/Red_X.png) |
| macOS clients | ![Not supported](media/Red_X.png) |
| Peer cache | ![Not supported](media/Red_X.png) |
| On-premises MDM | ![Not supported](media/Red_X.png) |
| Alternate content providers | ![Not supported](media/Red_X.png) |

|Key|
|--|
|![Supported](media/green_check.png) = This feature is supported with CMG by all supported versions of Configuration Manager  |
|![Supported](media/green_check.png) (*YYMM*) = This feature is supported with CMG starting with version *YYMM* of Configuration Manager  |
|![Not supported](media/Red_X.png) = This feature isn't supported with CMG |

### Support notes

#### <a name="bkmk_note1"></a> Note 1: Support for endpoint protection

Starting in version 2006, clients that communicate via a CMG can immediately apply endpoint protection policies without an active connection to Active Directory.<!--4773948-->

<!-- 4350561 -->
In version 2002 and earlier, for domain-joined devices to apply endpoint protection policy, they require access to the domain. Devices with infrequent access to the internal network may experience delays in applying endpoint protection policy. If you require that devices immediately apply endpoint protection policy after they receive it, consider one of the following options:

- Update the site and clients to version 2006.

- Use co-management and switch the [Endpoint Protection workload](../../../../comanage/workloads.md#endpoint-protection) to Intune, and manage [Microsoft Defender Antivirus](../../../../../intune/configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) from the cloud.

- Use [configuration items](../../../../compliance/deploy-use/create-configuration-items.md) instead of the native [antimalware polices](../../../../protect/deploy-use/endpoint-antimalware-policies.md) feature to apply endpoint protection policy.

#### <a name="bkmk_note2"></a> Note 2: Support for task sequences

For more information about support for deploying a task sequence to a client via the CMG, see [Deploy a task sequence over the internet](../../../../osd/deploy-use/deploy-task-sequence-over-internet.md).

## Next steps

Next, understand the costs associated with operating an Azure service for the CMG:
  
> [!div class="nextstepaction"]
> [Cost of cloud management gateway](cost.md)
