---
title: Common Education configuration overview
description: Learn about common configuration used by Education organizations in Intune.
#zone_pivot_groups: platforms-windows-ios
ms.date: 5/2/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Windows, Autopatch, Autopilot, Edge, Apple]
ms.service: microsoft-intune
ms.subservice: education
---

# Common Education configuration overview

Intune is a powerful tool that can help Education organizations manage their devices and data efficiently. However, configuring the right settings can be a time-consuming task, especially for those new to the platform. To help accelerate the process, we have assembled common configurations based on customer engagements into this reference document. These settings can help ensure the security and compliance of your devices and data, while maximizing the user experience for your students and staff. Whether you're setting up a new tenant or need a quick reference guide, this document is a valuable resource for any Education organization looking to optimize their use of Intune.

## Guiding Principles and Methodology

The recommended settings in this document are built from real-world customer configurations, reflecting how Education organizations are currently using Microsoft Intune to manage their Windows and iPadOS devices. The goal is to provide policies that prevent unintentional use, maintain consistency across devices, and ensure that devices are used solely for educational purposes. At the same time, these settings optimize the overall device experience for students.

Key areas of focus include:

- **Disabling AI capabilities**: Keep students focused by preventing distractions and the inappropriate use of OS AI features.
- **Update experience**: Ensure that devices are secure and up to date, while minimizing disruptions during class time.
- **Disabling changes to settings**: Maintain consistent device configurations and prevent tampering by locking critical settings.
- **Browsing experience**: Protect student privacy and data by ensuring a safe browsing environment, free from distractions and potential security risks.

These policies are commonly used but not mandatory. Schools can tailor their configurations based on their specific needs, and optional policies are provided for more situational use cases.

> [!CAUTION]
> Adding these settings to your existing Intune tenant and assigning them to devices could potentially cause conflicts with your existing Intune policies. For more information, see [Compliance and device configuration policies that conflict](/mem/intune-service/configuration/device-profile-troubleshoot#conflicts) and [Avoiding policy conflicts](manage-avoid-policy-conflicts.md).

## Intune policies for Windows in Education

### Configuration sections

- [Device restrictions](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-settings-catalog-device-restrictions)
- [Windows Update](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-windows-update)
- [Microsoft Edge](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-settings-catalog-edge)
- [Delivery Optimization](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-settings-catalog-delivery-optimization)

### Optional

- [Windows privacy](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-settings-catalog-windows-privacy)
- [Start menu customization](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-settings-catalog-start-menu)
- [OneDrive Known Folder Move](/mem/intune-service/industry/education/tutorial-school-deployment/common-config-settings-catalog-onedrive-knownfoldermove)

## Intune policies for iPads in Education

- [Device restrictions](common-config-ipads-device-restrictions.md)
- [Apple Intelligence](common-config-ipads-ai.md)
- [iPads with no user affinity](common-config-ipads-nouser.md)
- [Optional restrictions](common-config-ipads-optional.md)
