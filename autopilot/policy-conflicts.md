---
title: Windows Autopilot policy conflicts
description: Inform yourself about policy conflicts that may occur during Windows Autopilot deployment.
ms.technology: itpro-deploy
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/16/2023
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot - Policy Conflicts

There are a significant number of policy settings available for Windows, including:

- Native MDM policies
- Group policy (ADMX-backed) settings

Some policy settings can cause issues in some Windows Autopilot scenarios. These issues can arise because of how the policies change Windows behavior. If you find any of these issues, remove the policy in question to resolve the issue.

| Policy | More information |
|-------|---------------|
| Disallow changing of language/region/keyboard | This GPO isn't supported during the OOBE flow as it impacts the autologon experience. If you need to set this policy for users, you should select to hide these pages in the Autopilot profile to prevent users from making changes. |
| [AppLocker CSP](/windows/client-management/mdm/applocker-csp) | The AppLocker CSP isn't supported in the Enrollment Status Page as it triggers a reboot when a policy is applied or a deletion occurs. |
|Device restriction / [Password Policy](/windows/client-management/mdm/devicelock-csp) | The out-of-box experience (OOBE) or user desktop autologon can fail when a device reboots during the device Enrollment Status Page (ESP). This failure can occur when certain [DeviceLock policies](/windows/client-management/mdm/policy-csp-devicelock) are applied to a device. Such policies can include:<ul><li>Minimum password length and password complexity</li><li>Any similar group policy settings (including any that disable autologon)</li></ul>This possible failure is especially true for kiosk scenarios where passwords are automatically generated. |
| Windows Security Baseline / [Administrator elevation prompt behavior](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions)<br><br>Windows Security Baseline / [Require admin approval mode for administrators](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions)<br><br>Windows Security Baseline / [Enable virtualization based security](/windows/client-management/mdm/policy-csp-deviceguard) | These policies require a reboot, as a result more prompts may appear when modifying user account control (UAC) settings during the OOBE using the device Enrollment Status Page (ESP). Increased prompts are more likely if the device reboots after policies are applied. To work around this issue, the policies can be targeted to users instead of devices so that they apply later in the process. |
| Device restrictions / Cloud and Storage / [Microsoft Account sign-in assistant](/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage) | Setting this policy to "disabled" turns off the Microsoft Sign-in Assistant service (wlidsvc). Windows Autopilot requires this service to get the Windows Autopilot profile. |
| Registry keys that affect Windows Autopilot if a device setting requires a reboot during device ESP<br><br>**Registry path**:<br>`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Automatic logon` | **Registry key**:<br>If the [AutoAdminLogon](/troubleshoot/windows-server/user-profiles-and-logon/turn-on-automatic-logon) registry key is set to `0` (disabled), this breaks Windows Autopilot. |
| [MDM wins over Group Policy](/windows/client-management/mdm/policy-csp-controlpolicyconflict) | This policy allows you to control which policy is used when both the MDM policy and its equivalent Group Policy (GP) are set on the device. |
| Group Policy Objects (GPOs) that affect Windows Autopilot for [pre-provisioned deployment](pre-provision.md)<br><br>**GPO path**: <br>Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options<br><br>**Policies**:<br>[Interactive logon: Message title for users attempting to log on](/windows/security/threat-protection/security-policy-settings/interactive-logon-message-title-for-users-attempting-to-log-on)<br><br>[Interactive logon: Message text for users attempting to log on](/windows/security/threat-protection/security-policy-settings/interactive-logon-message-text-for-users-attempting-to-log-on)<br><br>[Interactive logon: Require Windows Hello for Business or smart card](/windows/security/threat-protection/security-policy-settings/interactive-logon-require-smart-card)<br><br>[User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode - Prompt for credentials on the secure desktop](/windows/security/threat-protection/security-policy-settings/user-account-control-behavior-of-the-elevation-prompt-for-administrators-in-admin-approval-mode) | Windows Autopilot pre-provisioning doesn't work when any of the four GPO policy settings listed here are enabled. |
| [PreferredAadTenantDomainName](/windows/client-management/mdm/policy-csp-authentication#preferredaadtenantdomainname) | When this policy is enabled, it will add to **DefaultUser0**, which will cause autologon to fail. |

For more information, see [Troubleshooting Windows Autopilot](troubleshooting.md).
