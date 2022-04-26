---
# required metadata

title: Update your workloads to support cloud native endpoints
titleSuffix: Microsoft Endpoint Manager
description: To support hybrid and remote workers, convert or migrate your workloads to support cloud native endpoints. This planning guide focuses on deploying apps and updates with Endpoint Manager, moving from group policy objects, and using Windows Autopilot.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 04/26/2022
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

This high level planning guide includes ideas and suggestions you need to consider for your adoption and migration to cloud native endpoints. It discusses managing devices, reviewing & transitioning existing workloads, making organization changes, using Windows Autopilot, and more.

This feature applies to:

- Windows cloud native endpoints

Moving your Windows endpoints to cloud native has many advantages, including in the long term. It's not an overnight process and must be planned to avoid issues, outages, and negative user impact.

For more information on the benefits to the organization and its users, see [Get started with cloud native endpoints and Microsoft Endpoint Manager](cloud-native-endpoints-overview.md).

To be successful, consider these key areas during planning and deployment. With proper planning, communications, and process updates, your organization can be cloud native.

## Manage devices using a cloud native MDM provider

Managing your endpoints, including cloud native endpoints, is an important task for all organizations. With cloud native endpoints, the management tools you use must manage the endpoints wherever they go.

If you don't currently use a mobile device management (MDM) solution, or want to move to a Microsoft solution, then look at [Microsoft Endpoint Manager](/mem/endpoint-manager-overview).

With Microsoft Endpoint Manager, you get the following endpoint management options:

- **[Microsoft Intune](/mem/intune/)**: Intune is 100% cloud-based, and used the Endpoint Manager admin center to manage devices, manage apps on devices, create & deploy policies, review reporting data, and more. 

  For more information on using Intune to manage your endpoints, see:

  - [Microsoft Intune is an MDM and MAM provider for your devices](/mem/intune/fundamentals/what-is-intune)
  - [Deployment guide: Setup or move to Microsoft Intune](/mem/intune/fundamentals/deployment-guide-intune-setup)
  - [Microsoft Intune planning guide](/mem/intune/fundamentals/intune-planning-guide)

- **[Microsoft Endpoint Configuration Manager](/mem/configmgr/)**: Configuration Manager uses an on-premises infrastructure, and can manage servers. When you use [co-management](/mem/configmgr/comanage/overview), some workloads use Configuration Manager (on-premises), and some workloads use Microsoft Intune (cloud).

  For cloud-native endpoints, your Configuration Manager solutions should use a [Cloud Management Gateway (CMG)](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10).

## Review your endpoint and user workloads

At a high level, deploying cloud native endpoints requires modern strategies for identity, software distribution, device management, OS updates, and managing user data & configuration. Microsoft has solutions that support these areas for your cloud native endpoints.

To start, review each workload, and determine how it can or will support your cloud native endpoints. Some workloads may already support cloud native endpoints. Native support depends on the specific workload, how your organization implements the workload services, and how your users use the services.

To determine if your workloads support cloud native endpoints, you need to research and validate these services.

If a service or solution doesn't support cloud native endpoints, then determine its impact and its criticality on your users and your organization. When you have this information, you can determine the next steps, which may include:

- Working with the service vendor
- Updating to a new version
- Using a new service
- Implementing a work-around for accessing and using that service from a cloud native endpoint
- Validating the service requirements
- Accepting that the service isn't cloud native friendly, which may be acceptable for your users and your organization

Either way, you should plan to update your workloads to support cloud native endpoints. 

Your workloads should have the following characteristics:

- Securely access apps and data from anywhere users are located. Access doesn't require a connection to a corporate or internal network.
- Hosted in, hosted by, or hosted through a cloud service.
- Doesn't require or depends on a specific device.

Cloud native endpoints also include the services and workloads that support the endpoints.

### Common workloads and solutions

The following workloads are configuration, tools, processes, and services for enabling user productivity and endpoint management.

Your exact workloads, details, and how to update the workloads for cloud native endpoints might be different. Also, you don’t need to transition every workload. But, you do need to consider each workload, its impact on user productivity, and the device management abilities. Converting some workloads to use cloud native endpoints might take longer than others. Workloads may also have interdependencies on each other.

- **Device identity**
  
  A device's identity is determined by the identity providers (IdP) that have knowledge of the device and a security trust with the device. For Windows endpoints, the most common IdP's are on-premises Active Directory (AD) and Azure Active Directory (Azure AD). Endpoints with identities from one of these two IdP's are typically joined to one or both.

  - For cloud native endpoints, Azure AD join is the best choice for the device's identity. It doesn't require any connectivity to an on-premises network, resource, or service.
  - On-premises AD join and hybrid Azure AD join require connectivity to an on-premises domain controller. They need connectivity for initial user sign-in, to deliver group policies, and change passwords. These options aren’t suitable for cloud native endpoints.

  > [!NOTE]
  > Azure AD registration, sometimes referred to as workplace join, is for BYOD scenarios only. It shouldn't be for organization owned Windows endpoints. Some functionality may not be supported or work as expected on Azure AD registered Windows endpoints.

- **Provision your endpoints**

  For newly deployed Azure AD join endpoints, use Windows Autopilot to pre-configure devices. Joining Azure AD is typically a user-driven task, and Windows Autopilot is designed with users in mind. Windows Autopilot enables provisioning using the cloud from anywhere on the Internet, and by any user.

  For more information, see:

  - [Windows Autopilot overview](/mem/autopilot/windows-autopilot)
  - [Windows Autopilot scenarios and capabilities](/mem/autopilot/windows-autopilot-scenarios)

- **Deploy software and applications**

  Most users need and use software and applications not included with the core operating system. In many cases, IT doesn't know or understand the specific app requirements. However, delivering and managing these applications is still the responsibility of your IT team. Users should be able to request and install the applications they need to do their jobs, regardless of the endpoint they're using or where they're using it from.

  - To deploy software and applications, use a cloud-based system, like Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)).

  - Create a baseline of apps that your endpoints must have, like Microsoft Outlook and Teams. For other apps, let users install their own apps.

    On your endpoints, you can use the [Company Portal app](/windows/application-management/private-app-repository-mdm-company-portal-windows-11) as your app repository. Or, use a user-facing portal that lists the apps that can be installed. This self-service option reduces provisioning time of new and existing devices, reduces the burden on IT, and you don't have to deploy apps that users don't need.

  For more information, see:

  - [Windows 10/11 app deployment using Microsoft Intune](/mem/intune/apps/apps-windows-10-app-deploy)
  - [Introduction to app management in Configuration Manager](/mem/configmgr/apps/understand/introduction-to-application-management)
  - [Private app repository in Windows 11](/windows/application-management/private-app-repository-mdm-company-portal-windows-11)

- **Configure device settings using policies**

  Policy and security management is core in endpoint management. Endpoint policies allow your organization to enforce a specific security baseline and a standard configuration on your managed endpoints. There are many settings you can manage and control on your endpoints. Create policies that only configure what's required in your baseline. Don't create policies that control common user preferences.

  - Traditional policy enforcement using group policy isn't possible with cloud native endpoints. Instead, you can use Intune to create policies to configure many settings, including built-in features like the [Settings Catalog](/mem/intune/configuration/settings-catalog) and [administrative templates](/mem/intune/configuration/administrative-templates-windows).

    [Group Policy analytics](/mem/intune/configuration/group-policy-analytics) can analyze your on-premises GPOs, see if those same settings are supported in the cloud, and create a policy using those settings.

  - If you have existing policies that issue certificates, manage BitLocker, and provide endpoint protection, then these features will need moved ??"moved"?? to Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)).

    For more information, see:

    - [Use certificates for authentication in Microsoft Intune](/mem/intune/protect/certificates-configure)
    - [Disk encryption policy for endpoint security in Intune](/mem/intune/protect/endpoint-security-disk-encryption-policy)
    - [Add Endpoint protection settings in Intune](/mem/intune/protect/endpoint-protection-configure)
    - [Certificates in Configuration Manager](/mem/configmgr/core/plan-design/security/certificates-overview)
    - [BitLocker management in Configuration Manager](/mem/configmgr/protect/plan-design/bitlocker-management)
    - [Endpoint Protection in Configuration Manager](/mem/configmgr/protect/deploy-use/endpoint-protection)

- **Deploy security, feature, and app updates**

  Many on-premises solutions can't deploy updates to cloud native endpoints or deploy them efficiently. From a security perspective, this workload may be the most important. It should be the first workload that you transition to support cloud native Windows endpoints.

  - **Deploy Windows updates** using a cloud-based system, like Windows Update for Business. Using Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)), you can use Windows Update for Business to deploy security updates and feature updates.

    For more information, see:

    - [Manage Windows 10 and Windows 11 software updates in Intune](/mem/intune/protect/windows-update-for-business-configure)
    - [Integrate Configure Manager with Windows Update for Business](/mem/configmgr/sum/deploy-use/integrate-windows-update-for-business-windows-10)

  - **Deploy Microsoft 365 app updates** using the following options:

    - **Office Content Delivery Network** (CDN): Manage the CDN using a servicing profile in the Microsoft 365 Apps admin center or using an Intune policy ??How do you manage CDN using Intune policy? I don't see any docs on this??.
    - **Intune**: Create a policy that sets the Update Channel, removes other app versions, and more.
    - **Configuration Manager** (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)): Manage your apps, including update stats, copy, retire, and more.

    For more information, see:

    - [Content Delivery Networks (CDNs)](/microsoft-365/enterprise/content-delivery-networks)
    - [Add Microsoft 365 apps to Windows 10/11 devices with Microsoft Intune](/mem/intune/apps/apps-add-office365)
    - [Management tasks for Configuration Manager apps](/mem/configmgr/apps/deploy-use/management-tasks-applications)

- **Manage user data and settings**

  User data includes the following items:

  - User documents
  - Mail app configuration
  - Web browser favorites
  - Line of Business (LOB) application specific data
  - Line of Business (LOB) application specific configuration settings
  
  Users need to create and access their data from any endpoint. This data also needs to be protected, and might need to be shared with other users.
  
  - Store user data and settings in a cloud storage provider, like Microsoft OneDrive. Cloud storage providers can handle data synchronization, sharing, offline access, conflict resolution, and more.
  
    For more information, go to [OneDrive guide for enterprises](/onedrive/plan-onedrive-enterprise).

  > [!IMPORTANT]
  > Some user settings, like OS preferences or application-specific settings, are stored in the registry. Accessing these settings from anywhere may not be realistic, and might be prohibited from synchronizing with different endpoints. 
  >
  > It's possible these settings can be exported, and then imported in another device. For example, you can export user settings from Outlook, Word, and other Office apps.
  >
  > If you need to export user settings for the OS or a specific app, then review the vendor's documentation.

- **Access on-premises resources**
  
  Some organizations can't transition some workloads to cloud native solutions. The only option might be accessing existing on-premises resources or services from a cloud native endpoint. For these scenarios, users need access.
  
  For these on-premises services, resources, and applications, consider the following tasks:

  - **Authentication and authorization**: To access on-premises resources from cloud native endpoints, users need to authenticate and verify who they are. For more specific information, see [Authentication and access to on-premises resources with cloud native endpoint](cloud-native-endpoints-on-premises.md#authentication-and-access-to-on-premises-resources).

  - **Connectivity**: Review and evaluate apps and resources that only live on-premises. Connectivity and access to these resources should be available off-premises, and without any direct connectivity, like a VPN. This task might include moving to SaaS versions of your apps, using [Azure AD Application Proxy](/azure/active-directory/app-proxy/application-proxy), [Azure Virtual Desktop](/azure/virtual-desktop/overview), [Windows 365](/windows-365/overview), [SharePoint](/sharepoint/introduction), [OneDrive](/onedrive/plan-onedrive-enterprise), or [Microsoft Teams](/microsoftteams/teams-overview).

  > [!NOTE]
  > Azure AD doesn't support the Kerberos authentication protocol. On-premises AD does support the Kerberos authentication protocol. In your planning, you may learn more about Azure AD Kerberos (preview). When configured, users sign in to a cloud native endpoint using their Azure AD account, and can access on-premises apps or services that use Kerberos authentication.
  >
  > Azure AD Kerberos:
  > 
  > - Isn't used in cloud native solutions.
  > - Doesn't solve any connectivity issues for resources that require authentication through Azure AD.
  > - Isn't the answer or work-around for any domain authentication requirements through Azure AD.
  > - Doesn't address the machine authentication challenges listed at [Known Issues and important information](cloud-native-endpoints-known-issues.md).
  >
  > For a deeper understanding of Azure AD Kerberos (preview) and the scenarios it can address, see the following blogs:
  > 
  > - [Why We Built Azure AD Kerberos](https://syfuhs.net/why-we-built-azure-ad-kerberos) (opens an external website)
  > - [Deep dive: How Azure AD Kerberos works](https://techcommunity.microsoft.com/t5/itops-talk-blog/deep-dive-how-azure-ad-kerberos-works/ba-p/3070889) (opens another Microsoft website)
  > - [How Azure AD Kerberos Works (syfuhs.net)](https://syfuhs.net/how-azure-ad-kerberos-works) (opens an external website)

## Transition your workloads in phases

Modernizing workloads and adopting cloud native endpoints will require changes to operational processes and procedures. For example:

- Administrators need to understand how changes to existing workloads might change their processes.
- The service desk needs to understand the new scenarios they'll be supporting.

When reviewing your endpoints and workloads, break down the transition into phases. This section provides an overview on some recommended phases your organization can use. These phases can be repeated as many times as needed.

??I feel like we need a common example, and we can build off that example with each phase. It might make more sense to readers??

### ✅ Phase 1: Get info on your workloads

In this phase:

1. Inventory your current workload information and details, including their current state. Understand and define the end goal for all workloads, which should be to support cloud native endpoints.

2. Verify the end-state for each workload. Identify known blockers that prevent getting to this end-state or prevent supporting cloud native endpoints.

    Getting to the end-state for each workload may include updating software, "lifting and shifting" to a new platform, migrating to a new solution, or making configuration changes. The steps needed for each workload are different with each organization.

### ✅ Phase 2: Prioritize any blockers

After you've identified the key workloads and their end-state blockers, then:

1. Prioritize each blocker and evaluate each blocker for resolution.

    You may not want or need to address all blockers. For example, your organization might have workloads, or a part of workloads, that won’t support your cloud native endpoints. This lack of support may or may not be significant for your organization or users. You and your organization can make this decision.

2. To support testing and proof of concept, start with a minimum set of workloads. The goal is to test and validate a sample of your workloads.

### ✅ Phase 3: Transition your workloads

In this phase, you're ready to implement your changes.

1. Move unblocked workloads to your planned cloud native solutions or end-state. Ideally, this step should be broken into smaller work items. The goal is to continue business operations with minimal disruption.

2. After the first set of workloads support cloud native endpoints, identify more workloads, and continue the process.

### ✅ Phase 4: Prepare your users

Users will have different experiences for receiving, deploying, and being supported on their devices. Administrators should:

- Review existing processes and documentation to identify where changes will be visible to users.
- Update documentation.
- Develop an education strategy to share the changes and benefits users will experience.

## Transition your organization in phases

The following phases contain a high-level approach for organizations to move their environment to fully support cloud-native Windows endpoints. These phases are parallel to transitioning endpoints and user workloads. They may depend on certain workloads being partially or fully transitioned to support cloud-native Windows endpoints.

### ✅ Phase 1: Define endpoints, dependencies, and milestones

This phase is the first step for your organization migration to be fully cloud native. Look at what you currently have, define success criteria, and start planning how your devices will be added to Azure AD.

1. **Define the endpoints that require a cloud identity**

    - Endpoints that use internet access require a cloud identity. You'll add these endpoints to Azure AD.
    - Endpoints that don't use the internet or are only used on-premises shouldn't have a cloud identity. Don't migrate these scenarios to be cloud native.

2. **Define dependencies**

    Workloads, users, and devices have technical and non-technical dependencies. To transition with minimal impact to users and the organization, you must account for these dependencies.

    For example, a dependency can be:

    - Business processes and continuity
    - Security standards
    - Local laws and regulations
    - User knowledge and use of the workload
    - Capital, operational costs and budget

    For each workload, ask "What will be affected if we change anything about the services provided by this workload?". You must account for the effects of this change.

3. **Define milestones and success criteria for each workload**

    Each workload has its own milestones and success criteria. They can be based on the organization's use of the workload and its applicability to specific endpoints and users.

    To understand and define the progress of the transition, track and monitor this information.

4. **Plan your Windows Autopilot deployment**

    - Determine how and when devices will be registered to your organization.
    - Determine and create the necessary group tags to target your Windows Autopilot policies.
    - Create your Windows Autopilot profile with its configuration settings, and target the devices that will receive your profile.

### ✅ Phase 2: Enable endpoint cloud hybrid identity (optional)

To be fully cloud native, your existing Windows endpoints must be reset. When you reset, the endpoint is restored back to factory settings. All apps, settings, and personal data on the device is deleted.

If you're not ready to reset your endpoints, then you can enable hybrid Azure AD join. A cloud identity is created for hybrid Azure AD join endpoints. Remember, hybrid Azure AD join still requires on-premises connectivity.

Hybrid Azure AD join is a transitionary step to cloud native, and isn't the end goal. The end goal is for all existing endpoints to be fully cloud native. 

When endpoints are fully cloud native, user data is stored in a cloud storage provider, like OneDrive. So when an endpoint is reset, the user applications, configuration, and data is still accessible, or will replicate to a newly provisioned endpoint.

For more information, go to:

- [Azure AD joined (AADJ) vs. Hybrid Azure AD joined (HAADJ)](azure-ad-joined-hybrid-azure-ad-joined.md)
- [Configure hybrid Azure AD join](/azure/active-directory/devices/howto-hybrid-azure-ad-join)
  
> [!NOTE]
> There isn't a Microsoft supported path to convert existing endpoints from on-premises domain joined or hybrid Azure AD joined to Azure AD joined. These endpoints must be reset.

### ✅ Phase 3: Cloud attach Configuration Manager (optional)

If you use Configuration Manager, then cloud attach your environment to Microsoft Intune. If you don't use Configuration Manager, then skip this step.

When you cloud attach, you can remotely manage your client endpoints, co-manage your endpoints with Intune (cloud) and Configuration Manager (on-premises), and access the Endpoint Manager admin center.

For more specific information, see [Cloud attach your Configuration Manager environment](/mem/configmgr/cloud-attach/overview) and [Walk through the Microsoft Endpoint Manager](/mem/intune/fundamentals/tutorial-walkthrough-endpoint-manager).

### ✅ Phase 4: Create an Azure AD joined proof of concept

This critical phase can start at any time. It helps identify potential issues, unknown issues, and validates overall functionality and resolutions to those issues. As with all POCs, the goal is to prove and validate functionality in an actual enterprise environment instead of a lab environment.

Important steps for this phase include:

1. **Implement a minimum baseline configuration using Intune**

    This step is important. You don't want to introduce endpoints to your network or to production that:

    - Don't follow your organization's security standards
    - Aren't configured for users to do their work.

    This minimum configuration doesn't and shouldn't have all possible configurations applied. Remember, the intent is to discover additional configuration that's required for users to be successful.

2. **Configure Windows Autopilot for Azure AD joined endpoints**

    Using Windows Autopilot to provision new endpoints and reprovision existing endpoints is the fastest way to introduce Azure AD joined systems to your organization. It's an important part of the POC.

3. **Deploy a POC for Azure AD joined systems**

    - Use a mix of endpoints that represent different configurations and users. You want as much validation of this new system state as possible.

    - Only real production use by real production users will fully validate the workloads and their functionality. Through natural, day-to-day use of the POC Azure AD endpoints, users organically test and validate your workloads.

    - Create checklists of business critical functionality and scenarios, and give these lists to your POC users. The checklists are specific to each organization and may change as workloads are transitioned to cloud native friendly workloads.

4. **Validate functionality**

    Validation is a repetitive process. It's based on the workloads and their configuration within your organization.

    - Collect user feedback on the POC endpoints, workloads, and their functionality. This feedback should be from users that used the cloud native endpoints.

      Additional blockers, and previously unknown or unaccounted for workloads/scenarios may be discovered.

    - Use the milestones and success criteria previously established for each workload. They'll help determine the progress and scope of the POC.

### ✅ Phase 5: Implement full modern provisioning

?? This whole section needs rewritten. This needs explained. Is a whole phase needed for just one sentence? ??

This phase transitions new Windows endpoint provisioning to Azure AD joined.

### ✅ Phase 6: Azure AD join your existing Windows endpoints

Once all blockers and issues have been resolved, you can move existing devices to be fully cloud native. You have the following options:

- **Option 1: Replace your devices**. If the devices are end-of-life or don't support modern security, then replacing them is the best choice. Modern devices support new and enhanced security features, including the Trusted Platform Module (TPM) technology.

- **Option 2: Reset the Windows devices**. If your existing devices support the newer security features, then you can reset the devices. During the out of box experience (OOBE) or when users sign in, they can join the devices to Azure AD.

  When resetting an existing Windows endpoint, be sure to clean up (??Does this mean delete? Need more info??) the existing Azure AD device object, the Intune device object, and the Windows Autopilot device registration. Then, reprovision the endpoint.

When the devices are ready, join these devices to Azure AD using the option that best for your organization. For more specific information, see [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join) and [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan).

## Move from group policy objects (GPOs)

Many organizations use GPOs to configure and manage their Windows endpoints. 

Over time, it gets complicated due to a lack of documentation, lack of clarity in the policy's purpose or requirements, using legacy or non-functional policies, and using complex features. For example, there might be policies that include WMI filters, have complex OU structures, and use inheritance blocking, loopback, or security filtering.

### Manage settings using Intune

Microsoft Intune has many built-in settings that can be configured and deployed to your cloud native endpoints. When moving to Intune for policy management, you have some options.

These options aren't necessarily mutually exclusive. You can migrate a subset of policies and start new for others.

- **Option 1: Start new** (recommended): Intune has many settings to configure and manage your endpoints. You can create a policy, add and configure settings in the policy, and then deploy the policy.

  Many existing group policies include policies that might not apply to cloud native endpoints. Starting fresh enables an organization to validate and simplify their existing enforced policies, while eliminating legacy, forgotten, or even harmful policies. Endpoint Manager has built-in templates that group common settings together, like [VPN, Wi-Fi, endpoint protection, and more](/mem/intune/configuration/device-profiles).

- **Option 2: Migrate**: This option involves lifting the existing policies and shifting them to the Intune policy engine. It can be cumbersome and time consuming. For example, you may have a lot of existing group policies and there will be differences with settings on-premises vs. in the cloud.

  If you choose this option, you must review and analyze your existing group policies, and determine if they're still needed or valid on your cloud native endpoints. You want to eliminate unnecessary policies, including the policies that may cause overhead, or degrade system performance or the user experience. Don't move your group policies to Intune until you know what they do.

### Intune features you should know

Intune also has built-in features that can help you configure your cloud native endpoints:

- **[Group Policy Analytics](/mem/intune/configuration/group-policy-analytics)**: You can import your GPOs in the Microsoft Endpoint Manager admin center, and run an analysis on the policies. You can see the policies that exist in Intune, and see the policies that are deprecated.

  If you use GPOs, then using this tool is a valuable first step.

  For more information, see [Group Policy Analytics in Endpoint Manager](/mem/intune/configuration/group-policy-analytics).

- **[Settings catalog](/mem/intune/configuration/settings-catalog)**: See all the settings available in Intune, and create, configure, & deploy a policy using these settings. If you create GPOs, then the settings catalog is a natural transition to cloud native endpoint configuration.

  When combined with [Group Policy Analytics](/mem/intune/configuration/group-policy-analytics), you can deploy the policies you used on-premises to your cloud native endpoints.

  For more information, see [Settings catalog in Endpoint Manager](/mem/intune/configuration/settings-catalog).

- **[Administrative templates](/mem/intune/configuration/administrative-templates-windows)**: These are similar to the ADMX templates used on-premises, and are built in to Intune. You don't downloaded them. These templates include many settings that control features in Microsoft Edge version 77 and later, Internet Explorer, Microsoft Office programs, remote desktop, OneDrive, passwords, PINs, and more.

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

## Use Windows Autopilot to provision new or existing Windows endpoints

If you purchase endpoints from an OEM or partner, then you should use Windows Autopilot.

Some of the benefits include:

- **Built-in Windows setup process**: It presents a branded, guided, and simplified end-user experience.

- **Drop-ship endpoints directly to end-users**: Vendors and OEMs can ship endpoints directly to your users. Users receive the endpoints, sign in with their organization account (`user@contoso.com`), and Windows Autopilot automatically provisions the endpoint.

  This feature helps limit overhead and costs involved with high-touch internal IT processes and shipping.

  For best results, pre-register your endpoints with the OEMs or vendors. Pre-registering helps avoid any delays that can occur when manually registering endpoints.

- **End-users can reset existing endpoints themselves**: If users have existing Windows endpoints, they can reset the devices themselves. When they're reset, it restores the endpoints to a minimum baseline and managed state. It doesn't require a high cost IT intervention or physical access to the endpoint.

> [!NOTE]
> It's not recommended to use Windows Autopilot to hybrid Azure AD join newly provisioned endpoints. It works, but there are some challenges. On newly provisioned endpoints, use Windows Autopilot to Azure AD join (not hybrid Azure AD join).
>
> To help determine the join method that's right for your organization, see [Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md).

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
