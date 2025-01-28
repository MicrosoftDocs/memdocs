---
title: Guidance for creating elevation rules with Endpoint Privilege Management
description: View guidance on how to create strong file elevation rules with Microsoft Intune Endpoint Privilege Management
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/28/2025
ms.topic: Concept
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mattcall
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Guidance for creating elevation rules with Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

## Overview

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

## Defining rules for use with Endpoint Privilege Management

Endpoint Privilege Management rules consist of two fundamental elements: a *detection* and an *elevation action*.

**Detections** are defined as the set of attributes used to identify an application or binary. These attributes include file name, file version, and signature properties.

**Elevation actions** are the resulting elevation that occurs after an application or binary is detected.

It's important when defining *detections* that they're defined to be as *descriptive* as possible. To be descriptive, use strong attributes, or multiple attributes to increase the strength of the detection. The goal when defining detections should be to eliminate the ability for multiple files to fall into the same rule, unless that is explicitly the intent.

### File hash rules

File hash rules are the strongest rules that can be created with Endpoint Privilege Management. These rules are *highly recommended* to ensure the file you intend to elevate is the file that is elevated.

File hash can be gathered from the direct binary using the [Get-Filehash PowerShell method](/powershell/module/microsoft.powershell.utility/get-filehash) or directly from the [reports for Endpoint Privilege Management](../protect/epm-reports.md).

### Certificate rules

Certificate rules are a strong type of attribute and should be paired with other attributes. Pairing a certificate with attributes like product name, internal name, and description, drastically improves the security of the rule. These attributes are protected by a files signature, and often indicate specifics about the signed file.

> [!CAUTION]
> Using just a certificate and a file name provides very limited protection for misuse of a rule. Any *standard user* with access to a directory where the file resides can change the file name. This issue might not be a concern for files that reside in a write-protected directory.

### Rules containing file name

File name is an attribute that can be utilized to detect an application that needs to be elevated. However, file names aren't protected by the signature of the file.

This means that file names are *highly susceptible* to change. Files that are signed by a certificate that you trust could have their name changed to be *detected* and subsequently *elevated*, which might not be your intended behavior.

> [!IMPORTANT]
> Always ensure that rules including a file name include other attributes that provide a strong assertion to the file's identity. Attributes like file hash or properties that are included in the files signature are good indicators that the file you intend is likely the one being elevated.

### Rules based on attributes gathered by PowerShell

To help you build more accurate file detection rules, you can use the **Get-FileAttributes** PowerShell cmdlet. Available from the EpmTools PowerShell module, *Get-FileAttributes* can retrieve file attributes and the certificate chain material for a file and you can use the output to populate elevation rule properties for a particular application.

Example module import steps and output from Get-FileAttributes run against msinfo32.exe on Windows 11 version 10.0.22621.2506:

```powershell
PS C:\Windows\system32> Import-Module 'C:\Program Files\Microsoft EPM Agent\EpmTools\EpmCmdlets.dll'
PS C:\Windows\system32> Get-FileAttributes -FilePath C:\Windows\System32\msinfo32.exe -CertOutputPath C:\CertsForMsInfo\

FileName      : msinfo32.exe
FilePath      : C:\Windows\System32
FileHash      : 18C8442887C36F7DB61E77013AAA5A1A6CDAF73D4648B2210F2D51D8B405191D
HashAlgorithm : Sha256
ProductName   : Microsoft® Windows® Operating System
InternalName  : msinfo.dll
Version       : 10.0.22621.2506
Description   : System Information
CompanyName   : Microsoft Corporation

```

> [!NOTE]
> The certificate chain for msinfo32.exe is output to the C:\CertsForMsInfo directory listed in the command example.

For more information, see [EpmTools PowerShell module](../protect/epm-overview.md#epmtools-powershell-module).

### Controlling child process behavior

Child process behavior allows you to control the context when a process elevated with EPM creates a child process. This behavior allows you to further restrict processes which normally would be automatically delegated the context of its parent process.

Windows automatically delegates the context of a parent to a child, so take special care in controlling the behavior for your allowed applications. Ensure you evaluate what is needed when you create elevation rules, and implement the principle of least privilege.

> [!NOTE]
>
> Changing the child process behavior might have compatibility issues with certain applications that expect the default Windows behavior. Make sure you thoroughly test applications when manipulating the child process behavior.

## Deploying rules created with Endpoint Privilege Management

Endpoint Privilege Management rules are deployed like any other policy in Microsoft Intune. This means that rules can be deployed to users or devices, and rules are merged on the client side and selected at run time. Any conflicts are resolved based on the [policy conflict behavior](../protect/epm-policies.md#policy-conflict-handling-for-endpoint-privilege-management).

Rules deployed to a device apply to *every user* that uses that device. Rules that are deployed to a *user* apply only to that user on each device that they utilize. When an elevation action occurs, rules deployed to the user are given precedence to rules deployed to a device. This behavior allows you to deploy a set of rules to devices that might apply to all users on that device, and a more permissive set of rules to a support admin to allow them to elevate a broader set of applications when they sign-in to the device temporarily.

*Default Elevation behavior* is used only when no rule match can be found. This also requires use of the *Run with elevated access* right-click menu, which is interpreted as a user *explicitly* asking for an application to be elevated.

## Endpoint Privilege Management and User Account Control

Endpoint Privilege Management and Windows built-in user account control (UAC) are separate products with separate functionality.

When moving users to run as standard users and utilizing Endpoint Privilege Management, you might choose to change the default UAC behavior for standard users. This change can reduce confusion when an application requires elevation and create a better end user experience. Examine [behavior of the elevation prompt for standard users](/windows/security/identity-protection/user-account-control/user-account-control-security-policy-settings#user-account-control-behavior-of-the-elevation-prompt-for-standard-users) for more information.

> [!NOTE]
> Endpoint Privilege Management doesn't interfere with user account control actions (or UAC) that's run by an Administrator on the device. It's possible to create rules that apply to Administrators on the device, so give special consideration to rules that are applied to all users on a device and the impact on users with Administrator rights.

## Related content

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
