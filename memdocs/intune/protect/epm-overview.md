---
title: Learn about using Endpoint Privilege Management with Microsoft Intune
description: To enhance the security of your organization, set your users to run with standard permissions while Endpoint Privilege Management ensures those users can seamlessly run specified files with elevated rights. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/07/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

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

# Use Endpoint Privilege Management with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges.

Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your [Zero Trust](/security/zero-trust/zero-trust-overview) journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive. For more information, see [Zero Trust with Microsoft Intune](../fundamentals/zero-trust-with-microsoft-intune.md)

The following sections of this article discuss requirements to use EPM, provide a functional overview of how this capability works, and introduce important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

## Prerequisites

### Licensing

Endpoint Privilege Management requires an additional license beyond the *Microsoft Intune Plan 1* license. You can choose between an stand-alone license that adds only EPM, or license EPM as part of the Microsoft Intune Suite. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

### Windows Client requirements

Endpoint Privilege Management has the following operating system requirements:

- Windows 11, version 22H2 (22621.1344 or later) with [KB5022913](https://support.microsoft.com/en-us/topic/february-28-2023-kb5022913-os-build-22621-1344-preview-3e38c0d9-924d-4f3f-b0b6-3bd49b2657b9)
- Windows 11, version 21H2 (22000.1761 or later) with [KB5023774](https://support.microsoft.com/en-us/topic/march-28-2023-kb5023774-os-build-22000-1761-preview-67b4cfda-120a-422f-98c0-35124ddba839)
- Windows 10, version 22H2 (19045.2788 or later) with [KB5023773](https://support.microsoft.com/en-us/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23)
- Windows 10, version 21H2 (19044.2788 or later) with [KB5023773](https://support.microsoft.com/en-us/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23)
- Windows 10, version 20H2 (19042.2788 or later) with [KB5023773](https://support.microsoft.com/en-us/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23)

> [!IMPORTANT]
> Elevation settings policy will show as not applicable if a device is not at the minimum version specified above.
>
> Endpoint Privilege Management has some new networking requirements, see [Network Endpoints for Intune](../../intune/fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management).
>
> Endpoint Privilege Management has some new networking requirements, see [Network Endpoints for Intune](../../intune/fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management).
>
> Only devices with a Hybrid Azure Active Directory join or Azure Active Directory join are supported. Workplace join is not a supported trust type.
> Devices can be either Intune managed or [co-managed](https://learn.microsoft.com/mem/configmgr/comanage/overview)

## Getting started with Endpoint Privilege Management

Endpoint Privilege Management (EPM) is built into Microsoft Intune, which means that all configuration is completed within the [Microsoft Intune Admin Center](https://intune.microsoft.com). When organizations get started with EPM, they use the high-level process that's outlined as follows:

- **License Endpoint Privilege Management** - Before you can use Endpoint Privilege Management policies, you must license EPM in your tenant as an Intune add-on. For licensing information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

- **Deploy an *elevation settings* policy** - An elevation settings policy *activates* EPM on the client device. This policy also allows you to configure settings that are specific to the client but aren't necessarily related to the elevation of individual applications or tasks.
- **Deploy *elevation rule* policies** - An elevation rule policy *links* an application or task to an elevation action. Use this policy to configure the elevation behavior for applications your organization allows when the applications run on the device.

## Important concepts for Endpoint Privilege Management

When you configure the *elevation settings* and *elevation rules* policies mentioned previously, there are some important concepts that should be understood to ensure you configure EPM to meet the needs of your organization. Before you widely deploy EPM, the following concepts should be well understood as well as the impact they have on your environment:

- **Run with elevated access** - A right-click context menu option that appears when EPM is activated on a device. When this option is used, the devices elevation rules policies are checked for a match to determine if, and how, that file can be elevated to run in an administrative context. If there's no applicable elevation rule, then the device uses the default elevation configurations as defined by the elevation settings policy.

- **File elevation and elevation types** – EPM allows users without administrative privileges to run processes in the administrative context. When you create an elevation rule, that rule allows EPM to proxy the target of that rule to run with administrator privileges on the device. The result is that the application has *full administrative* capability on the device.

  When you use Endpoint Privilege Management, there are two options for elevation behavior:
  - For automatic elevation rules, EPM *automatically* elevates these applications without input from the user. Broad rules in this category can have widespread impact to the security posture of the organization.
  - For user confirmed rules, end users use a new right-click context menu *Run with elevated access*. User confirmed rules require the end-user to complete some additional requirements before the application is allowed to elevate. These requirements provide an extra layer of protection by making the user acknowledge that the app will run in an elevated context, before that elevation occurs.

- **Client-side components** – To use Endpoint Privilege Management, Intune provisions a small set of components on the device that receive elevation policies and enforces them. The components are provisioned only when an elevation settings policy is received, and the policy has expressed the intent to *enable* Endpoint Privilege management.

- **Disabling and deprovisioning** – As a component that installs on a device, Endpoint Privilege Management can be disabled from within an elevation settings policy. Use of the elevation settings policy is **required** to remove Endpoint Privilege Management from a device.

  Once the device has received an elevation settings policy requiring EPM to be disabled, Intune immediately disables the client-side components. EPM will remove the EPM component after a period of seven days. The delay is to ensure temporary or accidental changes in policy or assignments don't result in mass *de-provisioning*/*re-provisioning* events that might have a substantial impact on business operations.

- **Managed elevations vs unmanaged elevations** – These terms might be used in our reporting and usage data. These terms refer to the following descriptions:
  - **Managed elevation**: Any elevation that Endpoint Privilege Management facilitates. Managed elevations include all elevations that EPM ends up facilitating for the standard user. This could include elevations that happen as the result of an elevation rule or as part of default elevation action.
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

You can add this permission with one or more rights to your own custom RBAC roles, or use a built-in RBAC role dedicated to managing Endpoint Privilege Management:

- **Endpoint Privilege Manager** – This built-in role is dedicated to managing Endpoint Privilege Management in the Intune console. This role includes all rights for *Endpoint Privilege Management Policy Authoring*.

- **Endpoint Privilege Reader** - Use this built-in role to view Endpoint Privilege Management policies in the Intune console, including reports. This role includes the following rights for *Endpoint Privilege Management Policy Authoring*:
  - View Reports
  - Read

In addition to the dedicated roles, the following built-in roles for Intune also include rights for *Endpoint Privilege Management Policy Authoring*:

- **Endpoint Security Manager** - This role includes all rights for *Endpoint Privilege Management Policy Authoring*.

- **Read Only Operator** - This role includes the following rights for *Endpoint Privilege Management Policy Authoring*:
  - View Reports
  - Read

 For more information, see [Role-based access control for Microsoft Intune](../fundamentals/role-based-access-control.md).

## Next steps

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-policies.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)

