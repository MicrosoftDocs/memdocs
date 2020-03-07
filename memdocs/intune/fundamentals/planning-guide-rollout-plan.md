---
# required metadata

title: Determine groups targeted for rollout and timeframes
titleSuffix: Microsoft Intune
description: This article helps you decide which groups to roll out to Microsoft Intune and timeframes for those deployments.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 3a63f78f-a7e7-4f44-9288-16b28d5d58ca

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Develop a rollout plan

Your rollout plan identifies the organizational groups you want to target for your Intune rollout, the rollout timeframe for each group, and the enrollment approaches you will use.

## Targeted groups and timeframes

First, review the groups that are targeted with your Intune rollout and that you identified in your [use-case scenarios](planning-guide-scenarios.md).

Second, determine the time frame for each targeted group. This task typically requires a discussion between the Intune deployment team and the targeted groups to determine the most appropriate rollout time frame for each group. Points to cover in such a discussion include:
* The group's willingness for change
* The number of users and devices
* Types of device platforms
* Requirements
* Geographic location
* Business risk

## Rollout phases
Organizations commonly choose to start the Intune rollout with an initial pilot, targeting a small group of users in the IT department. The pilot can be expanded to include a broader set of IT users and may include participation from other organizational groups.

### Pilot
The first phase to rollout should be to pilot users. The pilot users should understand they are the first users in a new solution. They must be willing to provide feedback to help improve configuration, documentation, notifications, and ease the way for all other users in later rollout phases. These users should not be executives or VIPs.

The pilot is a good opportunity for you to test the [challenges](planning-guide-deployment-goals.md) and refine [requirements](planning-guide-requirements.md) you gathered earlier.

Include your [communication](planning-guide-communication-plan.md) plan, [support](planning-guide-support-plan.md) plan, and [testing and validation](planning-guide-test-validation.md) to work out any problems while the impact to users is still small.

### Production rollout
After a successful pilot, you're ready to start a full production rollout, targeting the rest of your organization's groups. Some examples of different rollout groups and phases are:

- **Departments** <br/>Each department can be a rollout phase. You target an entire department at a time. In this type of rollout, users in each department tend to use the mobile device in the same way and access the same applications. Users will likely have the same types of policies.

- **Geography** <br/>In this approach, you deploy to all users in a specific geography whether it's the same continent, country/region, or same company's building. This type of phased deployment lets you focus on the specific location of users. This could let you provide more of a  [white glove](#user-assisted-enrollment) approach because the number of locations deploying Intune at the same time is reduced. Because there are chances of different departments or use cases being at the same location, different use cases might be deployed at the same time.

- **Platform** <br/>This type of deployment consists of deploying similar platforms at the same time. An example might be all iOS/iPadOS devices the first month, followed by Android, followed by Windows. This type of phased deployment helps simplify helpdesk support because helpdesk would only have to support a single platform at a time.

Here's an example of an Intune rollout plan that includes targeted groups and timelines:

| **Rollout phase** | **July** | **August** | **September** | **October** |
|:---:|:---:|:---:|:---:|:---:|
| Limited Pilot | IT (50 users) |  |  |  |                                                         
| Expanded Pilot | IT (200 users), IT Executives (10 users) |  |  |  |                                                         
| Production rollout phase 1 |  | Sales and Marketing (2000 users) |  |  |
| Production rollout phase 2 |  |  | Retail (1000 users) |  |
| Production rollout phase 3 |  |  |  | HR (50 users), Finance (40 users), Executives (30 users) |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to enter your organization's rollout phases.
## Match rollout groups to enrollment approaches

Now that you have determined the targeted groups and time frames for your Intune rollout, the next step is to choose the most appropriate Intune enrollment approach for each group. There are different enrollment approaches you can use including:
* User self-service
* User assisted-enrollment
* IT tech fair

### User self-service

In this case, the user is responsible for enrolling their own device, usually following enrollment instructions provided by their IT organization. This approach is most commonly used in organizations and is more scalable than user-assisted enrollment.

### User-assisted enrollment

This is known as a "white glove" approach. An IT team member helps the user through the enrollment process, in person or with Skype. This approach is commonly used with executive staff and other groups that might need more assistance during the enrollment process.

### IT tech fair

Another option for Intune user enrollment is to have an IT technical fair. At this event, the IT group sets up an Intune enrollment assistance booth where users could receive information on Intune enrollment, ask questions, and receive assistance with the enrollment process. This option can be beneficial for both the IT group and users, especially during early phases of Intune rollout.

Here's an updated example of the above Intune rollout plan to include enrollment approaches:

| **Rollout phase** | **July** | **August** | **September** | **October** |
|:---:|:---:|:---:|:---:|:---:|
| Limited Pilot |  |  |  |  |
| Self-service | IT |  |  |  |
| Expanded Pilot |  |  |  |  |
| Self-service | IT |  |  |  |
| White glove | IT Executives |  |  |  |
| Production rollout phase 1 |  | Sales, Marketing |  |  |
| Self-service |  | Sales and Marketing |  |  |
| Production rollout phase 2 |  |  | Retail |  |
| Self-service |  |  | Retail |  |
| Production rollout phase 3 |  |  |  | Executives, HR, Finance |
| Self-service |  |  |  | HR, Finance |
| White glove |  |  |  | Executives |

## Next steps

The next section provides guidance on [developing an Intune rollout communication plan](planning-guide-communication-plan.md).
