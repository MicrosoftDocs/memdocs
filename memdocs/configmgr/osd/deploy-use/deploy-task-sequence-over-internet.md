---
title: Deploy a task sequence over the internet
titleSuffix: Configuration Manager
description: Use this information to deploy a task sequence to remote computers.
ms.date: 12/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 7cffcfc0-14da-4518-9cb2-aaec990448c2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Deploy a task sequence over the internet

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports various methods to deploy a task sequence to remote clients over the internet. You can deploy a Windows 10 upgrade, use bootable media, or start it from Software Center. This article covers the particular configurations for these scenarios. First use [Deploy a task sequence](deploy-a-task-sequence.md) to create the basic deployment. Then use the configurations in this article to customize it for internet-based clients.

> [!WARNING]  
> You can manage the behavior for high-risk task sequence deployments. A high-risk deployment is a deployment that is automatically installed and has the potential to cause unwanted results. For example, a task sequence that has a purpose of **Required** that deploys an OS is considered a high-risk deployment. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

## Allow task sequence to run on internet

On the **User Experience** page of the Deploy Software Wizard, you can configure the deployment to **Allow task sequence to run for client on the Internet**. This setting is required for all internet-based client scenarios. The following sections cover the main scenarios when you enable this setting.

> [!NOTE]
> The task sequence advanced setting to **Run another program first** doesn't apply to task sequences that run on clients that communicate via a cloud management gateway (CMG). This option uses the UNC network path of the package, which isn't accessible via CMG.<!-- 8674270 -->

### Windows 10 in-place upgrade

Use this setting for deployments of a Windows 10 in-place upgrade task sequence to internet-based clients through the cloud management gateway (CMG). All supported versions of Configuration Manager support this scenario. For more information, see [Deploy Windows 10 in-place upgrade via CMG](#deploy-windows-10-in-place-upgrade-via-cmg).

### Install a Windows imaging task sequence from Software Center

Starting in version 2006, you can deploy a task sequence with a boot image to a device that communicates through the CMG. The user needs to start the task sequence from Software Center.<!--6997525-->

> [!NOTE]
> When an Azure Active Directory (Azure AD)-joined client runs an OS deployment task sequence, the client in the new OS won't automatically join Azure AD. Even though it's not Azure AD-joined, the client is still managed.
>
> When you run an OS deployment task sequence on an internet-based client, that's either Azure AD-joined or uses token-based authentication, you need to specify the **CCMHOSTNAME** property in the [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) step.

### Use bootable media to install a Windows imaging task sequence

Starting in version 2010, you can use bootable media to reimage internet-based devices that connect through a CMG. This scenario helps you better support remote workers. If Windows won't start so that the user can access Software Center, you can now send them a USB drive to reinstall Windows. For more information, see [Deploy an OS over CMG using bootable media](#deploy-an-os-over-cmg-using-bootable-media).<!--3555923-->

In version 2002 and earlier, operations that require a boot media aren't supported with this setting. Allow a task sequence to run on the internet only for generic software installations or script-based task sequences that run operations in the standard OS.

> [!NOTE]
> For all internet-based task sequence scenarios in version 2002 and earlier, start the task sequence from Software Center. They don't support Windows PE, PXE, or task sequence media.

## Deploy Windows 10 in-place upgrade via CMG

<!-- 1357149 -->
The Windows 10 in-place upgrade task sequence supports deployment to internet-based clients managed through the [cloud management gateway](../../core/clients/manage/cmg/overview.md) (CMG). This ability allows remote users to more easily upgrade to Windows 10 without needing to connect to the intranet.

Make sure all of the content referenced by the in-place upgrade task sequence is distributed to a content-enabled CMG. Enable the [CMG setting](../../core/clients/manage/cmg/modify-cloud-management-gateway.md#settings-tab): **Allow CMG to function as a cloud distribution point and serve content from Azure storage**. You can also use a [cloud distribution point](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Otherwise devices can't run the task sequence.

When you deploy an upgrade task sequence, use the following settings:

- **Allow task sequence to run for client on the Internet**, on the User Experience tab of the deployment.

- Choose one of the following options on the Distribution Points tab of the deployment:

  - **Download content locally when needed by the running task sequence**. Starting in version 1910, the task sequence engine can download packages on-demand from a content-enabled CMG or a cloud distribution point. This change provides additional flexibility with your Windows 10 in-place upgrade deployments to internet-based devices.<!--3601238-->

  - **Download all content locally before starting task sequence**. In Configuration Manager version 1906 and earlier, other options such as **Download content locally when needed by the running task sequence** don't work in this scenario. The task sequence engine can't download content from a cloud source. The Configuration Manager client must download the content from the cloud source before starting the task sequence. You can still use this option in version 1910 if needed to meet your requirements.

- (*Optional*) **Pre-download content for this task sequence**, on the General tab of the deployment. For more information, see [Configure pre-cache content](configure-precache-content.md).

> [!NOTE]
> Start the task sequence from Software Center. This scenario doesn't support Windows PE, PXE, or task sequence media.

## Bootable media support for cloud-based content

<!--6209223-->

Starting in version 2010, [bootable media](create-task-sequence-media.md#BKMK_PlanBootableMedia) can download cloud-based content. For example, you send a USB key to a user at a remote office to reimage their device. Or an office that has a local PXE server, but you want devices to prioritize cloud services as much as possible. Instead of further taxing the WAN to download large OS deployment content, boot media and PXE deployments can now get content from cloud-based sources. For example, a cloud management gateway (CMG) that you enable to share content.

> [!NOTE]
> The device still needs an intranet connection to the management point.

When the task sequence runs, it downloads content from the cloud-based sources. Review **smsts.log** on the client.

### Prerequisites for bootable media

- Enable the following client setting in the **Cloud Services** group: **Allow access to cloud distribution point**. Make sure the client setting is deployed to the target clients. For more information, see [About client settings - Cloud services](../../core/clients/deploy/about-client-settings.md#cloud-services).

- For the boundary group that the client is in:

  - Associate the content-enabled CMG or cloud distribution point site systems. For more information, see [Configure a boundary group](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Enable the following option: **Prefer cloud based sources over on-premises sources**. For more information, see [Boundary group options for peer downloads](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribute the content referenced by the task sequence to the content-enabled CMG or cloud distribution point.

## Deploy an OS over CMG using bootable media

<!--3555923-->

Starting in version 2010, you can use boot media to reimage internet-based devices that connect through a CMG. This scenario helps you better support remote workers. If Windows won't start so that the user can access Software Center, you can now send them a USB drive to reinstall Windows.

### Prerequisites for boot media via CMG

- [Set up a CMG](../../core/clients/manage/cmg/overview.md)

- For all content referenced in the task sequence, distribute it to a content-enabled CMG or a cloud distribution point. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

- Enable the following client settings in the [Cloud services](../../core/clients/deploy/about-client-settings.md#cloud-services) group:

  - **Allow access to cloud distribution point**

  - **Enable clients to use a cloud management gateway**

- Configure the **Apply Network Settings** task sequence step to join a workgroup. During the task sequence, the device can't join the on-premises Active Directory domain. It doesn't have connectivity to a domain controller to join the domain.

- When you [deploy the task sequence](deploy-a-task-sequence.md) to a collection, configure the following settings:

  - User experience page: **Allow task sequence to run for client on the internet**

  - Deployment settings page: Make available to an option that includes media.

  - Distribution points page, deployment options: **Download content locally when needed by the running task sequence**. For more information, see [Deployment options](deploy-a-task-sequence.md#bkmk_deploy-options).

- Make sure the device has a constant internet connection while the task sequence runs. Windows PE doesn't support wireless networks, so the device needs a wired network connection.

- For version 2010 early update ring, if you use a PKI-based certificate for the boot media, configure it for SHA256 with the Microsoft Enhanced RSA and AES provider.<!-- 8837546 --> For later releases, including globally available version 2010, this certificate configuration is recommended but not required. The certificate can be a v3 (CNG) certificate.<!-- MEMDocs#1095 -->

### Create boot media to use a CMG

Start the create task sequence media wizard for bootable media. For more information, see [Create bootable media](create-bootable-media.md). Modify the standard process using the following steps:

- On the **Media Management** page of the wizard, select the option for **Site-based media**.

- On the **Security** page, set a strong password to protect this media.

- On the **Boot Image** page, select the **Cloud management gateway** for this boot media to use.

When you boot an internet-connected device using this media, it communicates with the specified CMG. The boot media downloads the policy for the task sequence deployment via the CMG. As the task sequence runs, it downloads any additional content and policies over the internet.

After the task sequence runs, the client uses token-based authentication.

## Next steps

[Monitor OS deployments](monitor-operating-system-deployments.md)

[Manage task sequences to automate tasks](manage-task-sequences-to-automate-tasks.md)
