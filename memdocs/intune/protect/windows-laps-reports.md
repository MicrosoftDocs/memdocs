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

After devices are assigned Microsoft Intune policy for Windows LAPS, you can view policy details from within the Microsoft Intune admin center. Reports for LAPS include details about the devices and users that have been assigned policies, which settings from those policies  have been set successfully, have errors or conflicts, and which devices are pending the submission of device status for assigned policy.

Reports for Windows LAPS policies are found in the Endpoint security node for Account protection policies. The Reports node of the Intune admin center doesn't have dedicated reports for Windows LAPS.

## View and use the LAPS Report

You can use the LAPS report to view the configuration and assignments for a LAPS policy, and to drill in and identify the source of conflicts that prevent devices from applying your policies.

To use the report, sign into the Intune admin center and navigate to the Account protection policy node. (**Endpoint security** > **Account protection**). Here you can view a list of all Account protection policies, including the policies for LAPS that use the *Local admin password solution (Windows LAPS) (preview)* profile. You can identify the profile by the *Policy type* column:

:::image type="content" source="./media/windows-laps-reports/laps-policy-list.png" alt-text="Screen shot of the policy list for Account protection policies." lightbox="./media/windows-laps-reports/laps-policy-list.png":::

When you select any row from the list of policies, Intune displays details for that policy that include:

- A summarization of the *Device and user check-in status* that displays the count of devices that the policy targets and that have succeeded in reporting status, have errors, and so forth.

- A link labeled **View report** that opens a detailed report for each device or user that’s been assigned the policy.  This report can help you understand the policy configuration and identify the source of conflicts that might prevent the policy from applying to a device.  

- Each policy includes tiles you can use to investigate specific aspects of the LAPS report:

  - **Device assignment status** - This tile opens a customized report you can use to review details for a subset of assignment status, like devices with Success, Conflict, or devices that are Pending and haven’t yet reported their status.

    To use this report option, select one or more *Assignment status* options and then select **Generate again** to run the report for current details.

    The results you see are a subset of the results that are available from the *View report* option. This custom view includes support to drill in to device details to view more information about the selected assignment status that was selected for this report.  

  - **Per setting status** - A report that lists each setting in policy, and the count of devices that have Success in applying the setting, have an Error, or a Conflict. This report view doesn’t support drilling in for more detail.  

In the following image, we’ve selected the policy named *LAPSSHTest*. We use this policy as we examine what you can learn by using the **View report** button to drill in for more information:

:::image type="content" source="./media/windows-laps-reports/check-in-status.png" alt-text="Screen shot of the Device and user check-in status view for a Windows LAPS policy." lightbox="./media/windows-laps-reports/"check-in-status.png:::

While viewing the details for a policy, select the **View report** button to view a list that identifies each device that has been assigned the policy. The device list includes the following information:

- Device name - Devices that have been assigned this policy.

- Logged in user – Identifies the name of the user logged into the device at the time the policy last reported status.

- Check-in status - The policy status for the device. In the following example, the device shows a status of *Conflict*. Conflicts indicate that one or more other policies that are assigned to this device uses a different configuration for a setting.
- Filter

- Last report modification time – When the policy was last updated.

In the following image, we see that our example policy is assigned to a single device. The view also shows that there's a conflict for the devices *Check-in status*:

:::image type="content" source="./media/windows-laps-reports/check-in-status.png" alt-text="Screen shot of the list of devices that are assigned a Windows LAPS policy." lightbox="./media/windows-laps-reports/check-in-status.png":::

When you select the name of a device from the *Device name* column Intune displays details about the settings assigned to that device. IN the following image, we see that the device we selected has two assigned settings. Of the twos settings, *Password Age Days* is identified as being in conflict per the Setting status column. When you select a setting from the setting name column, Intune opens the *Settings Details* pane where you can view details about that setting.

In the following image, we’ve selected *Password Age Days* so we can learn more about its conflict:

:::image type="content" source="./media/windows-laps-reports/check-in-status.png" alt-text="Screen shot of settings from a LAPS policy, with the Settings Details pane." lightbox="./media/windows-laps-reports/check-in-status.png":::

The Settings Details pane shows us that the selected setting, *Password Age Days*,  is configured through two profiles, one named *LAPSSHTest* (the profile we have been viewing), and the other named *Lapsshtestapril*.

With the *source profiles* that are in conflict now identified by name, you can go back to the list of policies to  view the *Password Age Days*,  setting from each, and resolve the conflict.

## Events and Audit logs

When you use Intune policies to manage Windows LAPS, the following events are audited and logged in Azure Active Directory (Azure AD):

- Automatic password rotation managed by policy
- Manual password rotation through a device action.
- Requests to view the password for an account.

For information about Azure AD event logs, see [Audit logs in Azure Active Directory](/azure/active-directory/reports-monitoring/concept-audit-logs).

## Next steps

- [Introduction to Intune policy for LAPS](../protect/windows-laps-overview.md)
- [Create policy for LAPS](../protect/windows-laps-policy.md)
- [Account protection policy for endpoint security in Intune](../protect/endpoint-security-account-protection-policy.md)