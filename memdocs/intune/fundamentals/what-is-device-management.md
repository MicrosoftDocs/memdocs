---
# required metadata

title: Device management in Microsoft 365
description: Microsoft 365 Enterprise includes Microsoft Intune. See how Intune provides mobile device management and mobile application management for your organization. Read common scenarios, and use Intune to deploy Microsoft 365 in your environment. 
author: MandiOhlinger 
ms.author: mandia 
manager: dougeby 
ms.date: 01/25/2022
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
  - M365-identity-device-management
  - highpri
---

# Device management overview

A key task of any Administrator is to protect and secure an organization’s resources and data on devices in their organization. This task is **device management**. Users receive and send email from personal accounts, browse websites from home and from restaurants, and install apps and games. These users are also employees and students. On their devices, they want to access work and school resources, such as email and OneNote, and access them quickly. As an administrator, your goal is to protect these resources, and provide easy access for users across their many devices, all at the same time.

Device management enables organizations to protect and secure their resources and data, and from different devices.

Using a device management provider, organization can make sure that only authorized people and devices get access to proprietary information. Similarly, device users can feel at ease accessing work data from their phone, because they know their device meets their organization's security requirements. As an organization, you might ask - **What should we use to protect our resources?**

The answer is [Microsoft Intune](what-is-intune.md). Intune offers mobile device management (MDM) and mobile application management (MAM). Some key tasks of any MDM or MAM solution are to:

- Support a diverse mobile environment and manage iOS/iPadOS, Android, Windows, and macOS devices securely.
- Make sure devices and apps are compliant with your organization's security requirements.
- Create policies that help keep your organization data safe on organization-owned and personal devices.
- Use a single, unified mobile solution to enforce these policies, and help manage devices, apps, users, and groups.
- Protect your company information by helping to control the way your workforce accesses and shares its data.

Intune is included with Microsoft Azure, Microsoft 365, and integrates with Azure Active Directory (Azure AD). Azure AD helps control who has access, and what they have access to.

## Microsoft Intune

Many organizations, including Microsoft, use Intune to secure proprietary data that users access from their company-owned and personally owned devices. Intune includes device and app configuration policies, software update policies, and installation statuses (charts, tables, and reports). These resources help you secure and monitor data access.

It's common for people to have multiple devices that use different platforms. For example, an employee might use Surface Pro for work, and an Android mobile device in their personal life. And, it's common for a person to access organizational resources, such as Microsoft Outlook and SharePoint, from these multiple devices.

With Intune, you can manage multiple devices per person, and the different platforms that run on each device, including iOS/iPadOS, macOS, Android, and Windows. Intune separates policies and settings by device platform. So it's easy to manage and view devices of a specific platform.

**[Common scenarios](common-scenarios.md)** is a great resource to see how Intune answers common questions when working with mobile devices. You'll find scenarios about:  

- Protecting email with on-premises Exchange
- Accessing Microsoft 365 safely and securely
- Using personal devices to access organizational resources

For more information about Intune, see [What is Intune](what-is-intune.md).

## Co-management and tenant attach

Many organizations use on-premises Configuration Manager to manage devices, including desktops and servers. You can cloud-attach your on-premises Configuration Manager to Microsoft Intune. When you cloud-attach, you get the benefits of Intune and the cloud, including [conditional access](../../configmgr/comanage/quickstart-conditional-access.md), [running remote actions](../../configmgr/comanage/quickstart-remote-actions.md), [using Windows Autopilot](../../configmgr/comanage/quickstart-autopilot.md), and more.

[Microsoft Endpoint Manager](../../endpoint-manager-overview.md) is a solution platform that unifies several services. It includes [Microsoft Intune](what-is-intune.md) for cloud-based device management, and [Configuration Manager + Intune](../../configmgr/comanage/overview.md) for cloud-attach device management.

If you use Configuration Manager, and you're ready to move some tasks to the cloud, then co-management is your answer. For more information about cloud-attaching your Configuration Manager, see [What is co-management](../../configmgr/comanage/overview.md).

Endpoint Manager tenant attach is also an option. You upload your devices to the Endpoint Manager admin center, without enabling automatic enrollment for co-management or switching workloads to Intune. You can see your devices, and run actions on Configuration Manager managed devices. For more information, see [Microsoft Endpoint Manager tenant attach](../../configmgr/tenant-attach/device-sync-actions.md).

## Integration with secure-and-protect services

A key task of any device management solution is to provide security and protection. Intune does a great job of integrating with other services to achieve this task. For example:

- **Microsoft 365** is a key component to simplifying common IT tasks. In the Microsoft 365 admin center, you create users, and manage groups. You also get access to other services, such as Intune, Azure AD, and more.

  For example, create an iOS/iPadOS devices group in Microsoft 365. Then, use Intune to push policies to the iOS/iPadOS devices group that focus on iOS/iPadOS features, such as access to the app store, using AirDrop, backing up to iCloud, using Apple's web filter, and more.

- **Windows Defender** includes many security features to help protect Windows client devices. For example, using Intune and Windows Defender together, you can:

  - Enable [Windows Defender SmartScreen](../protect/endpoint-protection-windows-10.md) to look for suspicious activity in files and apps on mobile devices.
  - Use [Microsoft Defender for Endpoint)](../protect/advanced-threat-protection.md) to help prevent security breaches on mobile devices. And, help limit the impact of a security breach by blocking a user from corporate resources.

- **Conditional Access** is a feature of Azure Active Directory, and integrates nicely with Intune. Using [Conditional Access](../protect/conditional-access.md), make sure only compliant devices are allowed access to email, SharePoint, and other apps.

## Choose the device management solution that's right for you

There are a couple of ways to approach device management. First, you can manage different aspects of devices using the features built in to Intune. This approach is called **Mobile device management (MDM)**. Users "enroll" their devices, and use certificates to communicate with Intune. As an IT administrator, you push apps on devices, restrict devices to a specific operating system, block personal devices, and more. If a device is ever lost or stolen, you can also remove all data from the device.

In the second approach, you manage apps on devices. This approach is called **Mobile application management (MAM)**. Users can use their personal devices to access organizational resources. When opening an app, such as email or SharePoint, users can be prompted to authenticate. If a device is ever lost or stolen, you can remove all organization data from the Intune managed applications.

You can also use a combination of [MDM and MAM](byod-technology-decisions.md) together.

## Simplify IT tasks using the Device Management admin center

The [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) is a one-stop shop to manage and complete tasks for your mobile devices. This admin center includes the services used for device management, including Intune and Azure Active Directory, and to also manage client apps.

On the Device Management admin center, you can:

- [Enroll devices](../enrollment/device-enrollment.md)
- [Set device compliance](../protect/device-compliance-get-started.md)
- [Manage devices](../remote-actions/device-management.md)
- [Manage apps](../apps/app-management.md)  
- [iOS eBooks](../apps/vpp-ebooks-ios.md)  
- [Install Exchange on-premises connector](../protect/exchange-connector-install.md)  
- [Manage roles](role-based-access-control.md)  
- Manage software updates
  - [Manage Windows client updates](../protect/windows-update-for-business-configure.md)  
  - [Manage iOS/iPadOS updates](../protect/software-updates-ios.md)  
- [Azure active directory](/azure/active-directory)  
- [Manage users](/azure/active-directory/fundamentals/add-users-azure-active-directory)
- [Manage groups and members](/azure/active-directory/fundamentals/active-directory-manage-groups)
- [Troubleshoot](help-desk-operators.md)

## Next steps

When you're ready to get started with an MDM or MAM solution, walk through the different steps to set up Intune, enroll devices, and start creating policies. The [Microsoft Intune planning guide](intune-planning-guide.md) is a good resource.

Microsoft IT case study: [Migrating mobile device management to Intune in the Azure portal](https://www.microsoft.com/itshowcase/Article/Content/1042/Migrating-mobile-device-management-to-Intune-in-the-Azure-portal)
