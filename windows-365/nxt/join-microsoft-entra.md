---
# required metadata
title: Join NXT to Microsoft Entra
titleSuffix:
description: Learn about the joining NXT to Microsoft Entra
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

# Join NXT to Microsoft Entra

[!INCLUDE [MS confidential, draft docs](../includes/draft-doc.md)]

NXT devices must be Entra joined. The first time the device is powered on, the Out of Box Experience (OOBE) will prompt a user to sign in and will then join the device to their tenant. This user must have permission to join and not be blocked by any Intune device enrollment restrictions.

Allowing users to join devices to Microsoft Entra ID can be configured in the Entra portal:

1. Sign in to the Microsoft Entra admin center and expand the **Identity** section.
2. Go to **Devices** / **Overview** and select **Device Settings**.
3. In the **Devices** | **Device settings** screen, under **Users may join devices to Microsoft Entra**, choose either **All** or **Selected**:
  - If **All** is chosen, all users can join their devices to Microsoft Entra ID.
  -If **Selected** is chosen, only the those specified under **Selected** can join devices to Microsoft Entra ID. Any selected groups must be a Microsoft Entra group that contains user objects.
4. In the **Devices** | **Overview** screen, if any changes were made, select **Save**.

Also in the **Devices** | **Device settings** screen, confirm the **Maximum number of devices per user** is set to a reasonable value that will not prevent users from joining new devices. The default maximum is 50 and applies to all users, including device enrollment managers. See the Configure device settings documentation for more information.

<!-- ########################## -->
## Next steps

[Enable automatic enrollment](intune-automatic-enrollment.md).