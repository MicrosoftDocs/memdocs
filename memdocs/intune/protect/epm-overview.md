---
title: Learn about using Endpoint Privilege Management with Microsoft Intune
description: To enhance the security of your organization, set your users to run with standard permissions while Endpoint Privilege Management ensures those users can seamlessly run specified files with elevated rights. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/01/2024
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
- sub-intune-suite
---

# Use Endpoint Privilege Management with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your [Zero Trust](/security/zero-trust/zero-trust-overview) journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive. For more information, see [Zero Trust with Microsoft Intune](../fundamentals/zero-trust-with-microsoft-intune.md).

The following sections of this article discuss requirements to use EPM, provide a functional overview of how this capability works, and introduce important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

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

- Windows 11, version 23H2 (22631.2506 or later) with [KB5031455](https://support.microsoft.com/topic/october-31-2023-kb5031455-os-builds-22621-2506-and-22631-2506-preview-6513c5ec-c5a2-4aaf-97f5-44c13d29e0d4)
- Windows 11, version 22H2 (22621.2215 or later) with [KB5029351](https://support.microsoft.com/topic/august-22-2023-kb5029351-os-build-22621-2215-preview-9af25662-083a-43f5-b3a7-975fe25cc692)
- Windows 11, version 21H2 (22000.2713 or later) with [KB5034121](https://support.microsoft.com/topic/january-9-2024-kb5034121-os-build-22000-2713-f5847e32-0b71-4151-8190-54d3e36386f0)
- Windows 10, version 22H2 (19045.3393 or later) with [KB5030211](https://support.microsoft.com/topic/september-12-2023-kb5030211-os-builds-19044-3448-and-19045-3448-c0dee353-f025-4f03-bcc1-336f74fb992c)
- Windows 10, version 21H2 (19044.3393 or later) with [KB5030211](https://support.microsoft.com/topic/september-12-2023-kb5030211-os-builds-19044-3448-and-19045-3448-c0dee353-f025-4f03-bcc1-336f74fb992c)

> [!IMPORTANT]
>
> - Elevation settings policy will show as not applicable for devices that don't run a supported operating system version.
> - Endpoint Privilege Management has some new networking requirements, see [Network Endpoints for Intune](../../intune/fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management).

## Government cloud support

Endpoint Privilege Management is supported with the following sovereign cloud environments:

- U.S. Government Community Cloud (GCC) High
- U.S. Department of Defense (DoD)

For more information, see [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md).

## Getting started with Endpoint Privilege Management

Endpoint Privilege Management (EPM) is built into Microsoft Intune, which means that all configuration is completed within the [Microsoft Intune Admin Center](https://intune.microsoft.com). When organizations get started with EPM, they use the following high-level process:

- **License Endpoint Privilege Management** - Before you can use Endpoint Privilege Management policies, you must license EPM in your tenant as an Intune add-on. For licensing information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

- **Deploy an *elevation settings* policy** - An elevation settings policy *activates* EPM on the client device. This policy also allows you to configure settings that are specific to the client but aren't necessarily related to the elevation of individual applications or tasks.
- **Deploy *elevation rule* policies** - An elevation rule policy *links* an application or task to an elevation action. Use this policy to configure the elevation behavior for applications your organization allows when the applications run on the device.

## Important concepts for Endpoint Privilege Management

When you configure the *elevation settings* and *elevation rules* policies that were mentioned previously, there are some important concepts to understand ensuring you configure EPM to meet the needs of your organization. Before you widely deploy EPM, the following concepts should be well understood as well as the effect they have on your environment:

- **Run with elevated access** - A right-click context menu option that appears when EPM is activated on a device. When this option is used, the devices elevation rules policies are checked for a match to determine if, and how, that file can be elevated to run in an administrative context. If there's no applicable elevation rule, then the device uses the default elevation configurations as defined by the elevation settings policy.

- **File elevation and elevation types** – EPM allows users without administrative privileges to run processes in the administrative context. When you create an elevation rule, that rule allows EPM to proxy the target of that rule to run with administrator privileges on the device. The result is that the application has *full administrative* capability on the device.

  When you use Endpoint Privilege Management, there are a few options for elevation behavior:

  - For automatic elevation rules, EPM *automatically* elevates these applications without input from the user. Broad rules in this category can have widespread impact to the security posture of the organization.
  - For user confirmed rules, end users use a new right-click context menu *Run with elevated access*. User confirmed rules require the end-user to complete some additional requirements before the application is allowed to elevate. These requirements provide an extra layer of protection by making the user acknowledge that the app will run in an elevated context, before that elevation occurs.
  - For support approved rules, end users must submit a request to approve an application. Once the request is submitted, an administrator can approve the request. Once the request is approved, the end user is notified that they can complete the elevation on the device. For more information about using this rule type, see [Support approved elevation requests](../protect/epm-support-approved.md)

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

## Role-based access controls for Endpoint Privilege Management

To manage Endpoint Privilege Management, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permission with sufficient rights to complete the desired task:

- **Endpoint Privilege Management Policy Authoring** – This permission is required to work with policy or data and reports for Endpoint Privilege Management, and supports the following rights:
  - View Reports
  - Read
  - Create
  - Update
  - Delete
  - Assign

- **Endpoint Privilege Management Elevation Requests** - This permission is required to work with elevation requests that are submitted by users for approval, and supports the following rights:
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

Following are the available cmdlets:

- **Get-Policies**: Retrieves a list of all policies received by the Epm Agent for a given PolicyType (ElevationRules, ClientSettings).
- **Get-DeclaredConfiguration**: Retrieves a list of WinDC documents that identify the policies targeted to the device.
- **Get-DeclaredConfigurationAnalysis**: Retrieves a list of WinDC documents of type MSFTPolicies and checks if the policy is already present in Epm Agent (Processed column).
- **Get-ElevationRules**: Query the EpmAgent lookup functionality and retrieves rules given lookup and target. Lookup is supported for FileName and CertificatePayload.
- **Get-ClientSettings**: Process all existing client settings policies to display the effective client settings used by the EPM Agent.
- **Get-FileAttributes**: Retrieves File Attributes for a .exe file and extracts its Publisher and CA certificates to a set location that can be used to populate Elevation Rule Properties for a particular application.

For more information about each cmdlet, review the **readme.txt** file from the *EpmTools* folder on the device.

## Next steps

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Approving elevation requests](../protect/epm-support-approved.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
