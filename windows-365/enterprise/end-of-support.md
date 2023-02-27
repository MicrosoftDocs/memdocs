---
# required metadata
title: End of support for Windows operating system on Cloud PCs
titleSuffix:
description: Learn about lifecycle policies and end of support for operating systems on Cloud PCs and device images.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/30/2021
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: naramkri
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Lifecycle policies and end of support for Cloud PC operating systems

Lifecycle policies govern operating system (OS) servicing and support (including end of support). The lifecycle is the time period during which Microsoft supports the OS and releases monthly security updates for it. For more information about lifecycles, see [Lifecycle FAQ - General](/lifecycle/faq/general-lifecycle) and [Lifecycle FAQ - Windows](/lifecycle/faq/windows).

A Windows 365 Cloud PC runs on the Windows OS and follows the [Microsoft Lifecycle Policy](/lifecycle). After the OS on a Cloud PC reaches the end of support, it stops receiving:

- Security updates
- Non-security updates
- Assisted support

## Image status

Windows 365 tracks end of support information in Microsoft Endpoint Manager on the **Provisioning policies** page under **Image status**. This column lets you know if the OS on the image used by each provisioning policy is supported or not.

| Image status | Gallery image | Custom image |
| --- |--- | --- |
| Supported | Cloud PCs created using this policy have a Windows OS that is supported by Microsoft and can receive updates. | Same as gallery image. |
| Warning | OS Support expired less than six months ago. Cloud PCs created using this policy have an OS that isn’t supported. Such Cloud PCs are vulnerable and not receiving security updates. | Cloud PCs created using this policy have an OS that isn’t supported. Such Cloud PCs are vulnerable and not receiving security updates.  |
| Unsupported | Cloud PCs created using this policy have a Windows OS that hasn’t been supported for over six months. This policy can no longer be assigned to users. To resolve this issue, update the OS image in the provisioning policy to an image with a supported OS. Existing Cloud PCs previously created with this policy:<br>- Are vulnerable and not receiving security updates.<br>- Can’t be provisioned or reprovisioned. Attempts to provision a Cloud PC from this policy will fail with a **Windows Image out of Support** message. | Not applicable |

These status values for custom images also appear under the **OS support status** column on the **Device images** page.

## Provisioning policies

Starting on the end of support date, gallery images that use the expired OS won’t be selectable for newly created provisioning policies. The images also won’t be available for use when editing existing provisioning policies.

<!-- ########################## -->
## Next steps

To change the device image for a provisioning policy, see [Edit provisioning policies](edit-provisioning-policy.md).
