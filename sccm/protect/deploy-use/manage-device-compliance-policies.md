---
title: "Manage device compliance policies | System Center Configuration Manager"
ms.custom: na
ms.date: 2016-04-07
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 353ec99a-9982-4dab-ae21-d7fb595b3c50
caps.latest.revision: 22
author: karthikaraman
robots: noindex
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Manage device compliance policies in System Center Configuration Manager
**Compliance policies** in System Center Configuration Manager define the rules and settings that a device must comply with in order to be considered compliant by conditional access polices. You can also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access.  
  
 
> [!IMPORTANT]  
>  This article describes the compliance policies for devices managed by Microsoft Intune.    The compliance policies for PCs managed by System Center Configuration Manager is described in [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  
  
 These rules include:  
  
-   PIN and passwords  
  
-   Encryption  
  
-   Whether the device is jailbroken or rooted  
  
-   Whether email on the device is managed by an Intune policy, or if the device is reported as unhealthy by the Windows device health attestation service.  
  
-   Minimum OS version required - Typically, this depends on your company compliance policies and security requirements. This helps to prevent access to devices that might have security vulnerabilities because they are using an older OS version.  
  
-   Maximum OS version allowed - You may choose not to support the latest OS version available before testing or other reasons. You can choose to block devices that have a version later than the one you have specified.   The device will not be able to access company resources until the policy is changed.  
  
> [!NOTE]  
>  On Windows PCs, Windows Operating System version 8.1, is reported as 6.3 instead of 8.1.    If the OS version rule is set to Windows 8.1 for Windows, then the device will be reported as non-compliant even if the device has Windows OS 8.1. Make sure you are setting the right **reported** version of Windows for the Minimum and Maximum OS rules. The version number must match the version returned by the winver command. Windows Phones do not have this issue; the version is reported as 8.1 as expected.  
>   
>  Windows PCs with Windows 10 operating system, the version should be set as "10.0"+ the OS Build number returned by the winver command. For example, it could be something like 10.0.10586.  
> Windows 10 Mobile does not have this issue.  
>   
>  ![CA&#95;Win10OSversion](../../protect/deploy-use/media/CA_Win10OSversion.png "CA_Win10OSversion")  
  
 You deploy compliance policies to user collections. When a compliance policy is deployed to a user, then all of the users devices are checked for compliance.  
  
 The following table lists the device types supported by compliance policies and how noncompliant settings are managed when the policy is used with a conditional access policy.  
  
|Rule|Windows 8.1 and later|Windows Phone 8.1 and later|iOS 6.0 and later|Android 4.0 and later|Samsung KNOX Standard 4.0 and later|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|PIN or password configuration|Remediated|Remediated|Remediated|Quarantined|Quarantined|  
|Device encryption|N/A|Remediated|Remediated (by setting PIN)|Quarantined|Quarantined|  
|Jailbroken or rooted device|N/A|N/A|Quarantined (not a setting)|Quarantined (not a setting)|Quarantined (not a setting)|  
|Email profile|N/A|N/A|Quarantined|N/A|N/A|  
|Minimum OS version|Quarantined|Quarantined|Quarantined|Quarantined|Quarantined|  
|Maximum OS version|Quarantined|Quarantined|Quarantined|Quarantined|Quarantined|  
|Device Health Attestation (1602 update)|Setting is not applicable to Windows 8.1<br /><br /> Windows 10 and Windows 10 Mobile are Quarantined.|N/A|N/A|N/A|N/A|  
  
 **Remediated** = Compliance is enforced by the device operating system (for example, the user is forced to set a PIN).  There is never a case when the setting will be noncompliant.  
  
 **Quarantined** = The device operating system does not enforce compliance (for example, Android devices do not force the user to encrypt the device).  In this case:  
  
-   The device will be blocked if the user is targeted by a conditional access policy.  
  
-   The company portal or web portal will notify the user about any compliance issues.  
  
##  <a name="BKMK_Compliance"></a> Step 1: Create a compliance policy  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then click **Compliance Policies**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Compliance Policy**.  
  
4.  On the **General** page of the **Create Compliance Policy Wizard**, specify the following information:  
  
    |Setting|More information|  
    |-------------|----------------------|  
    |**Name**|Enter a unique name for the compliance policy. You can use a maximum of 256 characters.|  
    |**Description**|Enter a description that gives an overview of the VPN profile and helps identify it in the Configuration Manager console. You can use a maximum of 256 characters.|  
    |**Type of compliance policy**|**Beginning in version 1602 of Configuration Manager**, select the type of policy you want to create depending on whether the device is managed by Configuration Manager.<br /><br /> For devices managed by Intune, choose the **Compliance rules for devices managed without configuration manager client** option.  When you select this option you can also select the type of platform you want this policy to apply to.|  
    |**Noncompliance severity for reports**|Specify the severity level that is reported if this compliance policy is evaluated as noncompliant. The available severity levels are the following:<br /><br /> -**None** - devices that fail this compliance rule do not report a failure severity for Configuration Manager reports.<br /><br /> -<br />                            **Information** - devices that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.<br /><br /> -<br />                            **Warning** - devices that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.<br /><br /> -<br />                            **Critical** - devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.<br /><br /> -<br />                            **Critical with event** - devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also be logged as a Windows event in the application event log.|  
  
5.  On the **Supported Platforms** page, choose the device platforms that this compliance policy will be evaluated on, or click **Select all** to choose all device platforms.  
  
6.  On the **Rules** page, you define one or more rules that define the configuration that devices must have in order to be evaluated as compliant. The following table shows the available rules. When you create a compliance policy, some rules are enabled by default, but you can edit or delete these.  
  
    |Rule name|More information|Windows Phone 8+|Windows RT/8.1|Windows 8.1|Windows 10/Windows 10 Mobile|iOS 6+|Android 4.0+|Samsung KNOX Standard 4.0+|  
    |---------------|----------------------|-----------------------|---------------------|-----------------|-----------------------------------|-------------|-------------------|---------------------------------|  
    |**Require password settings on mobile devices**|Require users to enter a password before they can access their device.<br /><br /> (Enabled by default)|✓||||✓|✓|✓|  
    |**Require a password to unlock an idle device** (1602 update)|Require users to enter a password to access device that is locked.|✓||||✓|✓|✓|  
    |**Minutes of inactivity before password is required** (1602 update)|Specifies the idle time before the user must re-enter their password.<br /><br /> Set the value to one of the available options: 1 minute, 5 minutes, 15 minutes, 30 minutes, I hour.<br /><br /> This rule when must be used with the **Require a password to unlock an idle device**. The value set here determines when the device is considered idle and is locked, and  **Require a password to unlock an idle device** is set to **True**, will then require that the user enters a password in order to access the locked device.|✓|✓|||✓|✓|✓|  
    |**Require automatic updates** (1602 update)|You can require devices with Windows 8.1 or later to automatically install updates, and specify the class of updates.<br /><br /> The value should be set to **None** to prevent automatic installation, to **Recommended** to automatically install all recommended updates, or to **Important** to only install updates classified as important.|✓|||||||  
    |**Allow simple passwords**|Let users create simple passwords such as ‘**1234**’ or ‘**1111**’.<br /><br /> (Disabled by default)|✓||||✓|||  
    |**Minimum password length** <sup>1</sup>|Specifies the minimum number of digits or characters that the user’s password must contain.<br /><br /> (**6** by default)|✓||✓||✓|✓|✓|  
    |**File encryption on mobile device**|Requires the device to be encrypted in order to connect to resources.<br /><br /> Devices that run Windows Phone 8 are automatically encrypted.<br /><br /> Devices that run iOS are encrypted when you configure the setting **Require password settings on mobile devices**.<br /><br /> (Enabled by default)|✓||✓|||✓|✓|  
    |**Device must not be jailbroken or rooted**|If enabled, jailbroken (iOS), or rooted (Android) devices will not be compliant.<br /><br /> (Disabled by default)|||||✓|✓|✓|  
    |**Email profile must be managed by Intune**|When this option is set to Yes, the device must use the email profile deployed to the device.<br /><br /> The device is considered noncompliant if the email profile is not deployed to the same user group as the user group targeted by the compliance policy.<br /><br /> It is also noncompliant if the user has already set up an email account on the device that matches the Intune email profile that is deployed to the device. In this case, Intune cannot overwrite the user-provisioned profile and therefore cannot manage it. The user can bring the device into compliance by removing the existing email settings, which allows Intune to install the managed email profile.<br /><br /> For details about email profiles, see [Enable access to corporate email using email profiles with Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx).<br /><br /> (Disabled by default)|||||✓|||  
    |**Email profile**|If **Email account must be managed by Intune** is selected, click **Select** to choose the email profile that devices must be managed by. The email profile must be present on the device.|||||✓|||  
    |**Minimum OS required**|When  a device does not meet the minimum OS version requirement, it will be reported as non-compliant. A link with information on how to upgrade will be displayed. The end-user can choose to upgrade their device after which they will be able to access company resources.|✓||✓||✓|✓|✓|  
    |**Maximum OS version allowed**|When a device is using an OS version later than the one specified in the rule, access to company resources is blocked and the user is asked to contact their IT admin. Until there is a change in rule to allow the OS version, this device cannot be used to access company resources.|✓||✓||✓|✓|✓|  
    |**Require devices to be reported as healthy**(1602 update)|You can set a rule to require that Windows 10 devices must be reported as healthy in new or existing Compliance Policies. If this setting is enabled, Windows 10 devices will be evaluated via the Health Attestation Service (HAS) for the following data points:<br /><br /> - **BitLocker is enabled**<br /><br /> When Bitlocker is on, the device is able to protect data that is stored on the drive from unauthorized access, when the system is turned off or goes to hibernation. <br />Windows BitLocker Drive Encryption encrypts all data stored on the Windows operating system volume. BitLocker uses the TPM to help protect the Windows operating system and user data and helps to ensure that a computer is not tampered with, even if it is left unattended, lost, or stolen.<br />If the computer is equipped with a compatible TPM, BitLocker uses the TPM to lock the encryption keys that protect the data. As a result, the keys cannot be accessed until the TPM has verified the state of the computer.<br /><br /> **- Code integrity is enabled**<br /><br /> Code integrity is a feature that validates the integrity of a driver or system file each time it is loaded into memory. Code integrity detects whether an unsigned driver or system file is being loaded into the kernel, or whether a system file has been modified by malicious software that is being run by a user account with administrator privileges.<br /><br /> **- Secure boot is enabled**<br /><br /> When Secure Boot is enabled, the system is forced to boot to a factory trusted state. Also, when Secure Boot is enabled, the core components used to boot the machine must have correct cryptographic signatures that are trusted by the organization that manufactured the device. The UEFI firmware verifies this before it lets the machine start. If any files have been tampered with, breaking their signature, the system will not boot.<br /><br /> **- Early-launch antimalware is enabled (this setting only applies to PCs.)**<br /><br /> Early launch anti-malware (ELAM) provides protection for the computers in your network when they start up and before third-party drivers initialize.<br />This rule is turned off by default.<br /><br /> For information on how the HAS service works, see [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).||||✓||||  
  
     <sup>1</sup> For devices that run Windows and are secured with a Microsoft Account, the compliance policy will fail to evaluate correctly if **Minimum password length** is greater than 8 characters or if **Minimum number of character sets** is more than 2.  
  
7.  On the **Summary** page of the wizard, review the settings you made, and then complete the wizard.  
  
 The new policy displays in the **Compliance Policies** node of the **Assets and Compliance** workspace.  
  
## Deploy a compliance policy  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then click **Compliance Policies**.  
  
3.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
4.  In the **Deploy Compliance Policy** dialog box, click **Browse** to select the user collection to which to deploy the policy.  
  
     Additionally, you can select options to generate alerts when the policy is not compliant, and also to configure the schedule by which this policy will be evaluated for compliance.  
  
5.  When you are done, click **OK**.  
  
## Monitor the compliance policy  
  
#### To view compliance results in the Configuration Manager console  
  
1.  In the Configuration Manager console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, click **Deployments**.  
  
3.  In the **Deployments** list, select the compliance policy deployment for which you want to review compliance information.  
  
4.  You can review summary information about the compliance of the policy deployment on the main page. To view more detailed information, select the deployment, and then on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  
  
     The **Deployment Status** page contains the following tabs:  
  
    -   **Compliant**: Displays the compliance of the policy based on the number of assets affected. You can click a rule to create a temporary node under the **Users** or **Devices** node that are in the **Assets and Compliance** workspace, which contains all users or devices that are compliant with this rule. The **Asset Details** pane displays the users or devices that are compliant with the policy. Double-click a user or device in the list to display additional information.  
  
    -   **Error**: Displays a list of all errors for the selected policy deployment based on number of assets affected. You can click a rule to create a temporary node under the **Users** or **Devices** node of the **Assets and Compliance** workspace, which contains all users or devices that generated errors with this rule. When you select a user or device, the **Asset Details** pane displays the users or devices that are affected by the selected issue. Double-click a user or device in the list to display additional information about the issue.  
  
    -   **Non-Compliant**: Displays a list of all noncompliant rules within the policy based on number of assets affected. You can click a rule to create a temporary node under the **Users** or **Devices** node of the **Assets and Compliance** workspace, which contains all users or devices that are not compliant with this rule. When you select a user or device, the **Asset Details** pane displays the users or devices that are affected by the selected issue. Double-click a user or device in the list to display further information about the issue.  
  
    -   **Unknown**: Displays a list of all users and devices that did not report compliance for the selected policy deployment together with the current client status of devices.  
  
#### To view a Health Attestation Report  
  
1.  **Beginning in version 1602 of Configuration Manager**, in the Configuration Manager console, click **Monitoring**.  
  
2.  To view a summary report of the current status of devices by their compliance status,  click **Security**. and then click **Health Attestation**.  
  
3.  To view a report that lists all devices and all the health attestation attributes,   click **Security**. and then click **Health Attestation**.  
  
## Next Steps  
 You can now use the compliance policy with conditional access policies to control access to services in your organization.  
  
### See also  
 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)