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

When you use the *support approved* file elevation type for Endpoint Privilege Management (EPM), Intune prompts a device user to submit a request when they attempt to run a file in an administrator context. An Intune admin must review and approve the elevation request before the file is eligible to run by the user in the elevated context. To approve requests, an admins account must have extra permissions that are specific to the review and approval task.

The support-approved elevation process provides you with more control for sensitive files. With this elevation type you can manage which files you allow to run as elevated on a case-by-case basis.

Applies to:

- Windows 10
- Windows 11

## About support approved elevation requests

EPM elevation rule policies that you configure for *support approved* elevations are similar to those created for the other elevation types. They have a few differences that can require extra planning.

> [!TIP]
>
> To review the three elevation types and other policy options, see [Windows elevation rules policy](../protect/epm-policies.md#windows-elevation-settings-policy).

The following subjects are details to plan for and expect when you use the support approved elevation type:

- **Elevation requests**

  When a user invokes the right-click option **Run with elevated access** for a file managed by a support approved elevation rule, Intune opens a prompt for submitting an elevation request to the Intune admin center.

  - The prompt provides space for the user to specify a business justification for the file elevation. This justification becomes part of the file elevation request, which also includes the user's name, device, and the file name.
  - When the user submits the request, it appears in the Intune admin center where an Intune admin with sufficient rights to manage these requests can review and choose to approve or deny the request.

  The following image displays an example of the file elevation prompt that users experience:

  :::image type="content" source="./media/epm-support-approved/user-prompt.png" alt-text="Screen capture that displays an example of the user elevation request prompt." lightbox="./media/epm-support-approved/user-prompt.png":":::code language="{language}" source="{source}" range="{range}":::

- **Administrative review**

Only an Intune admin who’s account has *view* and *manage* rights for the Intune **Endpoint Privilege Management Elevation Requests** permission can review and approval elevation requests.

  To discover and act on requests, applicable admins use the **Elevation requests** tab of the Endpoint Privilege Management page in the admin center. Because Intune doesn’t have a method to alert admins to the presence of active elevation requests, admins should plan to periodically review the tab for pending requests.

  Admins who can manage requests for elevation can approve or deny the request, and specify a justification for their decision. This justification becomes part of the audit record for the request.

  - **For approvals**: When an admin approves an elevation request, Intune sends a policy to the device where the user submitted the request, which enables that user to run the file as elevated for the next 24 hours. This period begins at the time the admin approves the request. There's no current support for a custom time period and, or revocation of the approved elevation before the 24-hour period expires.

    Because approval isn't immediate, Intune also uses a notification on the device to alert the user that they can now successfully run the file with the *Run with elevated* access right-click option.

  - **For denials**: Intune sends a notification to the user on the device that the request was denied, and the user can’t run that file in an elevated context. The can submit a new request, which is again subject to review and approval.

- **Auditing for support approved elevation requests**

  An Intune admin with sufficient permissions can view details about EPM policy including creation, editing, and the management of elevation requests in the [Intune Audit logs](../fundamentals/monitor-audit-logs.md), available at **Tenant administration** > **Audit logs**.

  The following screen capture displays an example of the audit log for the duplication of a *Support approved* elevation policy, originally named *Test policy - support approved*:

  :::image type="content" source="./media/epm-support-approved/sample-audit-log.png" alt-text="Image that displays an audit log entry for a support approved elevation rules policy." lightbox="./media/epm-policies/sample-audit-log.png":::

## RBAC permissions for elevation requests

To provide oversight for elevation approvals, only Intune administrators who have the following role-based access control (RBAC) permissions in Intune can view and approve elevation requests:

- **Endpoint Privilege Management Elevation Requests** - This permission is required to work with elevation requests that are submitted by users for approval, and supports the following rights:

  - View elevation requests
  - Modify elevation requests

For more information about all the permissions for managing EPM, see [Role-based access controls for Endpoint Privilege Management](../protect/epm-overview.md#role-based-access-controls-for-endpoint-privilege-management).

### Create policy for support approved file elevations

To create support-approved elevation policy, use the same workflow for creating other EPM elevation rule policies. See [Create a Windows elevation rules policy](../protect/epm-policies.md#create-a-windows-elevation-rules-policy) in *Configure policies for Endpoint Privilege Management*.

### Manage pending elevation requests

Use the following as guidance when reviewing and managing elevation requests.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > **Elevation requests** tab.
2. *Pending*
3. *Pending*

## Next steps

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
