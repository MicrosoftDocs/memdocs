---
# required metadata

title: Licenses available for Microsoft Intune
description: Intune is available with these licenses
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 4/14/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 4a94440c-11cb-11e8-b642-0ed5f89f718b



# optional metadata

#ROBOTS:
#audience:
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Microsoft Intune licensing
Microsoft Intune is available for different customer needs and organization sizes, from a simple-to-use management experience for schools and small businesses, to more advanced functionality required by enterprise customers. Most licenses that include Microsoft Intune also grant the rights to use Microsoft Endpoint Configuration Manager, as long as the subscription remains active. An admin must have a license assigned to them to administer Intune (unless you [allow unlicensed admins](unlicensed-admins.md)).

## Microsoft Intune

Intune is included in the following licenses:

- Microsoft 365 E5
- Microsoft 365 E3
- Enterprise Mobility + Security E5
- Enterprise Mobility + Security E3
- Microsoft 365 Business Premium
- Microsoft 365 F1
- Microsoft 365 F3
- Microsoft 365 Government G5
- Microsoft 365 Government G3
- Intune for Education

## Microsoft Intune for Education

Intune for Education is included in the following licenses:

- Microsoft 365 Education A5
- Microsoft 365 Education A3

## Licensing for Configuration Manager-managed devices in Intune

For existing Configuration Manager-managed devices to enroll into Intune for co-management at scale without user interaction, co-management uses an Azure Active Directory (Azure AD) feature called Windows 10 auto-enrollment. Auto-enrollment with co-management requires licenses for both Azure AD Premium (AADP1) and Intune. Starting on December 1, 2019, you no longer need to assign individual Intune licenses for this scenario. Microsoft Endpoint Manager now includes the Intune licenses for co-management. The separate AADP1 licensing requirement remains the same for this scenario to work. You still need to assign Intune licenses for other enrollment scenarios.

## Additional information

- A Microsoft Intune user and device subscription is available as a standalone, in addition to the bundles listed above.
- A Microsoft Intune device-only subscription is available to manage kiosks, dedicated devices, phone-room devices, IoT, and other single-use devices that don't require user-based security and management features. For more information, see [Introduction to device licenses in Microsoft Intune](/troubleshoot/mem/intune/device-licenses-introduction).
- The appropriate Microsoft Intune license is required if a user or device benefits directly or indirectly from the Microsoft Intune service, including access to the Microsoft Intune service through a [Microsoft API](/legal/microsoft-apis/terms-of-use).
- Intune isn't included in licenses not in the previous tables.

## Unlicensed admins

For more information about giving administrators access to Microsoft Endpoint Manager without them having an Intune license, see [Unlicensed admins](unlicensed-admins.md).

Visit the [Microsoft Licensing](https://www.microsoft.com/licensing/default) page for the latest information about product editions, product licensing updates, volume licensing plans, and other information related to your specific use cases.  

For information about how user and device licenses affect access to services, as well as how to assign a license to a user, see the [Assign Intune licenses to your user accounts article](licenses-assign.md).
