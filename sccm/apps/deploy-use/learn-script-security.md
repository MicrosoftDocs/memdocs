---
title: "Learn more about PowerShell script security"
titleSuffix: "System Center Configuration Manager"
description: "Resources to help learn about PowerShell script security."
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby

---

# Learn more about PowerShell script security

*Applies to: System Center Configuration Manager (Current Branch)*

It is the administrator’s responsibility to validate proposed PowerShell and PowerShell parameter usage in their environment. Here are some helpful resources to help educate administrators about the power of PowerShell and potential risk surfaces. This is to help mitigate potential risk surfaces and allow safe scripts to be used.

## PowerShell Script Security
Built into the Run Scripts is a feature to visually review and approve scripts that are requested to be run in the environment. Administrators should be aware PowerShell scripts can have obfuscated script: script that is malicious and difficult to detect with visual inspection during the script approval process. As a best practice, using certain inspection tools, in additional to visually reviewing PowerShell scripts, will help detect suspicious scripts issues. These tools can’t always determine the PowerShell author's intent so it can bring attention to a suspicious script. However, the tools will require the administrator to judge if it is malicious or intentional script syntax.

## Recommendations
- Familiarize yourself with PowerShell security best practices using the various links referenced below.
- **Sign your scripts**: Another method for keeping scripts Secure is by having them vetted and then signed, before importing them for usage.
- Don’t store secrets (such as passwords) in PowerShell scripts and learn more about how to handle secrets.


## General information about PowerShell security best practices

This collection of links was chosen to give Configuration Manager administrators a starting point for learning about PowerShell script security best practices.  

[Introduction to PowerShell Security Best Practices](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell Security Best Practices PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Defending Against PowerShell Attacks, PowerShell team blog](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Defending Against PowerShell Attacks twitter, from a Microsoft PowerShell and Security advocate Lee Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Protecting Against Malicious Code Injection](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[Information about security from the PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2015/08/06/powershell-gallery-new-security-scan/)

[PowerShell The Blue Team, discusses Deep Script block logging, Protected Event Logging , Antimalware Scan Interface, Secure Code Generation APIs](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[For Windows 10, there is an API for an anti-malware scan interface](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## PowerShell parameters security
Passing parameters is a way to have flexibility with your scripts and defer decisions until run time. It also opens up another risk surface. 
Best practices for preventing malicious parameters or script injection are:

- Only allow usage of pre-defined parameters.
- Use the regular expression feature, to validate parameters that are allowed.
    - Example: If only a certain range of values are allowed, use a regular expression to check for only those characters or values that can make up the range.
    - Validating parameters can help prevent users trying use certain characters that can be escaped, like quotes. Be aware that there can be multiple types of quotes, so using regular expressions to validate which characters you’ve decided are permissible is often easier than trying to define all the inputs that not permissible.
- Leverage the PowerShell module ["injection hunter"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) in the PowerShell Gallery.
    - There can be false positives, so look for intent when something is flagged as suspicious to determine if it is a real issue or not. 
- Microsoft Visual Studio has a Script analyzer, that can assist with checking PowerShell syntax.
- This video titled: “DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server” gives an overview of the types of issues that you can secure against (especially the section 12:20 to 17:50):
      <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Environment Recommendations
General recommendations for PowerShell administrators.
1. Deploy latest version of PowerShell, such as version 5 or greater, built into Windows 10. Alternatively, you can deploy the [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616), available down to, and including Windows 7 and Windows Server 2008 R2. 
2. Enable, and collect PowerShell logs, optionally including Protected Event Logging. Incorporate these logs into your signatures, hunting, and incident response workflows.
3. Implement Just Enough Administration on high-value systems to eliminate or reduce unconstrained administrative access to those systems.
4. Deploy Device Guard/Application Control policies to allow pre-approved administrative tasks to use the full capability of the PowerShell language, while limiting interactive and unapproved use to a limited subset of the PowerShell language.
5. Deploy Windows 10 to give your antivirus provider full access to all content (including content generated or de-obfuscated at runtime) processed by Windows Scripting Hosts including PowerShell.