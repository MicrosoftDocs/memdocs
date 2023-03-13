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

With Endpoint Privilege Management (EPM), your organization’s users can run as standard users, yet complete tasks that require an elevation of user rights, like installing Office 365, updating device drivers, and running Task Manager or Windows diagnostics. Through integration with Microsoft Intune, EPM supports your zero-trust journey by helping your organization achieve a broad least-privilege user base that doesn't face added barriers to worker productivity.
 
To use EPM, you deploy *Windows elevation settings* and *Windows elevation rule* policies. Elevation settings policies define a default behavior for a device that applies to elevation requests for files not managed by a dedicated rule. Elevation rule policies contain one or more elevation rules, with each rule configuring a file that can be run in an elevated context by non-administrative users. Your elevation rules:

- Include conditions for user interaction before allowing the file to run or allow a file to run elevated but invisibly to the user, keeping them in their workflow without disruption.
- Define a default behavior for the elevation of files that are not yet managed by a dedicated rule.
- Can use certificates to help validate the integrity of a file before allowing it to run.

With these policies in place, a standard rights user can seek to run necessary files in an elevated context. The policies manage how or even if that file is run. File elevation can be silent without any interruption to the user’s workflow or require some level of user interaction before being run in the elevated context. The policies also determine what information is reported back to Intune about elevation requests and can include which files were elevated by users outside the EPM workflow should some users retain permissions to do so. This information can help you tune your EPM policies, which can help you further improve security for your organization.

The following sections of this article discuss requirements to use EPM, provide a functional overview of how this capability works, and introduce important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

## Architecture

*Pending*

## Prerequisites

The following sections detail the requirements to use Endpoint Privilege Management with your Intune Tenant.

### Licensing

During the public preview, there are no licensing requirements to use Endpoint Privilege Management. After the preview ends, your tenant must be licensed for Endpoint Privilege Management, which requires purchase of an [Intune Suite add-on](../fundamentals/intune-add-ons.md) that includes Endpoint Privilege Management.

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

EPM uses the two policy types that you configure to manage how a file elevation request is handled. Together, the policies set the conditions for managed files and unmanaged files. Managed files are defined by elevation rules while unmanaged files are all other files.

**Elevate requests**:  
After EPM is enabled on a device, each file on the device includes a new right-click option for running files in an elevated context: *Elevate request*. *Elevate request* is in addition to *Run as administrator* which always remains available. To run a file in an elevated context, a standard user must select the *Elevate request* options:

- When a standard uses selects *Elevate request* option, the devices EPM rules evaluate the file and apply conditions to that request. For a standard user, the *Run as administrator* option will not work, as the user lacks the necessary permissions by definition of being a standard user.
- When users that retain administrative rights uses either option, EPM policies do not manage the request, leaving it to the default Windows elevation process. However, information about the files elevation can still be reported back to Intune if all elevations are enabled for reporting through  through elevation settings policy.

**File elevation**:  
For files that are elevated through EPM policy:

- When configured for automatic elevation, the file runs without any interruption to the user.
- When configured for user confirmation, the user must respond to a confirmation prompt and meet any additional configurations, such as authenticating with their organizations credentials, or providing a business justification, before the file runs.

**Vile validation**:  
To ensure that only the correct file and version are elevated, you specify file details and can specify a file hash. You can also use certificates to validate the files you configure for elevation, which we recommend as a best practice.

If you use certificates to validate file integrity, you add a certificate directly to each policy that requires it, or add the certificate to a [reusable settings group](../protect/reusable-settings-groups.md) that you then assign to multiple policies. The use of reusable settings groups for the certificate can make it easier to manage certificate changes. If you need to update a certificate that’s in a reusable group, those changes automatically apply to each policy that includes the reusable group. This is more efficient than making separate edits to each policy to update the certificate.

For guidance on how to configure the policies and reusable settings group, see [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md).

### Windows elevation settings policy

Use *Windows elevation settings policy* when you want to:
<!-- To enable Endpoint Privilege Management (EPM) on a device, a *Windows elevation settings policy* must be assigned to it. This policy is necessary for EPM to be enabled, and includes the following uses: -->

- **Enable Endpoint Privilege Management** on devices. By default, this policy enables EPM. When first enabled for EPM, a device installs components that monitor elevation requests and enforce elevation rules.

  If a device has EPM disabled, there is a delay of seven days before the EPM component is deprovisioned. The delay is intended to reduce the time it takes to restore EPM  should a device have accidentally had EPM disabled, or its elevation settings policy unassigned.
- **Set a default response for an *Elevate request*** of any file that’s not managed by a *Windows elevation rule policy*. By default, this option is not configured.  <!-- Pending details as to what happens here, does the file elevate, or is it blocked? -->
  
  Options include:
  - Deny all requests - This option blocks the *elevate request* action for files that are not defined in a Windows elevation rules policy.
  - Require user confirmation - When confirmation is required you can choose from the same options as found for Windows elevation rules policy. 
- **Configure what Endpoint Privilege Management reports to Intune**. You can choose between:
  - Not reporting any data.
  - Reporting only diagnostic data.
  - Reporting diagnostic data and all endpoint elevations, which are file elevations managed by a Windows elevation rules policy.
  - Reporting diagnostic data and all elevations (default), which includes those managed by a rules policy as well any *Elevate request* for a file not managed by elevation rules.

### Windows elevation rules policy

Use profiles for *Windows elevation rules policy* to manage the identification of specific files, and how to elevation requests for those files are handled. Each *Windows elevation rule policy* includes one or more *elevation rules*. Its within the elevation rules that you'll configure details about the file being managed and requirements for it to be elevated.

Each elevation rule:

- **Uses the file name and file extension to identify the file the rule applies to.** The rule also supports optional conditions like a minimum build version, product name, or internal name. Optional conditions are not used byh Intune to identify the file, but can help admins identify which actual file the rule applies to.
- **Supports use of a certificate to validate the files integrity before its run on a device.** Certificates can be added directly to a rule, or through the use of a reusable settings group. We recommend the use of reusable settings groups as they can be more efficient and simplify a future change to the certificate. For more information on this, see the next section [Reusable settings groups](#reusable-settings-group).
- **Supports use of a file hash to validate the file.** A file hash is required unless you use a certificate, in which case the file hash becomes optional.
- **Configures the files evaluation type.** Evaluation type identifies what happens when an elevation request is made for the file. By default, this is set to *User confirmed*, which is our recommendation for most managed files.
  - **User confirmed** (Recommended): A user confirmed elevation always requires the user to click on a confirmation prompt to run the file. There are two additional user confirmations you can add. One require users to authenticate using their organization credentials. The second option requires the use to enter a business justification. What must be entered for justification isn't managed, but the justification text can collected for reporting when the device is configured to report elevation data as part of its Windows elevation settings policy.
  - **Automatic** elevation happens invisibly to the user. There is no prompt, and no indication that the file is running in an elevated context. 

    >[!CAUTION]  
    > We recommend automatic elevation be used sparingly, and only for trusted files that are business critical. Examples include a common printer-driver which users are expected to install, or a productivity app like the setup file for Microsoft Office 365.

### Reusable settings group

Endpoint Privilege Management supports using reusable settings groups to manage the certificates in place of adding that certificate directly to an elevation rule. Like all reusable settings groups for Intune, configurations and changes made to a reusable settings group are automatically passed to the policies that reference the group.
We recommend using a reusable settings group when you plan to use the same certificate for validating files in multiple elevation rules. This is because using reusable settings groups will be more efficient when you use the same certificate in multiple elevation rules:

- Certificates you add directly to an elevation rule: Each certificate is added directly to a rule is uploaded as a unique instance by Intune, and that certificate instance is then associated with the file for that rule. Later, if you must change the certificate, you must edit each individual rule that contains it. This results in Intune uploading the updated certificate a single time for each rule.
- Certificates you manage through a reusable settings group: Each time a certificate is added to a reusable settings group, that certificate is uploaded by Intune a single time no matter how many elevation rules include that group. That instance of the certificate is then associated with the file from each rule that uses that group. Later, if you must change the certificate, you can make he change one time to the reusable settings group, resulting in Intune uploading the updated file a single time, which also applies the change to each elevation rule that references the group.

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