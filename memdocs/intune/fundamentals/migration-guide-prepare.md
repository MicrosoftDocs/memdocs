---
# required metadata

title: Prepare Intune for mobile device management
titleSuffix: Microsoft Intune
description: Evaluate your business and technical requirements before migrating to Microsoft Intune.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 58591442-6606-4f39-a06b-f17a1f25af25

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Phase 1: Prepare Microsoft Intune for mobile device management (MDM)

Before diving into the details of setting up Intune, let’s review the mobile device management requirements of your organization. It might be helpful to run reports of active users in your current MDM provider to identify the critical user groups. Then you can begin addressing the questions in the [Assess MDM requirements](migration-guide-prepare.md#assess-mdm-requirements) section.

## Assess MDM requirements

### What kinds of devices do you need to manage?

- Which [platforms](supported-devices-browsers.md) do you need to support?

- Are the devices you need to support corporate-owned or personal devices?

- What kind of connectivity do you use? Wi-Fi, cellular, VPN?

### What do your users need to do on managed devices?

- Do you need to provision apps to your end-users?

- Do you use custom line-of-business apps? Or do you only need public store apps?

- Do you need to provision email accounts?

### What kinds of users?

- How many users will use a single device?

- What terms of use do you need?

  - Make sure to involve your legal department early in this.
  - What localization is required?

- Are the users familiar with technology and IT in general?

### What is your device security policy?

- Do you need device-level encryption?

- What are your current device passcode/pin code lengths?

- Do you need to disable device features, or restrict certain device behaviors? You can control a variety of platform-specific settings with device configuration profiles, for example:
  - Disable camera
  - Lock to single-app mode<br/>

- What kinds of authentication must you support? If you need certificate-based authentication, what kinds of certificates must be provisioned?
  - Intune can provision certificates with resource access profiles for enrolled devices.
  - What kind of Public Key Infrastructure (PKI) infra do you need to support?
  <br></br>
- Do you need to support Virtual Private Network (VPN) at the device or app level?

  - Intune can provision VPN configurations for third-party VPN providers.
  <br/><br/>
- Can temporary exceptions be made for certain requirements to avoid downtime? Or must devices with access always comply with all security requirements?

## Next steps
Read these [case studies](https://customers.microsoft.com/story/mwh-global-now-part-of-stantec-secures-mobile-devices-with-intune) from different industry sectors to see how organizations assessed their requirements for mobile device management.

Review the [basic Intune setup](migration-guide-setup.md).
