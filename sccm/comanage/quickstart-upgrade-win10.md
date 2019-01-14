---
title: Upgrade Windows 10
titleSuffix: Configuration Manager
description: Upgrade devices to Windows 10 version 1709 or later, which is required for co-management
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Upgrade Windows 10 for co-management

As you work towards onboarding your organization to co-management, getting current is a significant hurdle for some customers. Co-management requires [Windows 10 version 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) or later. Once you update Windows and configure auto-enrollment, your clients are automatically enrolled to co-management.

In the following video, senior program manager Rob York and product marketing manager Locky Ainley discuss and demo upgrading to Windows 10 for co-management:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## Why upgrade?

Among other platform advancements, Windows 10 version 1709 and later supports auto-enrollment. This behavior makes a device automatically enroll to Intune when it joined Azure Active Directory (Azure AD). 

For more information, see [Enable Windows 10 automatic enrollment](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## How to do it

Here are some tips we've learned from helping thousands of customers get current quickly:

- Use phased deployments to roll out this upgrade to the right people at the right times. For more information, see [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Use pre-caching to reduce user wait times. For more information, see [Configure pre-cache content](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Use the default in-place upgrade task sequence template. Then configure your steps for pre- and post-upgrade, and any failure actions. For more information, see [Recommended task sequence steps for post-processing](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- If your environment has a highly mobile workforce, Configuration Manager supports in-place upgrade over the cloud management gateway (CMG). This feature allows you to upgrade your Windows 10 clients when they're internet-based. For more information on the CMG, see [](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Offer an opt-in to co-management for users who want to be early adopters. This approach accelerates initial adoption. By identifying these people in advance, you can make sure good coverage in the early days of a rollout. You also receive validation and feedback from users that are happy for change and interested in more frequent releases. Early adopter programs generate interest in the new technologies and grow in size over time.  


## Case studies

Microsoft IT deployed Windows 10 to 96,000 distributed users at Microsoft. The deployment included both remote users and users on the corporate network. The deployment completed in nine weeks. For more information on their experience, see [Deploying Windows 10 at Microsoft as an in-place upgrade](https://www.microsoft.com/download/details.aspx?id=50377).  

A large European software manufacturer successfully uses an early adopter group. After initial testing and piloting groups, approximately 2,000 employees receive the first update, upgrades, and software. This group includes IT staff and opt-in volunteers. This level of engagement with their users gives them a greater level of confidence when testing, and more credibility when mass rollouts begin.



## Contact FastTrack

If you need assistance with your Windows 10 upgrade at any point in the process, go to [Microsoft FastTrack](https://Microsoft.com/FastTrack/), sign in, and request assistance. 

For more information, see [Get help from FastTrack](/sccm/comanage/quickstart-fasttrack). 

