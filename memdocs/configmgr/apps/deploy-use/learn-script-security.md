---
title: Learn more about PowerShell script security
titleSuffix: Configuration Manager
description: Resources to help learn about PowerShell script security.
ms.date: 10/01/2021
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: conceptual
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Learn more about PowerShell script security

*Applies to: Configuration Manager (current branch)*

It's the administrator's responsibility to validate proposed PowerShell and PowerShell parameter usage in their environment. Here are some helpful resources to help educate administrators about the power of PowerShell and potential risk surfaces. This guidance is to help you mitigate potential risk surfaces and allow safe scripts to be used.

## PowerShell Script Security

The Configuration Manager scripts feature lets you visually review and approve scripts. Another administrator can request that their script is allowed. Administrators should be aware PowerShell scripts can have obfuscated scripts. An obfuscated script could be malicious and difficult to detect with visual inspection during the script approval process. Visually review PowerShell scripts and use inspection tools to help detect suspicious script issues. These tools can't always determine the PowerShell author's intent, so it can bring attention to a suspicious script. However, the tools will require the administrator to judge if it's malicious or intentional script syntax.

## Recommendations

- Familiarize yourself with PowerShell security guidance using the various links referenced below.
- **Sign your scripts**: Another method for keeping scripts secure is by having them vetted and then signed, before importing them for usage.
- Don't store secrets (such as passwords) in PowerShell scripts and learn more about how to handle secrets.

## General information about PowerShell security

This collection of links was chosen to give Configuration Manager administrators a starting point for learning about PowerShell script security recommendations.

<!-- [PowerShell Security Best Practices](https://devblogs.microsoft.com/powershell/powershell-security-best-practices/)

> [!VIDEO https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player] -->

[Defending Against PowerShell Attacks](https://devblogs.microsoft.com/powershell/defending-against-powershell-attacks/)

[Protecting Against Malicious Code Injection](https://devblogs.microsoft.com/powershell/protecting-against-malicious-code-injection/)

[PowerShell - The Blue Team, discusses Deep Script block logging, Protected Event Logging, Antimalware Scan Interface, and Secure Code Generation APIs](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)

[API for anti-malware scan interface](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/)

## PowerShell parameters security

Passing parameters is a way to have flexibility with your scripts and defer decisions until run time. It also opens up another risk surface.

The following list includes recommendations to prevent malicious parameters or script injection:

- Only allow usage of pre-defined parameters.
- Use the regular expression feature, to validate parameters that are allowed.
  - Example: If only a certain range of values are allowed, use a regular expression to check for only those characters or values that can make up the range.
  - Validating parameters can help prevent users trying use certain characters that can be escaped, like quotes. There can be multiple types of quotes, so using regular expressions to validate which characters you've decided are permissible is often easier than trying to define all the inputs that not permissible.
- Use the PowerShell module ["injection hunter"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) in the PowerShell Gallery.
  - There can be false positives, so look for intent when something is flagged as suspicious to determine if it's a real issue or not.
- Microsoft Visual Studio has a script analyzer, that can assist with checking PowerShell syntax.

The following video titled: "DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server" gives an overview of the types of issues that you can secure against (especially the section 12:20 to 17:50):

> [!VIDEO https://www.youtube.com/embed/ahxMOAAani8]

## Environment recommendations

The following list includes general recommendations for PowerShell administrators:

- Deploy the latest version of PowerShell, such as version 5 or later, which is built into Windows 10 or later. You can also deploy the [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616).
- Enable, and collect PowerShell logs, optionally including Protected Event Logging. Incorporate these logs into your signatures, hunting, and incident response workflows.
- Implement Just Enough Administration on high-value systems to eliminate or reduce unconstrained administrative access to those systems.
- Deploy Windows Defender Application Control policies to allow pre-approved administrative tasks to use the full capability of the PowerShell language, while limiting interactive and unapproved use to a limited subset of the PowerShell language.
- Deploy Windows 10 or later to give your antivirus provider full access to all content (including content generated or de-obfuscated at runtime) processed by Windows Scripting Hosts including PowerShell.
