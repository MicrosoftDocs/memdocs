---
# required metadata

title: Manage and secure user and group identities in Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn more about the concepts and features you should know when managing identities in Microsoft Intune. Use existing users and groups, control access using RBAC, establish user affinity, and secure and authenticate users.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 02/28/2023
ms.topic: conceptual
ms.service: mem
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Manage user and group identities in Microsoft Intune

Managing and protecting user identities is a significant part of any endpoint management strategy and solution. Identity management includes the user accounts and groups that access your organization resources.

:::image type="content" source="./media/manage-identities/identities-different-user-types.png" alt-text="Diagram that shows addings users to the Microsoft Intune admin center and assigning policies to different user types in Microsoft Intune." lightbox="./media/manage-identities/identities-different-user-types.png":::

Admins have to manage account membership, authorize and authenticate access to resources, manage settings that affect user identities, and secure & protect the identities from malicious intent.

Microsoft Intune can do all these tasks, and more. Intune is a cloud-based service that can manage user identities through policy, including security and authentication policies. For more information on Intune and its benefits, go to [What is Microsoft Intune?](what-is-intune.md).

From a service perspective, Intune uses Azure Active Directory (AD) for identity storage and permissions. Using the [Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md), you can manage these tasks in a central location designed for endpoint management.

This article discusses concepts and features you should consider when managing your identities.

## Use your existing users and groups

A large part of managing endpoints is managing users and groups. If you have existing users and groups or will create new users and groups, Intune can help.

In on-premises environments, user accounts and groups are created and managed in on-premises Active Directory. You can update these users and groups using any domain controller in the domain.

It's a similar concept in Intune.

The Intune admin center includes a central location to manage users and groups. The admin center is web-based and can be accessed from any device that has an internet connection. Admins just need to sign into the admin center with their Intune administrator account.

An important decision is to determine how to get the user accounts and groups into Intune. Your options:

- If you **currently use Microsoft 365** and have your users and groups in the Microsoft 365 admin center, then these users and groups are also available in the Intune admin center.

  Azure AD and Intune use a "tenant", which is your organization, such as Contoso or Microsoft. If you have multiple tenants, sign into the Intune admin center in the same Microsoft 365 tenant as your existing users and groups. Your users and groups will automatically be shown and available.

  For more information on what a tenant is, go to [Quickstart: Set up a tenant](/azure/active-directory/develop/quickstart-create-new-tenant).

- If you **currently use on-premises Active Directory**, then you can use Azure AD Connect to synchronize your on-premises AD accounts to Azure AD. When these accounts are in Azure AD, then they're also available in the Intune admin center.

  For more specific information, go to [What is Azure AD Connect sync?](/azure/active-directory/hybrid/how-to-connect-sync-whatis).

- You can also **import existing users and groups** from a CSV file into the Intune admin center, or create the users and groups from scratch. When adding groups, you can add users and devices to these groups to organize them by location, department, hardware, and more.

  For more information on group management in Intune, go to [Add groups to organize users and devices](groups-add.md).

By default, Intune automatically creates the **All users** and **All devices** groups. When your users and groups are available to Intune, then you can assign your policies to these users and groups.

### Move from machine accounts

When a Windows endpoint, like a Windows 10/11 device, joins an on-premises Active Directory (AD) domain, a computer account is automatically created. The computer/machine account can be used to authenticate on-premises programs, services, and apps.

These machine accounts are local to the on-premises environment and can't be used on devices that are joined to Azure AD. In this situation, you need to switch to user-based authentication to authenticate to on-premises programs, services, and apps.

For more information and guidance, go to [Known issues and limitations with cloud-native endpoints](/mem/cloud-native-endpoints-known-issues).

## Roles and permissions control access

For the different admin-type of tasks, Intune uses role-based access control (RBAC). The roles you assign determine the resources an admin can access in the Intune admin center, and what they can do with those resources. There are some built-in roles focused on endpoint management, such as Application Manager, Policy and Profile Manager, and more.

Since Intune uses Azure AD, you also have access to the built-in Azure AD roles, such as Global Administrator and Intune Service Administrator.

Each role has its own create, read, update or delete permissions as needed. You can also create custom roles if your admins need a specific permission. When you add or create your administrator-type of users and groups, you can assign these accounts to the different roles. The Intune admin center has this information in a central location and can be easily updated.

For more information, go to [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)

## Create user affinity when devices enroll

When users sign into their devices the first time, the device becomes associated with that user. This feature is called user affinity.

Any policies assigned or deployed to the user identity go with the user to all of their devices. When a user is associated with the device, they can access their email accounts, their files, their apps, and more.

When you don't associate a user with a device, then the device is considered user-less. This scenario is common for kiosks devices dedicated to a specific task and devices that are shared with multiple users.

In Intune, you can create policies for both scenarios on Android, iOS/iPadOS, macOS, and Windows. When getting ready to manage these devices, be sure you know the intended purpose of the device. This information helps in the decision making process when devices are being enrolled.

For more specific information, go to the enrollment guides for your platforms:

- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS and iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)
- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Assign policies to users and groups

On-premises, you work with domain accounts and local accounts, and then deploy group policies and permissions to these accounts at the local, site, domain, or OU level (LSDOU). An OU policy overwrites a domain policy, a domain policy overwrites a site policy, and so on.

Intune is cloud-based. Policies created in Intune include settings that control device features, security rules, and more. These policies are assigned to your users and groups. There isn't a traditional hierarchy like LSDOU.

The settings catalog in Intune includes thousands of settings to manage iOS/iPadOS, macOS, and Windows devices. If you currently use on-premises Group Policy Objects (GPOs), then using the settings catalog is a natural transition to cloud-based policies.

For more information on policies in Intune, go to:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md)

## Secure your user identities

Your user and group accounts access organization resources. You need to keep these identities secure and prevent malicious access to the identities. Here are some things to consider:

- **Windows Hello for Business** replaces username and password sign-in and is part of a password-less strategy.

  Passwords are entered on a device and then transmitted over the network to the server. They can be intercepted and used by anyone and anywhere. A server breach can reveal stored credentials.

  With Windows Hello for Business, users sign in and authenticate with a PIN or biometric, such as facial and fingerprint recognition. This information is stored locally on the device and isn't sent to external devices or servers.

  When Windows Hello for Business is deployed to your environment, you can use Intune to create Windows Hello for Business policies for your devices. These policies can configure PIN settings, allowing biometric authentication, use security keys, and more.

  For more information, go to:

  - [Windows Hello for Business Overview](/windows/security/identity-protection/hello-for-business/hello-overview)
  - [Manage Windows Hello for Business on devices when devices enroll with Intune](../protect/windows-hello.md)
  - [Use identity protection profiles to manage Windows Hello for Business in Microsoft Intune](../protect/identity-protection-configure.md)

- **Certificate-based authentication** is also a part of a password-less strategy. You can use certificates to authenticate your users to applications and organization resources through a VPN, a Wi-Fi connection, or email profiles. With certificates, users don't need to enter usernames and passwords, and can make access to these resources easier.

  For more information, go to [Use certificates for authentication in Microsoft Intune](../protect/certificates-configure.md).

- **Multi-factor authentication (MFA)** is a feature available with Azure AD. For users to successfully authenticate, at least two different verification methods are required. When MFA is deployed to your environment, you can also require MFA when devices are enrolling into Intune.

  For more information, go to:

  - [Plan an Azure Active Directory Multi-Factor Authentication deployment](/azure/active-directory/authentication/howto-mfa-getstarted)
  - [Require multi-factor authentication for Intune device enrollments](../enrollment/multi-factor-authentication.md)

- **Zero trust** verifies all endpoints, including devices and apps. The idea is to help keep organization data in the organization, and prevent data leaks from accidental or malicious intent. It includes different feature areas, including Windows Hello for Business, using MFA, and more.

  For more information, see [Zero Trust with Microsoft Intune](zero-trust-with-microsoft-intune.md).

## Next steps

- [Manage devices](manage-devices.md)
- [Manage apps](manage-apps.md)
