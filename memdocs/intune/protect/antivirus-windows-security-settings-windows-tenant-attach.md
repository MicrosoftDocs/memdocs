---
# required metadata

title: Windows Antivirus policy settings from Windows security settings for tenant attached devices in Microsoft Intune | Microsoft Docs
description: Review the settings in the *Windows Security experience* profile for tenant attached devices. To use this Endpoint security Antivirus policy, you must first configure tenant attach for Configuration Manager for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/27/2021
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
ms.collection:
- tier3
- M365-identity-device-management
ms.reviewer: mattcall

---

# Settings for Windows Security experience Antivirus policy for tenant attached devices in Microsoft Intune

View the Windows Security experience settings you can manage with the **Windows Security experience (preview)** profile from Intune.

The profile is available when you configure [Intune Endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md). This profile supports devices you manage with Configuration Manager after configuring the [tenant attach](../protect/tenant-attach-intune.md) scenario for Intune.

## Windows Security

- **Enable tamper protection to prevent Microsoft Defender being disabled**  
  [Prevent changes to security settings with Tamper Protection](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Not configured**
  - **Enabled**
  - **Disabled**

- **Hide the Account protection area in the Windows Security app**  
  CSP: [DisableAccountProtectionUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disableaccountprotectionui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the Account protection area in Windows Defender Security Center.
  - **(Enable)** The users can see the display of the Account protection area in Windows Defender Security Center.

- **Hide the App and browser control area in the Windows Security app**  
  CSP: [DisableAppBrowserUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disableappbrowserui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the app and browser protection area in Windows Defender Security Center.
  - **(Enable)** The users cannot see the display of the app and browser protection area in Windows Defender Security Center.

- **Disable the Clear TPM option in the Windows Security app**  
  CSP: [DisableClearTpmButton](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter)

  - **Not configured** (*default*)
  - **(Disable)** The security processor troubleshooting page shows a button that initiates the process to clear the security processor (TPM).
  - **(Enable)** The security processor troubleshooting page will not show a button that initiates the process to clear the security processor (TPM).

- **Hide the Family options area in the Windows Security app**  
  CSP: [DisableFamilyUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablefamilyui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the family options area in Windows Defender Security Center.
  - **(Enable)** The users cannot see the display of the family options area in Windows Defender Security Center.

- **Hide the Device security area in the Windows Security app**  
  CSP: [DisableDeviceSecurityUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disabledevicesecurityui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the Device security area in Windows Defender Security Center.
  - **(Enable)** The users cannot see the display of the Device security area in Windows Defender Security Center.

- **Hide the Device performance and health area in the Windows Security app**  
  CSP: [DisableHealthUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablehealthui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the device performance and health area in Windows Defender Security Center.
  - **(Enable)** The users cannot see the display of the device performance and health area in Windows Defender Security Center.

- **Hide the Firewall and network protection area in the Windows Security app**  
  CSP: [DisableNetworkUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablenetworkui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the firewall and network protection area in Windows Defender Security Center.
  - **(Enable)** The users cannot see the display of the firewall and network protection area in Windows Defender Security Center.

- **Hide the Windows Security icon from the notification area**  
  CSP: [HideWindowsSecurityNotificationAreaControl](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter)

  - **Not configured** (*default*)
  - **Enabled**
  <!-- This setting appears to be incomplete in the UI at last check  -->

- **Hide the Ransomware data recovery option in the Windows Security app**  
    CSP: [HideRansomwareDataRecovery](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-hideransomwaredatarecovery)

  - **Not configured** (*default*)
  - **(Disable)** The Ransomware data recovery area will be visible.
  - **(Enable)** The Ransomware data recovery area is hidden.

- **Hide the Virus and threat protection area in the Windows Security app**  
  CSP: [DisableVirusUI](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablevirusui)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of the virus and threat protection area in Windows Defender Security Center.
  - **(Enable)** The users cannot see the display of the virus and threat protection area in Windows Defender Security Center.

- **Prompt users to update TPM firmware if vulnerability is discovered**  
  CSP: [DisableTpmFirmwareUpdateWarning](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter)

  - **Not configured** (*default*)
  - **(Disabled or Not configured)** A warning will be displayed if the firmware of the security processor (TPM) should be updated for TPMs that have a vulnerability.
  - **(Enabled)** No warning will be displayed if the firmware of the security processor (TPM) should be updated.

- **Organization's support email address**  
  CSP: [EnableCustomizedToasts](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-enablecustomizedtoasts)

- **Organization's support phone number**  
  CSP: [EnableCustomizedToasts](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-enablecustomizedtoasts)

- **Organization's support web address**  
  CSP: [EnableCustomizedToasts](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-enablecustomizedtoasts)

- **Organization's support contact name**  
  CSP: [EnableCustomizedToasts](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-enablecustomizedtoasts)

- **Disable Notifications**  
  CSP: [DisableNotifications](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disablenotifications)

  - **Not configured** (*default*)
  - **(Disable)** The users can see the display of Windows Defender Security Center notifications.
  - **(Enable)** The users cannot see the display of Windows Defender Security Center notifications.

- **Disable Enhanced Notifications**  
  CSP: [DisableEnhancedNotifications](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disableenhancednotifications)

  - **Not configured** (*default*)
  - **(Disable)** Windows Defender Security Center will display critical and non-critical notifications to users.
  - **(Enable)** Windows Defender Security Center only displays notifications that are considered critical on clients.
