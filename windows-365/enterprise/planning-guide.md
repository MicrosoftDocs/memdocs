---
# required metadata
title: Windows 365 planning guide
titleSuffix:
description: Windows 365 planning guide
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 05/09/2023
ms.topic: conceptual
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Planning guide for Windows 365

A successful Windows 365 deployment starts with careful planning. This planning guide walks through common steps to guide you through deployment.

## Determine your objectives

Organizations use Windows 365 to provide a Windows desktop environment to end users. Look at what the goal is and what you want to achieve.

In this section, we’ll discuss common objectives when using Windows 365. Work through the objectives for each of your different Windows 365 use cases.

### Objective: Access organizational apps and data

Determine what your end users need to access on their Cloud PC. If your end users will use Windows 365 as a desktop replacement, then consider productivity apps like Office 365 or collaboration tools like Teams. If your end users use Windows 365 to access specialized software, then make sure to consider installing all line of business apps.

**Task**: Make a list of the applications that need to be used. This list should be tailored to the specific use case.

### Objective: Geographical Regions

Determine where your end users are physically located. Windows 365 can provide Cloud PCs in multiple Azure locations around the world. Provide the Cloud PCs in a location with the lowest latency to your end users' physical location. For more information, see [Supported Azure regions for Cloud PC provisioning](requirements.md#supported-azure-regions-for-cloud-pc-provisioning).

> [!TIP] 
> If you currently use another Azure region not in the list of Windows 365 supported Azure regions, consider leveraging Virtual Network peering to connect a virtual network in a supported Azure region to networks and resources in an Azure regions already in use in your subscription. For more information, see [hub-spoke network topology in Azure](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke). You can also create [hub-spoke network topology with Azure Virtual WAN](/azure/architecture/networking/hub-spoke-vwan-architecture).

**Task**: Map out where your end users are located. List the groups and Azure regions required for all use cases.

### Objective: Management of Cloud PCs

You’ll manage your Cloud PC devices by using the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Your Cloud PCs are automatically enrolled during provisioning. Evaluate who will manage the Cloud PCs and what [permissions](role-based-access.md) should be given to different management groups.

**Task**: Map out which management groups will perform the configuration of the Cloud PC service, management of the Cloud PC device, and software distribution to the devices. Determine which Microsoft Endpoint Manager and Windows 365 permissions will be assigned to different groups to manage the devices.

## Inventory your environment

All users [connect to a Cloud PC](../end-user-access-cloud-pc.md) through a Remote Desktop Client or a supported browser. This connection lets users access their Cloud PC from a wide range of devices.

**Task**: For each use case, determine how your end users will connect to their Cloud PC. Determine which platforms they'll use to connect. Will they use a browser or a Remote Desktop Client to connect?

For information on connectivity requirements and supported configurations, see [Requirements](requirements.md).

## Determine licensing

Each Cloud PC device’s specifications are determined by a [specific license](assign-licenses.md).

**Task**: Review each use case and map the workload to the specific license needed. You should test all workloads per use case.

## Review endpoint management and infrastructure

Many organizations already have a management plan for devices. If you have an existing plan, you should decide if Cloud PC devices will be folded into it, or if you’ll develop a new process.

Review all networking policies and requirements. Many organizations will have policies for how traffic is routed and monitored. For more information on Windows 365 requirements, see [Requirements](requirements.md).

**Task**: Determine how all Cloud PCs will be managed. Determine how policies will be applied (GPO or Intune), applications will be distributed, and the devices will be kept up to date. Review the network topology and determine how the network will route to and from Cloud PCs.

## Create a rollout plan

The next step is to determine how and when your users will receive their Cloud PCs.

- **Define rollout phases**. Create multiple rollout phases based on your environment. Start with pilot and/or testing groups. Early phases should include end users who are ok with change, willing to give feedback, and know that they're the first users. Use this feedback to improve the rollout experience. Later phases should include VIPs and executives. This rollout allows you to improve the deployment as you advance through the phases. Before ending a phase, determine if the phase is successful based on the goals. Modify the configuration, documentation, or notifications based on the feedback.
- **Define your goals and success metrics**.  Make sure goals are SMART (Specific, Measurable, Attainable, Realistic, and Timely). Plan to measure against your goals at each phase so your rollout project stays on track. Possible success metrics include: end user survey results are 80%+ satisfied, usage on provisioned devices is 85% or more.
- **Communicate goals**. Include the goals in all awareness and training activities so that end users understand why your organization chose Windows 365.

**Task**: Create a rollout plan. Include all use cases, phased deployments, and measurable success criteria.

## Communicate Changes

Change management relies on clear and helpful communication about upcoming changes. The best way to have a smooth deployment is to make sure users are aware of all changes and disruptions.

**Task**: Your rollout communication plan should include important information, how to notify users, and when to communicate. Have a plan that includes when, what, and how to communicate.

- Determine what information to communicate. Communicate multiple times to different phases of end users.
  - **Kickoff Phase**: Broad communication that introduces Windows 365. In this communication, make sure to answer these key questions.
    - What is Cloud PC?
    - Why is the organization using Cloud PC? Include benefits to end users and the organization.
    - Provide a high level plan of deployment.
  - **Pilot phase**: Include additional information to the pilot phase end users. Make sure they understand that they're in a pilot phase and should submit feedback.
  - **Onboarding phase**: Communication targeting specific end users and groups that are scheduled to begin using Cloud PC. This communication should inform end users that their Cloud PC is ready to go. Include instructions on how to connect to Cloud PC from any platform the end user might use. In case end users have issues, you should also provide a help desk contact.
- Choose how to communicate Cloud PC to your targeted groups and users. Examples include:
  - Company wide meetings, Microsoft Teams, company newsletters, and email.
  - For onboarding communication, consider sending information in an email to end users.

## Support help desk and end users

Include your IT support and help desk in the early stages of the Windows 365 deployment and planning process. Early involvement lets the support staff gain knowledge and experience in identifying and resolving issues more effectively. It also prepares them for support production rollouts. Knowledgeable help desk and support teams also help end users adopt to changes.

**Task**: Incorporate support training. Validate the end user experience in support with success metrics in your deployment plan.

- Consider who will support end users. Many organizations have multiple tiers and levels for support. Consider how each level can support end users onboarding and using Windows 365.
- Create a help desk workflow. Constantly communicate support issues, trends, and other important information to all tiers in your support team.
- Train your help desk and support teams. Consider training to include all scenarios Windows 365 will be used in. Also consider training on all supported Windows 365 platforms.

## Educate end users

Educate your end users by creating guides on how to:

- Connect to their Cloud PC.
- Use their Cloud PC for their specific scenario.
- Get help and support when needed.

<!-- ########################## -->
## Next steps

[Learn about requirements for Windows 365](requirements.md)
