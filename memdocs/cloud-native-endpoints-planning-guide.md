---
# required metadata

title: Update your workloads to support cloud native endpoints
titleSuffix: Microsoft Endpoint Manager
description: To support hybrid and remote workers, convert or migrate your workloads to support cloud native endpoints. This planning guide focuses on deploying apps and updates with Endpoint Manager, moving from group policy objects, and using Windows Autopilot.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 04/04/2022
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

For more information on the benefits to the organization and its end users, see [Get started with cloud native endpoints and Microsoft Endpoint Manager](cloud-native-endpoints-overview.md).

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
- Implementing a work around for accessing and using that service from a cloud native endpoint
- Validating the service requirements
- Accepting that the service isn't cloud native friendly, which may be acceptable for your users and your organization

Either way, you should plan to update your workloads to support cloud native endpoints. 

Your workloads should have the following characteristics:

- Securely accessible from anywhere an end user is located or connected without requiring a connection to a corporate or internal network
- Hosted in, by, or through a cloud service
- Not dependant on the use of any specific end user device

Remember, it's common for workloads to depend on other workloads. Cloud native endpoints also include the services and workloads that support the endpoints.

### Common workloads and solutions

The following workloads are customer specific configuration, tools, processes, and services for enabling user productivity and endpoint management.

Your exact workloads, details, and how to update the workloads for cloud native endpoints might be different. Also, you don’t need to transition every workload. But, you do need to consider each workload, its impact on user productivity, and the device management abilities. Converting some workloads to use cloud native endpoints might take longer than others. Workloads may also have interdepdnancies on one another that must be considered.

- **Device identity**
  
  A device's identity is determined by which identity providers (IdP) have knowledge of and a seucirty trust with the device. For Windows endpoints, the two prevalent IdP's are on-premises Active Directory (AD) and Azure Active Directory (AAD). Endpoint's with identities from one of these two IdP's are typically joined to one or both.

  - For cloud native endpoints, AAD join is the best choice for the device's identity as this requires no connectivity to an on-premises network, resource, or service.
  - On-premises AD join and hybrid Azure AD join require connectivity to an on-premises domain controller. They need connectivity for initial user sign in, to delivery group policies, and change passwords. These options aren’t suitable for cloud native endpoints.

> [!NOTE]
> AAD registration, sometimes referred to as workplace join, is intended as a BYOD scenario only and should not be considered for use on corporate owned Windows endpoints. Because of this, some functionality may not be supported or work as expected on AAD registered Windows endpoints.

- **Provision your endpoints**

  For newly deployed Azure AD join endpoints, use Windows Autopilot to pre-configure devices. Joining Azure AD is typically a user-driven task, and Windows Autopilot is designed with end users in mind. Windows Autopilot enables provisioning using the cloud from anywhere on the Internet, and by any user.

  For more information, see:

  - [Windows Autopilot overview](/mem/autopilot/windows-autopilot)
  - [Windows Autopilot scenarios and capabilities](/mem/autopilot/windows-autopilot-scenarios)

- **Deploy software and applications**

  Nearly all users rely heavily on software and applications not included with the core operating system to be productive and perform their job. Which software applications each user may need is highly variable in most organizations based on many different circumstances and criteria. In many cases, the full matrix of these requirements may not be fully known or understood by the central IT department, however, delivering and managing these applications is still the repsonsbility of that same IT department. Users should be able to request and install the applications they need to complete their job functions regardless of which endpoint they are using or where they are using it from.

  - Software and applications should be deployed from a cloud-based system, like Intune or Configuration Manager (with a [CMG](/mem/configmgr/core/clients/manage/cmg/overview) and [co-management](/mem/configmgr/comanage/how-to-prepare-win10)).
  - User self-service should be considered to reduce initial provisioning time, eliminate unnecessary complexity, and reduce user confusion that may result from deploying software not needed by the end user. This is reduces the buden from IT from attempting to micro-manage and pre-determine every possible permutation or combination of software to install to users within the origanization.

  For more information, see:

  - [Windows 10/11 app deployment using Microsoft Intune](/mem/intune/apps/apps-windows-10-app-deploy)
  - [Introduction to app management in Configuration Manager](/mem/configmgr/apps/understand/introduction-to-application-management)

- **Configure device settings using policies**

  Policy management, including security, is the foundation for most endpoint management. Endpoint policies enable an organization to enforce a specific security baseline as well as a standard configuration on managed endpoints. With a cloud-native endpoint, a lighter-touch approach is strongly recommended particularily for items considered user preferences.

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

  The requirement and need to deploy updates, particularily security updates, is universally understood and accepted so no justification is needed for this workload. However, many traditional on-prem solutions are not capable of delviering updates to cloud-native endpoints at all or in an efficient manner. From a security perspective, this may be the most important, and thus first worload that you should transition to support cloud-native Windows endpoints.

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

  <JS> We need some more discussion on this as these are great questions that we (Microsoft) have provided no good answers for.
  
  User data is the most critical product of a user's work. This data is often shared with other users, both internal and external to an organization for a variety of purposes. For a user to be productive in a cloud-native context, they must have the ability to produce data and access that content on any endpoint they choose to work on. Depending on the application used to create the content and how that content is stored, the content may or may not synchronized to the local endpoint. Also, Depending on the criticiality and sensitivity of the data, this data may be protected, but it must still be accesible. User data includes the following items:

    - User documents
    - Mail app configuration
    - Browser favorites
    - LOB application-specific data
    - LOB application-specific configuration
  
  User settings, while not necessarily as critical as user data, may still be important to a user's productivity. These settings include user preferences for operating system and application settings as well as configuration for applications and the operating system that enable the user to complete their work. Most operating system specific settings and configuration are stored in the registry. This is true for many applications as well but this is application specific and determined by the application vendor and not Microsoft.
  
  User data is best stored in a cloud storage provider that handles underlying details like synchronization, sharing, offline access, and conflict resolution. Microsoft OneDrive is the best example of a cloud storage provider. User settings, because of their variable nature and possible volatility have no one solution to meet the requirements of cloud-native endpoints.

- **Access on-premises resources**
  
  While you can transition most workloads to a cloud-native friendly solution, this will some amount of time in most cases. In some cases, your organization may simply not be able to transition to a cloud-native firendly solution in the forseeable future. For these scenarios, accessing the existing on-p;remises resource or service may be the only viable choice and thus some level of access for at least some users will still be required. For these on-premises services, resources, and applications, there are two main consideration that you must reconcile.

  - **Authentication and authorization**: To access on-premises resources from cloud native endpoints, users need to authenticate and verify who they are. For more specific information, see [Authentication and access to on-premises resources with cloud native endpoint](cloud-native-endpoints-on-premises.md#authentication-and-access-to-on-premises-resources).

  - **Connectivity**: Review and evaluate apps and resources that only live on-premises. Connectivity and access to these resources should be available off-premises, and without any direct connectivity, like a VPN. This task might include moving to SaaS versions of your apps, using [Azure AD Application Proxy](/azure/active-directory/app-proxy/application-proxy), [Azure Virtual Desktop](/azure/virtual-desktop/overview), [Windows 365](/windows-365/overview), [SharePoint](/sharepoint/introduction), [OneDrive](/onedrive/plan-onedrive-enterprise), or [Microsoft Teams](/microsoftteams/teams-overview).

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

2. After the initial set of workloads support cloud native endpoints, identify more workloads, and continue the process.

### ✅ Phase 4: Prepare your end users

End users will have different experiences for receiving, deploying, and being supported on their devices. Administrators should:

- Review existing processes and documentation to identify where changes will be visible to end users.
- Update documentation.
- Develop an education strategy to share the changes and benefits users will experience.

## Transition your organization in phases

The following phases contain a high-level approach for organizations to move their environment to fully support cloud-native Windows endpoints. These phases are parallel to transitioning endpoints and user workloads. They may depend on certain workloads being partially or fully transitioned to support cloud-native Windows endpoints.

### ✅ Phase 1: Planning

Define and clarify additional items that need to be planned logistically to support workloads and their move to supporting cloud-native.

1. Define the endpoints that require a cloud identity. This is necessary as not all endpoints in an organization may require a cloud identity. Endpoints not connected to the Internet or for on-premises use only cannot or should not have a cloud identity and thus should not be considered for migration to cloud-native.
2. Define dependencies. Workloads, users, and devices have many technical and non-technical dependancies. To successfully transition a workload with minimal impact to users and the orgnaization, you must account for these dependancies. A wide variety of things may be a dpednancy depending on the workload including business processes and continuity, security standards, local laws and regulations, user knowledge and use of the workload, and cpaital or operational costs and budget. The basic question to answer for each workload is what will be affected if we change anything about the services provided by this workload. You must account for the effects of this change.
3. Define milestones and success criteria for each workload's transition to cloud-native friendly. This is a basic tracking mechanism to understand and define the progress of the transition. Each workload will have it's own milestones and success criteria based on the organization's use of the workload and it's applicability to specific endpoints and users.
4. Autopilot planning including the following items:
  - How and when devices will be registered
  - Necessary group tags for targeting policies
  - Profile creation, configuration, and targeting

### ✅ Phase 2: Enable endpoint cloud hybrid identity

For existing Windows endpoints that you do not wish to reset at this time, enable hybrid Azure AD join so that these existing endpoints can use cloud services that require a cloud identity. This is a trasitory step on your organization's path to cloud-native and is not a final stage or expected end state for any endpoints. All existing endpoints should eventually be reset to fully embrace cloud-native. See [Configure hybrid Azure AD join](/azure/active-directory/devices/howto-hybrid-azure-ad-join) for complete details on enabling hybrid Azure AD join.
  
> [!NOTE]
> There is no Microsoft supported path to convert existing endpoints from on-premises domain joined or hybrid Azure Active Directory joined to Azure Active Directory joined. One end-result of using fully cloud-native endpoints is enabling user independence from their devices such that resetting an endpoint is does not impact the end-user. This is because their applications, configuration, and data is still readily accessible or will replicate to the newly provisioned endpoint in a short-amount of time.

### ✅ Phase 3: Cloud attach Configuration Manager (optional)

If you use Configuration Manager, then cloud attach your environment to Microsoft Intune. If you don't use Configuration Manager, then skip this step.

When you cloud attach, you can remotely manage your client endpoints, co-manage your endpoints with Intune (cloud) and Configuration Manager (on-premises), and access the Endpoint Manager admin center.

For more specific information, see [Cloud attach your Configuration Manager environment](/mem/configmgr/cloud-attach/overview) and [Walk through the Microsoft Endpoint Manager](/mem/intune/fundamentals/tutorial-walkthrough-endpoint-manager).

### ✅ Phase 4: Create an Azure AD joined proof of concept

This phase can start at nearly any time and is critical to identify potential (and possibly unknown) issues and validate overall functionality and resolutions to those issues. As with all proofs of concept, the ultimate intent is to prove and validate functionality in an actual enterpise environment instead of a pristine lab environment. Important steps for this phase include the following:

1. Implement a minimum viable configuration for enforcement using Intune. This is important as you do not want to introduce endpoints onto your internal network or for production use that do not adhere to your organization's security standards or are not configured for an end user to perform their work. This minimum configuration does not and should not have all possible configuration applied as the intent is to discover additional configuration required for end users to be succesful.
2. Configure Windows Autopilot for Azure AD joined. Provisioning new endpoints and reprovisioning existing endpoints using Autopilot is the best and fastest way to introduce AAD joined systems to your organization and is thus an important part of the POC. 
3. Deploy POC Azure AD joined systems. POC endpoints should be a cross-section of endpoints in the environment that are indicative and representative of various configurations and users to enable as much validation of this new system state as possible. Only real production use by real production users will fully validate the functionality of all workloads within an organization. Through natural, day-to-day use of the POC AAD endpoints, users will organicly test and validate all workloads in an organization. Checklists of business critical functionality and scenarios can be provided to users of these POC devices as well if desired to ensure these are accounted for. These will be specific to each organization and may evolve or change as workloads are transitioned to cloud-native friendly workloads.
4. Validate functionality. Based on feedback from the users of the POC endpoints, workloads and their functionality with repect to cloud-native endpoints is validated through actual use. In some cases, additional blockers or previously unknown or unaccounted for workloads or scenarios may also be discovered. Validation is utlimately an interative process based on the workloads and their configuration within an organization. Using the milestones and success criteria previously established for each workload is key in determining the progress and scope of the POC. 

### ✅ Phase 5: Implement full modern provisioning

?? This whole section needs rewritten. This needs explained. Is a whole phase needed for just one sentence? ??

This phase transitions new Windows endpoint provisioning to Azure AD joined.

### ✅ Phase 6: Azure AD join your existing Windows endpoints

Once all blockers and issues have been resolved, you can move existing devices to be fully cloud native. You have the following options:

- **Option 1: Replace your devices**. If the devices are end-of-life or don't support modern security, then replacing them is the best choice. Modern devices support new and enhanced security features, including the Trusted Platform Module (TPM) technology.

- **Option 2: Reset the Windows devices**. If your existing devices support the newer security features, then you can reset the devices. During the out of box experience (OOBE) or when users sign in, they can join the devices to Azure AD.

  When resetting an existing Windows endpoint, be sure to clean up (??Does this mean delete? Need more info??) the existing Azure AD device object, the Intune device object, and the Windows Autopilot device registration. Then, re-provision the endpoint.

When the devices are ready, join these devices to Azure AD using the option that best for your organization. For more specific information, see [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join) and [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan).

## Move from group policy objects (GPOs)

Many organizations use GPOs to configure and manage their Windows endpoints. 

Over time, it gets complicated due to a lack of documentation, lack of clarity in the policy's purpose or requirements, using legacy or non-functional policies, and using complex features. For example, there might be policies that include WMI filters, have complex OU structures, and use inheritance blocking, loopback, or security filtering.

### Manage settings using Intune

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
