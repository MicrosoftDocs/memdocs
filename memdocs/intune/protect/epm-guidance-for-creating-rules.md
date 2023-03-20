---
title: Guidance for creating elevation rules with Endpoint Privilege Management
description: View guidance on how to create strong rules with Endpoint Privilege Management
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

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
---

# Guidance for creating elevation rules with Endpoint Privilege Management

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->

> [!NOTE]  
> This capability is in public preview and available to use without a license. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

## Overview

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges.

Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

## Defining rules for use with Endpoint Privilege Management

Endpoint Privilege Management rules consist of two fundamental element: a *detection* and an *elevation action*.

**Detections** are classified as the set of attributes that are used to identify an application or binary. Detections are comprised of attributes such as file name, file version, or attributes of a signature.

**Elevation actions** are the resulting elevation that occurs after an application or binary has been detected. Included in the elevation action.

It's important when defining *detections* that they're defined to be as *descriptive* as possible. To be descriptive, use strong attributes, or multiple attributes to increase the strength of the detection. The goal when defining detections should be to eliminate the ability for multiple files to fall into the same rule (unless that is explicitly the intent).

### File hash rules

File hash rules are the strongest rules that can be created with Endpoint Privilege Management. These rules are *highly recommended* to ensure the file you intend to elevate is the file that is elevated.

File hash can be gathered from the direct binary using the [Get-Filehash PowerShell method](/powershell/module/microsoft.powershell.utility/get-filehash) or directly from the [reports for Endpoint Privilege Management](../protect/epm-reports.md).

### Certificate rules

Certificate rules are a strong type of attribute and should be paired with additional attributes. Pairing a certificate with attributes like product name, internal name, description drastically improves the security of the rule. These attributes are protected by signature, and often indicate specifics about the signed file.

> [!CAUTION]
> Using just a certificate and a file name provides very limited protection for misuse of a rule. File names can be changed by any *standard user* provided they have access to the directory where the file resides. This might not be a concern for files that reside in a write-protected directory.

### Rules containing file name

File name is an attribute that can be utilized to detect an application that needs to be elevated. However, file names aren't protected by the signature of the file.

This means that file names are *highly susceptible* to change. Files that are signed by a certificate that you trust could have their name changed to be *detected* and subsequently *elevated*, which might not be your intended behavior.

> [!IMPORTANT]
> Always ensure that rules including a file name include other attributes that provide a strong assertion to the file's identity. Attributes like file hash or properties that are included in the files signature are good indicators that the file you intend is likely the one being elevated.

## Deploying rules created with Endpoint Privilege Management

Endpoint Privilege Management rules are deployed like any other policy in Microsoft Intune. This means that rules can be deployed to users or devices, and rules are merged on the client side and selected at run time. Any conflicts are resolved based on the [policy conflict behavior](../protect/epm-policies.md#policy-conflict-handling-for-endpoint-privilege-management).

Rules deployed to a device are applied to *all users* on that device. Rules that are deployed to a *user* apply only to that user on devices they utilize. When an elevation action occurs, rules deployed to the user are given precedence to rules deployed to a device. This allows you to deploy a set of rules to devices that might apply to all users on that device, but a more permissive set of rules to a support admin that allows them the ability to elevate a broader set of applications when they're logged in on the device temporarily.

*Default Elevation behavior* is used only when no rule match can be found. This also requires use of the *Run with elevated access* right-click menu, which is interpreted as a user *explicitly* asking for an application to be elevated.

## Endpoint Privilege Management and User Account Control

Endpoint Privilege Management and Windows built-in user account control (UAC) are separate products with separate functionality. 

When moving to standard user and utilizing Endpoint Privilege Management, you might choose to change the default UAC behavior for standard users. This change can reduce confusion when an application requires elevation and create a better end user experience. Examine [behavior of the elevation prompt for standard users](/windows/security/identity-protection/user-account-control/user-account-control-security-policy-settings#user-account-control-behavior-of-the-elevation-prompt-for-standard-users) for more information.

> [!NOTE]
> Endpoint Privilege Management will not interfere with user account control actions (or UAC) being run by an Administrator on the device. It is possible to create rules that apply to Administrators on the device, so special considerations should be given to rules that are applied to all users on a device and the impact on users with Administrator.

## Next steps

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-policies.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
