---
# required metadata
title: Automatically enroll NXT in Intune
titleSuffix:
description: Learn about automatically enrolling NXT in Intune
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

# Automatically enroll NXT in Intune

[!INCLUDE [MS confidential, draft docs](../includes/draft-doc.md)]

After a NXT device is joined to Entra ID, it can be managed with Intune if Automatic Enrollment is enabled and the user has the appropriate Entra Premium license. Without Automatic Enrollment, NXT devices may be joined to Entra but would be unmanaged and will not appear in Intune. Enabling automatic enrollment in Intune Management can be configured in then Entra portal: 

1. Sign in to the Microsoft Entra admin center and expand the Identity section.
2. Go to Show more / Settings / Mobility and under Name select Microsoft Intune.
3. In the Microsoft Intune page that opens, under MDM user scope, select either All or Some: 
 - If All is selected, all users can automatically enroll their devices in Intune. 
 - If Some is selected, only users in the groups specified in the link under Groups can automatically enroll their devices in Intune. Make sure the groups selected are Microsoft Entra user groups that contain the desired users.
4. In the Microsoft Intune screen, if any changes were made, select Save.

NOTE: In Mobility (MDM and WIP) list, if there is more than one application, then the users who will be enrolling Windham devices must be in the MDM User scope of Microsoft Intune only. Confirm one of the following is true in your tenant:

1. Only Microsoft Intune has the MDM user scope set to All and each of the other applications are set to None. Or,
2. That Microsoft Intune has the MDM user scope set to Some and the each of the other applications are set to None. Or,
3. If Microsoft Intune has the MDM user scope set to Some, none of the other applications are set to All. If any of the other applications are set to Some, then no users belong to more than one of the selected groups.

Confirm that Microsoft Intune is configured as the MDM Authority in the tenant.

1. Sign in to the Microsoft Intune admin center.
2. Go to Tenant administration / Tenant status.
3. Under the Tenant details tab, confirm that “MDM authority” is set to “Microsoft Intune”.

<!-- ########################## -->
## Next steps

TBS