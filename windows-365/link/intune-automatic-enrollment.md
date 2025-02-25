---
# required metadata
title: Automatically enroll Windows 365 Link in Intune
titleSuffix:
description: Learn about automatically enrolling Windows 365 Link in Intune
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365-link
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

# Automatically enroll Windows 365 Link in Intune

As the second step to [set up your organization's environment to support Windows 365 Link](deployment-overview.md), you must make sure they can be managed by Microsoft Intune.

After a Windows 365 Link device is [joined to Entra ID](join-microsoft-entra.md), it can be managed with Intune if automatic enrollment is enabled by setting **MDM user scope**. The user must also have the appropriate Microsoft Entra Premium license. Without setting **MDM user scope**, automatic enrollment doesn't occur and Windows 365 Link devices can't be managed by, and don't appear in, Intune.

To set up automatic enrollment in Intune for Windows 365 Link devices:

1. Sign in to the [Microsoft Entra admin center](https://aad.portal.azure.com/) > **Show more** > **Settings** > **Mobility**.
2. On the **Mobility (MDM and WIP)** page, select **Microsoft Intune**.
3. On the **Microsoft Intune** page, under **MDM user scope**, select either **All** or **Some**.

   - **All**: All users can automatically enroll their devices in Intune.
   - **Some**: Only users in the groups specified in the link under **Groups** can automatically enroll their devices in Intune. Make sure the groups selected are Microsoft Entra user groups that contain the desired users.

4. If there's more than one application listed on the **Mobility (MDM and WIP)** page, confirm that one of the following is true:

    - Only **Microsoft Intune** has **MDM user scope** set to **All** and each of the other applications are set to **None**. Or,
    - Only **Microsoft Intune** has **MDM user scope** set to **Some** and each of the other applications are set to **None**. Or,
    - If **Microsoft Intune** has **MDM user scope** set to **Some**, none of the other applications are set to **All**. If any of the other applications are set to **Some**, then no users belong to more than one of the selected groups.

5. Select **Save**.
6. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >**Tenant administration** > **Tenant status** > **Tenant details**.
7. Confirm that **MDM authority** is set to *Microsoft Intune*.

<!-- ########################## -->
## Next steps

[Create an Intune filter for Windows 365 Link devices](create-intune-filter.md).
