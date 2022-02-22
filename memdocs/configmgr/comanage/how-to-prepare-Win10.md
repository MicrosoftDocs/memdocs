---
title: Co-manage internet-based devices
titleSuffix: Configuration Manager
description: Learn how to prepare your Windows internet-based devices for co-management.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 02/16/2022
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.localizationpriority: medium
ms.collection: highpri
---

# How to prepare internet-based devices for co-management

This article focuses on the second path to co-management, for new internet-based devices. This scenario is when you have new Windows 10 or later devices that join Azure AD and automatically enroll to Intune. You install the Configuration Manager client to reach a co-management state.

## Windows Autopilot

For new Windows devices, you can use the Autopilot service to configure the out of box experience (OOBE). This process includes joining the device to Azure AD and enrolling the device in Intune.

For more information, see [Overview of Windows Autopilot](../../autopilot/windows-autopilot.md).

To configure your devices to be automatically enroll into Intune when they join Azure AD, see [Enroll Windows devices for Microsoft Intune](../../intune/enrollment/windows-enroll.md).

> [!NOTE]
> As we talk with our customers that are using Microsoft Endpoint Manager to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and hybrid Azure Active Directory (Azure AD) joined devices. Many customers confuse these two topics. Co-management is a management option, while Azure AD is an identity option. For more information, see [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog post aims to clarify hybrid Azure AD join and co-management, how they work together, but aren't the same thing.
>
> You can't deploy the Configuration Manager client while provisioning a new computer in Windows Autopilot user-driven mode for hybrid Azure AD join. This limitation is due to the identity change of the device during the Azure AD-join process. Deploy the Configuration Manager client after the Autopilot process.<!-- CMADO-10205503 --> For alternative options to install the client, see [Client installation methods in Configuration Manager](../core/clients/deploy/plan/client-installation-methods.md).

### Gather information from Configuration Manager

Use Configuration Manager to collect and report the device information required by Intune. This information includes the device serial number, Windows product identifier, and a hardware identifier. It's used to register the device in Intune to support Windows Autopilot.

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand the **Reporting** node, expand **Reports**, and select the **Hardware - General** node.

2. Run the report, **Windows Autopilot Device Information**, and view the results.

3. In the report viewer, select the **Export** icon, and choose the **CSV (comma-delimited)** option.

4. After saving the file, upload the data to Intune.

For more information, see [Manually register devices with Windows Autopilot](../../autopilot/add-devices.md).

### Autopilot for existing devices
<!--1358333-->

[Windows Autopilot for existing devices](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) is available in Windows 10, version 1809 or later. This feature allows you to reimage and provision a Windows 7 device for [Windows Autopilot user-driven mode](../../autopilot/user-driven.md) using a single, native Configuration Manager task sequence.

For more information, see [Windows Autopilot for existing devices task sequence](../../autopilot/existing-devices.md).

## Install the Configuration Manager client

For internet-based devices in the second path, you need to create an app in Intune. Deploy this app to Windows 10 or later devices that aren't already Configuration Manager clients.

> [!NOTE]
> Before you assign this app to devices in Intune, make sure that the devices trust the CMG server authentication certificate. For more information, see [CMG server authentication certificate](../core/clients/manage/cmg/server-auth-cert.md). If a device doesn't trust the CMG server authentication certificate, you'll see a WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA error in the ccmsetup.log on the client.

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

- If a device uses Azure AD for client authentication and also has a PKI-based client authentication certificate, specify the following properties to use Azure AD:<!-- MEMDocs#1483 -->

  - `AADCLIENTAPPID`

  - `AADRESOURCEURI`

- If the client roams back to the intranet, use the `SMSMP` property.

- If you use your own PKI certificate, and your CRL isn't published to the internet, use the `/NoCRLCheck` parameter. For more information, see [About client installation properties: /NoCRLCheck](../core/clients/deploy/about-client-installation-properties.md#nocrlcheck).

  > [!IMPORTANT]
  > Microsoft recommends publishing the CRL. For more information, see [Planning for CRLs](../core/plan-design/security/plan-for-certificates.md#pki-certificate-revocation).<!-- memdocs#1942 -->

- To bootstrap a task sequence immediately after client registration, use the `PROVISIONTS` property. For more information, see [About client installation properties: PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

The site publishes other Azure AD information to the cloud management gateway (CMG). An Azure AD-joined client gets this information from the CMG during the ccmsetup process, using the same tenant to which it's joined. This behavior further simplifies enrolling devices to co-management in an environment with more than one Azure AD tenant. The only two required ccmsetup properties are `CCMHOSTNAME` and `SMSSITECODE`.<!--3607731-->

> [!NOTE]
> If you're already deploying the Configuration Manager client from Intune, update the Intune app with a new command line and new MSI.<!-- SCCMDocs-pr issue 3084 -->

The following example includes all of these properties:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

For more information, see [Client installation properties](../core/clients/deploy/about-client-installation-properties.md).

### Create the app in Intune

1. Go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com), and then expand the left navigation pane.

1. Select **Apps** > **All Apps** > **Add**.

1. Under **Other**, select **Line-of-business app**.

1. Upload the **ccmsetup.msi** app package file. Find this file in the following folder on the Configuration Manager site server: `<ConfigMgr installation directory>\bin\i386`.

    > [!TIP]
    > When you update the site, make sure you also update this app in Intune.

1. After the app is updated, configure the app information with the command line that you copied from Configuration Manager.

> [!IMPORTANT]
> If you customize this command line, make sure it isn't more than 1024 characters long. When the command line length is greater than 1024 characters, the client installation fails.

## Next steps

[Switch workloads to Intune](how-to-switch-workloads.md)
