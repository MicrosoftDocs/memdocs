---
title: Create and deploy a device compliance policy | Microsoft Docs
description: "Learn how to create and deploy device compliance policies in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
---

# Create and deploy a device compliance policy

*Applies to: System Center Configuration Manager (Current Branch)*


## Create a compliance policy

1.  In the System Center Configuration Manager console, choose **Assets and Compliance**.

2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then choose **Compliance Policies**.

3.  On the **Home** tab, in the **Create** group, choose **Create Compliance Policy**.

4.  On the **General** page of the Create Compliance Policy Wizard, specify the following information:

  * **Name**. Enter a unique name for the compliance policy. You can use up to 256 characters.

  * **Description**. Enter a description that gives an overview of the VPN profile and helps identify it in the Configuration Manager console. You can use up to 256 characters.

  * **Type of compliance policy**. Select the type of policy that you want to create, depending on whether the device is managed by Configuration Manager. This applies to version  or later.<br /><br /> For devices managed by Intune, choose the **Compliance rules for devices managed without configuration manager client** option. When you select this option, you can also select the type of platform that you want this policy to apply to.

  * **Noncompliance severity for reports**. Specify the severity level that is reported if this compliance policy is evaluated as noncompliant. The available severity levels are:

     * **None**. Devices that fail this compliance rule do not report a failure severity for Configuration Manager reports.
     * **Information**. Devices that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.   
     * **Warning**. Devices that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.
     * **Critical**. Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.
     * **Critical with event**. Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also logged as a Windows event in the application event log.      

5.  On the **Supported Platforms** page, choose the device platforms that this compliance policy will be evaluated on, or choose **Select all** to choose all device platforms. The supported platforms are: Windows 7, Windows 8.1, and Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.

6.  On the **Rules** page, you define one or more rules that define the configuration that devices must have in order to be evaluated as compliant. When you create a compliance policy, some rules are enabled by default, but you can edit or delete these. For a full list of all the rules, see the "Compliance policy rules" section later in this topic.

  > [!NOTE]  
  >  On Windows PCs, Windows operating system version 8.1 is reported as 6.3 instead of 8.1. If the OS version rule is set to Windows 8.1 for Windows, then the device will be reported as noncompliant even if the device has Windows 8.1. Make sure you are setting the right *reported* version of Windows for the minimum and maximum OS rules. The version number must match the version that the **winver** command returns. Windows Phones do not have this issue; the version is reported as 8.1 as expected. 
  >  For Windows PCs with the Windows 10 operating system, the version should be set as **10.0** plus the OS build number that the **winver** command returns.

7.  On the **Summary** page of the wizard, review the settings that you made, and then finish the wizard.

 The new policy appears in the **Compliance Policies** node of the **Assets and Compliance** workspace.

## Deploy a compliance policy

1.  In the Configuration Manager console, choose **Assets and Compliance**.

2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then choose **Compliance Policies**.

3.  On the **Home** tab, in the **Deployment** group, choose **Deploy**.

4.  In the **Deploy Compliance Policy** dialog box, choose **Browse** to select the user collection to which to deploy the policy.

     Additionally, you can select options to generate alerts when the policy is not compliant, and to set the schedule by which this policy will be evaluated for compliance.

5.  When you are done, choose **OK**.

## Monitor the compliance policy

#### To view compliance results in the Configuration Manager console

1.  In the Configuration Manager console, choose **Monitoring**.

2.  In the **Monitoring** workspace, choose **Deployments**.

3.  In the **Deployments** list, select the compliance policy deployment for which you want to review compliance information.

4.  You can review summary information about the compliance of the policy deployment on the main page. To view more detailed information, select the deployment, and then on the **Home** tab, in the **Deployment** group, choose **View Status** to open the **Deployment Status** page.

    The **Deployment Status** page has the following tabs:

    -   **Compliant**. Shows the compliance of the policy based on the number of assets affected. You can choose a rule to create a temporary node under the **Users** or **Devices** node of the **Assets and Compliance** workspace, which contains all users or devices that comply with this rule. The **Asset Details** pane shows the users or devices that comply with the policy. Double-click a user or device in the list to show additional information.

    -   **Error**. Shows a list of all errors for the selected policy deployment based on number of assets affected. You can choose a rule to create a temporary node under the **Users** or **Devices** node of the **Assets and Compliance** workspace, which contains all users or devices that generated errors with this rule. When you select a user or device, the **Asset Details** pane shows the users or devices that an issue affects. Double-click a user or device in the list to show additional information about the issue.

    -   **Non-Compliant**. Shows a list of all noncompliant rules within the policy, based on the number of assets affected. You can choose a rule to create a temporary node under the **Users** or **Devices** node of the **Assets and Compliance** workspace, which contains all users or devices that do not comply with this rule. When you select a user or device, the **Asset Details** pane shows the users or devices that an issue affects. Double-click a user or device in the list to show further information about the issue.

    -   **Unknown**. Shows a list of all users and devices that did not report compliance for the selected policy deployment, together with the current client status of devices.

#### To monitor the compliance status of an individual device

1.  In the Configuration Manager console, choose the **Assets and compliance** workspace.

2.  Choose **Devices**.

3.  Right-click one of the columns to enable more columns.

  You can add the following columns:

  - **Azure Active Directory device ID**.  Unique identifier for the device in Azure Active Directory.

  - **Compliance Error Details**.  Error message details when the end-to-end process goes wrong. If this column is blank, it means no errors were found, and the compliance status was successfully reported.

  - **Compliance Error Location**.  More details on where the compliance failed. If this column is blank, it means no errors were found, and the compliance status was successfully reported. Examples of where the compliance process might fail: 
	  - ConfigMgr Client
	  - Management point
	  - Intune
	  - Azure Active Directory
<br></br>
  - **Compliance Evaluation Time**. Last time the compliance was checked.

  - **Compliance Set Time**. Last time the compliance was updated to Azure Active Directory.

  - **Conditional Access Compliant**.  Whether or not the machine complies with conditional access policies.

  > [!IMPORTANT]
  > These columns are not shown by default.

#### To view Intune compliance policies charts
1. Beginning in version 1610 of Configuration Manager, in the Configuration Manager console, choose **Monitoring**.

2. In the **Monitoring** workspace, go to **Overview** > **Compliance Settings** > **Compliance Policies**.

   The following charts appear:

    - **Overall Device Compliance**. Shows the overall compliance of devices for all compliance policies.
    - **Top Non-Compliance Reasons**. Shows the top policies for which devices are noncompliant.

3. Choose a section in either chart to drill down to a list of the devices within that category.

#### To view a health attestation report

1.  Beginning in version 1602 of Configuration Manager, in the Configuration Manager console, choose **Monitoring**.

2.  To view a summary report of the current status of devices by their compliance status, choose **Security**, and then choose **Health Attestation**.

3.  To view a report that lists all devices and all the health attestation attributes, choose **Security**, and then choose **Health Attestation**.

## Compliance policy rules
* **Require password settings on mobile devices**. You can require users to enter a password before they can access their device.

  **Supported on:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Require a password to unlock an idle device** (1602 update). You can require users to enter a password to access device that is locked.

  **Supported on:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutes of inactivity before password is required** (1602 update). You can specify the idle time before the user must reenter their password. Set the value to one of the available options: **1 minute**, **5 minutes**, **15 minutes**, **30 minutes**, **1 hour**.

  This rule must be used with **Require a password to unlock an idle device**. The value set here determines when the device is considered idle and is locked. When **Require a password to unlock an idle device** is set to **True**, the user must enter a password to access the locked device.

  **Supported on:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Require automatic updates** (1602 update). You can require devices with Windows 8.1 or later to automatically install updates, and you can specify the class of updates.

  The value should be set to **None** to prevent automatic installation, to **Recommended** to automatically install all recommended updates, or to **Important** to install only updates classified as important.

  **Supported on:**
  * Windows Phone 8+

* **Allow simple passwords**. You can let users create simple passwords like "1234" or "1111." This setting is disabled by default.

  **Supported on:**
  * Windows Phone 8+
  * iOS 6+

* **Minimum password length**. You can specify the minimum number of digits or characters that the user's password must have (6 by default).

  **Supported on:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >For devices that run Windows and are secured with a Microsoft account, the compliance policy will fail to evaluate correctly if **Minimum password length** is greater than 8 characters or if **Minimum number of character sets** is more than 2.

* **File encryption on mobile device**. You can require the device to be encrypted in order to connect to resources. Devices that run Windows Phone 8 are automatically encrypted. Devices that run iOS are encrypted when you configure the setting **Require password settings on mobile devices**. This setting is enabled by default.

  **Supported on:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Device must not be jailbroken or rooted**. If you enable this setting, jailbroken (iOS) or rooted (Android) devices are not compliant. This setting is disabled by default.

  **Supported on:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Email profile must be managed by Intune**. When you set this option to **Yes**, the device must use the email profile deployed to the device. The device is considered noncompliant if the email profile is not deployed to the same user group as the user group targeted by the compliance policy.

  It is also noncompliant if the user has already set up an email account on the device that matches the Intune email profile that is deployed to the device. In this case, Intune cannot overwrite the user-provisioned profile and therefore cannot manage it. The user can bring the device into compliance by removing the existing email settings, which lets Intune install the managed email profile.

  For details about email profiles, see [Enable access to corporate email using email profiles with Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). This setting is disabled by default.

  **Supported on:**
  * iOS 6+

* **Email profile**. If **Email account must be managed by Intune** is selected, choose **Select** to choose the email profile that devices must be managed by. The email profile must be present on the device.

  **Supported on:**
  * iOS 6+

* **Minimum OS required**. When a device does not meet the minimum OS version requirement that you specify, it is reported as noncompliant. A link with information on how to upgrade appears. The user can choose to upgrade their device, after which they will be able to access company resources.

  **Supported on:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Maximum OS version allowed**. When a device uses an OS version later than the one that you specify in the rule, access to company resources is blocked and the user is asked to contact their IT admin. Until you change the rule to allow the OS version, this device cannot be used to access company resources.

  **Supported on:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Require devices to be reported as healthy** (1602 update). You can set a rule to require that Windows 10 devices must be reported as healthy in new or existing compliance policies. If you enable this setting, Windows 10 devices are evaluated via the Health Attestation Service (HAS) for the following data points:

  - **BitLocker is enabled**. When BitLocker is on, the device can protect data that is stored on the drive from unauthorized access, when the system is turned off or goes to hibernation.

   Windows BitLocker Drive Encryption encrypts all data stored on the Windows operating system volume. BitLocker uses the TPM to help protect the Windows operating system and user data. It helps to ensure that a computer is not tampered with, even if it is left unattended, lost, or stolen.
   
   If the computer is equipped with a compatible TPM, BitLocker uses the TPM to lock the encryption keys that protect the data. As a result, the keys cannot be accessed until the TPM has verified the state of the computer.

  - **Code integrity is enabled**. Code integrity is a feature that validates the integrity of a driver or system file each time it is loaded into memory. Code integrity detects whether an unsigned driver or system file is being loaded into the kernel. It also detects whether a system file has been changed by malicious software that is being run by a user account with admin privileges.

  - **Secure boot is enabled**. When Secure Boot is enabled, the system is forced to start in a factory trusted state. Also, when Secure Boot is enabled, the core components used to start the machine must have correct cryptographic signatures that are trusted by the organization that manufactured the device. The UEFI firmware verifies this before it lets the machine start. If any files have been tampered with, breaking their signature, the system will not start.

  - **Early-launch antimalware is enabled**. This setting applies only to PCs. Early launch anti-malware (ELAM) provides protection for the computers in your network when they start up and before third-party drivers initialize.
  
   This rule is turned off by default.

  For information on how the HAS service works, see [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).

  **Supported on:**
  * Windows 10 and Windows 10 Mobile

- **Apps that cannot be installed on the device**. If users install an app from the admin-noncompliant list of apps, they’ll be blocked when they try to access corporate email and other corporate resources that support conditional access. This rule requires the app name and the app ID when adding an app to the noncompliant list defined by the admin. The app publisher can also be added, but it’s not required.

	**Supported on:**
	  * iOS 6+
	  * Android 4.0+
	  * Samsung KNOX Standard 4.0+
<br></br>
* **Required password type**. Specify whether the user must create an Alphanumeric password or a Numeric password. For Alphanumeric passwords, you also specify the minimum number of character sets that the password must have. The four character sets are: Lowercase, uppercase letters, Symbols and Numbers.

  	**Supported on:**
  	* Windows Phone 8+
  	* Windows 8.1+
  	* iOS 6+
<br></br>
* **Block USB debugging on device**. You do not have to configure this settings as USB debugging is already disabled on Android for Work devices.

 	**Supported on:**
  	* Android 4.0+
  	* Samsung KNOX Standard 4.0+
<br></br>
* **Block apps from unknown sources**. Require that devices prevent installation of apps from unknown sources. You do not have to configure this setting as Android for Work devices always restrict installation from unknown sources.

  	**Supported on:**
  	* Android 4.0+
  	* Samsung KNOX Standard 4.0+
<br></br>
* **Require threat scan on apps**. This setting specifies that the Verify apps feature is enabled on the device. 

  	**Supported on:**
  	* Android 4.2 through 4.4
  	* Samsung KNOX Standard 4.0+

### Find an app ID

An app ID is an identifier that uniquely identifies the app within the Apple and Google application services. An example is com.contoso.myapp. To find one:

- **Android**
	- You can find the app ID in the Google Play store URL that was used to create the app. An example app ID is: *…?id=com.companyname.appname&hl=en*

- **iOS**
	1. In the iTunes store URL, find the ID number, like the one in this example: */id875948587?mt=8*

	2. In a web browser, go to the following URL, replacing the number with the ID number that you just found (in this case, the previous example): https://itunes.apple.com/lookup?id=875948587

	3. Download and open the text file.
  
	4. Search for the text **bundleId**.

    An example app ID is: "*bundleId*":"*com.companyname.appname*" 

