---
# required metadata

title: Update your workloads to support cloud-native endpoints
titleSuffix: Microsoft Intune
description: To support hybrid and remote workers, convert or migrate your workloads to support cloud-native endpoints. This planning guide focuses on deploying apps and updates with Intune, moving from Group Policy Objects, and using Windows Autopilot.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/08/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high
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
  - intune-scenario
---

# High level planning guide to move to cloud-native endpoints

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](../../includes/cloud-native-endpoints-definitions.md)]

This high level planning guide includes ideas and suggestions you need to consider for your adoption and migration to cloud-native endpoints. It discusses managing devices, reviewing & transitioning existing workloads, making organization changes, using Windows Autopilot, and more.

This feature applies to:

- Windows cloud-native endpoints

Moving your Windows endpoints to cloud-native has many advantages, including long term advantages. It's not an overnight process and must be planned to avoid issues, outages, and negative user impact.

For more information on the benefits to the organization and your users, go to [What are cloud-native endpoints](cloud-native-endpoints-overview.md).

To be successful, consider the key areas described in this article for your planning and deployment. With proper planning, communications, and process updates, your organization can be cloud-native.

## Manage devices using a cloud-native MDM provider

Managing your endpoints, including cloud-native endpoints, is an important task for all organizations. With cloud-native endpoints, the management tools you use must manage the endpoints wherever they go.

If you don't currently use a mobile device management (MDM) solution, or want to move to a Microsoft solution, then the following articles are good resources:

- [What is Microsoft Intune?](../../intune/fundamentals/what-is-intune.md)
- [Get started with Microsoft Intune](../../intune/fundamentals/get-started-with-intune.md)

With the Microsoft Intune family of products and services, you have the following endpoint management options:

- **[Microsoft Intune](../../intune/index.yml)**: Intune is 100% cloud-based, and uses the Intune admin center to manage devices, manage apps on devices, create & deploy policies, review reporting data, and more.

  For more information on using Intune to manage your endpoints, go to:

  - [Microsoft Intune securely manages identities, manages apps, and manages devices](../../intune/fundamentals/what-is-intune.md)
  - [Deployment guide: Setup or move to Microsoft Intune](../../intune/fundamentals/deployment-guide-intune-setup.md)
  - [Microsoft Intune planning guide](../../intune/fundamentals/intune-planning-guide.md)

- **[Microsoft Configuration Manager](../../configmgr/index.yml)**: Configuration Manager uses an on-premises infrastructure, and can manage servers. When you use [co-management](../../configmgr/comanage/overview.md), some workloads use Configuration Manager (on-premises), and some workloads use Microsoft Intune (cloud).

  For cloud-native endpoints, your Configuration Manager solutions should use a [Cloud Management Gateway (CMG)](../../configmgr/core/clients/manage/cmg/overview.md) and [co-management](../../configmgr/comanage/how-to-prepare-win10.md).

## Review your endpoint and user workloads

At a high level, deploying cloud-native endpoints requires modern strategies for identity, software distribution, device management, OS updates, and managing user data & configuration. Microsoft has solutions that support these areas for your cloud-native endpoints.

To start, review each workload, and determine how it can or will support your cloud-native endpoints. Some workloads may already support cloud-native endpoints. Native support depends on the specific workload, how your organization implements the workload services, and how your users use the services.

To determine if your workloads support cloud-native endpoints, you need to investigate and validate these services.

If a service or solution doesn't support cloud-native endpoints, then determine its impact and its criticality on your users and your organization. When you have this information, you can determine the next steps, which may include:

- Working with the service vendor
- Updating to a new version
- Using a new service
- Implementing a work-around for accessing and using that service from a cloud-native endpoint
- Validating the service requirements
- Accepting that the service isn't cloud-native friendly, which may be acceptable for your users and your organization

Either way, you should plan to update your workloads to support cloud-native endpoints.

Your workloads should have the following characteristics:

- Securely access apps and data from anywhere users are located. Access doesn't require a connection to a corporate or internal network.
- Hosted in, hosted by, or hosted through a cloud service.
- Doesn't require or depend on a specific device.

### Common workloads and solutions

Cloud-native endpoints also include the services and workloads that support the endpoints.

The following workloads are configuration, tools, processes, and services for enabling user productivity and endpoint management.

Your exact workloads, details, and how to update the workloads for cloud-native endpoints might be different. Also, you don't need to transition every workload. But, you do need to consider each workload, its impact on user productivity, and the device management abilities. Converting some workloads to use cloud-native endpoints might take longer than others. Workloads may also have interdependencies on each other.

- **Device identity**

  A device's identity is determined by the identity providers (IdP) that have knowledge of the device and a security trust with the device. For Windows endpoints, the most common IdP's are on-premises Active Directory (AD) and Microsoft Entra ID. Endpoints with identities from one of these IdP's are typically joined to one or joined to both.

  - For cloud-native endpoints, Microsoft Entra join is the best choice for the device's identity. It doesn't require any connectivity to an on-premises network, resource, or service.
  - On-premises AD join and hybrid Microsoft Entra join require connectivity to an on-premises domain controller. They need connectivity for initial user sign-in, to deliver group policies, and change passwords. These options aren't suitable for cloud-native endpoints.

  > [!NOTE]
  > Microsoft Entra registration, sometimes referred to as workplace join, is for bring your own device (BYOD) scenarios only. It shouldn't be used for organization owned Windows endpoints. Some functionality may not be supported or work as expected on Microsoft Entra registered Windows endpoints.

- **Provision your endpoints**

  For newly deployed Microsoft Entra join endpoints, use Windows Autopilot to preconfigure devices. Joining Microsoft Entra is typically a user-driven task, and Windows Autopilot is designed with users in mind. Windows Autopilot enables provisioning using the cloud from anywhere on the Internet, and by any user.

  For more information, go to:

  - [Windows Autopilot overview](/autopilot/overview)
  - [Windows Autopilot scenarios and capabilities](/autopilot/windows-autopilot-scenarios)

- **Deploy software and applications**

  Most users need and use software and applications not included with the core operating system. In many cases, IT doesn't know or understand the specific app requirements. However, delivering and managing these applications is still the responsibility of your IT team. Users should be able to request and install the applications they need to do their job, regardless of the endpoint they're using or where they're using it from.

  - To deploy software and applications, use a cloud-based system, like Intune or Configuration Manager (with a [CMG](../../configmgr/core/clients/manage/cmg/overview.md) and [co-management](../../configmgr/comanage/how-to-prepare-win10.md)).

  - Create a baseline of apps that your endpoints must have, like Microsoft Outlook and Teams. For other apps, let users install their own apps.

    On your endpoints, you can use the [Company Portal app](/windows/application-management/private-app-repository-mdm-company-portal-windows-11) as your app repository. Or, use a user-facing portal that lists the apps that can be installed. This self-service option reduces provisioning time of new and existing devices. It also reduces the burden on IT, and you don't have to deploy apps that users don't need.

  For more information, go to:

  - [Windows 10/11 app deployment using Microsoft Intune](../../intune/apps/apps-windows-10-app-deploy.md)
  - [Introduction to app management in Configuration Manager](../../configmgr/apps/understand/introduction-to-application-management.md)
  - [Private app repository in Windows 11](/windows/application-management/private-app-repository-mdm-company-portal-windows-11)

- **Configure device settings using policies**

  Policy and security management is core in endpoint management. Endpoint policies allow your organization to enforce a specific security baseline and a standard configuration on your managed endpoints. There are many settings you can manage and control on your endpoints. **DO** create policies that only configure what's required in your baseline. **DON'T** create policies that control common user preferences.

  - Traditional policy enforcement using group policy isn't possible with cloud-native endpoints. Instead, you can use Intune to create policies to configure many settings, including built-in features like the [Settings Catalog](../../intune/configuration/settings-catalog.md) and [administrative templates](../../intune/configuration/administrative-templates-windows.md).

    You can reference and analyze existing GPOs using [Group Policy analytics in Intune](../../intune/configuration/group-policy-analytics.md), which allows you to see if settings within your GPOs are supported in the cloud. Group Policy analytics also allows you to create Intune policies from GPOs, if that's the right step for your organization. In general, we recommend that customers implement policies that conform to their requirements, instead of directly migrating existing GPOs to Intune. When you create policies based off your requirements, then you rationalize, optimize, and streamline your Intune policies.

  - If you have existing policies that issue certificates, manage BitLocker, and provide endpoint protection, then you need to create new policies in Intune or Configuration Manager (with a [CMG](../../configmgr/core/clients/manage/cmg/overview.md) and [co-management](../../configmgr/comanage/how-to-prepare-win10.md)).

    For more information, go to:

    - [Use certificates for authentication in Microsoft Intune](../../intune/protect/certificates-configure.md)
    - [Disk encryption policy for endpoint security in Intune](../../intune/protect/endpoint-security-disk-encryption-policy.md)
    - [Add Endpoint protection settings in Intune](../../intune/protect/endpoint-protection-configure.md)
    - [Certificates in Configuration Manager](../../configmgr/core/plan-design/security/certificates-overview.md)
    - [BitLocker management in Configuration Manager](../../configmgr/protect/plan-design/bitlocker-management.md)
    - [Endpoint Protection in Configuration Manager](../../configmgr/protect/deploy-use/endpoint-protection.md)

- **Deploy security, feature, and app updates**

  Many on-premises solutions can't deploy updates to cloud-native endpoints or deploy them efficiently. From a security perspective, this workload may be the most important. It should be the first workload that you transition to support cloud-native Windows endpoints.

  - **Deploy Windows updates** using a cloud-based system, like Windows Update for Business. Using Intune or Configuration Manager (with a [CMG](../../configmgr/core/clients/manage/cmg/overview.md) and [co-management](../../configmgr/comanage/how-to-prepare-win10.md)), you can use Windows Update for Business to deploy security updates and feature updates.

    For more information, go to:

    - [Manage Windows 10 and Windows 11 software updates in Intune](../../intune/protect/windows-update-for-business-configure.md)
    - [Integrate Configure Manager with Windows Update for Business](../../configmgr/sum/deploy-use/integrate-windows-update-for-business-windows-10.md)
    - [Choose how to manage updates to Microsoft 365 Apps](/deployoffice/choose-how-manage-updates-microsoft-365-apps)

  - **Deploy Microsoft 365 app updates** using the following options:

    - **Intune**: Create a policy that sets the Update Channel, removes other app versions, and more.
    - **Configuration Manager** (with a [CMG](../../configmgr/core/clients/manage/cmg/overview.md) and [co-management](../../configmgr/comanage/how-to-prepare-win10.md)): Manage your apps, including update stats, copy, retire, and more.

    For more information, go to:

    - [Add Microsoft 365 apps to Windows 10/11 devices with Microsoft Intune](../../intune/apps/apps-add-office365.md)
    - [Management tasks for Configuration Manager apps](../../configmgr/apps/deploy-use/management-tasks-applications.md)

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

- **Access on-premises resources**

  Some organizations can't transition some workloads to cloud-native solutions. The only option might be accessing existing on-premises resources or services from a cloud-native endpoint. For these scenarios, users need access.

  For these on-premises services, resources, and applications, consider the following tasks:

  - **Authentication and authorization**: To access on-premises resources from cloud-native endpoints, users need to authenticate and verify who they are. For more specific information, go to [Authentication and access to on-premises resources with cloud-native endpoint](cloud-native-endpoints-on-premises.md#authentication-and-access-to-on-premises-resources).

  - **Connectivity**: Review and evaluate apps & resources that only live on-premises. Connectivity and access to these resources should be available off-premises, and without any direct connectivity, like a VPN. This task might include moving to SaaS versions of your apps, using [Microsoft Entra Application Proxy](/entra/identity/app-proxy/overview-what-is-app-proxy), [Azure Virtual Desktop](/azure/virtual-desktop/overview), [Windows 365](/windows-365/overview), [SharePoint](/sharepoint/introduction), [OneDrive](/onedrive/plan-onedrive-enterprise), or [Microsoft Teams](/microsoftteams/teams-overview).

  > [!NOTE]
  > Microsoft Entra doesn't support the Kerberos authentication protocol. On-premises AD does support the Kerberos authentication protocol. In your planning, you may learn more about Microsoft Entra Kerberos. When configured, users sign in to a cloud-native endpoint using their Microsoft Entra account, and can access on-premises apps or services that use Kerberos authentication.
  >
  > Microsoft Entra Kerberos:
  >
  > - Isn't used in cloud-native solutions.
  > - Doesn't solve any connectivity issues for resources that require authentication through Microsoft Entra.
  > - Isn't the answer or work-around for any domain authentication requirements through Microsoft Entra.
  > - Doesn't address the machine authentication challenges listed at [Known Issues and important information](cloud-native-endpoints-known-issues.md).
  >
  > For a deeper understanding of Microsoft Entra Kerberos and the scenarios it can address, go to the following blogs:
  >
  > - [Why We Built Microsoft Entra Kerberos](https://syfuhs.net/why-we-built-azure-ad-kerberos) (opens an external website)
  > - [Deep dive: How Microsoft Entra Kerberos works](https://techcommunity.microsoft.com/t5/itops-talk-blog/deep-dive-how-azure-ad-kerberos-works/ba-p/3070889) (opens another Microsoft website)
  > - [How Microsoft Entra Kerberos Works (syfuhs.net)](https://syfuhs.net/how-azure-ad-kerberos-works) (opens an external website)

## Transition your workloads in phases

Modernizing workloads and adopting cloud-native endpoints requires changes to operational processes and procedures. For example:

- Administrators need to understand how changes to existing workloads might change their processes.
- The service desk needs to understand the new scenarios they'll be supporting.

When reviewing your endpoints and workloads, break down the transition into phases. This section provides an overview on some recommended phases your organization can use. These phases can be repeated as many times as needed.

### ✅ Phase 1: Get info on your workloads

This phase is the information gathering phase. It helps you establish the scope of what you must consider for your organization to transition to cloud-native. It involves defining exactly what services, products, and applications involved with each workload in your environment.

In this phase:

1. Inventory your current workload information and details. For example, know their current state, what they provide, who they serve, who maintains them, if they're critical to cloud-native, and how they're hosted.

    When you have this information, you can understand and define the end goal, which should be:

    - To support cloud-native endpoints
    - To know the services, products, and applications used by each workload

    You need to coordinate with the owners of the different services, products, and applications. You want to make sure that cloud-native endpoints support user productivity without connectivity or location constraints.

    Examples of common services and applications include line of business (LOB) applications, internal websites, file shares, authentication requirements, application and OS update mechanisms, and application configuration. Basically, they include anything and everything users need to fully do their jobs.

2. Verify the end-state for each workload. Identify known blockers that prevent getting to this end-state or prevent supporting cloud-native endpoints.

    Some workloads and their services & applications may already be cloud-friendly or enabled. Some may not. Getting to the end-state for each workload may require organization investment & effort. It may include updating software, "lifting and shifting" to a new platform, migrating to a new solution, or making configuration changes.

    The steps needed for each workload are different with each organization. They depend on how the service or application is hosted and accessed by users. This end-state should address the primary challenge of enabling users to do their work on a cloud-native endpoint, regardless of location or connectivity to the internal network.

    Based on each defined end-state, you may discover or define that cloud-enabling a service or application is difficult or blocked. This situation can happen for different reasons, including technical or financial limitations. These limitations need to be clear and be understood. You need to review their impact and determine how to move each workload to be cloud-native friendly.

### ✅ Phase 2: Prioritize any blockers

After you've identified the key workloads and their end-state blockers, then:

1. Prioritize each blocker and evaluate each blocker for resolution.

    You may not want or need to address all blockers. For example, your organization might have workloads, or a part of workloads, that don't support your cloud-native endpoints. This lack of support may or may not be significant for your organization or users. You and your organization can make this decision.

2. To support testing and proof of concept (POC), start with a minimum set of workloads. The goal is to test and validate a sample of your workloads.

    As part of the POC, identify a set of users and devices in a pilot to run a real world production scenario. This step helps prove if the end-state enables user productivity.

    In many organizations, there's a role or business group that is easier to migrate. For example, you can target the following scenarios in your POC:

    - Highly mobile sales team whose primary requirements are productivity tools and an online customer relationship management solution
    - Knowledge workers who primarily access content that's already in the cloud and rely heavily on Microsoft 365 apps
    - Frontline worker devices that are highly mobile, or are in environments where they don't have access to the organization network

    For these groups, review their workloads. Determine how these workloads can move to modern management, including identity, software distribution, device management, and more.

    For each of the areas in your pilot, the number of items or tasks should be low. This initial pilot helps you create the processes and procedures required for more groups. It also helps create your long term strategy.

    For more guidance and tips, go to the [Microsoft Intune planning guide](../../intune/fundamentals/intune-planning-guide.md). It applies to Intune, but also includes some guidance when using pilot groups and creating rollout plans.

### ✅ Phase 3: Transition your workloads

In this phase, you're ready to implement your changes.

1. Move unblocked workloads to your planned cloud-native solutions or end-state. Ideally, this step is broken into smaller work items. The goal is to continue business operations with minimal disruption.

2. After the first set of workloads support cloud-native endpoints, identify more workloads, and continue the process.

### ✅ Phase 4: Prepare your users

Users have different experiences for receiving, deploying, and being supported on their devices. Administrators should:

- Review existing processes and documentation to identify where changes are visible to users.
- Update documentation.
- Create an education strategy to share the changes and benefits users will experience.

## Transition your organization in phases

The following phases are a high-level approach for organizations to move their environment to support cloud-native Windows endpoints. These phases are parallel to transitioning endpoints and user workloads. They may depend on certain workloads being partially or fully transitioned to support cloud-native Windows endpoints.

### ✅ Phase 1: Define endpoints, dependencies, and milestones

This phase is the first step for your organization migration to be fully cloud-native. Review what you currently have, define success criteria, and start planning how your devices will be added to Microsoft Entra.

1. **Define the endpoints that require a cloud identity**

    - Endpoints that use internet access require a cloud identity. You'll add these endpoints to Microsoft Entra.
    - Endpoints that don't use the internet or are only used on-premises shouldn't have a cloud identity. Don't migrate these scenarios to be cloud-native.

2. **Define dependencies**

    Workloads, users, and devices have technical and non-technical dependencies. To transition with minimal impact to users and the organization, you must account for these dependencies.

    For example, a dependency can be:

    - Business processes and continuity
    - Security standards
    - Local laws and regulations
    - User knowledge and use of the workload
    - Capital, operational costs and budget

    For each workload, ask "What is affected if we change anything about the services provided by this workload?". You must account for the effects of this change.

3. **Define milestones and success criteria for each workload**

    Each workload has its own milestones and success criteria. They can be based on the organization's use of the workload and its applicability to specific endpoints and users.

    To understand and define the progress of the transition, track and monitor this information.

4. **Plan your Windows Autopilot deployment**

    - Determine how and when devices will be registered to your organization.
    - Determine and create the necessary group tags to target your Windows Autopilot policies.
    - Create your Windows Autopilot profile with its configuration settings, and target the devices that will receive your profile.

    For more information, go to:

    - [Windows Autopilot overview](/autopilot/overview)
    - [Windows Autopilot scenarios and capabilities](/autopilot/windows-autopilot-scenarios)

### ✅ Phase 2: Enable endpoint cloud hybrid identity (optional)

To be fully cloud-native, Microsoft recommends existing Windows endpoints be reset as part of a hardware refresh cycle. When you reset, the endpoint is restored back to factory settings. All apps, settings, and personal data on the device is deleted.

If you're not ready to reset your endpoints, then you can enable hybrid Microsoft Entra join. A cloud identity is created for hybrid Microsoft Entra join endpoints. Remember, hybrid Microsoft Entra join still requires on-premises connectivity.

Remember, hybrid Microsoft Entra join is a transitionary step to cloud-native, and isn't the end goal. The end goal is for all existing endpoints to be fully cloud-native.

When endpoints are fully cloud-native, user data is stored in a cloud storage provider, like OneDrive. So when an endpoint is reset, the user applications, configuration, and data is still accessible, and can replicate to a newly provisioned endpoint.

For more information, go to:

- [Microsoft Entra joined vs. Hybrid Microsoft Entra joined](azure-ad-joined-hybrid-azure-ad-joined.md)
- [Configure hybrid Microsoft Entra join](/entra/identity/devices/how-to-hybrid-join)

> [!NOTE]
> Microsoft doesn't have a migration utility to convert existing endpoints from on-premises domain joined or hybrid Microsoft Entra joined to Microsoft Entra joined. Microsoft recommends these devices be reset and redeployed as part of a hardware refresh.

### ✅ Phase 3: Cloud attach Configuration Manager (optional)

If you use Configuration Manager, then cloud attach your environment to Microsoft Intune. If you don't use Configuration Manager, then skip this step.

When you cloud attach, you can remotely manage your client endpoints, co-manage your endpoints with Intune (cloud) and Configuration Manager (on-premises), and access the Intune admin center.

For more specific information, go to [Cloud attach your Configuration Manager environment](../../configmgr/cloud-attach/overview.md) and [Walk through the Microsoft Intune admin center](../../intune/fundamentals/tutorial-walkthrough-endpoint-manager.md).

### ✅ Phase 4: Create a Microsoft Entra joined proof of concept

This critical phase can start at any time. It helps identify potential issues, unknown issues, and validates overall functionality and resolutions to those issues. As with all POCs, the goal is to prove and validate functionality in an actual enterprise environment instead of a lab environment.

Important steps for this phase include:

1. **Implement a minimum baseline configuration using Intune**

    This step is important. You don't want to introduce endpoints to your network or to production that:

    - Don't follow your organization's security standards
    - Aren't configured for users to do their work.

    This minimum configuration doesn't and shouldn't have all possible configurations applied. Remember, the intent is to discover more configurations that are required for users to be successful.

2. **Configure Windows Autopilot for Microsoft Entra joined endpoints**

    Using Windows Autopilot to provision new endpoints and reprovision existing endpoints is the fastest way to introduce Microsoft Entra joined systems to your organization. It's an important part of the POC.

3. **Deploy a POC for Microsoft Entra joined systems**

    - Use a mix of endpoints that represent different configurations and users. You want as much validation of this new system state as possible.

    - Only real production use by real production users will fully validate the workloads and their functionality. Through natural, day-to-day use of the POC Microsoft Entra endpoints, users organically test and validate your workloads.

    - Create checklists of business critical functionality and scenarios, and give these lists to your POC users. The checklists are specific to each organization and may change as workloads are transitioned to cloud-native friendly workloads.

4. **Validate functionality**

    Validation is a repetitive process. It's based on the workloads and their configuration within your organization.

    - Collect user feedback on the POC endpoints, workloads, and their functionality. This feedback should be from users that used the cloud-native endpoints.

      Other blockers, and previously unknown or unaccounted for workloads/scenarios may be discovered.

    - Use the milestones and success criteria previously established for each workload. They'll help determine the progress and scope of the POC.

### ✅ Phase 5: Microsoft Entra join your existing Windows endpoints

This phase transitions new Windows endpoint provisioning to Microsoft Entra joined. Once all blockers and issues have been resolved, you can move existing devices to be fully cloud-native. You have the following options:

- **Option 1: Replace your devices**. If the devices are end-of-life or don't support modern security, then replacing them is the best choice. Modern devices support new and enhanced security features, including the Trusted Platform Module (TPM) technology.

- **Option 2: Reset the Windows devices**. If your existing devices support the newer security features, then you can reset the devices. During the out of box experience (OOBE) or when users sign in, they can join the devices to Microsoft Entra.

  Before resetting an existing Windows endpoint, be sure to:

  1. [Delete the device in Intune](../../intune/remote-actions/devices-wipe.md#delete-devices-from-the-intune-admin-center).
  2. [Delete the Windows Autopilot device registration](/autopilot/add-devices).
  3. [Delete the existing Microsoft Entra device object](/entra/identity/devices/manage-stale-devices).

  Then, reset the device, and reprovision the endpoint.

When the devices are ready, join these devices to Microsoft Entra using the option that best for your organization. For more specific information, go to [Microsoft Entra joined devices](/entra/identity/devices/concept-directory-join) and [How to: Plan your Microsoft Entra join implementation](/entra/identity/devices/device-join-plan).

## Move from Group Policy Objects (GPOs)

Many organizations use GPOs to configure and manage their Windows endpoints.

Over time, it gets complicated due to a lack of documentation, lack of clarity in the policy's purpose or requirements, using legacy or non-functional policies, and using complex features. For example, there might be policies that include WMI filters, have complex OU structures, and use inheritance blocking, loopback, or security filtering.

### Manage settings using Intune

Microsoft Intune has many built-in settings that can be configured and deployed to your cloud-native endpoints. When moving to Intune for policy management, you have some options.

These options aren't necessarily mutually exclusive. You can migrate a subset of policies and start new for others.

- **Option 1: Start new** (recommended): Intune has many settings to configure and manage your endpoints. You can create a policy, add and configure settings in the policy, and then deploy the policy.

  Many existing group policies include policies that might not apply to cloud-native endpoints. Starting fresh enables an organization to validate and simplify their existing enforced policies, while eliminating legacy, forgotten, or even harmful policies. Intune has built-in templates that group common settings together, like [VPN, Wi-Fi, endpoint protection, and more](../../intune/configuration/device-profiles.md).

- **Option 2: Migrate**: This option involves lifting the existing policies and shifting them to the Intune policy engine. It can be cumbersome and time consuming. For example, you may have many existing group policies and there will be differences with settings on-premises vs. in the cloud.

  If you choose this option, you must review and analyze your existing group policies, and determine if they're still needed or valid on your cloud-native endpoints. You want to eliminate unnecessary policies, including the policies that may cause overhead, or degrade system performance or the user experience. Don't move your group policies to Intune until you know what they do.

### Intune features you should know

Intune also has built-in features that can help you configure your cloud-native endpoints:

- **[Group Policy analytics](../../intune/configuration/group-policy-analytics.md)**: You can import your GPOs in the Microsoft Intune admin center, and run an analysis on the policies. You can see the policies that exist in Intune, and see the policies that are deprecated.

  If you use GPOs, then using this tool is a valuable first step.

  For more information, go to [Group Policy analytics in Intune](../../intune/configuration/group-policy-analytics.md).

- **[Settings catalog](../../intune/configuration/settings-catalog.md)**: See all the settings available in Intune, and create, configure, & deploy a policy using these settings. [Tasks you can complete using the Settings Catalog in Intune](../../intune/configuration/settings-catalog-common-features.md) may also be a good resource. If you create GPOs, then the settings catalog is a natural transition to cloud-native endpoint configuration.

  When combined with [Group Policy analytics](../../intune/configuration/group-policy-analytics.md), you can deploy the policies you used on-premises to your cloud-native endpoints.

  For more information, go to [Settings catalog in Intune](../../intune/configuration/settings-catalog.md).

- **[Administrative templates](../../intune/configuration/administrative-templates-windows.md)**: These templates are similar to the ADMX templates used on-premises, and are built in to Intune. You don't download them. These templates include many settings that control features in Microsoft Edge, Internet Explorer, Microsoft Office apps, remote desktop, OneDrive, passwords, PINs, and more.

  If you use administrative templates on-premises, then using them in Intune is a natural transition.

  For more information, go to [Administrative templates in Intune](../../intune/configuration/administrative-templates-windows.md).

  You can also ingest an existing set of ADMX policies for Win32 and Desktop Bridge apps. For more information, go to:

  - [Understanding ADMX policies - Windows Client Management](/windows/client-management/mdm/understanding-admx-backed-policies)
  - [Enable ADMX policies in MDM - Windows Client Management](/windows/client-management/mdm/enable-admx-backed-policies-in-mdm)
  - [Win32 and Desktop Bridge app ADMX policy Ingestion - Windows Client Management](/windows/client-management/mdm/win32-and-centennial-app-policy-configuration#overview)

  > [!NOTE]
  > Starting in Windows 10 version 1703, Mobile Device Management (MDM) policy configuration support was expanded to allow access of [selected set of Group Policy administrative templates (ADMX policies)](/windows/client-management/mdm/policies-in-policy-csp-admx-backed) for Windows PCs using the [Policy configuration service provider (CSP)](/windows/client-management/mdm/policy-configuration-service-provider). Configuring ADMX policies in Policy CSP is different from the typical way you configure a traditional MDM policy.

- **[Security baselines](../../intune/protect/security-baselines.md)**: A security baseline is a group of pre-configured Windows settings. They help you apply and enforce granular security settings that are recommended by the security teams. When you create a security baseline, you can also customize each baseline to enforce only the settings you want.

  You can create a security baseline for Windows, Microsoft Edge, and more. If you're not sure where to start, or want the security settings recommended by security experts, then look at security baselines.

  For more information, go to [Security baselines in Intune](../../intune/protect/security-baselines.md).

## Use Windows Autopilot to provision new or existing Windows endpoints

If you purchase endpoints from an OEM or partner, then you should use Windows Autopilot.

Some of the benefits include:

- **Built-in Windows setup process**: It presents a branded, guided, and simplified end-user experience.

- **Drop-ship endpoints directly to end-users**: Vendors and OEMs can ship endpoints directly to your users. Users receive the endpoints, sign in with their organization account (`user@contoso.com`), and Windows Autopilot automatically provisions the endpoint.

  This feature helps limit overhead and costs involved with high-touch internal IT processes and shipping.

  For best results, pre-register your endpoints with the OEMs or vendors. Pre-registering helps avoid any delays that can occur when manually registering endpoints.

- **Users can reset existing endpoints themselves**: If users have existing Windows endpoints, they can reset the devices themselves. When they're reset, it restores the endpoints to a minimum baseline and managed state. It doesn't require a high cost IT intervention or physical access to the endpoint.

> [!NOTE]
> It's not recommended to use Windows Autopilot to hybrid Microsoft Entra join newly provisioned endpoints. It works, but there are some challenges. On newly provisioned endpoints, use Windows Autopilot to Microsoft Entra join (not hybrid Microsoft Entra join).
>
> To help determine the join method that's right for your organization, go to [Microsoft Entra joined vs. Hybrid Microsoft Entra joined](azure-ad-joined-hybrid-azure-ad-joined.md).

For more information on Windows Autopilot, go to:

- [Overview of Windows Autopilot](/autopilot/overview)
- [Windows Autopilot scenarios and features](/autopilot/windows-autopilot-scenarios)
- [Windows Autopilot FAQ](/autopilot/faq)

## Follow the cloud-native endpoints guidance

1. [Overview: What are cloud-native endpoints?](cloud-native-endpoints-overview.md)
2. [Tutorial: Get started with cloud-native Windows endpoints](cloud-native-windows-endpoints.md)
3. [Concept: Microsoft Entra joined vs. Hybrid Microsoft Entra joined](azure-ad-joined-hybrid-azure-ad-joined.md)
4. [Concept: Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
5. 🡺 **High level planning guide** (*You are here*)
6. [Known issues and important information](cloud-native-endpoints-known-issues.md)
