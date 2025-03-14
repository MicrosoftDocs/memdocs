---
title: Introduction to the tutorial for deploying and managing devices in a school
description: Introduction to deployment and management of devices in education environments.
ms.date: 5/2/2024
ms.topic: tutorial
ms.author: scbree
author: scottbreenmsft
ms.manager: dougeby
ms.service: microsoft-intune
ms.subservice: education
---

# Tutorial: deploy and manage devices in a school

This guide introduces the tools and services available from Microsoft to deploy, configure, and manage devices in an education environment.

## Audience and user requirements

This tutorial is intended for education professionals responsible for deploying and managing devices, including:

- School leaders
- IT administrators
- Teachers
- Microsoft partners

This content provides a comprehensive path for schools to deploy and manage new devices with Microsoft Intune. It includes step-by-step information how to manage devices throughout their lifecycle.

> [!NOTE]
> Depending on your school setup scenario, you may not need to implement all steps.

## Device lifecycle management

School IT administrators and educators need an easy-to-use, flexible, and secure way to manage the lifecycle of the devices in their schools. Microsoft has developed integrated suites of products for streamlined, cost-effective device lifecycle management.

Microsoft 365 Education provides tools and services that enable simplified management of all devices through Microsoft Intune services. With Microsoft's solutions, IT administrators have the flexibility to support diverse scenarios, including school-owned devices and bring-your-own devices.

Microsoft Intune services include:

- [Microsoft Intune][MEM-1]
- [Microsoft Intune for Education][INT-1]
- [Windows Autopilot][MEM-4]
- [Microsoft Surface Management Portal][MEM-5]

These services are part of the Microsoft 365 stack to help secure access, protect data, and manage risk.

## Why Intune?

Devices can be managed with Intune, enabling simplified management of multiple devices from a single point.

From enrollment, through configuration and protection, to resetting, Intune helps school IT administrators manage and optimize the devices throughout their lifecycle:

:::image type="content" source="./images/device-lifecycle.png" alt-text="The device lifecycle for Intune-managed devices" border="false":::

- **Enroll:** to enable remote device management, devices must be enrolled in Intune with an account in your Microsoft Entra tenant. Some enrollment methods require an IT administrator to initiate enrollment, while others require students to complete the initial device setup process. This document discusses the facets of various device enrollment methodologies
- **Configure:** once the devices are enrolled in Intune, applications and settings are applied.
- **Protect and manage:** in addition to its configuration capabilities, Intune helps protect devices from unauthorized access or malicious attacks. For example, managing Defender Antivirus and Bitlocker can make devices more secure. Policies are available that let you control settings for Windows Firewall, Endpoint Protection, and software updates
- **Retire:** when it's time to repurpose a device, Intune offers several options, including resetting the device, removing it from management, or wiping school data. In this document, we cover different device return and exchange scenarios

## Four pillars of modern device management

In the remainder of this tutorial, we discuss the key concepts and benefits of modern device management with Microsoft 365 solutions for education. The guidance is organized around the four main pillars of modern device management:

- **Identity management:** setting up and configuring the identity system, with Microsoft 365 Education and Microsoft Entra ID, as the foundation for user identity and authentication
- **Initial setup:** setting up the Intune environment for managing devices, including configuring settings, deploying applications, and defining updates cadence
- **Device enrollment:** Setting up devices for deployment and enrolling them in Intune
- **Device reset:** Resetting managed devices with Intune

---

## Next steps

Let's begin with the creation and configuration of your Microsoft Entra tenant and Intune environment.

> [!div class="nextstepaction"]
> [Next: Plan enrollment >](plan-enrollment.md)

<!-- Reference links in article -->

[MEM-1]: /mem/intune-service/fundamentals/what-is-intune
[MEM-2]: /mem/configmgr/core/understand/introduction
[MEM-4]: /mem/autopilot/windows-autopilot
[MEM-5]: /mem/intune-service/fundamentals/surface-management-portal

[INT-1]: /intune-education/what-is-intune-for-education
