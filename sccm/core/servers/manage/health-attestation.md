---
title: "Health attestation for System Center Configuration Manager"
ms.custom: na
ms.date: 08/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn

---
# Health attestation for System Center Configuration Manager
Begining with System Center Configuration Manager current branch version 1602, administrators can view the status of [Windows 10 Device Health Attestation](https://technet.microsoft.com/library/mt592023.aspx) in the Configuration Manager console.  This functionality is available for PCs and on-premises resources managed by Configuration Manager and mobile devices managed with Microsoft Intune. Administrators can specify whether reporting is done via the cloud or on-premises infrastructure. This enables client PCs without internet access to enable and monitor devices using health attestation. Device health attestation lets the administrator ensure that client computers have the following trustworthy BIOS, TPM, and boot software configurations enabled:  
  
-   Early-launch antimalware - Early launch anti-malware (ELAM) protects your computer when it starts up and before third-party drivers initialize. [How to turn on ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
  
-   BitLocker - Windows BitLocker Drive Encryption is software that lets you encrypt all data stored on the Windows operating system volume.  [How to turn on Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
  
-   Secure Boot - Secure Boot is a security standard developed by members of the PC industry to help make sure that your PC boots using only software that is trusted by the PC manufacturer. [Learn more about Secure Boot](https://technet.microsoft.com/library/hh824987.aspx)  
  
-   Code Integrity - Code Integrity is a feature that improves the security of the operating system by validating the integrity of a driver or system file each time it is loaded into memory. [Learn about Code Integrity](https://technet.microsoft.com/library/dd348642.aspx)  
  

  
##  <a name="bkmk_devicehealth"></a> Device Health Attestation  
 Configuration Manager Device Health Attestation displays the following:  
  
-   **Health Attestation Status** - Shows the share of devices in compliant, noncompliant, error, and unknown states  
  
-   **Devices Reporting Health Attestation** - Shows the percentage of devices reporting Health Attestation status  
  
-   **Noncompliant Devices by Client Type** - Shows share of mobile devices and computers that are noncompliant  
  
-   **Top Missing Health Attestation Settings** - Shows the number of devices missing the health attestation setting, listed per setting  
  
 **Requirements:**  
  
-   Client devices running Win10  

-   Windows Server 2016 Technical Preview 5 with [Device Health Attestation enabled](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)
  
-    TPM 2 enabled  
  
-   Unblock communication between Configuration Manager client agent and has.spserv.microsoft.com (port 443) Health Attestation service 
  
### How to enable Health Attestation service communication on Configuration Manager client computers  
  
1.  In the Configuration Manager console, choose **Administration** > **Overview** > **Client Settings**.  Select the tab for **Computer Agent** settings.  
  
2.  In the **Default Settings** dialog box, select **Computer Agent** and then scroll down to **Enable communication with Health Attestation Service**  
  
3.  Set **Enable communication with Health Attestation Service** to **Yes**, and then click **OK**.  
  
### How to enable on-premises Health Attestation service communication on Configuration Manager client computers


1. In the Configuration Manager console, navigate **Administration** > **Overview** > **Client settings**, and then set **Use on-premises Healthy Attestation Service** to **Yes**.


2. Specify the **On-premise Health Attestation Service URL**, and then click
**OK**.

## How to view Health Attestation  

  
1.  To view the device health attestation view, in the Configuration Manager console go to the **Monitoring** workspace of, click **Security** node, and then click **Health Attestation**.  
  
2.  Device Health Attestation is displayed.  
  
 Client device Health Attestation status can be used to define rules for conditional access in compliance policies for devices managed by Configuration Manager with Microsoft Intune. For details, see [Manage device compliance policies in System Center Configuration Manager](../../../protect/deploy-use/manage-device-compliance-policies.md).  
  
## See Also  
 [Monitor and maintain System Center Configuration Manager](../Topic/Monitor%20and%20maintain%20System%20Center%20Configuration%20Manager.md)

