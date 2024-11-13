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

NXT is a Windows 365 product and shares the same license requirements.

## Microsoft Entra ID requirements

NXT devices must be joined only to Microsoft Entra ID. The user who joins the device to Microsoft Entra ID must have permissions to join devices to Microsoft Entra ID. NXT devices can be used to connect to Cloud PCs that are either Entra joined or Entra hybrid joined.

NXT devices use Automatic MDM enrollment to become managed with Intune. To use this feature, the user who Entra joins the device must have a Microsoft Entra ID Premium license.

(see how-to guide for configuration guidance)

## Microsoft Intune Requirements

 NXT devices become managed with Intune during the Out of Box experience. The user performing enrollment must have permission to Enroll the devices and comply with any defined Enrollment restrictions.

Optionally,  NXT devices can be used with the Intune corporate identifier enrollment feature to pre-upload the serial number, manufacturer, model to ensure only trusted devices go through enrollment.

(see how-to guide for configuration guidance)

## Windows 365 Requirements

 NXT devices can only be used to connect to Windows 365 Cloud PCs that have Entra ID single sign-on (SSO) enabled. If SSO is not enabled on the Cloud PC, the user will see an error that their Cloud PC does not support Entra ID single sign-on and will be unable to connect.

There are a few options to enable SSO:

- Edit an existing Provisioning Policy to enable SSO, then apply the change to all Cloud PCs that are associated with the policy.
- Provision new Cloud PCs using a Provisioning Profile that has SSO Enabled

Once SSO is enabled,  NXT devices can be used to connect to those Cloud PCs. See the existing documentation for more information on enabling SSO for Windows 365.

NOTE: If Conditional Access is being used to protect access to Cloud PC, be sure to include the SSO Service Principal in the resources of those Conditional Access Policies. Also consider suppressing the SSO Consent Prompt by configuring the Single Sign-on Service Principals. (see how-to configure environment for guidance)

## Microsoft Teams requirements

 NXT devices can only leverage the new VDI solution for Teams for media optimizations. These optimizations are pre-installed as part of the operating system. Check the Microsoft Teams PowerShell policy for optimization to ensure that the users logging into  NXT devices are in scope for the new VDI policy.

## Network Requirements

 NXT shares the same network requirements as “End user device” already documented.

<!-- ########################## -->
## Next steps

[Join NXT devices to Microsoft Entra ID](join-microsoft-entra.md).