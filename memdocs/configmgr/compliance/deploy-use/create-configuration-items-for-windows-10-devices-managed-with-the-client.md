---
title: Create configuration items for Windows 10
titleSuffix: Configuration Manager
description: Use the Windows 10 configuration item to manage settings for Windows 10 computers that are managed by the Configuration Manager client.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz


---

# Create configuration items for Windows 10 devices

Use the Configuration Manager **Windows 10** configuration item to manage settings for Windows 10 computers that are managed by the Configuration Manager client.  
  
> [!IMPORTANT]  
>  In this release, if you created a **Password** setting as part of a configuration item of the type **Windows 10** (for a device managed with the Configuration Manager client), be aware of the following problem. If the setting doesn't already exist, or hasn't been configured on the Windows 10 device, it will incorrectly evaluate as compliant.  
>   
>  As a workaround, when you create a setting for these devices, ensure that **Remediate noncompliant settings** is selected on the settings pages of the Create Configuration Item wizard. In addition, when you deploy a configuration baseline containing a Windows 10 configuration item containing password settings, select **Remediate noncompliant rules when supported**. You make this selection in the Deploy Configuration Baselines dialog box. By using this workaround, the setting is monitored, and remediated if it's found to be noncompliant. After remediation, the setting is correctly reported as **Compliant** (unless a problem is encountered, in which case it will report **Error**).  
  
### To create a Windows 10 configuration item  
  
1. In the Configuration Manager console, select **Assets and Compliance**.  
  
2. In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then select **Configuration Items**.  
  
3. On the **Home** tab, in the **Create** group, select **Create Configuration Item**.  
  
4. On the **General** page of the **Create Configuration Item** wizard, specify a name and optional description for the configuration item.  
  
5. Under **Specify the type of configuration item that you want to create**, select **Windows 10**.  
  
6. If you create and assign categories to help you search and filter configuration items in the Configuration Manager console, select **Categories**.  
  
7. On the **Supported Platforms** page of the wizard, select the specific Windows 10 platforms that will evaluate the configuration item.  
  
8. On the **Device Settings** page of the wizard, select the settings group that you want to configure. (For details, see [Windows 10 configuration item settings reference](#BKMK_Ref) in this article.) Then select **Next**.  
  
   > [!TIP]  
   >  If the setting that you want isn't listed, select the **Configure additional settings that are not in the default setting groups check box**.  
  
9. On each settings page, configure the settings you require, and whether you want to remediate them when they aren't compliant on devices (when this is supported).  
  
10. For each settings group, you can also configure the severity reported when a configuration item is found to be noncompliant:  
  
    -   **None**: Devices that fail this compliance rule don't report a failure severity for Configuration Manager reports.  
  
    -   **Information**: Devices that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
    -   **Warning**: Devices that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
    -   **Critical**: Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
    -   **Critical with event**: Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also logged as a Windows event in the application event log.  
  
11. On the **Platform Applicability** page of the wizard, review any settings that aren't compatible with the supported platforms you selected earlier. You can go back and remove these settings, or you can continue.  
  
    > [!TIP]  
    >  Unsupported settings are not assessed for compliance.  
  
12. Complete the wizard.  
  
    You can view the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.  
  
## <a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### Password  
  
|Setting|Details|  
|-------------|-------------|  
|**Require password settings on devices**|Requires a password on supported devices.|  
|**Minimum password length (characters)**|The minimum length in characters for the password.|  
|**Password expiration in days**|The number of days before the password must be changed.|  
|**Number of passwords remembered**|Prevents reusing previous passwords.|  
|**Number of failed logon attempts before a device is wiped**|Wipes the device if sign-in fails this number of times.|  
|**Idle time before device is locked**|Specifies how many minutes the device must be inactive before it's automatically locked.|  
|**Password complexity**|Choose whether you can specify a PIN such as '1234', or whether you must supply a strong password.|
|**Number of complex character sets required in password**|If you selected a **Strong** password, use this setting to configure the number of complex character sets required. For a strong password, this setting should be set to at least **3**, which means both letters and numbers are required. Select **4** if you want to enforce a password that additionally requires special characters, such as **(%$**.<br>(Windows 10 only)  |
  
###  Device  
  
|Setting name|Details|  
|------------------|-------------|  
|**Bluetooth**|Allows use of the Bluetooth feature on the device.|  
  
### Cloud  
  
|Setting name|Details|  
|------------------|-------------|  
|**Settings synchronization**|Allows synchronization of settings between devices.|  
|**Credentials synchronization**|Allows synchronization of credentials between devices.|  
|**Settings synchronization over metered connections**|Allows settings to be synchronized when the internet connection is metered.|  
  
### Roaming  
  
|Setting name|Details|  
|------------------|-------------|  
|**Data roaming**|Allows roaming between networks when accessing data.|  
  
### Encryption  
  
|Setting name|Details|  
|------------------|-------------|  
|**File encryption on device**|Requires that files on the device are encrypted.|  
  
### System security  
  
|Setting name|Details|  
|------------------|-------------|  
|**User Account Control**|Configures how Windows User Account Control works on the device.<br />For example, you can disable it, or set the level at which it notifies you.|  
|**Network firewall**|Enables or disables Windows Firewall.|  
|**SmartScreen**|Enables or disables Windows SmartScreen.|  
|**Virus protection**|Requires that antivirus software must be installed and configured.|  
|**Virus protection signatures are up to date**|Requires that the signature files for the antivirus software on the device must be up to date.|  
  
### Windows Information Protection

With the increase of employee-owned devices in the enterprise, there's also an increasing risk of accidental data leaks through apps and services, like email, social media, and the public cloud. These are outside of the organization's control. Examples include when an employee:

- Sends the latest engineering pictures from their personal email account.
- Copies and pastes product info into a tweet.
- Saves an in-progress sales report to their public cloud storage.

Windows Information Protection (WIP, formerly enterprise data protection) helps to protect against this potential data leakage, without otherwise interfering with the employee experience. WIP also helps to protect enterprise apps and data against accidental data leaks on enterprise-owned devices and personal devices that employees bring to work. WIP doesn't require changes to your environment or other apps.

Configuration Manager Windows Information Protection configuration items manage the following:

- The list of apps protected by WIP
- Enterprise network locations
- Protection level
- Encryption settings
  
For information about how to configure WIP with Configuration Manager, see:

- [Protect your enterprise data using Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Create and deploy a Windows Information Protection (WIP) policy using Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Limitations while using Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## See also  
[Configuration items for devices managed with the Configuration Manager client](../../compliance/deploy-use/create-configuration-items.md)
