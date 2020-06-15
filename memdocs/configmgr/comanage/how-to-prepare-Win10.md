---
title: Co-manage internet-based devices
titleSuffix: Configuration Manager
description: Learn how to prepare your Windows 10 internet-based devices for co-management.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
---

# How to prepare internet-based devices for co-management

This article focuses on the second path to co-management, for new internet-based devices. This scenario is when you have new Windows 10 devices that join Azure AD and automatically enroll to Intune. You install the Configuration Manager client to reach a co-management state.  

## Windows Autopilot

For new Windows 10 devices, you can use the Autopilot service to configure the out of box experience (OOBE). This process includes joining the device to Azure AD and enrolling the device in Intune.  

For more information, see [Overview of Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

To configure your devices to be automatically enroll into Intune when they join Azure AD, see [Enroll Windows devices for Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

### Gather information from Configuration Manager

Use Configuration Manager to collect and report the device information required by Intune. This information includes the device serial number, Windows product identifier, and a hardware identifier. It's used to register the device in Intune to support Windows Autopilot.

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand the **Reporting** node, expand **Reports**, and select the **Hardware - General** node.  

2. Run the report, **Windows Autopilot Device Information**, and view the results.  

3. In the report viewer, select the **Export** icon, and choose the **CSV (comma-delimited)** option.  

4. After saving the file, upload the data to Intune.  

For more information, see [Add devices in Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### Autopilot for existing devices
<!--1358333-->

[Windows Autopilot for existing devices](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) is available in Windows 10, version 1809 or later. This feature allows you to reimage and provision a Windows 7 device for [Windows Autopilot user-driven mode](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) using a single, native Configuration Manager task sequence.

For more information, see [Windows Autopilot for existing devices task sequence](../../autopilot/windows-autopilot-for-existing-devices.md).

## Install the Configuration Manager client

For internet-based devices in the second path, you need to create an app in Intune. Deploy this app to Windows 10 devices that aren't already Configuration Manager clients.

> [!NOTE]
> Before you assign this app to devices in Intune, make sure that the devices trust the CMG server authentication certificate. For more information, see [CMG trusted root certificate to clients](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). If a device doesn't trust the CMG server authentication certificate, you'll see a WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA error in the ccmsetup.log on the client.

### Get the command line from Configuration Manager

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node.  

2. Select the co-management object, and then choose **Properties** in the ribbon.  

3. On the **Enablement** tab, copy the command line. Paste it into Notepad to save for the next process.  

The following command line is an example:
`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Decide which command-line properties you require for your environment:  

- The following command-line properties are required in all scenarios:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- The following properties are required when using Azure AD for client authentication instead of PKI-based client authentication certificates:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- If the client roams back to the intranet, use the following property:
  - SMSMP  

- If using your own PKI certificate, and your CRL isn't published to the internet, the following parameter is required:  
  - /noCRLCheck  

    For more information, see [Planning for CRLs](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Starting in version 2002, use the following property to bootstrap a task sequence immediately after client registration:
  - PROVISIONTS

    For more information, see [About client installation properties - PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

The site publishes additional Azure AD information to the cloud management gateway (CMG). An Azure AD-joined client gets this information from the CMG during the ccmsetup process, using the same tenant to which it's joined. This behavior further simplifies enrolling devices to co-management in an environment with more than one Azure AD tenant. The only two required ccmsetup properties are **CCMHOSTNAME** and **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> If you're already deploying the Configuration Manager client from Intune, update the Intune app with a new command line and new MSI. <!-- SCCMDocs-pr issue 3084 -->

The following example includes all of these properties:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

For more information, see [Client installation properties](../core/clients/deploy/about-client-installation-properties.md).

### Create the app in Intune

1. Go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com), and then expand the left navigation pane.  

2. Select **Apps** > **All Apps** > **Add**.  

3. Under **Other**, select **Line-of-business app**.  

4. Upload the **ccmsetup.msi** app package file. Find this file in the following folder on the Configuration Manager site server: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > When you update the site, make sure you also update this app in Intune.  

5. After the app is updated, configure the app information with the command line that you copied from Configuration Manager.  

> [!IMPORTANT]
> If you customize this command line, make sure it isn't more than 1024 characters long. When the command line length is greater than 1024 characters, the client installation fails.
