---
title: Supported configurations for CMG
titleSuffix: Configuration Manager
description: A list of the features and configurations that the Configuration Manager cloud management gateway supports.
ms.date: 07/12/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Supported configurations for cloud management gateway

*Applies to: Configuration Manager (current branch)*

Use this article as a reference for the features and configurations that are supported by the Configuration Manager cloud management gateway (CMG).

## Specifications

- All Windows versions listed in [Supported operating systems for clients and devices](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) are supported for CMG.

- CMG only supports the management point and software update point roles.

- CMG doesn't support clients that only communicate with IPv6 addresses.<!--495606-->

- Software update points using a network load balancer don't work with CMG. <!--505311-->

- Starting in version 2203, the option to deploy a CMG as a **cloud service (classic)** is removed.<!-- 13235079 --> All CMG deployments should use a [virtual machine scale set](plan-cloud-management-gateway.md#virtual-machine-scale-sets).<!--10966586--> For more information, see [Removed and deprecated features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

- CMG names need to be between 3-24 alphanumeric characters. The name must begin with a letter, end with a letter or digit, and not contain consecutive hyphens. <!--13222041-->

## Support for Configuration Manager features

The following table lists CMG support for Configuration Manager features:

| Feature | Support |
|--|--|
| Software updates | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Endpoint protection | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: <sup>[Note&nbsp;1](#bkmk_note1)</sup> |
| Hardware and software inventory | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Client status and notifications | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Run scripts | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| CMPivot | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Compliance settings | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Automatic client upgrade | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Client install<br>(with [Azure AD integration](../../deploy/deploy-clients-cmg-azure.md)) | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Client install<br>(with [token authentication](../../deploy/deploy-clients-cmg-token.md)) | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Software distribution (device-targeted) | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Software distribution (user-targeted, required)<br>(with Azure AD integration) | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Software distribution (user-targeted, available)<br>([all requirements](../../../../apps/plan-design/prerequisites-deploy-user-available-apps.md)) | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| BitLocker Management | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Pull distribution point source | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Windows [in-place upgrade task sequence](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) <sup>[Note&nbsp;2](#bkmk_note2)</sup> | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Task sequence without a boot image, deployed with the option to **Download all content locally before starting task sequence** <sup>[Note&nbsp;2](#bkmk_note2)</sup> | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Task sequence without a boot image, deployed with [either download option](../../../../osd/deploy-use/deploy-task-sequence-over-internet.md#deploy-windows-in-place-upgrade-via-cmg) <sup>[Note&nbsp;2](#bkmk_note2)</sup> | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Task sequence with a boot image, started from Software Center <sup>[Note&nbsp;2](#bkmk_note2)</sup> | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Task sequence with a boot image, started from bootable media <sup>[Note&nbsp;2](#bkmk_note2)</sup> | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Any other task sequence scenario <sup>[Note&nbsp;2](#bkmk_note2)</sup> | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Content for PXE or multicast-enabled deployments | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Client push | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Automatic site assignment | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Software approval requests | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Configuration Manager console | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Remote tools | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: <sup>[Note&nbsp;3](#bkmk_note3)</sup> |
| Reporting website | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Wake on LAN | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| macOS clients | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Peer cache | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| On-premises MDM | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Alternate content providers | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: <sup>[Note&nbsp;4](#bkmk_note4)</sup> |
| Content for App-V streaming applications | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Content for Microsoft 365 Apps updates <!--7366753--> | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| [Prestage content](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |

|Key|
|--|
|:::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: = This feature is supported with CMG by all supported versions of Configuration Manager  |
|:::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: (*YYMM*) = This feature is supported with CMG starting with version *YYMM* of Configuration Manager  |
|:::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: = This feature isn't supported with CMG |

### Support notes

#### <a name="bkmk_note1"></a> Note 1: Support for endpoint protection

Clients that communicate via a CMG can immediately apply endpoint protection policies without an active connection to Active Directory.<!--4773948-->

#### <a name="bkmk_note2"></a> Note 2: Support for task sequences

For more information about support for deploying a task sequence to a client via the CMG, see [Deploy a task sequence over the internet](../../../../osd/deploy-use/deploy-task-sequence-over-internet.md).

#### <a name="bkmk_note3"></a> Note 3: Support for remote tools

As announced at Microsoft Ignite 2021, a public preview of the new remote assistance solution is now available in the Microsoft Intune admin center. This cloud-based tool can help you more securely support users of Windows devices.

For more information, see the following resources:

- [Remote Help: a new remote assistance tool from Microsoft (blog post)](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/remote-help-a-new-remote-assistance-tool-from-microsoft/ba-p/2822622)

- [Enable remote help scenarios with Microsoft Intune (demo video)](https://techcommunity.microsoft.com/t5/video-hub/enable-remote-help-scenarios-with-microsoft-endpoint-manager/ba-p/2911349)

- [Use Remote Help with Intune and Configuration Manager](../../../../../intune/remote-actions/remote-help.md)

#### <a name="bkmk_note4"></a> Note 4: Support for alternate content providers

Alternate content providers aren't supported to get content from a content-enabled CMG. You can still use them on a client that communicates with a CMG and gets content from other supported content locations.<!-- CMADO-10205600 -->

> [!TIP]
> Starting in version 2203, you can also configure the task sequence to allow token authentication with alternate content providers. For more information, see [Task sequence variables: SMSTSAllowTokenAuthURLForACP](../../../../osd/understand/task-sequence-variables.md#smstsallowtokenauthurlforacp).<!-- 13788624 -->

## Next steps

Next, plan how the design the CMG for the best performance at the appropriate scale:
  
> [!div class="nextstepaction"]
> [CMG performance and scale](perf-scale.md)
