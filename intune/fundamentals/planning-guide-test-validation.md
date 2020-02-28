---
# required metadata

title: Intune testing and validation
titleSuffix: Microsoft Intune
description: How to test and validate in your Intune cloud-only solution in your environment.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 3/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 4f82ee0c-4bd6-4623-9b10-9249d316ccf5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Intune testing and validation

When testing the implementation of Microsoft Intune, consider functional validation and use-case validation. Functional validation consists of testing each component and configuration to determine if it is working correctly. Use-case validation involves testing to verify that the scenarios involving a series of tasks work as expected. 

We recommend that you incorporate your IT support and helpdesk staff in the testing phase so that support documentation is created, and the IT support and helpdesk staff become comfortable supporting the product. If a component or scenario does not function based on the use cases, make sure to document the necessary changes, and include the reason a change was made.

## Before you begin

We recommend that you document the following:

- **Test criteria:** Identify the benchmarks to be measured against.

- **Design components:** Must exist in at least one testing criteria.

If a design component does not exist in at least one test criteria that aligns to a requirement or scenario, consider whether the design component is required or not. In addition, make sure to have the following items:

- **Accounts:** Test accounts that are licensed for EMS and Office 365 to test all use-case scenarios.

- **Devices:** Test devices that can be wiped or reset to factory defaults.

- **Integration components:** All integration components (certificate connectors, and the Intune Exchange on-premises connector) should be installed and configured if needed.

You may need design changes to accommodate unforeseen difficulties. In addition, all design changes should be fully documented with the reason for each change. Here's an example to illustrate what a change could be:

<blockquote>You realize that you don’t meet the requirements of Network Device Enrollment Service (NDES), and you also learn that the VPN and Wi-Fi profiles can be configured with a root CA satisfying the same requirements without an NDES implementation.</blockquote>

You might experience challenges or issues that require technical guidance or specialized troubleshooting during the testing and validation process. We recommend that you seek assistance through the Microsoft support channels.

- [Learn how to get Intune support](../get-support.md)

- [Contact assisted phone support for Microsoft Intune](../get-support.md)

## Functional validation testing

Functional validation consists of testing each component and configuration to determine if it is working correctly. An example of validation testing is in the table below.

![Section 9 table 1](./media/planning-guide-test-validation/section-9-image-1-table.PNG)

## Use-case validation testing

Perform use-case validation testing to verify the scenarios are complete and functional. There are two types of use-case scenarios: IT admin and end user.

### IT admin

Perform IT admin validation testing to validate that administrative actions performed on a device or user function correctly. Below is an example of an IT admin end-to-end validation scenario.

![Section 9 table 2](./media/planning-guide-test-validation/section-9-image-2-table.PNG)

### End user

Perform end-user validation testing to validate that the end-user experience is as expected and presented correctly in all user communications. It is important to validate that the end-user experience is correct. If you fail to validate, it can lead to lower adoption rates and higher volumes of helpdesk calls.

![Section 9 table 3](./media/planning-guide-test-validation/section-9-image-3-table.PNG)

## Next steps

Now that you have tested and validated your Intune functional and use-case scenarios, you're ready for your [Intune production rollout](../planning-guide-rollout-plan.md).

See [additional resources](../planning-guide-resources.md) for more planning templates and information.
