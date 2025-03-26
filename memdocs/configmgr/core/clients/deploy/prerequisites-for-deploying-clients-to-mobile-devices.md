---
title: Mobile device client prerequisites
titleSuffix: Configuration Manager
description: Learn about the prerequisites for deploying the Configuration Manager client to mobile devices.
ms.date: 01/05/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: install-set-up-deploy
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Prerequisites for deploying clients to mobile devices in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> On-premises MDM and the Configuration Manager client for macOS are both [deprecated](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->
>
> Migrate management of macOS and mobile devices to Microsoft Intune. For more information, see [Supported clients and devices](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

Deploying Configuration Manager clients in your environment has the following external dependencies and dependencies within the product.

For more information on the minimum hardware and OS requirements for the Configuration Manager client, see [Supported configurations](../../plan-design/configs/supported-configurations.md).

> [!NOTE]
> The software version numbers shown in this article only list the minimum version numbers required.

When you install the Configuration Manager client on mobile devices and enroll them, use this information to determine the prerequisites.

## Dependencies external to Configuration Manager

- A Microsoft enterprise certification authority (CA) with certificate templates to deploy and manage the certificates required for mobile devices.

    The issuing CA must automatically approve certificate requests from the mobile device users during the enrollment process.

    For more information about the certificate requirements, see [Security and privacy for certificate profiles](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).

- A security group that contains the users that can enroll their mobile devices.

    This security group is used to configure the certificate template that is used during mobile device enrollment.

- Optional but recommended: a DNS alias (CNAME record) named **ConfigMgrEnroll**. Configure this alias for the server name of the enrollment proxy point.

    This DNS alias is required to support automatic discovery for the enrollment service. If you don't configure this DNS record, users must manually specify the name of the enrollment proxy point as part of the enrollment process.

- Site system role dependencies for the computers that run the enrollment point and the enrollment proxy point.

    For more information, see [Supported operating systems for site system servers](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

## Configuration Manager dependencies

For more information, see [Determine the site system roles for clients](plan/determine-the-site-system-roles-for-clients.md).

- Management point configurations:

  - HTTPS client connections
  - Enabled for mobile devices
  - An internet FQDN
  - Accept client connections from the internet

- Enrollment point and enrollment proxy point

    An enrollment proxy point manages enrollment requests from mobile devices and the enrollment point completes the enrollment process. The enrollment point must be in the same Active Directory forest as the site server, but the enrollment proxy point can be in another forest.

- Client settings for mobile device enrollment

    Configure client settings to allow users to enroll mobile devices and configure at least one enrollment profile.

- Reporting services point

    The reporting services point is an optional, but recommended site system role. It can display reports related to mobile device enrollment and client management. For more information, see [Introduction to reporting](../../servers/manage/introduction-to-reporting.md).

- To configure enrollment for mobile devices, your account needs the following security permissions:

  - To add, modify, and delete the enrollment site system roles: **Modify** permission for the **Site** object.

  - To configure client settings for enrollment: Default client settings require **Modify** permission for the **Site** object, and custom client settings require **Client agent** permissions.

  The **Full Administrator** default security role includes the required permissions to configure the enrollment site system roles.

- To manage enrolled mobile devices, your account needs the following security permissions:

  - To wipe or retire a mobile device: **Delete resource** for the **Collection** object.

  - To cancel a wipe or retire command: **Delete resource** for the **Collection** object.

  - To allow and block mobile devices: **Modify resource** for the **Collection** object.

  - To remote lock, or reset the passcode on a mobile device: **Modify** resource for the **Collection** object.

  The **Operations Administrator** default security role includes the required permissions to manage mobile devices.

For more information about how to configure security permissions, see [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md) and [Configure role-based administration](../../servers/deploy/configure/configure-role-based-administration.md).

## Firewall requirements

Intervening network devices such as routers and firewalls, and Windows Firewall if applicable, must allow the traffic associated with mobile device enrollment.

- Between mobile devices and the enrollment proxy point: HTTPS (by default, TCP 443)

- Between the enrollment proxy point and the enrollment point: HTTPS (by default, TCP 443)

If you use a proxy web server, configure it for SSL tunneling. SSL bridging isn't supported for mobile devices.

## Next steps

[Windows firewall and port settings for clients](windows-firewall-and-port-settings-for-clients.md)
