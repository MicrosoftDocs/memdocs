---
title: Upgrade Windows 10
titleSuffix: Configuration Manager
description: Upgrade devices to a supported version of Windows 10 or later, which is required for co-management.
ms.date: 11/08/2021
ms.subservice: co-management
ms.service: configuration-manager
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Upgrade Windows for co-management

As you work towards onboarding your organization to co-management, getting current is a significant hurdle for some customers. Co-management requires a supported version of Windows 10 or later. Once you update Windows and configure auto-enrollment, your clients are automatically enrolled to co-management.

In the following video, senior program manager Rob York and product marketing manager Locky Ainley discuss and demo upgrading to Windows 10 for co-management:

> [!VIDEO https://aka.ms/docs/player?id=3099c141-475c-42f9-a997-cb0dffb74788]

## Why upgrade?

Among other platform advancements, Windows 10 and later supports auto-enrollment. This behavior makes a device automatically enroll to Intune when it joined Microsoft Entra ID.

For more information, see [Enable Windows automatic enrollment](../../intune/enrollment/windows-enroll.md#enable-windows-automatic-enrollment).

## How to do it

Here are some tips we've learned from helping thousands of customers get current quickly:

- Use phased deployments to roll out this upgrade to the right people at the right times. For more information, see [Create phased deployments](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

- Use pre-caching to reduce user wait times. For more information, see [Configure pre-cache content](../osd/deploy-use/configure-precache-content.md).

- Use the default in-place upgrade task sequence template. Then configure your steps for pre- and post-upgrade, and any failure actions. For more information, see [Recommended task sequence steps for post-processing](../osd/understand/in-place-upgrade-recommendations.md#post-processing).

- If your environment has a highly mobile workforce, Configuration Manager supports in-place upgrade over the cloud management gateway (CMG). This feature allows you to upgrade your Windows clients when they're internet-based. For more information on the CMG, see [Deploy Windows in-place upgrade via CMG](../osd/deploy-use/deploy-task-sequence-over-internet.md#deploy-windows-in-place-upgrade-via-cmg).

- Offer an opt-in to co-management for users who want to be early adopters. This approach accelerates initial adoption. By identifying these people in advance, you can make sure good coverage in the early days of a rollout. You also receive validation and feedback from users that are happy for change and interested in more frequent releases. Early adopter programs generate interest in the new technologies and grow in size over time.

## Case studies

Microsoft IT deployed Windows 10 to 96,000 distributed users at Microsoft. The deployment included both remote users and users on the corporate network. The deployment completed in nine weeks. For more information on their experience, see [Deploying Windows 10 at Microsoft as an in-place upgrade](https://www.microsoft.com/insidetrack/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).

A large European software manufacturer successfully uses an early adopter group. After initial testing and piloting groups, approximately 2,000 employees receive the first update, upgrades, and software. This group includes IT staff and opt-in volunteers. This level of engagement with their users gives them a greater level of confidence when testing, and more credibility when mass rollouts begin.

## Contact FastTrack

If you need assistance with your Windows upgrade at any point in the process, go to [Microsoft FastTrack](https://microsoft.com/fasttrack/), sign in, and request assistance.

For more information, see [Get help from FastTrack](quickstart-fasttrack.md).
