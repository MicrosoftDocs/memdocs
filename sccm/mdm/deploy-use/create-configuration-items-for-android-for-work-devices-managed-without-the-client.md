---
title: "How to create configuration items for Android for Work devices managed with Intune"
titleSuffix: "Configuration Manager"
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
---
# How to create configuration items for Android for Work devices managed with Intune

 Use the System Center Configuration Manager **Android for Work** configuration item to manage settings for Android for Work devices that are enrolled in Microsoft Intune or managed on-premises by Configuration Manager.  

### To create an Android for Work configuration item  

1. In the Configuration Manager console, click **Assets and compliance**.  

2. In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then click **Configuration Items**.  

3. On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  

4. On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.  

5. Under **Specify the type of configuration item that you want to create**, select **Android for Work**.  

6. Choose **Categories** if you create and assign categories to help you search and filter configuration items in the Configuration Manager console.  

   Click **Next**.

7. On the **Device Settings** page of the wizard, select the settings groups that you want to configure. See [Android for Work configuration item settings](#android-for-work-configuration-item-settings-reference) for details, and then click **Next**.  

   > [!TIP]  
   >  If the setting that you want is not listed, select the **Configure additional settings that are not in the default setting groups check box**.  

8. On each settings page, configure the settings you require, and whether you want to remediate them when they are not compliant on devices (when this is supported).  

9. For each settings group, you can also configure the severity that will be reported when a configuration item is found to be noncompliant from:  

   -   **None** - Devices that fail this compliance rule do not report a failure severity for Configuration Manager reports.  

   -   **Information** - Devices that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  

   -   **Warning** - Devices that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  

   -   **Critical** - Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  

   -   **Critical with event** - Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also be logged as a Windows event in the application event log.  

10. On the **Platform Applicability** page of the wizard, review any settings that are not compatible with the supported platforms you selected earlier. You can go back and remove these settings, or you can continue.  

    > [!TIP]  
    >  Unsupported settings are not assessed for compliance.  

11. Complete the wizard.  

    You can view the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.  

##  Android for Work configuration item settings reference  

### Password  

|Setting|Details|  
|-------------|-------------|  
|**Require password settings on devices**|Require a password on supported devices.|  
|**Minimum password length (characters)**|The minimum length for the password.|  
|**Password expiration in days**|The number of days before a password must be changed.|  
|**Number of passwords remembered**|Prevents re-use of recent used passwords.|  
|**Number of failed logon attempts before device is wiped**|Wipes the device if this number of login attempts fail.|  
|**Idle time before device is locked**|Select the amount of time the device is unused before it locks.|
|**Password quality**|Select the password complexity level required and also whether biometric devices can be used.|  
|**Allow Smart Lock and other trust agents**|Let’s you control the Smart Lock feature on compatible Android devices. This phone capability, sometimes known as trust agents, lets you disable or bypass the device lock screen password if the device is in a trusted location such as when it is connected to a specific Bluetooth device, or when it is near to an NFC tag. You can use this setting to prevent end users from configuring Smart Lock.|
|**Fingerprint for unlocking**|&nbsp;|

###  Work Profile  
 These settings apply to Samsung KNOX devices only.  

|Setting name|Details|  
|------------------|-------------|  
|**Allow data sharing between work and personal profiles**|Choose from:<br>- **Not Configured**<br>- **Default sharing restrictions**<br>- **Apps in work profile can handle request from personal profile**<br>- **Apps in personal profile can handle request from work profile**<br><br>(See also [Copy-Paste settings](#copy-paste-configuration-item-settings) using custom URI)|  
|**Hide work profile notifications when device is locked (Android 6.0+)**||
|**Set default app permission policy (Android 6.0+)**|Choose from:<br>- **Not Configured**<br>- **Always prompt**<br>- **Auto Grant**<br>- **Auto Deny**|

### Copy-paste configuration item settings
None of the **Allow data sharing between work and personal profiles** options prevent copy-paste behavior. Use a custom setting that can be configured to prevent copy-paste. This can be set through custom URI.

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Value type: Boolean

Setting DisallowCrossProfileCopyPaste to true prevents copy-paste behavior between Android for Work personal and work profiles.

## See Also  
 [Configuration items for devices managed without the System Center Configuration Manager client](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
