---
title: "Capabilities in Technical Preview 1512"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1512."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
caps.latest.revision: 6
author: erikjems.author: erikjemanager: angrobe
robots: noindex,nofollow
---
# Capabilities in Technical Preview 1512 for System Center Configuration Manager*Applies to: System Center Configuration Manager (Technical Preview)*
This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1512. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.  

 The following are new features you can try out with this version.  

##  <a name="bkmk_devicehealth"></a> Device Health Attestation  
 Starting with Technical  Preview 1512, administrators can view the status of Windows 10 Device Health Attestation in the Configuration Manager console.  This functionality is available for Configuration Manager and Configuration Manager with Microsoft Intune. Device health attestation lets the administrator ensure that client computers have trustworthy BIOS, TPM, and boot software configurations. To support device health attestation, client devices must be running Win10 with TPM 2 enabled. Device health attestation displays the number of devices enabled for each of the following:  

-   Early-launch antimalware  

-   BitLocker  

-   Secure Boot  

-   Code Integrity  

The console also displays the top missing health attestation settings with the number of devices.  

In order to preview the device health attestation view, in the Configuration Manager console go to the **Monitoring** workspace of, click **Security** node, and then click **Health Attestation**.  

##  <a name="bkmk_viewterms"></a> In-console monitoring for terms and conditions  
Starting with Technical  Preview 1512, when you integrate Configuration Manager with Microsoft Intune, you can use the Configuration Manager console to view which users have accepted the terms and conditions configured by your IT department, and which users have not.  

**To view summary information:**  

-   In the Configuration Manager console go to **Monitoring** > **Overview** > **Deployments** and select the terms adn conditions deployment you want to view.  

**To view detailed information:**  

1.  In the Configuration Manager console go to **Assets and Compliance** > **Overview** > **Compliance Settings** > **Terms and Conditions**, and then select the terms and conditions you want to view.  

2.  At the bottom of the console, select the **Deployments** tab, select the deployment, and then click **View Status.**  

##  <a name="bkmk_EPpolicy"></a> Improvements to Endpoint Protection policy settings  
In the 1512 Technical Preview we have added the following new settings in Endpoint Protection antimalware policy:  

-   Real-time protection: **Block Potentially Unwanted Applications at download and prior to installation**  

    -   Potential Unwanted Applications (PUA) is a threat classification based on reputation and research-driven identification. Most commonly, these are unwanted application bundlers or their bundled applications.  

    -   The protection policy setting is enabled (set to "Yes") by default. When enabled, this setting blocks PUA at download and install time. However, you can exclude specific files or folders to meet the specific needs of your environment.  

-   Scan settings: **Scan mapped network drives when running a full scan**  

    -   This setting provides greater granularity for the administrator to allow on-demand scans of network files without the risk of always scanning mapped network drives during a scheduled full scan.  

    -   The setting **Scan network files** must first be enabled (“yes”) for this setting to be available to configure.  

    -   By default, this setting is “No” meaning that a full scan will not access mapped network drives.  

-   Auto sample file submission settings:  

     The antimalware engine may request file samples to be sent to Microsoft for further analysis. By default, it will always prompt before it sends such samples. Administrators can now manage the following settings to configure this behavior:  

    -   Advanced: **Enable auto sample file submission to help Microsoft determine whether certain detected items are Malicious**:  Change this setting to “Yes” to enable auto sample file submission. By default, this setting is “No” which means auto sample file submission is disabled and users will be prompted before sending samples.   (This setting was first introduced in System Center 2012 R2 Configuration Manager SP1)  

    -   Advanced: **Allow users to modify auto sample file submission settings**: This setting determines whether a user with local administrative rights on a device can change the auto sample file submission setting in the client interface. By default, this setting is “No” which means the settings can only be changed from within the Configuration Manager console, and local administrators on a device cannot change this configuration.  

         For example, the following shows the Windows Defender setting in Windows 10 set by the administrator as enabled, and the user is not allowed to modify it:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Additionally, the existing **Exclude files and folders** setting in the “Exclusion settings” section of endpoint protection antimalware policy is improved to allow device exclusions. For example, you can now specify the following as an exclusion: **\device\mvfs** (for Multiversion File System). The policy does not validate the device path; the endpoint protection policy is provided to the antimalware engine on the client which must be able to interpret the device string.  

**Prerequisites for using Endpoint Protection policies:**  

Before you can use Endpoint Protection policies you must install and manage the Endpoint Protection client by using the Endpoint Protection client settings. This is done using the System Center Endpoint Protection client for Windows 7, Windows 8, Windows 8.1, or managed Windows Defender for Windows 10. See [Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/endpoint-protection.md).  
