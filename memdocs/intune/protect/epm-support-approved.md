---
title: Use EPM support approvals for file elevation requests with Intune
description: Manage support approvals for elevation requests when you use Endpoint Privilege Management for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/25/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mattcall
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
---

# Support approved file elevations for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

This article explains how to use the **support approved** file *elevation type* in your Endpoint Privilege Management [Windows elevation rules policies](../protect/epm-policies.md#windows-elevation-rules-policy).

Support-approved elevation gives you more control over sensitive files than other elevation rule types, but it also requires Intune administrators to manage which files can run as elevated on a case-by-case basis.

When a user tries to run a file in an elevated context, and that file is managed by the *support approved* file elevation type, Intune shows a prompt to the user to submit an elevation request. The elevation request is then sent to Intune for review by an Intune admin. When an admin approves the elevation request, the user on the device is informed, and the file can then be run in the elevated context. To approve requests, the Intune admin's account must have extra permissions that are specific to the review and approval task.

Applies to:

- Windows 10
- Windows 11

## About support approved elevations

Use EPM policies with the *support approved* elevation type for files that need an admin's approval before they can run with higher access. They're similar to other EPM  elevation rules, but they have some differences that need extra planning.

> [!TIP]
>
> To review the three elevation types and other policy options, see [Windows elevation rules policy](../protect/epm-policies.md#windows-elevation-settings-policy).

The following subjects are details to plan for and expect when you use the support approved elevation type:

- **Elevation requests**

  When a user runs a file with the right-click option *Run with elevated access*, and that file is managed by policy with a *support approved* elevation rule, Intune shows the user a prompt for sending an elevation request to the Intune admin center.

  - The prompt lets the user enter a business reason for the elevation. This reason becomes part of the elevation request, which also contains the user's name, device, and file name.

  - When the user sends the request, it goes to the Intune admin center where an Intune admin with permissions to manage these requests decides to approve or deny it.

  The following image shows an example of the file elevation prompt that users experience:

  :::image type="content" source="./media/epm-support-approved/user-prompt.png" alt-text="Screen capture that displays an example of the user elevation request prompt." lightbox="./media/epm-support-approved/user-prompt.png":::

- **Review of elevation requests**

  An Intune admin must have *view* and *manage* rights for the **Intune Endpoint Privilege Management Elevation Requests** permission before they can review and approve elevation requests.

  To find and respond to requests, these admins use the **Elevation requests** tab of the *Endpoint Privilege Management* page in the admin center. Because Intune doesn't have a way to notify admins about new elevation requests, admins should plan to check the tab regularly for pending requests.

  Admins who can manage requests for elevation can accept or reject a request. They can also provide a reason for their decision. This reason becomes part of the audit record for the request.

  - **For approvals**: When an admin approves an elevation request, Intune sends a policy to the device where the user submitted the request, which enables that user to run the file as elevated for the next 24 hours. This period begins at the time the admin approves the request. There's no current support for a custom time period or cancellation of the approved elevation before the 24-hour period expires.

    Because approval isn't immediate, Intune also uses a notification on the device to alert the user that they can now successfully run the file with the *Run with elevated* access right-click option.

  - **For denials**: Intune sends a notification to the user on the device that the request was denied, and the user can’t run that file in an elevated context. The can submit a new request, which is again subject to review and approval.

- **Auditing for elevation requests**

  An Intune admin who has enough permissions can view information about EPM policy such as creation, editing, and the handling of elevation requests in the [Intune Audit logs](../fundamentals/monitor-audit-logs.md), available at **Tenant administration** > **Audit logs**.

  The following screen capture shows an example of the audit log for the duplication of a *Support approved* elevation policy, originally named *Test policy - support approved*:

  :::image type="content" source="./media/epm-support-approved/sample-audit-log.png" alt-text="Image that displays an audit log entry for a support approved elevation rules policy." lightbox="./media/epm-support-approved/sample-audit-log.png":::

## RBAC permissions for elevation requests

To provide oversight for elevation approvals, only Intune administrators who have the following role-based access control (RBAC) permissions in Intune can view and manage elevation requests:

- **Endpoint Privilege Management Elevation Requests** - This permission is required to work with elevation requests that are submitted by users for approval, and supports the following rights:

  - View elevation requests
  - Modify elevation requests

For more information about all the permissions for managing EPM, see [Role-based access controls for Endpoint Privilege Management](../protect/epm-overview.md#role-based-access-controls-for-endpoint-privilege-management).

### Create policy for support approved file elevations

To create support-approved elevation policy, use the same workflow for creating other EPM elevation rule policies. See [Create a Windows elevation rules policy](../protect/epm-policies.md#create-a-windows-elevation-rules-policy) in *Configure policies for Endpoint Privilege Management*.

### Manage pending elevation requests

Use the following procedure as guidance when reviewing and managing elevation requests.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > **Elevation requests** tab.
2. *Pending*
3. *Pending*

## Next steps

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
