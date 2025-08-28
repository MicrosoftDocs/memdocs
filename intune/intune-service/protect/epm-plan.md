---
title: Plan and Prepare for Endpoint Privilege Management Deployment
description: To enhance the security of your organization, set your users to run with standard permissions while Endpoint Privilege Management ensures those users can seamlessly run specified files with elevated rights. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/30/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Plan and Prepare for Endpoint Privilege Management Deployment

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

The following sections of this article discuss requirements to use EPM and introduce important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

## Planning Checklist

- Review technical and licensing pre-requisites in your tenant.
- Define your target user personas to enable you to build rules with logical grouping on these personas.
- Ensure you have a good understanding of EPM Settings Policies and Elevation Rules construct, including:
- Default elevation settings and diagnostic data collection.
- Defining elevation files using file hash, metadata, or certificates
- How certificate rules can allow any app signed by that certificate to elevate. Exercise caution for vendors who may sign all their apps with the same certificate.
- Rules argument support, and child process behaviour options
- Elevation types and the expected behaviour of each
- How rule conflicts are handled when you have overlapping rule assignments
  - Consider your EPM Settings Policies and Rules design carefully, finding the right balance between security and flexibility for your organization and user personas.
  - Ensure you have a robust rollout strategy, with clear stakeholder management, end user communication and training plans, and monitoring and exception plans.

## Prerequisites

### Licensing

Endpoint Privilege Management requires an additional license beyond the *Microsoft Intune Plan 1* license. You can choose between a stand-alone license that adds only EPM, or license EPM as part of the Microsoft Intune Suite. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

### Requirements

Endpoint Privilege Management has the following requirements:

- Microsoft Entra joined *or* Microsoft Entra hybrid joined
- Microsoft Intune Enrollment *or* Microsoft Configuration Manager [co-managed](../../configmgr/comanage/overview.md) devices (no workload requirements)
- Supported Operating System
- Clear line of sight (without SSL-Inspection) to the [required endpoints](../fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management)

> [!NOTE]
>
> - Windows 365 (CloudPC) is supported using a supported operating system version
> - Workplace-join devices are not supported by Endpoint Privilege Management
> - Azure Virtual Desktop is not supported by Endpoint Privilege Management

Endpoint Privilege Management supports the following operating systems:

- Windows 11, version 24H2
- Windows 11, version 23H2 (22631.2506 or later) with [KB5031455](https://support.microsoft.com/topic/october-31-2023-kb5031455-os-builds-22621-2506-and-22631-2506-preview-6513c5ec-c5a2-4aaf-97f5-44c13d29e0d4)
- Windows 11, version 22H2 (22621.2215 or later) with [KB5029351](https://support.microsoft.com/topic/august-22-2023-kb5029351-os-build-22621-2215-preview-9af25662-083a-43f5-b3a7-975fe25cc692)
- Windows 11, version 21H2 (22000.2713 or later) with [KB5034121](https://support.microsoft.com/topic/january-9-2024-kb5034121-os-build-22000-2713-f5847e32-0b71-4151-8190-54d3e36386f0)
- Windows 10, version 22H2 (19045.3393 or later) with [KB5030211](https://support.microsoft.com/topic/september-12-2023-kb5030211-os-builds-19044-3448-and-19045-3448-c0dee353-f025-4f03-bcc1-336f74fb992c)
- Windows 10, version 21H2 (19044.3393 or later) with [KB5030211](https://support.microsoft.com/topic/september-12-2023-kb5030211-os-builds-19044-3448-and-19045-3448-c0dee353-f025-4f03-bcc1-336f74fb992c)

> [!IMPORTANT]
>
> - Elevation settings policy will show as not applicable for devices that don't run a supported operating system version.
> - Endpoint Privilege Management is only compatible with 64-bit Operating System Architectures. This includes devices running Windows on Arm64.
> - Endpoint Privilege Management has some new networking requirements, see [Network Endpoints for Intune](../../intune-service/fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management).

## Government cloud support

Endpoint Privilege Management is supported with the following sovereign cloud environments:

- U.S. Government Community Cloud (GCC) High
- U.S. Department of Defense (DoD)

For more information, see [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md).

## Important concepts for Endpoint Privilege Management

When you configure the *elevation settings* and *elevation rules* policies that were mentioned previously, there are some important concepts to understand ensuring you configure EPM to meet the needs of your organization. Before you widely deploy EPM, the following concepts should be well understood as well as the effect they have on your environment:

- **Run with elevated access** - A right-click context menu option that appears when EPM is activated on a device. When this option is used, the devices elevation rules policies are checked for a match to determine if, and how, that file can be elevated to run in an administrative context. If there's no applicable elevation rule, then the device uses the default elevation configurations as defined by the elevation settings policy.

- **File elevation and elevation types** – EPM allows users without administrative privileges to run processes in the administrative context. When you create an elevation rule, that rule allows EPM to proxy the target of that rule to run with administrator privileges on the device. The result is that the application has *full administrative* capability on the device.

  When you use Endpoint Privilege Management, there are a few options for elevation behavior:

  - **Automatic**: For automatic elevation rules, EPM *automatically* elevates these applications without input from the user. Broad rules in this category can have widespread impact to the security posture of the organization.

  - **User confirmed**: With user confirmed rules, end users use a new right-click context menu *Run with elevated access*. User confirmed rules require the end-user to complete some additional requirements before the application is allowed to elevate. These requirements provide an extra layer of protection by making the user acknowledge that the app will run in an elevated context, before that elevation occurs.

  - **Deny**: A deny rule identifies a file that EPM blocks from running in an elevated context. While we recommend use of file elevation rules to allow users to elevate specific files, a deny rule can help you ensure that certain files like known and potentially malicious software can't be run in an elevated context.

  - **Support approved**: For support approved rules, end users must submit a request to approve an application. Once the request is submitted, an administrator can approve the request. Once the request is approved, the end user is notified that they can complete the elevation on the device. For more information about using this rule type, see [Support approved elevation requests](../protect/epm-support-approved.md)

  > [!NOTE]
  >
  > Each elevation rule can also set the elevation behavior for child processes that the elevated process creates.

- **Child process controls** - When processes are elevated by EPM, you can control how the creation of child processes is governed by EPM, which allows you to have granular control over any subprocesses that might be created by your elevated application.

- **Client-side components** – To use Endpoint Privilege Management, Intune provisions a small set of components on the device that receive elevation policies and enforces them. Intune provisions the components only when an elevation settings policy is received, and the policy expresses the intent to *enable* Endpoint Privilege management.

- **Disabling and deprovisioning** – As a component that installs on a device, Endpoint Privilege Management can be disabled from within an elevation settings policy. Use of the elevation settings policy is **required** to remove Endpoint Privilege Management from a device.

  Once the device has an elevation settings policy that requires EPM to be disabled, Intune immediately disables the client-side components. EPM will remove the EPM component after a period of seven days. The delay is to ensure temporary or accidental changes in policy or assignments don't result in mass *de-provisioning*/*re-provisioning* events that might have a substantial impact on business operations.

- **Managed elevations vs unmanaged elevations** – These terms might be used in our reporting and usage data. These terms refer to the following descriptions:

  - **Managed elevation**: Any elevation that Endpoint Privilege Management facilitates. Managed elevations include all elevations that EPM ends up facilitating for the standard user. These managed elevations could include elevations that happen as the result of an elevation rule or as part of default elevation action.

  - **Unmanaged elevation**: All file elevations that happen without use of Endpoint Privilege Management. These elevations can happen when a user with administrative rights uses the Windows default action of *Run as administrator*.

## EPM Policies

Endpoint Privilege Management uses two policy types that you configure to manage how a file elevation request is handled. Together, the policies configure the behavior for file elevations when standard users request to *run with administrative privileges*.

### About Windows elevation settings policy

Use *Windows elevation settings policy* when you want to:

- **Enable Endpoint Privilege Management** on devices. By default, this policy enables EPM. When first enabled for EPM, a device provisions the components that collect usage data on elevation requests and that enforce elevation rules.

  If a device has EPM disabled, the client components immediately disable. There's a delay of seven days before the EPM component is completely removed. The delay helps to reduce the time it takes to restore EPM should a device accidentally have EPM disabled or its elevation settings policy unassigned.

- **Default elevation response** - Set a default response for an *elevation request* of any file that isn't managed by a *Windows elevation rule policy*. For this setting to have an effect, no rule can exist for the application **AND** an end user must *explicitly request* elevation through the *Run with elevated access* right-click menu. By default, this option is set to *Not Configured*. If not setting is configured, the EPM components fall back to their built-in default, which is to **deny all requests**.

  Options include:

  - **Deny all requests** - This option blocks the *elevate request* action for files that aren't defined in a *Windows elevation rules policy*.
  - **Require user confirmation** - When user confirmation is required, you can choose from the same validation options as found for Windows elevation rules policy.

    - **Validation options** - Set validation options when the default elevation response is defined as *Require user confirmation*. Options include:
      - **Business justification** - This option requires the end user to provide a justification before completing an elevation that is facilitated by the default elevation response.
      - **Windows authentication** - This option requires the end user to authenticate before completing an elevation that is facilitated by the default elevation response.

     >[!NOTE]
     > Multiple validation options can be selected to satisfy the needs of the organization. If no options are selected, then the user is only required to select *continue* to complete the elevation.

  - **Require support approval** - When support approval is required, an administrator must approve elevation requests without a matching rule prior to the elevation being required.

  > [!TIP]  
  > We [recommend use of *Support Approved*](../protect/epm-overview.md#set-a-secure-default-elevation-response) as a default elevation response.

  > [!NOTE]  
  > Default responses are only processed for requests coming through the *Run with elevated access* right-click menu.

- **Send elevation data for reporting** - This setting controls whether your device shares diagnostic and usage data with Microsoft. When enabled to share data, the type of data is configured by the *Reporting scope* setting.

  Diagnostic data is used by Microsoft to measure the health of the EPM client components. Usage data is used to show you elevations that happen within your tenant. For more information about the types of data and how it's stored, see [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md).

  Options include:

  - **Yes** - This option sends data to Microsoft based on the *Reporting Scope* setting.
  - **No** - This option doesn't send data to Microsoft.

- **Reporting Scope** - This setting controls the amount of data being sent to Microsoft when *Send elevation data for reporting* is set to *Yes*. By default, *Diagnostic data and all endpoint elevations are selected.

  Options include:

  - **Diagnostic data and managed elevations only** - This option sends diagnostic data to Microsoft about the health of the client components **AND** data about elevations being facilitated by Endpoint Privilege Management.
  - **Diagnostic data and all endpoint elevations** - This option sends diagnostic data to Microsoft about the health of the client components **AND** data about *all* elevations happening on the endpoint.
  - **Diagnostic data only** - This option sends only the diagnostic data to Microsoft about the health of the client components.

### About Windows elevation rules policy

Use profiles for *Windows elevation rules policy* to manage the identification of specific files, and how elevation requests for those files are handled. Each *Windows elevation rule policy* includes one or more *elevation rules*. It's with elevation rules that you configure details about the file being managed and requirements for it to be elevated.

The following types of files are supported:

- Executable files with the `.exe` or `.msi` extension.
- PowerShell scripts with the `.ps1` extension.

Each elevation rule instructs EPM on how to:

- **Identify the file using**:

  - *File name (including extension).* The rule also supports optional conditions like a minimum build version, product name, or internal name. Optional conditions are used to further validate the file when elevation is attempted. The file name (excluding extensions) can include use of [variables](#use-variables-in-elevation-rules) for single characters through use of a question mark `?` or strings through use of an asterisk `*`.
  - *Certificate.* Certificates can be added directly to a rule, or by using a reusable settings group. When a certificate is used in a rule, it's also required to be valid. We recommend the use of reusable settings groups as they can be more efficient and simplify a future change to the certificate. For more information, see the next section [Reusable settings groups](#reusable-settings-group).

- **Validate the file**:

  - *File hash.* A file hash is required for automatic rules. For user confirmed rules, you can choose to either use a certificate or a file hash, in which case the file hash becomes optional.
  - *Certificate.* If a certificate is provided Windows APIs are used to validate the certificate and revocation status.
  - *Additional Properties.* Any additional properties specified in the rules must match.

- **Configure the files elevation type.** Elevation type identifies what happens when an elevation request is made for the file. By default, this option is set to *User confirmed*, which is our recommendation for elevations.

  - **User confirmed** (Recommended): A user confirmed elevation always requires the user to select on a confirmation prompt to run the file. There are more user confirmations you can add. One requires users to authenticate using their organization credentials. Another option requires the user to enter a business justification. While the text entered for a justification is up to the user, EPM can collect and report it when the device is configured to report elevation data as part of its Windows elevation settings policy.
  - **Automatic**: An automatic elevation happens invisibly to the user. There's no prompt, and no indication that the file is running in an elevated context.
  - **Deny**: Deny rules prevent the identified file from being run in an elevated context.
  - **Support approved**: An administrator must approve any [support-required elevation request](../protect/epm-support-approved.md) that doesn't have a matching rule, before the application is allowed to run with elevated privileges.

- **Manage the behavior of child processes.** You can set the elevation behavior that applies to any child processes that the elevated process creates.

  - **Require rule to elevate** - Configure a child processes to require its own rule before that child process can run in an elevated context.
  - **Deny all** - All child processes launch without elevated context.
  - **Allow child processes to run elevated** - Configure a child process to always run elevated.

> [!NOTE]
> For more information about creating *strong rules*, see our [guidance for creating elevation rules with Endpoint Privilege Management](../protect/epm-guidance-for-creating-rules.md).
>
> You can also use the `Get-FileAttributes` PowerShell cmdlet from the [EpmTools PowerShell module](../protect/epm-overview.md#epmtools-powershell-module). This cmdlet can retrieve file attributes for an .exe file and extract its Publisher and CA certificates to a set location that you can use to populate Elevation Rule Properties for a particular application.

> [!CAUTION]
>
> We recommend automatic elevation be used sparingly, and only for trusted files that are business critical. End users automatically elevate these applications at *every* launch of that application.

### Reusable settings group - publisher certificates

Endpoint Privilege Management supports using reusable settings groups to manage the certificates in place of adding that certificate directly to an elevation rule. Like all reusable settings groups for Intune, configurations and changes made to a reusable settings group are automatically passed to the policies that reference the group.
We recommend using a reusable settings group when you plan to use the same certificate to validate files in multiple elevation rules. The use of reusable settings groups is more efficient when you use the same certificate in multiple elevation rules:

- Certificates you add directly to an elevation rule: Each certificate that's added directly to a rule is uploaded as a unique instance by Intune, and that certificate instance is then associated with that rule. Adding the same certificate directly to two separate rules results in it uploading twice. Later, if you must change the certificate, you must edit each individual rule that contains it. With each rule change, Intune uploads the updated certificate a single time for each rule.
- Certificates you manage through a reusable settings group: Each time a certificate is added to a reusable settings group, Intune uploads the certificate a single time no matter how many elevation rules include that group. That instance of the certificate is then associated with the file from each rule that uses that group. Later, any change to the certificate you make can be made a single time in the reusable settings group. This change results in Intune uploading the updated file a single time, and then applying that change to each elevation rule that references the group.

## Policy conflict handling for Endpoint Privilege Management

Except for the following situations, conflicting policies for EPM are handled like any other [policy conflict](../configuration/device-profile-troubleshoot.md#conflicts).

**Windows elevation settings policy**:

When a device receives two separate elevation settings policies with conflicting values, the EPM client reverts to the default client behavior until the conflict is resolved.

> [!NOTE]
>
> If *Enable Endpoint Privilege Management* is in conflict, the default behavior of the client is to *Enable* EPM. This means the client components continue to function until an explicit value is delivered to the device.

**Windows elevation rules policy**:

If a device receives two rules targeting the same application, both rules are consumed on the device. When EPM goes to resolve rules that apply to an elevation, it uses the following logic:

- Rules with an *elevation type* of *Deny* always take precedence, and the file elevation is denied.
- Rules deployed to a user take precedence over rules deployed to a device.
- Rules with a hash defined are always deemed the most *specific* rule.
- If more than one rule applies (with no hash defined), the rule with the most defined attributes wins (most *specific*).
- If applying the proceeding logic results in more than one rule, the following order determines the elevation behavior: User Confirmed, Support Approved, and then Automatic.

> [!NOTE]
> If a rule does not exist for an elevation and that elevation was requested through the *Run with elevated access* right-click context menu, then the *Default Elevation Behavior* is used.

## Security recommendations

To help ensure a secure deployment of Endpoint Privilege Management, consider these recommendations when configuring elevation behavior and rules:

### Set a secure default elevation response

Set the [default elevation response](../protect/epm-plan.md#about-windows-elevation-settings-policy) to **Support Approval** or **Deny** rather than **User Confirmed**. This ensures that elevation is governed by predefined rules for known binaries, reducing the risk of users elevating arbitrary or potentially malicious executables.

### Require file path restrictions in all rule types

When [configuring an elevation rule](../protect/epm-plan.md#windows-elevation-rules-policy), specify a required **File path**. While the *file path* is optional, it can be an important security check for rules that leverage automatic elevation or wildcard-based attributes when the path points to a location that standard users can't modify, such as a secured system directory. Use of a secured file location helps prevent executables or their dependent binaries from being tampered with or replaced prior to elevation.

This recommendation applies to rules created [automatically](../protect/epm-deploy-create-rules.md#automatically-configure-elevation-rules-for-windows-elevation-rules-policy) based on details from the [Elevation report](../protect/epm-reports.md) or [support approved](../protect/epm-support-approved.md) request, and for elevation rules that you create [manually](../protect/epm-deploy-create-rules.md#manually-configure-elevation-rules-for-windows-elevation-rules-policy).

> [!IMPORTANT]  
> Files located on network shares aren't supported and shouldn't be used in rule definitions.

### Differentiate installer and runtime elevation

Be intentional about elevation for installer files versus application runtime. Elevation for installers should be tightly controlled to prevent unauthorized software installations. Runtime elevation should be minimized to reduce the overall attack surface.

### Apply stricter rules to high-risk applications

Use more restrictive elevation rules for applications with broader access or scripting capabilities, such as web browsers and PowerShell. For PowerShell, consider using script-specific rules to ensure only trusted scripts are allowed to run with elevated privileges.

## Role-based access controls for Endpoint Privilege Management

To manage Endpoint Privilege Management, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permission with sufficient rights to complete the desired task:

- **Endpoint Privilege Management Policy Authoring** – This permission is required to work with policy or data and reports for Endpoint Privilege Management, and supports the following rights:
  - View Reports
  - Read
  - Create
  - Update
  - Delete
  - Assign

- **Endpoint Privilege Management Elevation Requests** - This permission is required to work with support approved elevation requests that are submitted by users for approval, and supports the following rights:
  - View elevation requests
  - Modify elevation requests

You can add this permission with one or more rights to your own custom RBAC roles, or use a built-in RBAC role dedicated to managing Endpoint Privilege Management:

- **Endpoint Privilege Manager** – This built-in role is dedicated to managing Endpoint Privilege Management in the Intune console. This role includes all rights for *Endpoint Privilege Management Policy Authoring* and *Endpoint Privilege Management Elevation Requests*.

- **Endpoint Privilege Reader** - Use this built-in role to view Endpoint Privilege Management policies in the Intune console, including reports. This role includes the following rights:
  - View Reports
  - Read
  - View elevation requests

In addition to the dedicated roles, the following built-in roles for Intune also include rights for *Endpoint Privilege Management Policy Authoring*:

- **Endpoint Security Manager** - This role includes all rights for *Endpoint Privilege Management Policy Authoring* and *Endpoint Privilege Management Elevation Requests*.

- **Read Only Operator** - This role includes the following rights:
  - View Reports
  - Read
  - View elevation requests

 For more information, see [Role-based access control for Microsoft Intune](../fundamentals/role-based-access-control.md).

## EpmTools PowerShell module

Each device that receives Endpoint Privilege Management policies installs the EPM Microsoft Agent to manage those policies. The agent includes the *EpmTools* PowerShell module, a set of cmdlets that you can import to a device. You can use the cmdlets from EpmTools to:

- Diagnose and troubleshoot issues with Endpoint Privilege Management. 
- Get File attributes directly from a file or application for which you want to build a detection rule.

### Install the EpmTools PowerShell module

The EPM Tools PowerShell module is available from any device that has received EPM policy. To import the EpmTools PowerShell module:

```powershell
Import-Module 'C:\Program Files\Microsoft EPM Agent\EpmTools\EpmCmdlets.dll'
```

> [!NOTE]
> Windows on Arm64 requires the use of Windows PowerShell x64.

Following are the available cmdlets:

- **Get-Policies**: Retrieves a list of all policies received by the Epm Agent for a given PolicyType (ElevationRules, ClientSettings).
- **Get-DeclaredConfiguration**: Retrieves a list of WinDC documents that identify the policies targeted to the device.
- **Get-DeclaredConfigurationAnalysis**: Retrieves a list of WinDC documents of type MSFTPolicies and checks if the policy is already present in Epm Agent (Processed column).
- **Get-ElevationRules**: Query the EpmAgent lookup functionality and retrieves rules given lookup and target. Lookup is supported for FileName and CertificatePayload.
- **Get-ClientSettings**: Process all existing client settings policies to display the effective client settings used by the EPM Agent.
- **Get-FileAttributes**: Retrieves File Attributes for an .exe file and extracts its Publisher and CA certificates to a set location that can be used to populate Elevation Rule Properties for a particular application.

For more information about each cmdlet, review the **readme.md** file from the *EpmTools* folder on the device.

## Next Steps

> [!div class="nextstepaction"]
> [Next: Review privacy data collection >](epm-data-collection.md)
