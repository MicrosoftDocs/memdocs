---
title: View reports for Microsoft Intunes Windows LAPS policies
description: Use the Microsoft Intune admin center to view reports and details for Windows Local Administrator Policy Solution (LAPS)  policies.

keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/18/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Reports for LAPS policy in Intune

After your managed devices successfully process a Microsoft Intune policy for Windows LAPS, you can view details about those devices from within the Microsoft Intune admin center. The details that your Intune administrator account can view depends on the permissions it has been assigned. For information about the different permissions, see [Role based access controls for LAPS](../protect/windows-laps-overview.md#role-based-access-controls-for-laps).

Available information includes:

- **Policy details** - These are the standard details you can view for any Intune policies, that show details like how many devices have succeeded in processing a policy, have errors or conflicts, and so forth.  To view policy details, in the Microsoft Intune admin center go to **Endpoint security** > **Account protection**, and select a policy for Windows LAPS:

  :::image type="content" source="./media/windows-laps-reports/device-policy-1.png" alt-text="Screen shot of basic policy details for a Windows LAPS policy.":::

  While viewing a policy, you can select from two report tiles:
  - **Device assignment status** - A report that shows status for all the devices targeted by the policy.
  - **Per setting status** - View the configuration status of this policy across all devices and users.

***PENDING - functional details about reports, drill in, and details that are not universal to reports or need more explinatino to be provided to the admin.***

## Event Audit logs

***Pending - Information needed:***

- In which log on the device (?) do the Audit events appear?
- Where in the Intune admin center to audit events appear? (Is this Device action status when viewing a devices Overview page?)
- Which actions cause audit events (compile a central list here, even though we mention this action in various places)
- List of audit events/ID’s (Would this be of use)?


## Next steps

- [Introduction to Intune policy for LAPS](../protect/windows-laps-overview.md)
- [View reports for LAPS](../protect/windows-laps-reports.md)
- [Account protection policy for endpoint security in Intune](../protect/endpoint-security-account-protection-policy.md)