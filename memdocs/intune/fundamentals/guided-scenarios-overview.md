---
title: Guided scenarios overview
titleSuffix: Microsoft Intune
description: Learn about the Intune guided scenarios available in the Microsoft 365 Device Management portal.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/25/2023
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Intune guided scenarios overview

A guided scenario is a customized series of steps centered around one end-to-end use-case. Common scenarios are based on the role an admin, user, or device plays in your organization. These roles typically require a collection of carefully orchestrated profiles, settings, applications, and security controls. The goal is to provide the best user experience and security.

If you're not familiar with the steps and resources to implement a particular scenario, then start with guided scenarios. The guided scenarios assemble policies, apps, assignments, and other management configurations automatically. Additionally, the guided scenarios may deliberately omit certain options not applicable or uncommon for the given scenario. 

Guided scenarios aren't a different management space from Intune's normal workflows. These workflows are used with Intune's existing workflows for profiles, apps, and policies. Upon completing a guided scenario, all future management of the scenario must take place in the existing menus for policies, apps, and profiles. A guided scenario doesn't save a "guided scenario" resource type, or track future changes made to the resources. Every resource created by a guided scenario shows in its respective workload. All options, even those options omitted in the guided scenario, are available for editing in the existing menus.

## Types of guided scenarios

For simplicity, all guided scenarios omit scoping features, such as scope tags, exclusion groups, and virtual group assignments. All resources created by a guided scenario inherit every scope tag of the admin that completes the scenario. Some scenarios offer some customization for common settings to cover closely related scenarios. These scenarios support group assignment to inclusion groups only. For other guided scenarios, the entire scenario guarantees one consistent experience by offering no customization and automatically generates a new group to receive all assignments. Once the guided scenario completes, you can use more assignment features directly through existing policy, app, and profile workloads.

The following guided scenarios are available:

- [Secure Office apps for mobile](guided-scenarios-office-mobile.md)
- [Deploy Edge for mobile](guided-scenarios-edge.md)
- [Set up a test device to try out cloud management](guided-scenarios-cloud-managed-pc.md)
- [Deploy Windows 10 and later in cloud configuration](cloud-configuration.md)

## Guided scenario functionality

Guided scenarios offer specific functionality. The following details help explain what you can and can't do while following a guided scenario.

### Launching  

All guided scenarios are available from the **[Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)** > **Troubleshooting + support** > **Guided scenarios**.

Guided scenarios start with an introduction. It explains the purpose of the scenario, and any prerequisites required to complete the setup. At this point, your admin permissions are checked to verify you have all the necessary privileges to complete the scenario.  

After all prerequisite checks pass, the scenario offers appropriate settings for customization. Guided scenarios only require input for a minimum number of settings. They hide uncommon or advanced settings until needed, or based on special circumstances. Each guided scenario links to documentation that provides more details.

After all required settings are entered, the guided scenario shows a summary of the settings entered and the resources the scenario requires. At this point, nothing is saved unless explicitly noted.

The next step is to deploy the scenario. Deploying a scenario creates and saves all necessary resources and selected settings. The time it takes to complete a deployment varies by scenario. Once the deployment is complete, the guided scenario shows a list of the created resources. It also has links to each resource's management view, the resource's normal workload, and documentation.

> [!IMPORTANT]
> The list presented at the end of the guided scenario isn't saved, and is only viewable while the guided scenario is open.

If there's an error deploying the scenario, all changes are reverted.

### Editing

Guided scenarios can't be used to edit existing resources. Once created, all resources, groups, and assignments must be edited using the existing workloads.

### Monitoring

Guided scenarios can't be used to monitor existing resources apart from the initial creation process. Once created, all resources, groups, and assignments must be monitored using the existing workloads.

### Retiring

Guided scenarios can't be used to retire existing resources. Once created, all resources, groups, and assignments must be retired using the existing workloads.

### Updating

As technology evolves, Intune may update a guided scenario to improve the user experience, security, or other aspects of the scenario. This update only affects new guided scenario deployments. Intune won't update resources previously generated by the guided scenario.

## Next steps

To get running quickly on Microsoft Intune, step through the Intune guided scenarios. If you're new to Intune, set up your Intune tenant by following the [free trial quickstart](free-trial-sign-up.md).
