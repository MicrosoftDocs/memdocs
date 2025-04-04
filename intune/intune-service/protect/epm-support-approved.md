---
title: Use EPM support approvals for file elevation requests with Intune
description: Manage support approvals for elevation requests when you use Endpoint Privilege Management for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/12/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: miked"
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Support approved file elevations for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune Endpoint Privilege Management (EPM) your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

This article explains how to use the **support approved** workflow with Endpoint Privilege Management.

Support approved elevations allow you to require approval before an elevation being allowed. You can use the support approved functionality as part of an elevation rule, or as default client behavior. Requests that are submitted require Intune administrators to approve the request on a case-by-case basis.

When a user tries to run a file in an elevated context, and that file is managed by the *support approved* file elevation type, Intune shows a prompt to the user to submit an elevation request. The elevation request is then sent to Intune for review by an Intune admin. When an admin approves the elevation request, the user on the device is notified, and the file can then be run in the elevated context. To approve requests, the Intune admin's account must have extra permissions that are specific to the review and approval task.

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

  An Intune admin must have *view* and *manage* rights for the **Endpoint Privilege Management Elevation Requests** permission before they can review and approve elevation requests.

  To find and respond to requests, these admins use the **Elevation requests** tab of the *Endpoint Privilege Management* page in the admin center. Because Intune doesn't have a way to notify admins about new elevation requests, admins should plan to check the tab regularly for pending requests.

  Admins who can manage requests for elevation can accept or reject a request. They can also provide a reason for their decision. This reason becomes part of the audit record for the request.

  - **For approvals**: When an admin approves an elevation request, Intune sends a policy to the device where the user submitted the request, which enables that user to run the file as elevated for the next 24 hours. This period begins at the time the admin approves the request. There's no current support for a custom time period or cancellation of the approved elevation before the 24-hour period expires.

    Once the request is approved, Intune notifies the device and initiates a sync. *This can take some time.* Intune uses a notification on the device to alert the user that they can now successfully run the file with the *Run with elevated* access right-click option.

  - **For denials**: Intune doesn't notify the user. The administrator should manually notify the user that their request was denied.

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

## Create policy for support approved file elevations

To create support-approved elevation policy, use the same workflow for creating other EPM elevation rule policies. See [Windows elevation rules policy](../protect/epm-policies.md#windows-elevation-rules-policy) in *Configure policies for Endpoint Privilege Management*.

## Manage pending elevation requests

Use the following procedure as guidance for reviewing and managing elevation requests.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > **Elevation requests** tab.
1. The elevation requests tab shows **pending requests** and **requests from the last 30 days**. Selecting a row opens that entries elevation request properties, where you can review the request in detail.
1. The elevation request details include the following information:

    1. **General details**:
       - **File** - The name of the file that was requested for elevation.
       - **Publisher** - The name of the publisher that signed the file that was requested for elevation. The name of the publisher is a link that retrieves the certificate chain for the file for download.
       - **Device** - The device where the elevation was requested from. The device name is a link that opens the device object in the admin center.
       - **Intune compliant** - The Intune compliance state of the device.

    1. **Request details**:
       - **Status** - Status of the request. Requests start as *Pending* and can be either *approved* or *denied* by an administrator.
       - **By** - The account of the administrator who *approved* or *denied* the request.
       - **Last modified** - The last time the request entry was modified.
       - **User's justification** - The justification provided by the user for the elevation request.
       - **Approval expiration** - The time that the approval expires. Until this expiry time is reached, elevation of the approved file is allowed.
       - **Admin's reason** - Justification provided by the admin when an *approval* or *denial* is completed.

    1. **File information** - Specifics of the metadata for the file that was requested for approval.

   :::image type="content" source="./media/epm-support-approved/sample-request-detail.png" alt-text="Image that displays the detail of an elevation request." lightbox="./media/epm-support-approved/sample-request-detail.png":::

1. When your Tenant is licensed for [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot), you have access to use the [Analyze with Copilot](#use-microsoft-security-copilot-to-analyze-file-elevation-requests) option, which is at the upper right of the Elevation request properties pane. You can use this option to have Security Copilot work with Microsoft Defender for Endpoint to evaluate the file in the elevation request before you approve or deny it.

1. After an admin reviews a request, they can select **Approve** or **Deny**. With either selection, they're presented with the **justification** dialog where they can provide a *Reason* with detail about their decision. Providing a reason is optional. The following displays the approval dialog:

    - **For approvals** - The admin completes the justification dialog and then selects **Yes** to approve the request. Intune sends the approval to the device and the end user is notified via a toast notification that they're able to elevate the application.
  
      The end user can now complete the elevation activity by using the **Run with elevated access** right-click menu of the file.
    
      :::image type="content" source="./media/epm-support-approved/sample-request-approval-dialog.png" alt-text="Image that displays the elevation approval dialog with sample approval justification provided as the reason" lightbox="./media/epm-support-approved/sample-request-approval-dialog.png":::

    - **For denials** - The admin completes the justification dialog, and then selects **Yes** to deny the request.

      When an admin denies a request for approval, the elevation request isn't approved. Intune doesn't send a reply to the device and the user isn't notified.

      :::image type="content" source="./media/epm-support-approved/sample-request-denial-dialog.png" alt-text="Image that displays the elevation denial dialog with no sample approval justification provided" lightbox="./media/epm-support-approved/sample-request-denial-dialog.png":::

> [!NOTE]
>
> An elevation request contains all the information needed to create an elevation rule, including the *complete* certificate chain. Support approved elevations also show in the elevation usage data like any other elevation requests.

## Use Microsoft Security Copilot to analyze file elevation requests

With Endpoint Privilege Management (EPM) plus [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot), you can use Security Copilot to reduce the work required to identify and investigate the files in a file elevation request before you choose to approve or deny the request. The information Security Copilot uses to help you evaluate files and establish trust is collected and evaluated through [Microsoft Defender Threat Intelligence](/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti) (Defender TI).

For example, when viewing the file properties for an elevation request, you can select the option to **Analyze with Copilot** to have Security Copilot provide details that are often not apparent, including:

- The apps reputation 
- Information about the trust of the publisher
- The risk score for the user requesting the elevation
- The Risk score of the device from which the elevation was submitted. 

### Prerequisites for using Security Copilot with EPM

To use Microsoft Security Copilot with Endpoint Privilege Management, your tenant must be licensed to use Security Copilot(/copilot/security/get-started-security-copilot#minimum-requirements). This requirement is in addition to the [prerequisites](../protect/epm-overview.md#prerequisites) for using Endpoint Privilege Management.

If your Tenant is already licensed for EPM and for Security Copilot, no additional license or configuration is required.  

### Workflow to analyze file requests

You can have Microsoft Security Copilot analyze the properties of a file while you're reviewing a file elevation request:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Endpoint Privilege Management** and select the **Elevation requests** tab*.

2. On *Elevation requests*, select the name of an elevation request to open the *Elevation request properties* pane where you can then review that files details.

3. To direct Security Copilot to take a closer look at the file, select **Analyze with Copilot** on the *Elevation request properties* pane. When selected, Intune creates a closed Copilot prompt based on the files hash. This prompt uses Microsoft Defender for Endpoint to investigate the file. Custom or open prompts for file analysis aren't supported.

4. After the file is analyzed, the results are returned to the admin center where you can review the files details. You can use this detailed information to make a more informed decision to either approve or deny the elevation request.

**Example**:
The following images display the path and results of an admin using the Intune the admin center path to locate and select a file elevation request that was submitted by a user. The request is a file named *InstallPrinter.msi*. When the file is selected, its *Elevation request properties* open: 

:::image type="content" source="./media/epm-support-approved/analyze-with-copilot.png" alt-text="Screen capture that displays the path and location of the Analyze with Copilot option." lightbox="./media/epm-support-approved/analyze-with-copilot.png":::

When the admin reviews the file, they note that the file has an unknown publisher. To verify that this file is legitimate, they use the Analyze with Copilot option from the Elevation request properties to have Copilot take a closer look. 

Copilot reviews the file and reports back the following details:

:::image type="content" source="./media/epm-support-approved/malicious-file-results.png" alt-text="Screen capture that displays an example of results from use of the Analyze with Copilot option." lightbox="./media/epm-support-approved/malicious-file-results.png":::
 
The preceding image shows a screen capture of the Copilot report on the reputation of that *InstallPrinter.msi* file. In this example, the file is identified as malicious and shouldn’t be approved to run in an elevated context. The results also include additional information and links to references for the malicious file that was identified.

## Related content

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
