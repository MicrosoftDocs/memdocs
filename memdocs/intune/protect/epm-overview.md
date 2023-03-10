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
> This capability is in public preview, and free to try and use. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

With Endpoint Privilege Management (EPM), your organization’s users can run as standard users, yet complete tasks requiring elevation of user rights, like installing Office 365, updating device drivers, and running Task Manager or Windows diagnostics. Through integration with Microsoft Intune, EPM can help you to secure your organization by removing administrative permissions for most users.

To use EPM, you create elevation rules that identify files that can be run in an elevated context by standard users. Your rules:

- Include conditions for user interaction before allowing the file to run or allow a file to run elevated but invisibly to the user, keeping them in their workflow without disruption.
- Define a default behavior for the elevation of files that are not yet managed by a dedicated rule.
- Can use certificates to help validate the integrity of a file before allowing it to run.
 
EPM can also report back on the elevation of files, including which files were  elevated by users outside the EPM workflow by users who retain permissions to do so. This information can help you tune your EPM policies, which can help you further improve security for your organization.

The following sections of this article discuss requirements to use EPM, provide a functional overview of how the capability works, and introduces important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

## Architecture and work flows 


## Prerequisites

The following sections detail the requirements to use Endpoint Privilege Management with your Intune Tenant:

### Licensing

During the public preview, there are no licensing requirements to use Endpoint Privilege Management. After the preview ends, your tenant must be licensed for Endpoint Privilege Management, which requires purchase of an [Intune Suite add-on]( fundamentals/intune-add-ons.md) that includes Endpoint Privilege Management.

### Windows 10 and Windows 11 devices

To use EPM policy, devices must:

- Be enrolled with Microsoft Intune
- Run Windows 10 or Windows 11
- Have installed the March 2023 optional release for Windows

### Role-based access control requirements

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

## About EPM Policies

EPM uses two policy types that you configure and deploy to groups of users or devices. If you'll use certificates to validate file integrity, you can choose to add the certificate directly to a policy or add them to a [reusable settings group](../protect/reusable-settings-groups.md) that you then assign to one or more policies. Use of reusable settings groups can help you manage changes to a certificate, with any changes made to a certificate in a reusable group automatically being applied to the policies that include the group.

For guidance on how to configure the policies and reusable settings group, see [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md).

### Windows elevation settings policy

EPM uses the *Windows elevation settings policy* to configure the following on devices:

- Enable Endpoint Privilege Management on the device. When disabled, EPM elevation rules and settings are not processed by a device.
- Set a default evaluation response that applies when users invoke the *Elevate request* action of a file that’s not managed by a *Windows elevation rule policy*. Default responses can deny the request, require user confirmation using the same options available in an elevation rule, or be left unconfigured.
- Specify the type of information that Endpoint Privilege Management reports back from a device. You can choose between:
  - Not reporting any data.
  - Reporting only diagnostic data.
  - Reporting diagnostic data and all endpoint elevations, which are file elevations managed by a Windows elevation rules policy.
  - Reporting diagnostic data and all elevations, which includes those managed by a rules policy as well any *Elevate request* for a file not managed by elevation rules.





### Windows elevation rules policy

### Reusable settings group



## Important concepts for Endpoint Privilege Management

The following points summarize some key concepts for Endpoint Privilege Management.

- **File elevation** – The act of a file being run in an administrative context. When you use Endpoint Privilege Management, there are two options for this to occur:
  - By default, on  a Windows device you can right-click on the properties of a file and select **Run as administrator**.
  - For devices that are enabled for Endpoint Privilege Management, a second option appears, **Elevate request**. When this option is used, the devices elevation rules policies are checked for a match to determine if, and how, that file can be elevated to run in an administrative context. If there's no applicable elevation rule, then the device uses the default elevation configurations as defined by the elevation settings policy.

- **Elevation type** – Elevation type is how a rule is configured to manage the running the file defined by the rule. Elevation can be silent when configured as automatic, or can require user confirmation. We recommend automatic elevation only for trusted files that are business critical. Examples include a common printer-driver which users are expected to install, or a productivity app like the setup file for Microsoft Office 365.

  When user confirmation is required, the user will always experience a basic prompt to *Continue* with running the file in an elevated context, or to *Cancel*. In addition to the simple prompt, policies can require the user to enter a business justification, authenticate using their organizations credentials, or both.

- **What happens when an Administrator runs a file protected by Endpoint Privilege Management** – Endpoint Privilege Management doesn’t manage elevation requests by users that have administrative permissions on a device. This applies whether the administrative user selects an option to run a file in an elevated context, or simple runs the file, relying on their current permissions to be sufficient to do so.

- **Client-side component** – To use Endpoint Privilege Management, Windows devices install a component that is provisioned when the device receives a Windows elevation settings policy. While the component is installed when the policy is received, it activates only when the device has a settings policy set to enable Endpoint Privilege Management.

- **Disable vs Deprovision** – As a component that installs on a device, Endpoint Privilege Management can be disabled from within an elevation settings policy. However, so long as the policy applies to a device, Endpoint Privilege Management remains provisioned.

  If a device no longer had an elevation settings policy, Intune deprovisions the device by removing the client component after a period of seven days. This delay is to ensure temporary or accidental changes in policy or assignments doesn’t result in the need to reprovision the Endpoint Privilege Management components on a device.

- **Managed elevations vs unmanaged elevations** – When classifying how a file is elevated, Endpoint Privilege Management classifies and reports on the process to elevate the permissions of a file that is run, as follows:
  - **Managed elevation**: Any file elevation that is managed by Endpoint Privilege Management. Elevation can be by the direct run of a file that’s protected by an elevation  rule, or use of the *Elevate request* option that’s available to devices enabled to use Endpoint Privilege Management.
  - **Unmanaged elevation**: All file elevations that happen without use of Endpoint Privilege Management. This can happen when a user with administrative rights uses the Windows default action of *Run as administrator*.




## Next steps
[Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)