---
# required metadata
title: Requirements for NXT
titleSuffix:
description: Learn about the requirements of NXT
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Requirements for NXT deployment

[!INCLUDE [MS confidential, draft docs](../includes/draft-doc.md)]

The following lists the requirements to deploy and manage NXT devices using Intune.

## Licensing

NXT is a Windows 365 product and shares the same license requirements. For more information, see [??]().

## Microsoft Entra ID requirements

NXT devices must be [Microsoft Entra joined](/entra/identity/devices/concept-directory-join).

The user who joins the device to Microsoft Entra ID must have permissions to join devices to Microsoft Entra ID.

NXT devices can be used to connect to Cloud PCs that are either Entra joined or Entra hybrid joined.

NXT devices use automatic [mobile device management](/windows/client-management/mdm-overview) (MDM) enrollment to enroll in Intune for manaagment by the organization. To use this feature, the user who Entra joins the device must have a Microsoft Entra ID Premium license.

For more information, see []().

## Microsoft Intune requirements

 NXT devices enroll for management with Intune during the Out of Box experience. The user performing enrollment must have permission to enroll the devices and comply with any defined Enrollment restrictions.

Optionally, NXT devices can be used with the Intune corporate identifier enrollment feature to pre-upload the serial number, manufacturer, model to ensure only trusted devices go through enrollment.

For more information, see []().

## Windows 365 requirements

 NXT devices can only be used to connect to Windows 365 Cloud PCs that have Entra ID single sign-on (SSO) enabled. If SSO is not enabled on the Cloud PC, the user:

- Gets an error that their Cloud PC doesn't support Entra ID single sign-on
- Can't connect to their Cloud PC.

To [configure SSO](../enterprise/configure-single-sign-on.md), use either of the following options:

- Edit an existing provisioning Policy to enable SSO, then apply the change to all Cloud PCs that are associated with the policy.
- Provision new Cloud PCs using a provisioning profile with SSO enabled.

After SSO is enabled, NXT devices can be used to connect to those Cloud PCs. For more information, see [Configure single sign-on for Windows 365 using Microsoft Entra authentication](../enterprise/configure-single-sign-on.md).

### Conditional access

If you're using Conditional Access to protect access to Cloud PC, make sure to include the SSO service principal in the resources of those Conditional Access policies.

Also consider suppressing the SSO Consent Prompt by configuring the SSO on service principals. (see how-to configure environment for guidance)

## Microsoft Teams requirements

 ??NXT devices can only use the VDI solution for Teams for media optimizations??. These optimizations are pre-installed as part of the NXT's operating system. Check the Microsoft Teams PowerShell policy for optimization to ensure that the users signing in to NXT devices are in scope for the new VDI policy.

## Network Requirements

 NXT devices have the same network requirements as [Azure Virtual Desktop end user devices](/azure/virtual-desktop/required-fqdn-endpoint?tabs=azure#end-user-devices).

<!-- ########################## -->
## Next steps

[Join NXT devices to Microsoft Entra ID](join-microsoft-entra.md).