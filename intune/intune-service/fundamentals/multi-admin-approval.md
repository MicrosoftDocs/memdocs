---
title: Use Multi Admin Approval in Intune
description: Configure Multi Admin Approval to protect your tenant against the use of compromised administrative accounts in Intune.
author: brenduns
ms.author: brenduns
ms.date: 04/10/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.reviewer: davidra
ms.collection:
- M365-identity-device-management
- highpri
- setup
---

# Use access policies to require multi admin approval

To help protect against a compromised administrative account, use Microsoft Intune *access policies* to require that a second administrative account approves a change before the change is applied. This capability is known as Multi Admin Approval.

By using Multi Admin Approval, you can configure access policies that protect specific configurations, like Apps or Scripts for devices. Access policies specify what is protected and which group of accounts can approve changes to those resources.

When you use any account in the tenant to make a change to a resource that's protected by an access policy, Intune doesn't apply the change until a different account explicitly approves it. Only administrators who are members of an approval group that an access protection policy assigns a protected resource to can approve changes. Approvers can also reject change requests.

Intune supports access policies for the following resources:

- Apps – Applies to [app deployments](../apps/apps-add.md), but doesn't apply to app protection policies.  
- Compliance policies - Applies to creating and managing [compliance policies](../protect/create-compliance-policy.md).  
- Configuration policies - Applies to creating and managing policies via the [settings catalog](../../device-configuration/settings-catalog/index.md).  
- Device actions - Applies to [wipe](../../device-management/actions/wipe.md), [retire](../../device-management/actions/retire.md), and [delete](../../device-management/actions/delete.md) device actions.
- Role-based access control – Applies to changes to roles, including modifications to role permissions, admin groups, or member group assignments.
- Scripts – Applies to deploying scripts to devices that run [Windows](../apps/powershell-scripts.md).
- Access Policies - Applies to creating or managing multiple administrative approval policies.
- Tenant Configuration - Applies to managing [device categories](../enrollment/device-group-mapping.md), including creating, editing, or deleting them.

## Prerequisites for access policies and approvers

To use Multi Admin Approval, your tenant must have at least two administrator accounts. The MAA workflow has three distinct roles, each with different permission requirements:

### Administrator licensing

By default, every administrator who participates in the MAA workflow must have an Intune license assigned to their account. If your organization needs administrators to participate without individual Intune licenses, you can enable the **Allow access to unlicensed admins** setting.

> [!CAUTION]
> **This setting is irreversible.** Once enabled, you can't turn it off. Make sure your organization understands this limitation before proceeding.

Before enabling this setting, review [Unlicensed admins](../../fundamentals/licensing/unlicensed-admins.md) for important limits and behavior details, including group membership caps and how long access changes take to take effect.

### Role 1: Access policy manager

To create and manage access policies, use an account with one of the following options:

- **Custom Intune role** (recommended): Use a [custom role](create-custom-role.md) that includes the following [Multi Admin Approval permissions](create-custom-role.md#multi-admin-approval):

  | Permission | Description |
  |------------|-------------|
  | *Create access policy* | Create new MAA access policies |
  | *Read access policy* | View existing MAA access policies |
  | *Update access policy* | Modify existing MAA access policies |
  | *Delete access policy* | Remove MAA access policies |

- **Intune Administrator** [:::image type="icon" source="../../media/icons/16/privileged-label.svg" border="false":::](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) (also known as **Intune Service Administrator**): This Microsoft Entra role provides full read/write access to Intune. Because it's a [privileged role](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center), Microsoft recommends using a least-privileged custom Intune role for routine access policy management instead of this role. To learn more, see [Microsoft Entra built-in roles - Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).

### Role 2: Approver

To approve or reject MAA requests submitted by other admins, an account must meet all of the following requirements:

1. **Approver group membership**: The account must be a member of the approver group that's assigned to the access policy for the specific resource type.
2. **Intune role permission**: The account must have the *Approval for Multi Admin Approval* permission in their Intune role, plus the resource-specific Read permissions for the policy type they are approving. See [Permissions reference](#permissions-reference) for the full list.
3. **RBAC role assignment for the group**: The approver security group itself must be added as a member group to at least one Intune role assignment. If the approver group isn't added to a role assignment, approver group members are removed from the group periodically.

   > [!IMPORTANT]
   > The approver group has two requirements:
   > - It must be a **security group**. Distribution lists, Microsoft 365 groups, and mail-enabled security groups aren't supported and silently fail to resolve approver membership.
   > - It must be directly assigned to an Intune role as a member group. Intune role permissions held by individual members, whether through other groups or direct user assignments, don't satisfy this requirement.

### Role 3: Change requestor

To submit change requests and complete approved changes for protected resources, an administrator needs the standard Intune RBAC permissions for the specific action they're performing. The same account performs both steps — submitting the initial request and selecting **Complete** after approval by another admin. For example, *MobileApps/Create* to create an app, or *RemoteTasks/Wipe* to wipe a device. See [Permissions reference](#permissions-reference) for the full list by policy type.

> [!NOTE]
> An administrator can't approve their own requests, even if they're a member of the approver group. A different administrator must approve the request.

## How Multi Admin Approval and Access policies work

When an admin edits or creates a new object for an area that's protected by an access policy, they see an option on the *Save + Review* surface where they can enter a description of the change as a *business justification*.

- The *business justification* becomes part of the approval request for the change.
- An admin who submitted a change can view the status of their requests in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Tenant administration** > **Multi Admin Approval** and viewing the **My request** page.

After a change is submitted, an *approver* navigates to the **Received request** page of the **Multi Admin Approval** node. Here they see a list of requests that are active, or recently managed. This view provides some details about the request including when and who submitted it, the type of operation involved like *Create* or *Assign*, and its status. To manage the request:

- The approver selects the *Business justification* link for the request. This action opens the Access policy request pane where you can view more information about the change, including the full details provided in the Business justification field of the request.
- On the Access policy request pane, the approver can enter notes in the **Approver notes** field, and then select an option to **Approve request** or **Reject request**. These notes are added to the request and are visible to the individual who requested the change when they review their requests on the **My request** page. For example, if the request is rejected, the reason for the rejection can be passed back to the requestor through the Approver notes.
- Individuals who submit a request and are also members of the approval group for that can see their own requests on the Received request page. However, they can't approve their own requests.

If a change is approved, Intune processes the requested change and updates the object. While Intune processes the request, its status can display as **Approved**. The original requestor needs to view the request, and choose **Complete** to initiate the change. After being successfully processed, the status updates to **Completed**.

Each change of status remains visible for up to 30 days after the status changes. If a request isn't processed further within 3 days, it becomes **Expired**, and must be resubmitted.

## Create an access policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Multi Admin Administration** > **Access policies** > select **Create**.

1. On *Basics*, enter a *Name*, and optional *Description*. For *Profile type*, select from available options. Each policy supports a single profile type.

1. On *Approvers*, select **Add groups** and then select a group as the group of approvers for this policy. More complex configurations that exclude groups aren't supported.

1. On *Review + Create*, review, and then save your changes.

1. Next, use a separate administrative account with **Approval for Multi Admin Approval** permission to sign in to the admin center to review and approve the new access policy.

1. Sign back in to the admin center with the first admin account that created the access policy, view the policy, and finalize it by selecting **Complete**. After Intune applies this policy, configurations for the protected profile type require multiple admin approvals.

## Submit a request

To submit a request when Multi Admin Approval is enabled, use your normal process to create or edit a resource.

On the final page before you can save your changes, add details to the *Business justification* field, and then submit the request. For urgent requests, consider reaching out to a known list of approvers to ensure your request is seen in a timely manner.

When a request for the same object is already pending approval, you can't submit your request. Intune displays a message to alert you to this situation.

To monitor the status of your requests, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Tenant administration** > **Multi Admin Approval** > **My requests**.

You can cancel a request before it's approved by selecting it from the **My requests** page, and then selecting **Cancel request**.

## Approve requests

1. To find requests to approve, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Tenant administration** > **Multi Admin Administration** > **Received requests**.

1. Select the *Business justification* link for a request to open the review page where you can learn more about the request, and manage approval or rejection.

1. After reviewing the details, enter relevant details in the **Approver notes** field, and then select **Approve request** or **Reject request**.

1. After you approve a request, the requestor needs to select **Complete**. Intune processes the change, and changes the status to *Completed.* Verify the approval succeeded (or failed) by reviewing the console notification upon completion.

   To verify if the approval succeeded (or failed), look at the notifications in the Intune admin center. A message shows if the approval succeeded or failed.

[!INCLUDE [manage-admin-tasks](../../intune-service/fundamentals/includes/manage-admin-tasks.md)]

## More considerations

- Intune doesn't send notifications when new requests are created, or the status of an existing request changes. When you submit an urgent change request, contact individuals who have permission to approve those requests.

- Monitor the status of your requests through the *My requests* page of the *Multi Admin Approval* node in the Intune admin center.

- When an approval is already pending for an object, you can't submit a new request for it.

- All actions for a protected resource are protected, including but not limited to:
  - Edit
  - Create
  - Modify
  - Delete
  - Assign

- Intune audit logs record actions for requests and the approval process. For more information, see [Audit logs for Intune activities](../fundamentals/monitor-audit-logs.md).

- The following status conditions are available for a request:
  - Needs approval – This request is pending action by an approver.
  - Approved – This request is being processed by Intune.
  - Completed – This request has been successfully applied.
  - Rejected – This request was rejected by an approver.
  - Canceled – This request was canceled by the admin who submitted it.

- Be cautious when creating an access policy for the **Role** policy type. This policy type protects all role-related changes, including creating, updating, and deleting RBAC roles and role assignments. Once active, any attempt to modify roles, including the RBAC assignments that MAA itself requires, needs MAA approval first. This requirement can create a deadlock situation where you can't configure the RBAC assignments needed for MAA to function.

  If you experience this deadlock:
  1. Go to **Tenant administration** > **Multi Admin Approval** > **Access policies**.
  1. Find and delete the access policy configured for the **Role** policy type.
  1. Wait 3–5 minutes for the change to propagate.
  1. Go to **Tenant administration** > **Roles** and complete the required RBAC role assignments, adding the approver group to a role assignment.
  1. After RBAC is configured correctly, you can re-create the **Role** access policy if desired.

  To avoid this issue, configure all other MAA access policies and verify RBAC assignments are correct before enabling an access policy for the **Role** policy type.

## Permissions reference

The following tables list the core RBAC permissions required for each MAA role by policy type. These tables reflect known requirements at time of publication. As MAA support expands, use the full permissions list to verify requirements for any resource types not shown here. For descriptions of all available Intune RBAC permissions, see [Custom role permissions](create-custom-role.md#custom-role-permissions).

### Approver permissions

Approvers need **Read** permissions for the resources they are approving. The following table lists the required RBAC permissions by policy type:

| Policy type | Required RBAC permissions |
|-------------|---------------------------|
| Device Wipe | `ManagedDevices/Read` |
| Device Retire | `ManagedDevices/Read` |
| Device Delete | `ManagedDevices/Read` |
| Apps | `MobileApps/Read`, `ManagedApps/Wipe`, plus shared configuration permissions* |
| Configuration Policies | `DeviceConfigurations/Read`, plus shared configuration permissions* |
| Compliance Policies | `DeviceCompliancePolicies/Read`, `DeviceConfigurations/Read` |
| Scripts | `DeviceConfigurations/Read`, `SecurityBaselines/Read` |
| Roles | `Roles/Read` |
| Access Policies | `MultiAdminApproval/ReadAccessPolicy` and `MultiAdminApproval/ApprovalForMultiAdminApproval` |
| Tenant Configuration | `Organization/Read`, `DeviceConfigurations/Read`, plus 11 other Read permissions |

*Shared configuration permissions (required for Apps and Configuration Policies): `DeviceConfigurations/Read`, `SecurityBaselines/Read`, `QuietTimePolicies/Read`, `EpmPolicy/Read`, `AppleEnrollmentProfiles/Read`, `ASRPolicy/Read`, `EDRPolicy/Read`, `AppControlPolicy/Read`

### Change requestor permissions

Change requestors need **Write** or **Execute** permissions for the action they're performing:

| Policy type | Required RBAC permission |
|-------------|--------------------------|
| Device Wipe | `RemoteTasks/Wipe` |
| Device Retire | `RemoteTasks/Retire` |
| Device Delete | `ManagedDevices/Delete` |
| Apps | `MobileApps/Create` (or `Update` / `Delete` depending on the action) |
| Configuration Policies | `DeviceConfigurations/Create` (or `Update` / `Delete`) |
| Compliance Policies | `DeviceCompliancePolicies/Create` (or `Update` / `Delete`) |
| Scripts | `DeviceConfigurations/Create` (or `Update` / `Delete`) |
| Roles | `Roles/Create` (or `Update` / `Delete`) |
| Access Policies | `MultiAdminApproval/UpdateAccessPolicy` |
| Tenant Configuration | Depends on the specific tenant setting being modified |

> [!TIP]
> If an approver or requestor is missing permissions, their action might fail silently or return an error. When troubleshooting, always verify that permissions match the specific policy type, not just the general MAA permissions.

## Related content

Manage [role-based access control](../fundamentals/role-based-access-control.md)
