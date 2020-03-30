---
title: Guided scenarios overview
titleSuffix: Microsoft Intune
description: Learn about the Intune guided scenarios available in the Microsoft 365 Device Management portal.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Intune guided scenarios overview 

A guided scenario is a customized series of steps centered around one end-to-end use-case. Common scenarios are based on the role an admin, user, or device plays in your organization. These roles typically require a collection of carefully orchestrated profiles, settings, applications, and security controls to provide the best user experience and security.    

If you are not familiar with all the steps and resources needed to implement a particular Intune scenario, guided scenarios may be used as your starting point. The guided scenario will assemble policies, apps, assignments, and other management configurations automatically. Additionally, the guided scenarios may deliberately omit certain options not applicable or uncommon for the given scenario. 

Guided scenarios are not a different management space from Intune’s normal workflows. These workflows are intended to be used in conjunction with Intune’s existing workflows for profiles, apps, and policies. Upon completing a guided scenario, all future management of the scenario must take place in the existing menus for policies, apps, and profiles. A guided scenario does not save a “guided scenario” resource type or track future changes made to the resources. Every resource created by a guided scenario will appear in its respective workload. All options, even those options omitted in the guided scenario, will be available for editing in the existing menus.  

## Types of guided scenarios 

For the sake of simplicity, all guided scenarios omit complex scoping features such Scope Tags, exclusion groups and virtual group assignments. All resources created by a guided scenario will inherit every scope tag of the admin that completes the scenario. Certain scenarios offer some level of customization for common setting to cover closely related scenarios. These scenarios, support group assignment to inclusion groups only. For other guided scenarios, the entire scenario guarantees one consistent experience by offering no customization and automatically generates a new group to receive all assignments. Once the guided scenario completes, you are free to use more sophisticated assignments directly through existing policy, app and profile workloads.  

The following scenarios are guided: 
- Deploy Microsoft Edge for mobile 
- Try out a cloud managed PC
- Secure Microsoft Office for mobile 

## Guided scenario functionality 

Guided scenarios offer specific functionality. The following details help explain what you can and cannot do while following a guided scenario.

### Launching  

All guided scenarios are available from **[Device Management portal](https://endpoint.microsoft.com)** > **Troubleshooting + support** > **Guided scenarios**. 

The guided scenario begins with an introduction explaining the purpose of the scenario and any prerequisites required to complete the setup. At this point, your admin permissions are checked to verify you have all the necessary privileges to complete the scenario.  

After all prerequisite checks pass, the scenario offers appropriate settings for customization. Guided scenarios aim to only require input for the minimal number of settings and hide uncommon or advanced settings until needed, or based on special circumstances. Each guided scenario links to documentation that provides additional details. 

After all mandatory settings are entered, the guided scenario presents a summary of the settings entered and the resources the scenario requires. At this point, nothing has been saved unless explicitly noted.

The next step is to deploy the scenario. Deploying a scenario creates and saves all necessary resources and selected settings. The time it takes to complete a deployment varies by scenario. Once the deployment is complete, the guided scenario presents a list of the created resources with links to each resource’s management view, the resource's normal workload, and documentation. 

> [!IMPORTANT]
> The list presented at the end of the guided scenario is not saved and is only viewable while the guided scenario is open.  
If there is an error deploying the scenario, all changes will be reverted. 

### Editing 

Guided scenarios cannot be used to edit existing resources. Once created, all resources, groups, and assignments must be edited using the existing workloads.

### Monitoring 

Guided scenarios cannot be used to monitor existing resources apart from the initial creation process. Once created, all resources, groups, and assignments must be monitored using the existing workloads. 

### Retiring 

Guided scenarios cannot be used to retire existing resources, apart from the automated cleanup during an error in the initial deployment. Once created, all resources, groups, and assignments must be retired using the existing workloads. 

### Updating

As technology evolves, Intune may from time to time update a guided scenario to improve the user experience, security, or other aspects of the scenario. This update will only affect new deployments made by the guided scenario. Intune will not update existing resources previously generated by the guided scenario to match new best practices or recommendations.  

## Next steps

To get running quickly on Microsoft Intune, step through the Intune guided scenarios. If you are new to Intune, set up your Intune tenant by following the [free trial quickstart](free-trial-sign-up.md).
