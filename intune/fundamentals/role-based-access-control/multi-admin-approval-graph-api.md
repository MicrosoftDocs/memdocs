---
title: Use Multi Admin Approval with the Microsoft Graph API
description: Learn how to update your automation scripts and applications to work with Multi Admin Approval enforcement on app-authenticated API calls in Microsoft Intune.
ms.date: 05/19/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.reviewer: davidra

ms.collection:
- M365-identity-device-management
---

# Use Multi Admin Approval with the Microsoft Graph API

Multi Admin Approval (MAA) enforces approval workflows on application-authenticated (app-auth) API calls made through the Microsoft Graph API. If your organization uses service principals, automation scripts, or third-party applications to manage Intune resources, those calls are intercepted by MAA when the target resource is protected by an [access policy](multi-admin-approval.md).

This article explains how to update your automation to work with the MAA approval workflow, and how to exclude specific applications from enforcement when a code change isn't immediately feasible.

> [!IMPORTANT]
> MAA is opt-in per workload for every tenant. This enforcement applies only to tenants that have MAA access policies configured. It doesn't automatically enable MAA or change which tenants have MAA. For more information about configuring access policies, see [Use access policies to require multi admin approval](multi-admin-approval.md).

## What changes for app-auth calls

Previously, only interactive (delegated) admin actions were subject to MAA approval workflows. With this change, automated and scripted calls that use app-only tokens are also intercepted by MAA when the target resource is protected by an access policy.

If your application makes API calls to MAA-protected resources using app-auth and doesn't include the required approval headers, the call returns an HTTP 403 error. The response body indicates that the operation requires Multi Admin Approval.

### Affected resource types

MAA access policies can protect the following resource types. If your app-auth calls target any of these resources and an access policy is active, your automation is affected:

- Apps
- Compliance policies
- Configuration policies
- Device actions
- Role-based access control
- Scripts
- Tenant Configuration

MAA only applies to operations that modify protected resources (POST, PATCH, PUT, DELETE). Read-only operations (GET) aren't affected.

## Prerequisites

- An [app registration](/entra/identity-platform/quickstart-register-app) with the required Microsoft Graph application permissions for the Intune resources your app manages (for example, `DeviceManagementApps.ReadWrite.All`).
- MAA access policies configured for the relevant workloads. For more information, see [Create an access policy](multi-admin-approval.md#create-an-access-policy).
- A separate admin account that's a member of the approver group for the access policy. Applications can't approve or reject MAA requests — only interactive admin accounts can approve requests.

## Step 1: Submit a request with a justification header

When MAA is enabled, include a justification header with your request. The `x-msft-approval-justification` header value must be Base64-encoded.

The following example creates a PowerShell script resource in Intune and includes the required justification header:

```http
POST https://graph.microsoft.com/beta/deviceManagement/deviceManagementScripts
Content-Type: application/json
x-msft-approval-justification: YXBwIG9ubHkgdGVzdA==

{
  "displayName": "My Test Script",
  "description": "Testing MAA with app-only token",
  "scriptContent": "V3JpdGUtT3V0cHV0ICJIZWxsbyBXb3JsZCI=",
  "runAsAccount": "system",
  "fileName": "TestScript.ps1",
  "roleScopeTagIds": ["0"]
}
```

> [!TIP]
> The `x-msft-approval-justification` value is Base64-encoded. For example, `YXBwIG9ubHkgdGVzdA==` decodes to `app only test`. Encode your own justification string before sending.

Without the justification header, the request fails with an error indicating that the `x-msft-approval-justification` header is required.

## Step 2: Handle the approval response

The request returns an HTTP 403 error indicating that approval is required. The response includes an `x-msft-approval-code` header that you need for the remaining steps.

Example response:

```json
{
  "error": {
    "code": "ApprovalRequired",
    "message": "Approval Required. Request Approval using the request ID returned as part of the x-msft-approval-code response header. x-msft-approval-code: aabb1234-5678-9012-abcd-ef0123456789"
  }
}
```

Extract the `x-msft-approval-code` value from the response. You need it in Step 4 after the request is approved.

## Step 3: Wait for approval

At this point, the approval request must be reviewed and approved by another administrator in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Applications can't approve or reject MAA requests — only interactive admin accounts can approve them.

You can query the approval request status at any time using the approval code:

```http
GET https://graph.microsoft.com/beta/deviceManagement/operationApprovalRequests?$filter=requestId eq 'aabb1234-5678-9012-abcd-ef0123456789'
```

The `status` field indicates the current state of the request. Common values include `needsApproval`, `approved`, `rejected`, and `cancelled`. Wait until the status changes to `approved` before proceeding.

## Step 4: Resubmit with the approval code

After the request is approved, resubmit the original request. Replace the justification header with the `x-msft-approval-code` header and use the approval code from Step 2:

```http
POST https://graph.microsoft.com/beta/deviceManagement/deviceManagementScripts
Content-Type: application/json
x-msft-approval-code: aabb1234-5678-9012-abcd-ef0123456789

{
  "displayName": "My Test Script",
  "description": "Testing MAA with app-only token",
  "scriptContent": "V3JpdGUtT3V0cHV0ICJIZWxsbyBXb3JsZCI=",
  "runAsAccount": "system",
  "fileName": "TestScript.ps1",
  "roleScopeTagIds": ["0"]
}
```

The request completes successfully and the resource is created.

## Exclude an application from MAA enforcement

If an application needs to continue operating without going through the MAA approval workflow, you can exclude it using the app exclusion list in the MAA access policy. Use exclusions when a code change isn't immediately feasible. Microsoft recommends updating your application code to include the MAA approval workflow as the long-term solution.

To configure an app exclusion:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Multi Admin Approval** > **Access policies**.
1. Open the access policy for the workload your app calls (for example, Apps, Scripts, or Endpoint security).
1. Add the named application (service principal) to the policy's app exclusion list.
1. A second administrator must approve the exclusion before it takes effect.

Keep the following details in mind:

- Exclusions are per app, per workload. An exclusion in one access policy doesn't affect other workloads.
- App exclusions are capped at 50 applications per access policy.
- Each exclusion stays in effect until an admin removes it. Removing an exclusion also requires dual approval.
- All add, remove, and modify actions on the exclusion list are captured in the Intune audit log.

## Monitor MAA activity for app-auth calls

MAA-related events — including approve, block, pass, exclusion add, and exclusion remove — are recorded in the existing Intune audit log. Use the standard [audit log](../../governance/monitor-audit-logs.md) and Graph API export to see which app-auth calls are going through MAA and how they're being handled.

## Frequently asked questions

### Why are my automation scripts failing?

If your automation uses app-only tokens (client-credentials flow) to call Microsoft Graph and targets resources protected by an MAA access policy, those calls are now intercepted by the MAA approval workflow. Update your scripts to include the justification and approval headers described in this article, or [exclude the application](#exclude-an-application-from-maa-enforcement) from the access policy.

### Does MAA affect read-only API calls?

No. MAA only applies to operations that modify protected resources (POST, PATCH, PUT, DELETE). GET requests aren't affected.

### Can an application approve its own MAA requests?

No. Applications can't approve or reject MAA requests. A separate interactive admin account that's a member of the approver group must approve the request in the Microsoft Intune admin center.

### How do I check if my tenant has MAA enabled?

In the Microsoft Intune admin center, go to **Tenant administration** > **Multi Admin Approval** > **Access policies**. If there are active access policies listed, MAA is enabled for those workloads.

### Can I turn off MAA to stop the enforcement?

MAA access policies can be managed by administrators with the appropriate permissions. However, Microsoft strongly recommends keeping MAA enabled as a security best practice.

## Related content

- [Use access policies to require multi admin approval](multi-admin-approval.md)
- [Audit logs for Intune activities](../../governance/monitor-audit-logs.md)
