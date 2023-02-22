---
title: Troubleshoot Windows 365 Business Cloud PC setup issues
description: Troubleshoot issues in Windows 365 Business.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 09/29/2021
audience: Admin
ms.topic: article
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Troubleshoot Windows 365 Business Cloud PC setup issues

If your users get the “Setup failed” error, or if setup takes longer than 90 minutes after you assign them a license, use the steps in this article to resolve the issue.

> [!IMPORTANT]
> You must be a Global admin to do most of the tasks described in this article. If other admin roles can be used for a specific procedure, they are noted before the procedure. If you don’t have permission to log in to or access parts of the Azure portal, contact your IT admin. For more information about Azure rules, see [Azure AD built-in roles](/azure/active-directory/roles/permissions-reference). To learn more about the Azure portal, see [Azure portal overview](/azure/azure-portal/azure-portal-overview).


## Make sure MDM authority configuration is set up correctly

It’s possible that the setup failure is caused by the MDM authority configuration in your environment. If so, you have two paths to follow, depending on whether you plan to use Microsoft Intune to manage the Cloud PCs.

- If you use or plan to use Microsoft Intune for your Cloud PCs, follow the steps in [Path A: Make sure the Mobility (MDM and MAM) settings are correctly configured](#path-a-use-microsoft-intune-to-manage-your-cloud-pcs).
- If you don’t plan to use Microsoft Intune to manage your Cloud PCs, follow steps in [Path B: Turn off automatic MDM enrollment](#path-b-turn-off-automatic-mdm-enrollment-and-intune-enrollment-in-organization-settings).

### Path A. Use Microsoft Intune to manage your Cloud PCs

If you already use Microsoft Intune, or plan to use it to manage your Windows 365 Cloud PCs, make sure that your **Mobility (MDM and MAM)** settings in Azure AD are correctly configured.

1. In the Azure portal, go to the [Azure Active Directory Overview](https://go.microsoft.com/fwlink/p/?linkid=516942) page.
2. In the left nav, under **Manage**, select **Mobility (MDM and MAM)**, then select **Microsoft Intune**.
3. On the **Configure** page, next to **MDM user scope**, select **Some** or **All**, then select **Save**.
4. In the left nav, under **Manage**, select **Mobility (MDM and MAM)**, select **Microsoft Intune Enrollment**, then repeat step 3.

When enabling the automatic enrollment of new Cloud PCs into Microsoft Intune through the Organization Settings, users may see their Cloud PCs fail to complete their setup in the Windows 365 home page due to a variety of settings on your tenant. Please consult the table below for how to troubleshoot these issues.

| Error | Troubleshooting steps |
| --- | --- |
| To complete the setup ask your administrator to resolve the following: - Update policy settings in Microsoft Endpoint Manager to enroll this device. | Check the Intune settings you may have previously set on your tenant. For more, see [Troubleshoot policies and profiles](/troubleshoot/mem/intune/device-configuration/troubleshoot-policies-in-microsoft-intune). Once the issue has been fixed, either you or the user can reset the Cloud PC. |
| To complete the setup ask your administrator to resolve the following: - Remove restrictions preventing Intune from allowing Windows enrollment.| You may have set up enrollment restrictions on your Intune tenant. For more information, see [Enrollment restrictions overview](/mem/intune/enrollment/enrollment-restrictions-set). Once the restrictions have been removed, either you or the user can reset the Cloud PC. |
| To complete the setup ask your administrator to resolve the following:- Correct the configuration of the Mobile Device Management discovery URL in Intune.| Confirm that the MDM discovery URL is the default for Intune. Follow steps 1-4 to set it in [Configure automatic MDM enrollment](/mem/intune/enrollment/windows-enroll#configure-automatic-mdm-enrollment). Once the MDM discovery URL has been set to the default, either you or the user can reset the Cloud PC. |

Users who are assigned a Cloud PC must have an Intune license assigned to them to receive user policies. The CloudPCBPRT system account doesn't need to be assigned an Intune license.

> [!IMPORTANT]
> To assign licenses, you must be a Global or Licensing admin, or have a role with licensing permissions.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/p/?linkid=2169290), select **Users** > **All Users**.
2. In the **All users** list, select a user.
3. On the user **Profile** page, select **Licenses**.
4. On the **Licenses** page, select **Assignments**.
5. Find **Intune**, select the checkbox, then select **Save**. The user account now has the permissions needed to use the service and enroll devices.
6. Go to [Reset your Cloud PCs](#reset-your-cloud-pcs).

### Path B. Turn off automatic MDM enrollment and Intune enrollment in Organization Settings

If you don’t plan to use Microsoft Intune for your Cloud PC management, you must turn off automatic MDM enrollment and uncheck Enroll new Cloud PCs in Microsoft Endpoint Manager in Organization Settings.

> [!IMPORTANT]
> If you’re not the MDM administrator, don’t use either of the following procedures without first consulting with your IT admin. Only follow these procedures if Cloud PCs aren’t being set up. Any configuration changes could impact your management environment. If you need help, [contact Intune support](/mem/get-support).

#### Use the Azure AD portal to turn off automatic Intune enrollment

1. In the Azure portal, go to the [Azure Active Directory Overview](https://go.microsoft.com/fwlink/p/?linkid=516942) page.
2. In the left nav, under **Manage**, select **Mobility (MDM and MAM)**, then select **Microsoft Intune**.
3. On the **Configure** page, you'll see one of two things. If you have an Azure AD Premium subscription, select **None** next to MDM user scope, then select **Save**. If you don't have an Azure AD Premium subscription, select **Disable**.
4. In the left nav, under **Manage**, select **Mobility (MDM and MAM)**, select **Microsoft Intune Enrollment**.
5. Go to [Reset your Cloud PCs](#reset-your-cloud-pcs).

#### Turn off the automatic enrollment of newly-created Cloud PCs
1. In the [Windows 365 home page](https://windows365.microsoft.com), go to **Your organization's Cloud PCs", then select **Update organization settings**.
2. On the righthand side, scroll down to **Microsoft Endpoint Manager** and unselect the checkbox.
3. Click Save at the bottom.

## Reset your Cloud PCs

After you complete the troubleshooting steps in this article, your users must restart their Cloud PC setup. Tell all Cloud PC users who saw the “Setup failed” error to use the following steps to reset their Cloud PCs.

1. On the [Windows 365 home page](https://windows365.microsoft.com), select the gear icon for any Cloud PC that has the “Setup failed” status, then select **Reset**. This action restarts the setup process.
2. After the reset, if the “Setup failed” error still displays, and you skipped [Make sure MDM authority configuration is set up correctly](#make-sure-mdm-authority-configuration-is-set-up-correctly), complete that step, then reset the CloudPC again. Otherwise, in the left nav, select **New support request** to open a support ticket.
