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

After devices have successfully process a Microsoft Intune policy for Windows LAPS, you can view details about those devices from within the Microsoft Intune admin center. Reports that are specific to LAPS policy as well as standard details similar to those for other policies, can all be found in the Microsoft Intune admin center where you create policies to manage Windows LAPS:

In the Microsoft Intune admin center go to **Endpoint security** > **Account protection**, and select a policy for Windows LAPs. 

  :::image type="content" source="./media/windows-laps-reports/device-policy-1.png" alt-text="Screen shot of basic policy details for a Windows LAPS policy.":::

In addition to the standard policy details similar to other policy types, like how many devices have succeeded in processing a policy, have errors or conflicts, and so forth, you'll find the following two tiles that provide access to rep;orts for LAPS:  

- **Device assignment status** - A report that shows status for all the devices targeted by the policy.
- **Per setting status** - View the configuration status of this policy across all devices and users.
 
## Device assignment status

## Per setting status


## Events and Audit logs

Audit events are logged to your Azure Active Directory (Azure AD) each time an account password is rotated either by policy or manually. An event is also logged when a password is viewed for an account.

For information about Azure AD event logs, see [Audit logs in Azure Active Directory](/azure/active-directory/reports-monitoring/concept-audit-logs).

## Next steps

- [Introduction to Intune policy for LAPS](../protect/windows-laps-overview.md)
- [View reports for LAPS](../protect/windows-laps-reports.md)
- [Account protection policy for endpoint security in Intune](../protect/endpoint-security-account-protection-policy.md)