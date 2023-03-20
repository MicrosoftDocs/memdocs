---
title: Learn about using Endpoint Privilege Management with Microsoft Intune
description: To enhance the security of your organization, set your users to run with standard permissions while Endpoint Privilege Management ensures those users can seamlessly run specified files with elevated rights. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2023
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

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->
> [!NOTE]  
> This capability is in public preview and available to use without a license. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges.

Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The following sections of this article discuss requirements to use EPM, provide a functional overview of how this capability works, and introduce important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

## Prerequisites

### Licensing

During the public preview, EPM will not require acquiring or provisioning a license. Instead, you can [activate EPM](../protect/epm-policies.md#enable-your-tenant-for-endpoint-privilege-management) and validate the functionality.

Once the product becomes generally available, your tenant must be licensed for Endpoint Privilege Management. This license is available as an part of the [Intune Suite or as a standalone license](../fundamentals/intune-add-ons.md).

### Windows Client requirements

Endpoint privilege management has the following operating system requirements:

- Windows 11, version 22H2 with [KB5022913](https://support.microsoft.com/en-us/topic/february-28-2023-kb5022913-os-build-22621-1344-preview-3e38c0d9-924d-4f3f-b0b6-3bd49b2657b9)
- Windows 11, version 22H1 with KB5023774 (Pending Optional Update Release - March 2023)
- Windows 10, version 20H2 (or later) with KB5023773 (Pending Optional Update Release - March 2023)

> [!IMPORTANT]
> Only devices with a Hybrid Azure Active Directory join or Azure Active Directory join are supported. Workplace join is not a supported trust type.

## Getting started with Endpoint Privilege Management

Endpoint Privilege Management (EPM) is built-in to Microsoft Intune, which means that all configuration is completed within the [Microsoft Intune Admin Center](https://intune.microsoft.com). When organizations get started with EPM, they use the high level process that's outlined as follows:

- **Activate Endpoint Privilege Management** - Public Preview customers are not be required to obtain a license for Endpoint Privilege Management to try out the product. Instead, they activate the product by navigating to the Endpoint Privilege Management node and having a *Global Administrator* or *Intune Service Admin* activate the product experience.
- **Deploy an *elevation settings* policy** - An elevation settings policy *activates* EPM on the client device. This also allows you to configure settings that are specific to the client, but aren't necessarily related to the elevation of individual applications or tasks.
- **Deploy *elevation rule* policies** - An elevation rule policy *links* an application or task to an elevation action. This allows you to configure the elevation behavior for applications your organization allows, when the applications execute on the device.

## Important concepts for Endpoint Privilege Management

When you configure the *elevation settings* and *elevation rules* policies mentioned previously, there are some important concepts that should be understood to ensure you configure EPM to meet the needs of your organization. Before you widely deploy EPM, the following concepts should be well understood as well as the impact they have on your environment:

- **Run with elevated access** - This is a right-click context menu that appears when EPM is activated on a device. When this option is used, the devices elevation rules policies are checked for a match to determine if, and how, that file can be elevated to run in an administrative context. If there's no applicable elevation rule, then the device uses the default elevation configuration as defined by the elevation settings policy.

- **File elevation and elevation types** – EPM allows users without administrative privileges to run processes in the administrative context. When you create an elevation rule, that rule allows EPM facilitate the target of that rule to run with administrator privileges on the device. This means the application has *full administrative* capability on the device.

  When you use Endpoint Privilege Management, there are two options for this to occur:
  - For **automatic elevation** rules, EPM *automatically* elevates these applications without input from the user. Broad rules in this category can have wide spread impact to the security posture of the organization.
  - For **user confirmed** rules, end users leverage a new right-click context menu *Run with elevated access*. User confirmed rules require the end-user to complete some additional requirements before the application is allowed to elevate. This provides an additional layer of protection by providing visibility to the end user on the application prior to elevation and requires them to complete some additional steps before the elevation occurs.

- **Client-side components** – To use Endpoint Privilege Management, Intune provisions a small set of components on the device that receive elevation policies and enforces them. The components are provisioned only when a elevation settings policy is received and the policy has expressed the intent to *enable* Endpoint Privilege management.

- **Disabling and deprovisioning** – As a component that on the device, Endpoint Privilege Management can be disabled from within an elevation settings policy. This is **required** to remove Endpoint Privilege Management from a device.

  Once the device has received an elevation settings policy requiring EPM to be disabled, Intune immediately disables the client side components. The EPM component will be removed **after** a period of seven days. This delay is to ensure temporary or accidental changes in policy or assignments do not result in mass *de-provisioning*/*re-provisioning* events that might have a substantial impact on business operations.

- **Managed elevations vs unmanaged elevations** – These terms might be used in our reporting and usage data. Generally speaking these terms refer to the following descriptions:
  - **Managed elevation**: Any elevation that Endpoint Privilege Management facilitates. This includes all elevations that EPM ends up facilitating for the standard user. This could include elevations that happen as the result of an elevation rule or as part of default elevation action.
  - **Unmanaged elevation**: All elevations initiated by the end user that happen without use of Endpoint Privilege Management. This can happen when a user with administrative rights uses the Windows default action of *Run as administrator*.

## Role-based access controls for Endpoint Privilege Management

To manage Endpoint Privilege Management, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permission with sufficient rights to complete the desired task:

- **Endpoint Privilege Management Policy Authoring** – This permission is required to manage required to work with policy or data and reports for Endpoint Privilege Management, and supports the following rights:
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
