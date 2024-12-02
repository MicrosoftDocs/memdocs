---
# required metadata
title: Join Windows 365 Link to Microsoft Entra
titleSuffix:
description: Learn about joining Windows 365 Link to Microsoft Entra
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

# Join Windows 365 Link to Microsoft Entra

As the first step in setting up your organization's environment to support Windows 365 Link, you must allow Windows 365 Link devices to [join Microsoft Entra](/entra/identity/devices/concept-directory-join).

Prior to signing in, the user must have permission to join and not be blocked by any Intune device enrollment restrictions.

The first time the device is powered on, the Out of Box Experience (OOBE):

1. Prompts the user to sign in.
2. Joins the device to their tenant.

To set permissions to allow your organization's users to join their Windows 365 Link to Microsoft Entra, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://aad.portal.azure.com/) > **Identity** > **Devices** > **Overview** > **Device Settings**.
2. Under **Users may join devices to Microsoft Entra**, select either **All** or **Selected**:
  
    - **All**: All users can join their devices to Microsoft Entra ID.
    - **Selected**: Only users specified under **Selected** can join devices to Microsoft Entra ID. Selected groups must be a Microsoft Entra group that contains user objects.

3. Make sure that **Maximum number of devices per user** is set to a reasonable value that doesn't prevent users from joining new devices. The default maximum is 50 and applies to all users, including device enrollment managers.
4. Select **Save**.

For more about configuring device settings for Microsoft Entra ID, see [Configure your device settings](/entra/identity/devices/device-join-plan#configure-your-device-settings).

For full information about planning yoru join implementation, see [How to: Plan your Microsoft Entra join implementation](/entra/identity/devices/device-join-plan).

<!-- ########################## -->
## Next steps

[Enable automatic enrollment](intune-automatic-enrollment.md).