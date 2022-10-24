---
title: Health attestation
titleSuffix: Configuration Manager
description: Learn about the device health attestation functionality in Configuration Manager.
ms.date: 04/14/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Health attestation for Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can view the status of [Windows 10 Device Health Attestation](/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) in the Configuration Manager console. Device health attestation lets you make sure that client computers have the following trustworthy BIOS, TPM, and boot software configurations enabled:

- *Early-launch antimalware (ELAM)* protects your computer when it starts up and before third-party drivers initialize. For more information, see the[Overview of Early Launch AntiMalware](/windows-hardware/drivers/install/early-launch-antimalware).

- *Windows BitLocker Drive Encryption* encrypts all data stored on the OS and data volumes, including removable disks. For more information, see [Plan for BitLocker management](../../../protect/plan-design/bitlocker-management.md).

- *Secure Boot* is a security standard to help make sure that a device boots using only software that's trusted by the PC manufacturer. For more information, see [Secure Boot](/windows-hardware/design/device-experiences/oem-secure-boot).

- *Code Integrity* improves OS security by validating the integrity of a driver or system file each time it's loaded into memory. For more information, see [Enable virtualization-based protection of code integrity](/windows/security/threat-protection/device-guard/enable-virtualization-based-protection-of-code-integrity).

This functionality is available for on-premises resources managed by Configuration Manager and [mobile devices managed with Microsoft Intune](../../../../intune/protect/compliance-policy-create-windows.md#device-health). You can specify whether reporting is done via the cloud or on-premises infrastructure. On-premises device health attestation monitoring enables you to monitor client PCs without internet access.

## Enable health attestation

### Requirements

- Client devices running a supported version of Windows 10 or Windows Server 2016 or later, with [Device health attestation enabled](/windows-server/security/device-health-attestation).

- TPM 1.2 or TPM 2 enabled devices.

- When using cloud management, communication between the Configuration Manager client agent and the management point with `has.spserv.microsoft.com` (port 443) health attestation service. When on-premises, the client needs to communicate with the device health attestation-enabled management point.

### How to enable health attestation service communication on Configuration Manager client computers

Use this procedure to enable device health attestation monitoring for devices that connect to the internet.

1. In the Configuration Manager console, choose **Administration** > **Overview** > **Client Settings**. Select the tab for **Computer Agent** settings.

1. In the **Default Settings** dialog box, select **Computer Agent** and then scroll down to **Enable communication with Health Attestation Service**.

1. Set **Enable communication with Health Attestation Service** to **Yes**, and then select **OK**.

1. Target the collections of devices that should report device health.

### How to enable on-premises health attestation service communication on Configuration Manager client computers

Use this procedure to enable device health attestation monitoring for on-premises devices that don't connect to the internet.

You can configure the on-premises device health attestation service URL on the management point to support client devices without internet access.

1. In the Configuration Manager console, navigate **Administration** > **Overview** > **Site Configuration** > **Sites**.

1. Right-click the primary or secondary site with the management point that support on-premises device health attestation clients, and select **Configure site components** > **Management Point**. The **Management Point Component Properties** page opens.

1. On the **Advanced Options** tab, select **Add** and specify a valid on-premises device health attestation service URL. You can add multiple URLs. If multiple on-premises URLs are specified, clients receive the full set and randomly choose which to use.

1. In the Configuration Manager console, choose **Administration** > **Overview** > **Client Settings**. Select the tab for **Computer Agent** settings.

1. Scroll down to **Enable communication with Health Attestation Service**, and set to **Yes**.

1. Select the **Use on-premises Health Attestation Service** option, and set to **Yes**.

1. Target the collections of devices that should report device health with the client agent settings to enable device health attestation reporting.

You can also **Edit** or **Remove** device health attestation service URLs.

## Monitor device health attestation

To view the device health attestation status, in the Configuration Manager console go to the **Monitoring** workspace, expand the **Security** node, and then select **Health Attestation**.

Configuration Manager device health attestation displays the following information:

- **Health Attestation Status** - Shows the share of devices in compliant, noncompliant, error, and unknown states  

- **Devices Reporting Health Attestation** - Shows the percentage of devices reporting Health Attestation status  

- **Noncompliant Devices by Client Type** - Shows share of mobile devices and computers that are noncompliant  

- **Top Missing Health Attestation Settings** - Shows the number of devices missing the health attestation setting, listed per setting
