---
title: Co-manage internet-based devices
titleSuffix: Configuration Manager
description: Learn how to prepare your Windows internet-based devices for co-management.
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.date: 05/19/2022
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to prepare internet-based devices for co-management

This article focuses on the second path to co-management, for new internet-based devices. This scenario is when you have new Windows 10 or later devices that join Azure AD and automatically enroll to Intune. You install the Configuration Manager client to reach a co-management state.

## Windows Autopilot

For new Windows devices, use the Autopilot service to configure the out of box experience (OOBE). This process includes joining the device to Azure AD, enrolling the device in Intune, installing the Configuration Manager client, and configuring co-management.

For more information, see [How to enroll with Autopilot](autopilot-enrollment.md).

> [!NOTE]
> As we talk with our customers that are using Microsoft Endpoint Manager to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and hybrid Azure Active Directory (Azure AD) joined devices. Many customers confuse these two topics. Co-management is a management option, while Azure AD is an identity option. For more information, see [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog post aims to clarify hybrid Azure AD join and co-management, how they work together, but aren't the same thing.
>
> You can't deploy the Configuration Manager client while provisioning a new computer in Windows Autopilot user-driven mode for hybrid Azure AD join. This limitation is due to the identity change of the device during the hybrid Azure AD-join process. Deploy the Configuration Manager client after the Autopilot process.<!-- CMADO-10205503 --> For alternative options to install the client, see [Client installation methods in Configuration Manager](../core/clients/deploy/plan/client-installation-methods.md).

### Gather information from Configuration Manager

Use Configuration Manager to collect and report the device information required by Intune. This information includes the device serial number, Windows product identifier, and a hardware identifier. It's used to register the device in Intune to support Windows Autopilot.

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand the **Reporting** node, expand **Reports**, and select the **Hardware - General** node.

2. Run the report, **Windows Autopilot Device Information**, and view the results.

3. In the report viewer, select the **Export** icon, and choose the **CSV (comma-delimited)** option.

4. After saving the file, upload the data to Intune.

For more information, see [Manually register devices with Windows Autopilot](../../autopilot/add-devices.md).

### Autopilot for existing devices
<!--1358333-->

_Windows Autopilot for existing devices_ allows you to reimage and provision a Windows 8.1 device for [Windows Autopilot user-driven mode](../../autopilot/user-driven.md) using a single, native Configuration Manager task sequence.

For more information, see [Windows Autopilot for existing devices](../../autopilot/existing-devices.md).

## Install the Configuration Manager client

You no longer need to create and assign an Intune app to install the Configuration Manager client. The Intune enrollment policy automatically installs the Configuration Manager client as a first-party app. The device gets the client content from the Configuration Manager cloud management gateway (CMG), so you don't need to provide and manage the client content in Intune. For more information, see [How to enroll with Autopilot](autopilot-enrollment.md).<!-- Intune 11300628 -->

You do still specify the Configuration Manager client command-line parameters in Intune.

> [!NOTE]
> Make sure that the devices trust the CMG server authentication certificate. For more information, see [CMG server authentication certificate](../core/clients/manage/cmg/server-auth-cert.md). If a device doesn't trust the CMG server authentication certificate, you'll see a WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA error in the ccmsetup.log on the client.

### Get the command line from Configuration Manager

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Attach** node.

   > [!TIP]
   > For version 2103 and earlier, select the **Co-management** node.

1. Select the co-management object, and then choose **Properties** in the ribbon.

1. On the **Enablement** tab, copy the command line. Paste it into Notepad to save for the next process. The command line only shows if you've met all of the prerequisites, such as a cloud management gateway.<!-- MEMDocs#635 -->

The following command line is an example:
`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Decide which command-line properties you require for your environment:

- The following command-line properties are required in all scenarios:

  - `CCMHOSTNAME`

  - `SMSSITECODE`

- If devices use Azure AD for client authentication and also have a PKI-based client authentication certificate, specify the following properties to use Azure AD:<!-- MEMDocs#1483 -->

  - `AADCLIENTAPPID`

  - `AADRESOURCEURI`

- If the client roams back to the intranet, use the `SMSMP` property.

- If you use your own PKI certificate, and your CRL isn't published to the internet, use the `/NoCRLCheck` parameter. For more information, see [About client installation properties: /NoCRLCheck](../core/clients/deploy/about-client-installation-properties.md#nocrlcheck).

  > [!IMPORTANT]
  > Microsoft recommends publishing the CRL. For more information, see [Planning for CRLs](../core/plan-design/security/plan-for-certificates.md#pki-certificate-revocation).<!-- memdocs#1942 -->

- To bootstrap a task sequence immediately after client registration, use the `PROVISIONTS` property. For more information, see [About client installation properties: PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

- To make sure that internet-based devices get the latest version of the Configuration Manager client, use the `UPGRADETOLATEST` property. For more information, see [About client installation properties: `UPGRADETOLATEST`](../core/clients/deploy/about-client-installation-properties.md#upgradetolatest).<!-- Intune 13745717 -->

The site publishes other Azure AD information to the cloud management gateway (CMG). An Azure AD-joined client gets this information from the CMG during the ccmsetup process, using the same tenant to which it's joined. This behavior further simplifies enrolling devices to co-management in an environment with more than one Azure AD tenant. The only two required ccmsetup properties are `CCMHOSTNAME` and `SMSSITECODE`.<!--3607731-->

The following example includes all of these properties:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

For more information, see [Client installation properties](../core/clients/deploy/about-client-installation-properties.md).

> [!IMPORTANT]
> If you customize this command line, make sure it isn't more than 1024 characters long. When the command line length is greater than 1024 characters, the client installation fails.

## Next steps

[How to enroll with Autopilot](autopilot-enrollment.md)

[Switch workloads to Intune](how-to-switch-workloads.md)
