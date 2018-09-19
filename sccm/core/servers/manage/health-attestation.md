---
title: "Health attestation"
titleSuffix: "Configuration Manager"
description: "Learn about the Device Health Attestation functionality viewable in the Configuration Manager console."
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Health attestation for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Administrators can view the status of [Windows 10 Device Health Attestation](https://technet.microsoft.com/library/mt592023.aspx) in the Configuration Manager console.  Device health attestation lets the administrator ensure that client computers have the following trustworthy BIOS, TPM, and boot software configurations enabled:  

-   Early-launch antimalware - Early launch anti-malware (ELAM) protects your computer when it starts up and before third-party drivers initialize. [How to turn on ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Windows BitLocker Drive Encryption is software that lets you encrypt all data stored on the Windows operating system volume.  [How to turn on BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Secure Boot - Secure Boot is a security standard developed by members of the PC industry to help make sure that your PC boots using only software that is trusted by the PC manufacturer. [Learn more about Secure Boot](https://technet.microsoft.com/library/hh824987.aspx)  
-   Code Integrity - Code Integrity is a feature that improves the security of the operating system by validating the integrity of a driver or system file each time it is loaded into memory. [Learn about Code Integrity](https://technet.microsoft.com/library/dd348642.aspx)  

This functionality is available for PCs and on-premises resources managed by Configuration Manager and mobile devices managed with Microsoft Intune. Administrators can specify whether reporting is done via the cloud or on-premises infrastructure. On-premises device health attestation monitoring enables administrator to monitor client PCs without internet access.

## Enable Health Attestation

 **Requirements:**  

-   Client devices running Windows 10 version 1607 or Windows Server 2016 version 1607 with [Device Health Attestation enabled](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation).
-   TPM 1.2 or TPM 2 enabled devices.
-   When using cloud management, communication between the Configuration Manager client agent and the management point with *has.spserv.microsoft.com* (port 443) Health Attestation service (cloud management). When on-premises, the client must be able to communicate with the device health attestation-enabled management point.

### How to enable Health Attestation service communication on Configuration Manager client computers

Use this procedure to enable device health attestation monitoring for devices that connect to the internet.

1.  In the Configuration Manager console, choose **Administration** > **Overview** > **Client Settings**.  Select the tab for **Computer Agent** settings.  
2.  In the **Default Settings** dialog box, select **Computer Agent** and then scroll down to **Enable communication with Health Attestation Service**  
3.  Set **Enable communication with Health Attestation Service** to **Yes**, and then click **OK**.  
4. Target the collections of devices that should report device health.

### How to enable on-premises Health Attestation service communication on Configuration Manager client computers
Use this procedure to enable device health attestation monitoring for on-premises devices that don't connect to the internet.

Starting with Configuration Manager 1702, the on-premises device health attestation service URL can be configured on the management point to support client devices without internet access.

1. In the Configuration Manager console, navigate **Administration** > **Overview** > **Site Configuration** > **Sites**.
2. Right-click the primary or secondary site with the management point that support on-premises device health attestation clients, and select **Configure site components** > **Management Point**. The **Management Point Component Properties** page opens.
3. On the **Advanced Options** tab, select **Add** and specify a valid on-premises device health attestation service URL. You can add multiple URLs. If multiple on-premises URLs are specified, clients receive the full set and randomly choose which to use.
4.  In the Configuration Manager console, choose **Administration** > **Overview** > **Client Settings**.  Select the tab for **Computer Agent** settings.  
5.  Scroll down to **Enable communication with Health Attestation Service**, and set to **Yes**.
7.  Click the **Use on-premises Health Attestaion Service** option, and set to **Yes**.
8. Target the collections of devices that should report device health with the client agent settings to enable device health attestation reporting.

You can also **Edit** or **Remove** device health attestation service URLs.

> [!NOTE]
> If you used device health attestation prior to upgrading to Configuration Manager 1702, the on-premises URLs specified in the client agent settings is pre-populate in the management point properties during the upgrade. On-premises clients will continue to use the URL specified in client agent settings until they are upgraded. They will then switch to one of the URLs specified on the management point.

## Monitor device health attestation

1.  To view the device health attestation view, in the Configuration Manager console go to the **Monitoring** workspace of, click **Security** node, and then click **Health Attestation**.  
2.  Device Health Attestation is displayed.  

Configuration Manager Device Health Attestation displays the following:  

-   **Health Attestation Status** - Shows the share of devices in compliant, noncompliant, error, and unknown states  
-   **Devices Reporting Health Attestation** - Shows the percentage of devices reporting Health Attestation status  
-   **Noncompliant Devices by Client Type** - Shows share of mobile devices and computers that are noncompliant  
-   **Top Missing Health Attestation Settings** - Shows the number of devices missing the health attestation setting, listed per setting

Client Device Health Attestation status can be used to define rules for conditional access in compliance policies for devices managed by Configuration Manager with Microsoft Intune. For details, see [Manage device compliance policies in System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  
