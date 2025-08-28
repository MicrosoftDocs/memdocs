---
title: Learn about using Endpoint Privilege Management with Microsoft Intune
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

# Use Endpoint Privilege Management with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization's users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your [Zero Trust](/security/zero-trust/zero-trust-overview) journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive. For more information, see [Zero Trust with Microsoft Intune](../fundamentals/zero-trust-with-microsoft-intune.md).

The following sections of this article provide an overview of EPM and it's key features.

Applies to:

- Windows 10
- Windows 11

> [!NOTE]
> Add photo here

## Key Features and Benefits

- **Standard Users by Default**. Users operate without local admin rights enhancing security without disrupting productivity by allowing users to perform necessary tasks with EPM without waiting for IT – reducing helpdesk tickets and delays.
- **Support for Just-in-time elevation**. Users elevate temporarily for specific IT-approved tasks, with automatic, user confirmed or support approved elevations.
- **Policy-Based Control**. Admins define settings and rules to control elevation conditions and behaviour, with granular rule creation capabilities to suit organizational needs.
- **Audit Logging and Reporting**. Intune logs every elevation with detailed metadata.
- **Alignment to Zero Trust principles** by enabling least privilege access and minimizing lateral movement risks.

## EPM Fundamentals

Elevation can be triggered by EPM, or by a user right clicking on a supported file type and selecting the 'Run with elevated access' context menu option. EPM is controlled by two types of policies:

- **Elevation rules policy** - defines elevation behavior for apps based on criteria.
- **Elevation settings policy** - controls the EPM client, reporting level and default elevation capability.

Both rules and policies can be targeted at groups of users or devices. To perform the elevation on the device, the EPM service uses a virtual account, which is isolated from the logged on users' account. Neither of these accounts are added to the local administrators group. 

EPM does not require an agent to be installed – the client is initiated by deploying an Elevation settings policy from Intune, which creates a 'Microsoft EPM Agent Service' and a "C:\Program Files\Microsoft EPM Agent" directory.

## INSERT PICTURE HERE

### Elevation Types

EPM allows users without administrative privileges to run processes in the administrative context. When you create an elevation rule, that rule allows EPM to proxy the target of that rule to run with administrator privileges on the device. The result is that the application has *full administrative* capability on the device.

When you use Endpoint Privilege Management, there are a few options for elevation behavior:

- **Automatic**: For automatic elevation rules, EPM *automatically* elevates these applications without input from the user. Broad rules in this category can have widespread impact to the security posture of the organization.

- **User confirmed**: With user confirmed rules, end users use a new right-click context menu *Run with elevated access*. User confirmed rules require the end-user to complete some additional requirements before the application is allowed to elevate. These requirements provide an extra layer of protection by making the user acknowledge that the app will run in an elevated context, before that elevation occurs.

- **Deny**: A deny rule identifies a file that EPM blocks from running in an elevated context. While we recommend use of file elevation rules to allow users to elevate specific files, a deny rule can help you ensure that certain files like known and potentially malicious software can't be run in an elevated context.

- **Support approved**: For support approved rules, end users must submit a request to approve an application. Once the request is submitted, an administrator can approve the request. Once the request is approved, the end user is notified that they can complete the elevation on the device. For more information about using this rule type, see [Support approved elevation requests](../protect/epm-support-approved.md)

### Rule Capabilities

- **Child process controls** - When processes are elevated by EPM, you can control how the creation of child processes is governed by EPM, which allows you to have granular control over any subprocesses that might be created by your elevated application.

- **Argument support** - Allow only certain parameters for applications to be elevated. This enables an administrator to allow parameters that are considered safe and disallow others when elevating.

- **File Hash support** - Match the application based on the hash of the file.

- **Publisher certificate support** - Create rules that are based of trusting the publisher certificate of the application alongside other attributes.

### Supported file types

EPM supports elevating these types of files:

- Executable files with a .exe extension.
- Windows installer files with a .msi extension.
- PowerShell scripts with the .ps1 extension.

### Reporting

EPM includes reports to help you prepare for, monitor and use the service. Reports are provided for unmanaged and managed elevations:

- **Unmanaged elevation**: All file elevations that happen without use of Endpoint Privilege Management. These elevations can happen when a user with administrative rights uses the Windows default action of *Run as administrator*.

- **Managed elevation**: Any elevation that Endpoint Privilege Management facilitates. Managed elevations include all elevations that EPM ends up facilitating for the standard user. These managed elevations could include elevations that happen as the result of an elevation rule or as part of default elevation action.

## Getting started with Endpoint Privilege Management

Endpoint Privilege Management (EPM) is built into Microsoft Intune, which means that all configuration is completed within the [Microsoft Intune Admin Center](https://intune.microsoft.com). When organizations get started with EPM, they use the following high-level process:

- **License EPM** - Before you can use Endpoint Privilege Management policies, you must license EPM in your tenant as an Intune add-on. For licensing information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

- **Plan for EPM** - Before your start using EPM, there are some key requirements and concepts you should consider. To plan for EPM, see [Plan for EPM](epm-plan.md).

- **Deploy EPM** - For most customers, the high-level process of deploying EPM will include the following phases. More specific details on how to implement each of these phases is covered in [Deploy EPM](epm-deploy.md).

  - **Phase 1: Auditing** - Enable EPM client and silently gather reporting information
  - **Phase 2: Persona identification** - Identity groups of users with common requirements – likely focused on their personas
  - **Phase 3: Build rules** - Use reporting data (Phase 1) to create rules for different personas
  - **Phase 4: Remove local admin rights** - Move users from local administrators to std users on their device. Consider enabling 'Support Approved' so that users can request elevation for apps that aren't covered by rules.
  - **Phase 5: Monitoring** - Iterate and refine rules, identify new scenarios.

> [!div class="nextstepaction"]
> [Next: Plan for EPM >](epm-plan.md)

## Related articles

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Approving elevation requests](../protect/epm-support-approved.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
