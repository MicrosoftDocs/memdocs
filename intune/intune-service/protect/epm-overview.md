---
title: Learn about using Endpoint Privilege Management with Microsoft Intune
description: To enhance the security of your organization, set your users to run with standard permissions while Endpoint Privilege Management ensures those users can seamlessly run specified files with elevated rights.
author: brenduns
ms.author: brenduns
ms.date: 09/10/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Use Endpoint Privilege Management with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization's users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your [Zero Trust](/security/zero-trust/zero-trust-overview) journey by helping your organization achieve a broad user base running with least privilege, while still elevating selected tasks when necessary to remain productive. For more information, see [Zero Trust with Microsoft Intune](../fundamentals/zero-trust-with-microsoft-intune.md).

This overview provides information about EPM including the benefits, how it works, and how to get started.

Applies to:

- Windows

## Key Features and Benefits

✅ Find out the key features and benefits of EPM

- **Standard Users by Default**. Users can perform their tasks without local admin rights.
- **Support for just-in-time elevation**. Users can trigger specific IT-approved binaries or scripts to elevate temporarily.
- **Policy-Based Control**. Admins define settings and rules to control elevation conditions and behavior, with granular rule creation capabilities to suit organizational needs.
- **Audit Logging and Reporting**. Intune logs every elevation with detailed metadata.
- **Alignment to Zero Trust principles** by enabling least privilege access and minimizing lateral movement risks.

## EPM Fundamentals

✅ Learn how EPM works

EPM elevation can be triggered using two methods:

- Automatically, or;
- User initiated.

EPM can be configured using two types of policies:

- **Elevation settings policy** - controls the EPM client, reporting level and default elevation capability.
- **Elevation rules policy** - defines elevation behavior for binaries or scripts based on criteria.

Both rules and policies can be targeted at groups of users or devices. To perform the elevation on the device, the EPM service uses a virtual account, which is isolated from the logged on users' account. Neither of these accounts are added to the local administrators group.

The EPM client is installed automatically when an *Elevation settings policy* is assigned to devices or users. The EPM client uses the 'Microsoft EPM Agent Service' service and stores its binaries in the `"C:\Program Files\Microsoft EPM Agent"` directory.

This diagram shows a high level architecture of how the EPM client is triggered, checks for rules and then facilitates elevation:

:::image type="content" source="media/epm-overview/EPM-Elevation-Architecture.png" alt-text="A diagram representing how an EPM elevation starts, is matched against a rule and then elevated.":::

### Elevation Types

✅ Control how EPM elevates files

EPM allows users without administrative privileges to run processes in the administrative context. When you create an elevation rule, that rule allows EPM to proxy the target of that rule to run with administrator privileges on the device. The result is that the application has *full administrative* capability on the device.

When you use Endpoint Privilege Management, there are a few options for elevation behavior:

- **Automatic**: For automatic elevation rules, EPM *automatically* elevates these applications without input from the user. Broad rules in this category can have widespread impact to the security posture of the organization.

- **User confirmed**: With user confirmed rules, end users use a new right-click context menu *Run with elevated access*. Administrators can require the user to perform extra validation using an authentication prompt, business justification, or both.

  :::image type="content" source="media/epm-overview/epm-user-confirmed-inline.png" alt-text="A screenshot showing the prompt a user receives when they use user confirmed elevation." lightbox="media/epm-overview/epm-user-confirmed-expanded.png":::

- **Support approved**: For support approved rules, end users must submit a request to run an application with elevated permissions. Once the request is submitted, an administrator can approve the request. Once the request is approved, the end user is notified that they can retry the elevation on the device. For more information about using this rule type, see [Support approved elevation requests](../protect/epm-support-approved.md).

  :::image type="content" source="media/epm-overview/epm-support-approval-inline.png" alt-text="A screenshot showing the prompt a user receives when they request to run an application as administrator using support approval." lightbox="media/epm-overview/epm-support-approval-expanded.png":::

- **Deny**: A deny rule identifies a file that EPM blocks from running in an elevated context. In certain scenarios, deny rules can ensure that known files or potentially malicious software can't be run in an elevated context.

The EPM client can be configured with a default elevation response, or with specific rules that allow the specified elevation response.

### Rule Capabilities

✅ Granular targeting of files for elevation

EPM elevation rules can be created based on one or more attributes including file name, path, etc. Some examples of rule capabilities are:

- **Child process controls** - When processes are elevated by EPM, you can control how the creation of child processes is governed by EPM, which allows you to have granular control over any subprocesses that might be created by your elevated application.

- **Argument support** - Allow only certain parameters for applications to be elevated.

- **File hash support** - Match the application based on the hash of the file.

- **Publisher certificate support** - Create rules that are based on trusting the publisher certificate of the application alongside other attributes.

### Supported file types

EPM supports elevating these types of files:

- Executable files with a `.exe` extension.
- Windows installer files with a `.msi` extension.
- PowerShell scripts with the `.ps1` extension.

### Reporting

✅ Track elevations in your environment

EPM includes reports to help you prepare for, monitor, and use the service. Reports are provided for unmanaged and managed elevations:

- **Unmanaged elevation**: All file elevations that happen without use of Endpoint Privilege Management. These elevations can happen when a user with administrative rights uses the Windows default action of *Run as administrator*.

- **Managed elevation**: Any elevation that Endpoint Privilege Management facilitates. Managed elevations include all elevations that EPM ends up facilitating for the standard user. These managed elevations could include elevations that happen as the result of an elevation rule or as part of default elevation action.

## Getting started with Endpoint Privilege Management

✅ Start using EPM

:::image type="content" source="media/epm-overview/epm-lifecycle.png" alt-text="A diagram showing the lifecycle of deploying EPM by licensing and planning, deploying, and managing.":::

Endpoint Privilege Management (EPM) is administered from the [Microsoft Intune Admin Center](https://intune.microsoft.com). When organizations get started with EPM, they use the following high-level process:

- **License EPM and Plan**
  - **License EPM** - Before you can use Endpoint Privilege Management policies, you must license EPM in your tenant as an Intune add-on. For licensing information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).
  - **Plan for EPM** - Before you start using EPM, there are some key requirements and concepts you should consider. For more information, see [Plan for EPM](epm-plan.md).

- **Deploy EPM** - To deploy EPM, enable auditing, create rules, and monitor the deployment. For more information, see [Deploy EPM](epm-deploy.md).
- **Manage EPM** - After you deploy EPM, you can monitor [support approved requests](epm-support-approved.md) and [elevations](epm-reports.md). You can [maintain and update your rules](epm-elevation-rules.md) and [review user privileges](endpoint-security-account-protection-policy.md).

---

> [!div class="nextstepaction"]
> [Next: Plan for EPM >](epm-plan.md)
