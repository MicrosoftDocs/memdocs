---
# required metadata

title: What is device management?
description: Learn more about what device management means and how it can help organizations, including Microsoft 365 small & medium business, and enterprise. See a list of features and benefits, including mobile device management (MDM) and mobile application management (MAM), and learn about Microsoft Intune.
author: MandiOhlinger
ms.author: mandia 
manager: dougeby 
ms.date: 02/20/2025
ms.topic: overview 
audience: microsoft-business
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: microsoft-intune
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# What does device management mean for IT admins?

**Device management** enables organizations to administer and maintain devices, including virtual machines, physical computers, mobile devices, and IoT devices. Device management is a critical component of any organization's security strategy. It helps admins ensure that devices are secure, up-to-date, and compliant with organizational policies, with the goal of protecting the corporate network and data from unauthorized access.

As organizations support remote and hybrid workforces, it's more important than ever to have a solid device management strategy. Organizations must protect and secure their resources and data on any device.

:::image type="content" source="./media/what-is-device-management/device-management-features-mdm-mam.png" alt-text="Diagram that shows the features and benefits of modern device management using MDM and MAM with Microsoft Intune." lightbox="./media/what-is-device-management/device-management-features-mdm-mam.png":::

This article describes the features and benefits of device management, and how it can help organizations, including Microsoft 365 small & medium business, and enterprise. It also describes the different approaches to device management, including mobile device management (MDM) and mobile application management (MAM), and how Microsoft Intune can help.

## Features and benefits

Device management solutions have the following features and benefits:

> [!div class="checklist"]
>
> * The toolset to manage devices, including the ability to deploy and update software, configure settings, enforce policies, and monitor with data and reports
> * The ability to administer and manage virtual and physical devices, regardless of their physical location
> * Maintain a network of devices running common operating systems, including Windows, macOS, iOS/iPadOS, Linux, and Android
> * Automate policy management and deployment for apps, device features, security, and compliance
> * Optimize device features for business use
> * Provide a single point of management for devices, including the ability to manage devices from a central console
> * Secure and protect data on devices, including safeguards and measures to prevent unauthorized access

With device management solutions, organizations can make sure that only authorized people and devices get access to proprietary information. Similarly, device users can feel at ease accessing work data from their phone, because they know their device meets their organization's security requirements.

As an organization, you might ask - **What should we use to protect our resources?**.

## Microsoft Intune is a world class device management solution

Many organizations, including Microsoft, use Intune to secure proprietary data that users access from their company-owned and personally-owned devices. Intune includes device and app policies, software update policies, and installation statuses (charts, tables, and reports). These resources help you secure and monitor data access.

With Intune, you can manage multiple devices per person, and the different platforms that run on each device, including Android, iOS/iPadOS, Linux, macOS, and Windows. Intune separates policies and settings by device platform. So it's easy to manage and view devices of a specific platform.

For more information about Intune and its benefits, go to:

- [Microsoft Intune planning guide](intune-planning-guide.md)
- [What is Intune?](what-is-intune.md)
- [Get started with Microsoft Intune](get-started-with-intune.md)

### Cloud attach your on-premises Configuration Manager

Many organizations use on-premises Configuration Manager to manage devices, including desktops and servers. You can cloud-attach your on-premises Configuration Manager to Microsoft Intune. When you cloud-attach, you get the benefits of Intune and the cloud, including [Conditional Access](../../configmgr/comanage/quickstart-conditional-access.md), [running remote actions](../../configmgr/comanage/quickstart-remote-actions.md), [using Windows Autopilot](../../configmgr/comanage/quickstart-autopilot.md), and more.

For more information, go to:

- [What is co-management](../../configmgr/comanage/overview.md)
- [Configuration Manager tenant attach](../../configmgr/tenant-attach/device-sync-actions.md)

## Choose the device management solution that's right for you

There are a couple of ways to approach device management.

✅ **Mobile device management (MDM)**

First, you can manage different aspects of devices using the features built in to Intune. This approach is called mobile device management (MDM).

Users "enroll" their devices, and use certificates to communicate with Intune. As an IT administrator, you push apps on devices, restrict devices to a specific operating system, block personal devices, and more. If a device is ever lost or stolen, you can also remove all data from the device.

✅ **Mobile application management (MAM)**

In the second approach, you manage apps on devices. This approach is called mobile application management (MAM).

Users can use their personal devices to access organizational resources. When users open an app, such as Outlook or Teams, they can be prompted to authenticate. If a device is ever lost or stolen, you can remove all organization data from the Intune managed applications.

You can also use a combination of MDM and MAM together.

For more information, go to:

- [What is Intune?](what-is-intune.md)
- [Microsoft Intune planning guide](intune-planning-guide.md)

## Related articles

- [Microsoft Intune planning guide](intune-planning-guide.md)
- [Manage user and group identities in Microsoft Intune](manage-identities.md)
- [Manage your devices and control device features in Microsoft Intune](manage-devices.md)
- [Manage your apps and app data in Microsoft Intune](manage-apps.md)
