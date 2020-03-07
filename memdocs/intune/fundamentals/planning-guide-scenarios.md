---
# required metadata

title: Identify use case scenarios
titleSuffix: Microsoft Intune
description: This article helps you identify Intune use-case and sub-use-case scenarios for a Microsoft Intune cloud-only implementation.
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
ms.assetid: 4b3c9af9-78da-44d2-8bd2-3f0f8885952d

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

# Identify mobile device management use-case scenarios

Identifying your use-case scenarios is an important part of the planning process for a successful Intune deployment. Use-case scenarios are helpful because they let you segment your users into manageable groups by user type or role, and the ownership of the user's device (for example, company or personal).

Let’s discuss a few examples to help your organization identify Intune use-case scenarios, as well as organizational groups, and mobile device platforms associated with each use case.

## Device ownership
You can begin by referring to your organization's Intune deployment goals and objectives to help identity the main use-case scenarios for your deployment. Within the scope of your Intune deployment plan, answer the following questions:

- Are you planning to support corporate owned devices?

- Are you planning to support personally owned devices (BYOD)?

These are not either/or options. You may find you need to support both forms of device ownership to meet your organizational goals. The sub-use-cases will help clarify where to apply the different device management policies.

### User type or device role

Determine if each use-case scenario also includes sub-use-cases. For example, your organization may have identified requirements to support a corporate use-case scenario that includes additional sub-use-cases based on user type or device role, such as:

- Information worker

- Executive

- Kiosk

Here are a few examples of use-case and sub-use-case scenarios:

| **Use cases** | **Sub-use cases** |
|:---:|:---:|
| Corporate | Information worker |              
| Corporate | Executives |           
| Corporate | Kiosk |
| BYOD | Information worker |           
| BYOD | Executives |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to enter your organization’s use-case and sub-use-case scenarios.

## Organizational groups for your scenarios

Now you need to identify the organizational groups that are associated with each use-case and sub-use-case scenario. For example:

| **Use cases** | **Sub-use cases** | **Organizational groups** |
|:---:|:---:|:---:|
| Corporate | Information worker | HR, Finance |               
| Corporate | Executive | HR, Finance |            
| Corporate | Kiosk | Retail |
| BYOD | Information worker | Marketing, Sales |            
| BYOD | Executive | Marketing, Sales |


## Mobile device platforms for your scenarios

The next step is to identify the mobile device platforms associated with each use-case scenario. There may be more than one.

For example, your corporate use-case scenario may support iOS/iPadOS and Android Samsung Knox device platforms. Your BYOD policy may include support for additional mobile device platforms like Android (non-Samsung Knox) and Windows 10 Mobile. Building on the preceding examples, we've associated mobile device platforms with each use-case scenario.

| **Use cases** | **Sub-use cases** | **Groups** | **Device platforms** |   
|:---:|:---:|:---:|:---:|
| Corporate | Information worker | HR, Finance | iOS/iPadOS |                                                           
| Corporate | Executives | HR, Finance | iOS/iPadOS |                                                           
| Corporate | Kiosk | Retail | Android |
| BYOD | Information worker | Marketing, Sales | iOS/iPadOS |                                                           
| BYOD | Executives | Marketing, Sales | iOS/iPadOS |

## Next steps

The next section provides guidance on [how to identify the Intune requirements for each use case scenario](../planning-guide-requirements.md).
