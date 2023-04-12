---
title: View reports for Windows LAPS policies in Microsoft Intune
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

After devices have successfully processed a Microsoft Intune policy for Windows LAPS, you can view details about those devices from within the Microsoft Intune admin center.

For each of your LAPS policies, you can select the policy to view standard policy details like how many devices have succeeded in processing a policy, have errors or conflicts, and so forth. In the Microsoft Intune admin center go to **Endpoint security** > **Account protection**, and select a policy for Windows LAPs. 

:::image type="content" source="./media/windows-laps-reports/device-policy-1.png" alt-text="Screen shot of basic policy details for a Windows LAPS policy.":::

In addition to the standard policy details, there are dedicated reports for Windows LAPS policy that are available after you select a specific LAPS policy:

- **Device assignment status** - A report that shows status for all the devices targeted by the policy.
- **Per setting status** - View the configuration status of this policy across all devices and users.

## Device assignment status

## Per setting status


## Events and Audit logs

When you use Intune policies to manage Windows LAPS, the following events are audited and logged in Azure Active Directory (Azure AD):

- Automatic password rotation managed by policy
- Manual password rotation through a device action.
- Requests to view the password for an account.

For information about Azure AD event logs, see [Audit logs in Azure Active Directory](/azure/active-directory/reports-monitoring/concept-audit-logs).

## Next steps

- [Introduction to Intune policy for LAPS](../protect/windows-laps-overview.md)
- [View reports for LAPS](../protect/windows-laps-reports.md)
- [Account protection policy for endpoint security in Intune](../protect/endpoint-security-account-protection-policy.md)