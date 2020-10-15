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
author: mtniehaus
ms.author: mniehaus
ms.collection: M365-modern-desktop
ms.topic: article
---


# Windows Autopilot - Policy Conflicts

**Applies to**

- Windows 10

There are a significant number of policy settings available for Windows 10, including:
- Native MDM policies
- Group policy (ADMX-backed) settings

Some policy settings can cause issues in some Windows Autopilot scenarios. These issues can arise because of how the policies change Windows 10 behavior. If you find any of these issues, remove the policy in question to resolve the issue.

<table>
<th>Policy<th>More information

<tr><td width="50%">Device restriction / <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">Password Policy</a></td>
<td>The out-of-box experience (OOBE) or user desktop autologon can fail when a device reboots during the device Enrollment Status Page (ESP). This failure can occur when certain <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">DeviceLock policies</a> are applied to a device. Such policies can include:<ul><li>Minimum password length and password complexity</li><li>Any similar group policy settings (including any that disable autologon)</li></ul>
This possible failure is especially true for kiosk scenarios where passwords are automatically generated.</td>

<tr><td width="50%">Windows 10 Security Baseline / <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Administrator elevation prompt behavior</a>
<br>Windows 10 Security Baseline / <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Require admin approval mode for administrators</a></td>
<td>More prompts may appear when modifying user account control (UAC) settings during the OOBE using the device Enrollment Status Page (ESP). Increased prompts are more likely if the device reboots after policies are applied. To work around this issue, the policies can be targeted to users instead of devices so that they apply later in the process.</td>

<tr><td width="50%">Device restrictions / Cloud and Storage / <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Microsoft Account sign-in assistant</a></td>
<td>Setting this policy to "disabled" will disable the Microsoft Sign-in Assistant service (wlidsvc). This service is required by Windows Autopilot to obtain the Windows Autopilot profile.</td>

<tr><td width="50%">Group Policy Objects (GPOs) and registry keys that affect Windows Autopilot for pre-provisioned deployment.
<td>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\<a href="https://support.microsoft.com/help/324737/how-to-turn-on-automatic-logon-in-windows">Automatic logon</a>
<br>&nbsp;
<br>If the AutoAdminLogon registry key is set to 0 (disabled), this breaks Windows Autopilot pre-provisioning.<hr size="2"><br>
Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options
<br>&nbsp;
<br><a href="https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/interactive-logon-message-text-for-users-attempting-to-log-on">Interactive logon: Message text for users attempting to log on</a>
<br>&nbsp;

<a href="https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/interactive-logon-require-smart-card">Interactive logon: Require Windows Hello for Business or smart card</a>
<br>&nbsp;

<a href="https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/user-account-control-behavior-of-the-elevation-prompt-for-administrators-in-admin-approval-mode">User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode - Prompt for credentials on the secure desktop</a>
<br>&nbsp;
<br>Windows Autopilot pre-provisioning does not work when any of these GPO settings are enabled




</td></tr>

</table>

## Related topics

[Troubleshooting Windows Autopilot](troubleshooting.md)
