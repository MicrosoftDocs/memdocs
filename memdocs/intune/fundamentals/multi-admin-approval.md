---
# required metadata

title: Use multiple administrative approvals in Intune
titleSuffix: Microsoft Intune
description: Configure multi-admin approval to protect your tenant against the use of compromised administrative accounts in Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/17/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: craigma
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Use Access policies to require multiple administrative approvals

*This feature is in Public Preview*

To help protect against a compromised administrative account, use Intune *access policies* to require that a second administrative account is used to approve a change before the change is applied. This capability is known as multiple administrative approval (MAA).

With MAA, you configure access policies that protect specific configurations, like Apps or Scripts for devices. Access policies specify what is protected and which group of accounts are permitted to approve changes to those resources.

When any account in the Tenant is used to make a change to a resource that’s protected by an access policy, Intune won't apply the change until a different account explicitly approves it. Only administrators who are members of an approval group that’s assigned a protected resource in an access protection policy can approve changes. Approvers can also reject change requests.

Access policies are supported for the following resources:

- Apps – Applies to [app deployments](../apps/apps-add.md), but doesn't apply to app protection policies.
- Scripts – Applies to deploying scripts to devices that run [macOS](../apps/macos-shell-scripts.md) or [Windows](../apps/intune-management-extension.md).

## Prerequisites for access policies and approvers

To create an access policy, your account must be assigned the [*Intune Service Administrator* or *Azure Global Administrator*](../fundamentals/role-based-access-control.md) role.

To be an approver, an account must be in the group that’s assigned to the access policy for a specific type of resource.

## How multi admin approval and Access policies work

**When an admin edits** or creates a new object for an area that’s protected by an access policy, they see an option on the *Save + Review* surface where they can enter a description of the change as a *business justification*.

- The *business justification* becomes part of the approval request for the change.
- An admin who has submitted a change can view the status of their requests in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Tenant administration** > **Multi Admin Approval** and viewing the **My request** page.

**After a change is submitted**, an *approver* navigates to the **Received request** page of the **Multi Admin Approval** node. Here they’ll see a list of requests that are active, or recently managed. This view provides some details about the request including when and who submitted it, the type of operation involved like *Create* or *Assign*, and its status. To manage the request:

- The approver selects the *Business justification* link for the request. This action opens the Access policy request pane where you can view more information about the change, including the full details provided in the Business justification field of the request.
- On the Access policy request pane, the approver can enter notes in the **Approver notes** field, and then select an option to **Approve request** or **Reject request**. These notes are added to the request and are visible to the individual who requested the change when they review their requests on the **My request** page. For example, if the request is rejected, the reason for the rejection can be passed back to the requestor through the Approver notes.
- Individuals who submit a request and are also members of the approval group for that can see their own requests on the Received request page. However, they can't approve their own requests.

**If a change is approved**, Intune processes the requested change and updates the object. While Intune processes the request, its status can display as **Approved**. After it’s successfully processed, the status updates to **Completed**.

**Each change of status** remains visible for up to 30 days after the last change of status. If a request isn’t processed further within 30 days, it becomes **Expired**, and must be resubmitted.

## Create an access policy

1. To create an access policy, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Multi Admin Administration** > **Access policies** and select **Create**.

2. On the *Basics* page, provide a *Name*, and optional *Description*, and for *Profile type* select from available options. Each policy supports a single profile type.

   <!-- The following screen capture shows a new policy with **Apps**  selected for the profile type.  -->

3. On the *Approvers page*, select **Add groups** and then select a group as the group of approvers for this policy. More complex configurations that exclude groups aren't supported.

4. On the *Review + Create* page, review, and then save your changes. After Intune applies this policy, configurations for the protected profile type will require multiple admin approvals.

## Submit a request

To submit a request when MAA is enabled, use your normal process to create or edit a resource.

On the final page before you can save your changes, add details to the *Business justification* field and then submit the request. For urgent requests, consider reaching out to a known list of approvers to ensure your request is seen in a timely manner.

When there's a request for the same object that is already pending approval, you won't be able to submit your request. Intune displays a message to alert you to this situation.

To monitor the status of your requests, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Tenant administration** > **Multi Admin Approval** > **My requests**.

You can cancel a request before it’s approved by selecting it from the My requests page, and then selecting **Cancel request**.

## Approve requests

1. To find requests to approve, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Tenant administration** > **Multi Admin Administration** > **Received requests**.

2. Select the *Business justification* link for a request to open the review page where you can learn more about the request, and manage approval or rejection. 

3. After reviewing the details, enter relevant details in the Approver notes field, and then select **Approve request** or **Reject request**.

4. After you approve a request, Intune processes the change and updates the status to *Completed* after it’s successfully applied. The request status might change to *Approved* for a limited time if the update to the resource takes time to process.

## More considerations

- With the public preview, Intune doesn't send notifications when new requests are created, or the status of an existing request changes. We recommend that when submitting an urgent change request, you reach out to individuals who have permission to approve those requests.

- Plan to monitor the status of your requests through the *My requests* page of the *Multi Admin Approval* node in the Microsoft Intune admin center.

- When an approval is already pending for an object, a new request is can't be submitted for it.

- All actions for a protected resource are protected, including but not limited to:
  - Edit
  - Create
  - Modify
  - Delete
  - Assign

- Actions for requests and the approval process are logged in the Intune audit logs. For more information, see [Audit logs for Intune activities](../fundamentals/monitor-audit-logs.md).

- The following status conditions are available for a request:
  - Needs approval – This request is pending action by an approver.
  - Approved – This request is being processed by Intune.
  - Completed – This request has been successfully applied.
  - Rejected – This request was rejected by an approver.
  - Canceled – This request was canceled by the admin who submitted it.

## Next steps

Manage [role-based access control](../fundamentals/role-based-access-control.md)