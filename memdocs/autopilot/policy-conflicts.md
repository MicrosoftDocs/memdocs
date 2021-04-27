---
title: Windows Autopilot policy conflicts
ms.reviewer: 
manager: laurawi
description: Inform yourself about policy conflicts that may occur during Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Windows Autopilot - Policy Conflicts

**Applies to**

- Windows 10

There are a significant number of policy settings available for Windows 10, including:
- Native MDM policies
- Group policy (ADMX-backed) settings

Some policy settings can cause issues in some Windows Autopilot scenarios. These issues can arise because of how the policies change Windows 10 behavior. If you find any of these issues, remove the policy in question to resolve the issue.

| Policy | More information |
|-------|---------------|
|Device restriction / <a href="/windows/client-management/mdm/devicelock-csp">Password Policy</a> | The out-of-box experience (OOBE) or user desktop autologon can fail when a device reboots during the device Enrollment Status Page (ESP). This failure can occur when certain <a href="/windows/client-management/mdm/policy-csp-devicelock">DeviceLock policies</a> are applied to a device. Such policies can include:<ul><li>Minimum password length and password complexity</li><li>Any similar group policy settings (including any that disable autologon)</li></ul>This possible failure is especially true for kiosk scenarios where passwords are automatically generated. |
| Windows 10 Security Baseline / <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Administrator elevation prompt behavior</a><br><br>Windows 10 Security Baseline / <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Require admin approval mode for administrators</a> | More prompts may appear when modifying user account control (UAC) settings during the OOBE using the device Enrollment Status Page (ESP). Increased prompts are more likely if the device reboots after policies are applied. To work around this issue, the policies can be targeted to users instead of devices so that they apply later in the process. |
| Device restrictions / Cloud and Storage / <a href="/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Microsoft Account sign-in assistant</a> | Setting this policy to "disabled" will disable the Microsoft Sign-in Assistant service (wlidsvc). This service is required by Windows Autopilot to obtain the Windows Autopilot profile. |
| Registry keys that affect Windows Autopilot for <a href="pre-provision.md">pre-provisioned deployment</a><br><br><b>Registry path</b>:<br>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Automatic logon | <b>Registry key</b>:<br>If the <a href="https://support.microsoft.com/help/324737/how-to-turn-on-automatic-logon-in-windows">AutoAdminLogon</a> registry key is set to 0 (disabled), this breaks Windows Autopilot pre-provisioning. |
| <a href="/windows/client-management/mdm/policy-csp-controlpolicyconflict">MDM wins over Group Policy</a> | This policy allows the IT admin to control which policy will be used when both the MDM policy and its equivalent Group Policy (GP) are set on the device. |
| Group Policy Objects (GPOs) that affect Windows Autopilot for <a href="pre-provision.md">pre-provisioned deployment</a><br><br><b>GPO path</b>: <br>Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options<br><br><b>Policies</b>:<br><a href="/windows/security/threat-protection/security-policy-settings/interactive-logon-message-title-for-users-attempting-to-log-on">Interactive logon: Message title for users attempting to log on</a><br><br><a href="/windows/security/threat-protection/security-policy-settings/interactive-logon-message-text-for-users-attempting-to-log-on">Interactive logon: Message text for users attempting to log on</a><br><br><a href="/windows/security/threat-protection/security-policy-settings/interactive-logon-require-smart-card">Interactive logon: Require Windows Hello for Business or smart card</a><br><br><a href="/windows/security/threat-protection/security-policy-settings/user-account-control-behavior-of-the-elevation-prompt-for-administrators-in-admin-approval-mode">User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode - Prompt for credentials on the secure desktop</a> | Windows Autopilot pre-provisioning does not work when any of the four GPO policy settings listed here are enabled. |

## Related topics

[Troubleshooting Windows Autopilot](troubleshooting.md)