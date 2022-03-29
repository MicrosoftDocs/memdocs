---
# required metadata

title: Update your workloads to support cloud native endpoints
titleSuffix: Microsoft Endpoint Manager
description: To support hybrid and remote workers, convert or migrate your workloads to support cloud native endpoints. This planning guide focuses on deploying apps and updates with Endpoint Manager, moving from group policy objects, and using Windows Autopilot.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 03/28/2022
ms.topic: conceptual
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer: ahamil, jasandys, wicale
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
---

# High level planning guide to move to cloud native endpoints

??We need a few sentences for the intro??.

This feature applies to:

- Windows cloud native endpoints

To be successful, you need to consider these key areas during planning and deployment. With proper planning, communications, and process updates, the benefits of cloud native endpoints will be achieved.

## Manage devices using a cloud native MDM provider

Managing your endpoints, including cloud native endpoints, is an important task for all organizations. With cloud native endpoints, the management tools you use must manage the endpoints wherever they go.

If you don't currently use a mobile device management (MDM) solution to manage your endpoints, or want to move to a Microsoft solution, then look at [Microsoft Endpoint Manager](/mem/endpoint-manager-overview).

With Microsoft Endpoint Manager, you get the following endpoint management options:

- **[Microsoft Intune](/mem/intune/)**: Intune is 100% cloud-based, and used the Endpoint Manager admin center to manage devices, manage apps on devices, create & deploy policies, review reporting data, and more. 

  For more information on using Intune to manage your endpoints, see:

  - [Microsoft Intune is an MDM and MAM provider for your devices](/mem/intune/fundamentals/what-is-intune)
  - [Deployment guide: Setup or move to Microsoft Intune](/mem/intune/fundamentals/deployment-guide-intune-setup)
  - [Microsoft Intune planning guide](/mem/intune/fundamentals/intune-planning-guide)

- **[Microsoft Endpoint Configuration Manager](/mem/configmgr/)**: Configuration Manager uses an on-premises infrastructure, and can manage servers. When you use [co-management](/mem/configmgr/comanage/overview), some workloads use Configuration Manager (on-premises), and some workloads use Microsoft Intune (cloud).

  For cloud-native endpoints, your Configuration Manager solutions should use a [Cloud Management Gateway (CMG)](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10).

## Review your endpoint and user workloads

At a high level, deploying cloud native endpoints require modern strategies for identity, software distribution, device management, OS updates, and managing user data & configuration. Microsoft has solutions that support these areas for your cloud native endpoints.

To start, review each workload, and determine if it can support cloud native endpoints. If they don't support cloud native endpoints, then <need something>. Plan to update your workloads to support cloud native endpoints. Your workloads should have the following characteristics:

- Get access securely from anywhere
- Delivered from the cloud ??
- Device independent ??

Remember, it's common for workloads to depend on other workloads. Cloud native endpoints also include the services and workloads that support the endpoints.

### Common workloads and solutions

The following workloads are customer specific configuration, tools, processes, and services for enabling user productivity and endpoint management.

Your exact workloads, details, and how to update the workloads for cloud native endpoints might be different. Also, you don’t need to transition every workload. But, you do need to consider each workload, its impact on user productivity, and the device management abilities. Converting some workloads to use cloud native endpoints might take longer than others.

- Device identity and Join ??

  - For cloud native endpoints, Azure Active Directory (AD) join is the best choice.
  - On-premises AD join and hybrid Azure AD join require connectivity to an on-premises domain controller. They need connectivity for initial user sign in, to delivery group policies, and change passwords. These options aren’t suitable for cloud native endpoints.

- **Provision your endpoints**

  For newly deployed Azure AD join endpoints, use Windows Autopilot to pre-configure devices. Joining Azure AD is typically a user-driven task, and Windows Autopilot is designed with end users in mind. Windows Autopilot enables provisioning using the cloud from anywhere on the Internet, and by any user.

  For more information, see:

  - [Windows Autopilot overview](/mem/autopilot/windows-autopilot)
  - [Windows Autopilot scenarios and capabilities](/mem/autopilot/windows-autopilot-scenarios)

- **Deploy software and apps**

  - Programs and apps should be deployed from a cloud-based system, like Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)).
  - User self-service should be considered to reduce provisioning time and configuration bloat.??

  For more information, see:

  - [Windows 10/11 app deployment using Microsoft Intune](/mem/intune/apps/apps-windows-10-app-deploy)
  - [Introduction to app management in Configuration Manager](/mem/configmgr/apps/understand/introduction-to-application-management)

- **Configure device settings using policies**

  - Traditional policy enforcement using group policy isn't possible with cloud native endpoints. Instead, you can use Intune to create policies to configure many settings, including built-in features like the [Settings Catalog](/mem/intune/configuration/settings-catalog) and [administrative templates](/mem/intune/configuration/administrative-templates-windows).

    [Group Policy analytics](/mem/intune/configuration/group-policy-analytics) can analyze your on-premises GPOs, and see if those same settings are supported in the cloud.

  - If you have existing policies that issue certificates, manage BitLocker, and provide endpoint protection, then these features will need moved ??"moved"?? to Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)).

    For more information, see:

    - [Use certificates for authentication in Microsoft Intune](/mem/intune/protect/certificates-configure)
    - [Disk encryption policy for endpoint security in Intune](/mem/intune/protect/endpoint-security-disk-encryption-policy)
    - [Add Endpoint protection settings in Intune](/mem/intune/protect/endpoint-protection-configure)
    - [Certificates in Configuration Manager](/mem/configmgr/core/plan-design/security/certificates-overview)
    - [BitLocker management in Configuration Manager](/mem/configmgr/protect/plan-design/bitlocker-management)
    - [Endpoint Protection in Configuration Manager](/mem/configmgr/protect/deploy-use/endpoint-protection)

- **Deploy security, feature, and app updates**

  - **Deploy Windows updates** using a cloud-based system, like Windows Update for Business. Using Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)), you can use Windows Update for Business to deploy security updates and feature updates.

    For more information, see:

    - [Manage Windows 10 and Windows 11 software updates in Intune](/mem/intune/protect/windows-update-for-business-configure)
    - [Integrate Configure Manager with Windows Update for Business](/mem/configmgr/sum/deploy-use/integrate-windows-update-for-business-windows-10)

  - **Deploy Microsoft 365 app updates** using the following options:

    - **Office Content Delivery Network** (CDN): Manage the CDN using a servicing profile in the Microsoft 365 Apps admin center or using an Intune policy ??How do you manage CDN using Intune policy? I don't see any docs on this??.
    - **Intune**: Create a policy that sets the Update Channel, remove other versions, and more.
    - **Configuration Manager** (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)): Manage your apps, including update stats, copy, retire, and more.

    For more information, see:

    - [Content Delivery Networks (CDNs)](/microsoft-365/enterprise/content-delivery-networks)
    - [Add Microsoft 365 apps to Windows 10/11 devices with Microsoft Intune](/mem/intune/apps/apps-add-office365)
    - [Management tasks for Configuration Manager apps](/mem/configmgr/apps/deploy-use/management-tasks-applications)

- **Manage user data**

  ??This whole section needs rewritten. How do admins do this? What online resources do we link to? What does "This includes app configuration and settings as well" actually mean??

  - Without necessary user app data and configuration locally available and accessible on a device, users may not be able to be productive. This data and configuration should be universally available and accessible by the end user on any endpoint they use and should include the following items:

    - User documents
    - Mail app configuration
    - Browser favorites
    - LOB application-specific data
    - LOB application-specific configuration

  - This includes app configuration and settings as well.

- **Access on-premises resources**

  - **Authentication and authorization**: To access on-premises resources from cloud native endpoints, users need to authenticate and verify who they are. For more specific information, see [Authentication and access to on-premises resources with cloud native endpoint](cloud-native-endpoints-on-premises.md#authentication-and-access-to-on-premises-resources).

  - **Connectivity**: Review and evaluate apps and resources that only live on-premises. Connectivity and access to these resources should be available off-premises, and without any direct connectivity, like a VPN. This task might include moving to SaaS versions of your apps, using [Azure AD Application Proxy](/azure/active-directory/app-proxy/application-proxy), [Azure Virtual Desktop](/azure/virtual-desktop/overview), [Windows 365](/windows-365/overview), [SharePoint](/sharepoint/introduction), [OneDrive](/onedrive/plan-onedrive-enterprise), or [Microsoft Teams](/microsoftteams/teams-overview).

## Transition your workloads in phases

Modernizing workloads and adopting cloud native endpoints will require changes to operational processes and procedures. For example:

- Administrators need to understand how changes to existing workloads might change their processes.
- The service desk needs to understand the new scenarios that they'll be supporting.

When reviewing your endpoints and workloads, break down the transition into phases. This section provides an overview on some recommended phases your organization can use. These phases can be repeated as many times as needed.

### ✅ Phase 1: Get info on your workloads

In this phase:

1. Inventory your current workload information and details, including their current state. Understand and define the end goal for all workloads, which should be to support cloud native endpoints.

2. Verify the end-state for each workload. Identify known blockers that prevent getting to this end-state or prevent supporting cloud native endpoints.

    Getting to the end-state for each workload may include updating software, lifting and shifting to a new platform, migrating to a new solution, or making configuration changes. The steps needed for each workload are different with each organization.

### ✅ Phase 2: Prioritize any blockers

After you've identified the key workloads and their end-state blockers, then:

1. Prioritize each blocker and evaluate each blocker for resolution.

    You may not want or need to address all blockers. For example, your organization might have workloads, or a part of workloads, that won’t support your cloud native endpoints. This lack of support may or may not be significant for your organization or users. You and your organization can make this decision.

2. To support testing and proof of concept, start with a minimum set of workloads. The goal is to test and validate a sample of your workloads.

### ✅ Phase 3: Transition your workloads

1. Move unblocked workloads to your planned cloud native solutions or end-state. Ideally, this step should be broken into smaller work items. The goal is to continue business operations with minimal disruption.

2. After the initial set of workloads support cloud native endpoints, identify more workloads, and continue the process.

### ✅ Phase 4: Prepare your end users

End users will have different experiences for receiving, deploying, and being supported on their devices. Administrators should:

- Review existing processes and documentation to identify where changes will be visible to end users.
- Update documentation.
- Develop an education strategy to share the changes and benefits users will experience.

## Transition your organization in phases

The following phases contain a high-level approach for organizations to move their environment to fully support cloud-native Windows endpoints. These phases are parallel to transitioning endpoints and user workloads. They may depend on certain workloads being partially or fully transitioned to support cloud-native Windows endpoints.

### ✅ Phase 1: Planning

?? This whole section needs rewritten. The different items need explained. ??

Define and clarify additional items that need to be planned logistically to support workloads and their move to supporting cloud-native.

1. Define the endpoints that require cloud identity
2. Define dependencies
3. Define gates and exit criteria
4. Automatic connection
5. User-initiated
6. Autopilot device registration, group tag, profile, and targeting planning
7. tomato -> I added this to be funny. Currently, this list is just "words" that don't make any sense.

### ✅ Phase 2: Enable endpoint cloud hybrid identity

?? This section needs more explanations and detailed info ??

Enables use the services that require on an endpoint having a cloud identity.

1. Assumes hybrid user identity already in place
2. Azure AD Connect configuration
3. Only if needed, enable Hybrid Azure AD Joined for:

    1. Existing Windows endpoints that require a cloud identity
    2. New Windows endpoints that require a cloud identity (until all blockers to AADJ have been removed or mitigated)

> [!NOTE]
> There is no Microsoft supported path to convert existing endpoints from on-premises domain joined or hybrid Azure Active Directory joined to Azure Active Directory joined. One end-result of using fully cloud-native endpoints is enabling user independence from their devices such that resetting an endpoint is does not impact the end-user. This is because their applications, configuration, and data is still readily accessible or will replicate to the newly provisioned endpoint in a short-amount of time.

### ✅ Phase 3: Cloud attach Configuration Manager (optional)

If you use Configuration Manager, then cloud attach your environment to Microsoft Intune. If you don't use Configuration Manager, then skip this step.

When you cloud attach, you can remotely manage your client endpoints, co-manage your endpoints with Intune (cloud) and Configuration Manager (on-premises), and access the Endpoint Manager admin center.

For more specific information, see [Cloud attach your Configuration Manager environment](/mem/configmgr/cloud-attach/overview) and [Walk through the Microsoft Endpoint Manager](/mem/intune/fundamentals/tutorial-walkthrough-endpoint-manager).

### ✅ Phase 4: Create an Azure AD joined proof of concept

?? This section needs more explanations and detailed info. How do you do some of these, such as "validate functionality"? ??

This phase can start at nearly any time and is critical to identify potential (and possibly unknown) issues and validate overall functionality and resolutions to those issues.

1. Implement bare-minimum viable modern building block configuration
2. Configure Windows Autopilot for Azure AD joined
3. Deploy pilot Azure AD joined systems
4. Validate functionality

    1. Identity additional blockers or building blocks
    2. Validate previously identified blockers

### ✅ Phase 5: Implement full modern provisioning

?? This whole section needs rewritten. This needs explained. Is a whole phase needed for just one sentence? ??

This phase transitions new Windows endpoint provisioning to Azure AD joined.

### ✅ Phase 6: Azure AD join your existing Windows endpoints

Once all blockers and issues have been resolved, you can move existing devices to be fully cloud native. You have the following options:

- **Option 1: Replace your devices**. If the devices are end-of-life or don't support modern security, then replacing them is the best choice. Modern devices support new and enhanced security features, including the Trusted Platform Module (TPM) technology.

- **Option 2: Reset the Windows devices**. If your existing devices support the newer security features, then you can reset the devices. During the out of box experience (OOBE) or when users sign in, they can join the devices to Azure AD.

  When resetting an existing Windows endpoint, be sure to clean up (??Does this mean delete? Need more info??) the existing Azure AD device object, the Intune device object, and the Windows Autopilot device registration. Then, re-provision the endpoint.

## Move from group policy objects (GPOs)

Many organizations use GPOs to configure and manage their Windows endpoints. Over time, it gets complicated due to a lack of documentation, lack of clarity in the policy's purpose or requirements, using legacy or non-functional policies, and using complex features. For example, there might be policies that include WMI filters, have complex OU structures, and use inheritance blocking, loopback, or security filtering.

### ✅ Manage settings using Intune

Microsoft Intune has many built-in settings that can be configured and deployed to your cloud native endpoints. When moving to Intune for policy management, you have some options.

These options aren't necessarily mutually exclusive. You can migrate a subset of policies and start new for others.

- **Option 1: Start new** (recommended): Intune has many settings to configure and manage your endpoints. You can create a policy, add and configure settings in the policy, and then deploy the policy.

    Many existing group policies include policies that might not apply to cloud native endpoints. Starting fresh enables an organization to validate and simplify their existing enforced policies, while eliminating legacy, forgotten, or even harmful policies. Endpoint Manager has built-in templates that group common settings together, like [VPN, Wi-Fi, endpoint protection, and more](/mem/intune/configuration/device-profiles).

- **Option 2: Migrate**: This involves lifting the existing policies and shifting them to the Intune policy engine. This can be extremely cumbersome and time consuming, including the volume of existing group policy, targeting differences, and lack of complete policy parity between group policy and Intune.

  Analyzing and rationalizing existing group policies to validate their necessity should be prioritized as simply moving all policy defeats some (if not all) of the advantages of moving the policies to Intune. This enables you to validate policy requirements and functionality and eliminate unnecessary policies that may cause overhead or degrade system performance or user experience.

### Intune features you should know

Intune also has built-in features that can help you configure your cloud native endpoints:

- **[Group Policy Analytics](/mem/intune/configuration/group-policy-analytics)**: You can import your GPOs in the Microsoft Endpoint Manager admin center, and run an analysis on the policies. You can see the policies that exist in Intune, and see the policies that are deprecated.

  If you use GPOs, then using this tool is a valuable first step.

  For more information, see [Group Policy Analytics in Endpoint Manager](/mem/intune/configuration/group-policy-analytics).

- **[Settings catalog](/mem/intune/configuration/settings-catalog)**: See all the settings available in Intune, and create, configure, & deploy a policy using these settings. If you create GPOs, then the settings catalog is a natural transition to cloud native endpoint configuration.

  When combined with [Group Policy Analytics](/mem/intune/configuration/group-policy-analytics), you can deploy the policies you used on-premises to your cloud native endpoints.

  For more information, see [Settings catalog in Endpoint Manager](/mem/intune/configuration/settings-catalog).

- **[Administrative templates](/mem/intune/configuration/administrative-templates-windows)**: These are similar to the ADMX templates used on-premises, and are built-in to Intune. You don't downloaded them. These templates include many settings that control features in Microsoft Edge version 77 and later, Internet Explorer, Microsoft Office programs, remote desktop, OneDrive, passwords, PINs, and more.

  If you use administrative templates on-premises, then using them in Intune is a natural transition.

  For more information, see [Administrative templates in Endpoint Manager](/mem/intune/configuration/administrative-templates-windows).

  You can also ingest an existing set of ADMX policies for Win32 and Desktop Bridge apps. For more information, see:

  - [Understanding ADMX policies - Windows Client Management](/windows/client-management/mdm/understanding-admx-backed-policies)
  - [Enable ADMX policies in MDM - Windows Client Management](/windows/client-management/mdm/enable-admx-backed-policies-in-mdm)
  - [Win32 and Desktop Bridge app ADMX policy Ingestion - Windows Client Management](/windows/client-management/mdm/win32-and-centennial-app-policy-configuration#overview)

  > [!NOTE]
  > Starting in Windows 10 version 1703, Mobile Device Management (MDM) policy configuration support was expanded to allow access of [selected set of Group Policy administrative templates (ADMX policies)](/windows/client-management/mdm/policies-in-policy-csp-admx-backed) for Windows PCs using the [Policy configuration service provider (CSP)](/windows/client-management/mdm/policy-configuration-service-provider). Configuring ADMX policies in Policy CSP is different from the typical way you configure a traditional MDM policy.

- **[Security baselines](/mem/intune/protect/security-baselines)**: A security baseline is a group of pre-configured Windows settings. They help you apply and enforce granular security settings that are recommended by the security teams. When you create a security baseline, you can also customize each baseline to enforce only the settings you want.

  You can create a security baseline for Windows, Microsoft Edge, and more. If you're not sure where to start, or want the security settings recommended by security experts, then look at security baselines.

  For more information, see [Security baselines in Endpoint Manager](/mem/intune/protect/security-baselines).

## Windows Autopilot guidance

You purchase endpoints from an OEM or partner, and the OEM can send the devices directly to your end users. Users receive the endpoints, sign in with their organization account, and Windows Autopilot automatically provision these endpoints. You can also use Windows Autopilot to provision existing endpoints that you or end users reset.

### ✅ Use Windows Autopilot to provision new or existing Windows endpoints

Some of the benefits include:

- **Built-in Windows setup process**: It presents a branded, guided, and simplified end-user experience.
- **Drop-ship endpoints directly to end-users**: Vendors and OEMs can ship endpoints directly to your users. This feature helps limit overhead and costs involved with high-touch internal IT processes and shipping.

  For best results, pre-register your endpoints with the OEMs or vendors. Pre-registering helps avoid any delays that can occur when manually registering endpoints.

- **End-users can reset existing endpoints themselves**: If users have existing Windows endpoints, they can reset the devices themselves. When they're reset, it restores the endpoints to a minimum baseline and managed state. It doesn't require a high cost IT intervention or physical access to the endpoint.

> [!NOTE]
> It's not recommended to use Windows Autopilot to hybrid Azure AD join newly provisioned endpoints. It works, but there can be some challenges. It's recommended to use Windows Autopilot to Azure AD join newly provisioned endpoints

For more information on Windows Autopilot, see:

- [Overview of Windows Autopilot](/mem/autopilot/windows-autopilot)
- [Windows Autopilot scenarios and features](/mem/autopilot/windows-autopilot-scenarios)
- [Tutorial - Use Autopilot to enroll devices in Intune](/mem/intune/enrollment/tutorial-use-autopilot-enroll-devices)
- [Windows Autopilot FAQ](/mem/autopilot/autopilot-faq)

## Next steps

- [What are cloud native endpoints?](cloud-native-endpoints-overview.md)
- [Tutorial: Get started with cloud native Windows endpoints with Microsoft Endpoint Manager](cloud-native-windows-endpoints.md)
- [Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md)
- [Cloud native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
- [Known issues](cloud-native-endpoints-known-issues.md)
