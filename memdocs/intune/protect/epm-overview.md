---
title: Learn about using Endpoint Privilege Management with Microsoft Intune
description: To enhance the security of your organization, set your users to run with standerd permissions while Endpoint Privilege Management ensures those users can seamlessly run specified files with elevated rights. 
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

Use Endpoint Privilege Management to protect your organization.

To use Endpoint Privilege Management, you’ll configure the following objects that you can deploy to users or devices depending on your need. At a high level:

## Prerequisites

The following are requirements to use Endpoint Privilege Management with your Intune Tenant:

## Role-based access control requirements

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

## Important concepts for Endpoint Privilege Management

The following points summarize some key concepts for Endpoint Privilege Management.

- **File elevation** – The act of a file being run in an administrative context. When you use Endpoint Privilege Management there are two options for this to occur:
  - By default, on  a Windows device you can right-click on the properties of a file and select **Run as administrator**.
  - For devices that are enabled for Endpoint Privilege Management, a second option appears, **Elevate request**. When this option is used, the devices elevation rules policies are checked for a match to determine if, and how, that file can be elevated to run in an administrative context. If there is no applicable elevation rule, then the device uses the default elevation configurations as defined by the elevation settings policy.

- **Elevation type** – This refers to how the device is configured to manage the files elevation request. This can be silent, by being configured to be automatic, or can require user confirmation. We recommend automatic elevation only for trusted files that are business critical. Examples include a common printer-driver which users are expected to install, or a productivity app like the setup file for Microsoft Office 365.

  When user confirmation is required, the user will always experience a simple prompt to *Continue* with running the file in an elevated context, or to *Cancel*. In addition to the simple prompt, policies can require the user to enter a business justification, authenticate using their organizations credentials, or both.

- **What happens when an Administrator runs a file protected by Endpoint Privilege Management** – Endpoint Privilege Management doesn’t manage elevation requests by users that have administrative permissions on a device. This applies whether the administrative user selects an option to run a file in an elevated context, or simple runs the file, relying on their current permissions to be sufficient to do so.

- **Client-side component** – To use Endpoint Privilege Management, Windows devices install a component that is provisioned when the device receives a Windows elevation settings policy. While the component is installed when the policy is received, it activates only when the device has a settings policy set to enable Endpoint Privilege Management.

- **Disable vs Deprovision** – As a component that installs on a device, Endpoint Privilege Management can be disabled from within an elevation settings policy. However, so long as the policy applies to a device, Endpoint Privilege Management remains provisioned.

  If a device no longer had a elevation settings policy, Intune deprovisions the device by removing the client component after a period of seven days. This delay is to ensure temporary or accidental changes in policy or assignments doesn’t result in the need to reprovision the Endpoint Privilege Management components on a device.

- **Managed elevations vs unmanaged elevations** – When classifying how a file is elevated, Endpoint Privilege Management classifies and reports on the process to elevate the permissions of a file that is run, as follows:
  - **Managed elevation**: Any file elevation that is managed by Endpoint Privilege Management. This can be the direct run of a file that’s protected by an elevation  rule, or use of the *Elevate request* option that’s available to devices enabled to use Endpoint Privilege Management.
  - **Unmanaged elevation**: All file elevations that happen without use of Endpoint Privilege Management. This can happen when a user with administrative rights uses the Windows default action of *Run as administrator*.


 
## Next steps
[Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)