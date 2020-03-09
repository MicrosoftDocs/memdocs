---
# required metadata

title: Antivirus policy settings for Windows security for Intune | Microsoft Docs
description: See a list of the settings in the Windows Security experience profile you can configure as part of Endpoint security Antivirus policy in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
 
---

# Settings for Windows Security experience policy

View the Antivirus policy settings you can configure for the Windows Security experience profile in Microsoft Intune.

## Windows Security

- **Enable tamper protection to prevent Microsoft Defender being disabled**  
  CSP: See *Configuration/TamperProtection* in [Defender CSP](https://docs.microsoft.com/windows/client-management/mdm/defender-csp)

  When *Enabled* or *Disabled* was set by a device user, *Not configured* restores the device to its default state. When a state of *Enabled* or *Disabled* was set by this policy and not a user, deploying *Not configured* has no impact on the setting. To change the state, you must deploy either *Enable* or *Disable* to implement that as the new state.

  - **Not configured** (*default*) - This policy doesn't alter the state of Tamper Protection on a device when previously set by this policy. If the setting was configured by the device user, the setting is restored to the system default.
  - **Enable** - Turn on Tamper Protection restrictions. Device users can't change this setting.
  - **Disable** - Turn off Tamper Protection Restrictions. Device users can't change this setting.

- **Hide the Virus and threat protection area in the Windows Security app**  
  CSP: [DisableVirusUI](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablevirusui)

  Configure the Virus and threat protection area in the Microsoft Defender Security Center is hidden from device users. Hiding this section also blocks all notifications related to Virus and threat protection.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

  When set to *Yes*, you can configure the following setting:
  - **Hide the Ransomware data recovery option in the Windows Security app**  
    CSP: [HideRansomwareDataRecovery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-hideransomwaredatarecovery)

    This setting is only available when *Hide Virus and threat protection* is set to *Yes*.

    Configure if the Ransomware protection area in the Microsoft Defender Security Center is hidden from device users. Hiding this section also blocks all notifications related to Ransomware protection.
    - **Not configured** (*default*) - The setting is restored to the system default.
    - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Hide the Account protection area in the Windows Security app**  
  CSP: [DisableAccountProtectionUI](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disableaccountprotectionui)

  Configure if the Account protection area in the Microsoft Defender Security Center is hidden from device users. Hiding this section also blocks all notifications related to Account protection.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Hide the Firewall and network protection area in the Windows Security app**  
  CSP: [DisableNetworkUI](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablenetworkui)
  
  Configure if the Firewall and network protection area in the Microsoft Defender Security center is hidden from device users. Hiding this section also blocks all notifications related to Firewall and network protection.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Hide the App and browser control area in the Windows Security app**  
  CSP: [DisableAppBrowserUI](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disableappbrowserui)

  Configure if the App and browser control area in the Microsoft Defender Security center is hidden from device users. Hiding this section also blocks all notifications related to App and browser control.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Hide the Device security area in the Windows Security app**  
  CSP: [DisableDeviceSecurityUI](https://docs.microsoft.com/windows/client-management/mdm/policy-CSP:-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disabledevicesecurityui)

  Configure if the Device security area in the Microsoft Defender Security Center is hidden from device users. Hiding this section also blocks all notifications related to Hardware protection.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Hide the Device performance and health area in the Windows Security app**  
  CSP: [DisableHealthUI
](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablehealthui)

  Configure if the Device performance and health area in the Microsoft Defender Security center is hidden from device users. Hiding this section also blocks all notifications related to Device performance and health.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Hide the Family options area in the Windows Security app**  
  CSP: [DisableFamilyUI](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablefamilyui)

  Configure if the Family options area in the Microsoft Defender Security center is hidden from device users. Hiding this section also blocks all notifications related to Family options.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the area from device users and suppress notifications. Device users can't change this setting.

- **Windows Security app notifications**  
  CSP: [DisableNotifications](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablenotifications)

  Use this setting to block all Windows Security app notifications, based on your selection. This setting overrides the individual settings for different areas of the Security app.
  - **Not configured** (*default*) - All Windows Security app notifications that aren't controlled by another setting, are allowed.
  - **Block non-critical notifications** - Non-critical notifications are blocked for all Windows Security features. Critical notifications are allowed.
  - **Block all notifications** - Critical and non-critical notifications are blocked for all Windows Security features.

- **Hide the Windows Security icon from the notification area**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-hidewindowssecuritynotificationareacontrol)

  Configure the display of the notification area control. The user needs to either sign out and sign in or reboot the computer for this setting to take effect.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Hide the icon in the users system tray. Device users can't change this setting.

- **Disable the Clear TPM option in the Windows Security app**  
  CSP: [DisableClearTpmButton](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablecleartpmbutton)

  By default, the *Clear TPM* button is available for use on supported systems. Use this setting to manage if that button is available in Windows Security.
 - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Disable access to the clear TPM button in the Windows Security app.

  - **Prompt users to update TPM firmware if vulnerability is discovered**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disabletpmfirmwareupdatewarning)

  Configure if the device displays the recommendation to update TPM Firmware when a vulnerable firmware is detected.
  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Yes** - Prompt device users when a potential vulnerability is found in the devices TPM firmware.

- **Organization's support contact information**  
  CSP: [EnableCustomizedToasts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-enablecustomizedtoasts)

  Configure custom IT contact information for device users.
  - **Not configured** (*default*) - Instead of configuring contact information specific to your organization, Windows displays a default notification.
  - **Display in app and in notifications**
  - **Display only in app**
  - **Display only in notifications**

  When you select any option other than *Not Configured*, you can then specify your custom contact information.

  CSP: [CompanyName](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-companyname)

  - **Contact name** - The company name that is displayed to the users.
  - **Phone number** - Enter your support teams contact number.
  - **Email address** - Enter an email address for contacting your support team.
  - **Web address** - Enter the URL for a website for contacting your support team.


## Next steps

[Create or manage Antivirus policies](../protect/endpoint-security-antivirus-policy.md)