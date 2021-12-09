---
title: Client deployment recommendations
titleSuffix: Configuration Manager
description: Understand product recommendation for client deployment.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Recommendations for client deployment in Configuration Manager

*Applies to: Configuration Manager (current branch)*

## Planning

### Use a phased rollout to manage CPU usage

To minimize the effect of the CPU processing requirements on the site server, use a phased rollout of clients. Deploy clients outside of business hours. This practice allows other services to have more available bandwidth during the day. It also doesn't disrupt user productivity if their computer slows down or requires a restart.

### Prepare required PKI certificates in advance

PKI certificates enable the following scenarios:

- HTTPS-enabled client communication
- Manage devices on the internet
- Enroll mobile devices for on-premises MDM
- Enroll macOS devices

You need certificates on certain site systems and the client devices. The most common site systems are management points and distribution points. On production networks, you might require change management approval to use new certificates or restart site system servers. Users may also need to sign out of Windows to get new group membership. Make sure to allow sufficient time for replication of security permissions and new certificate templates.

For more information, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).

## Before you begin

### Extend the Active Directory schema and publish the site so that you can run CCMSetup without command-line options

When you extend the Active Directory schema for Configuration Manager, and publish the site to Active Directory Domain Services, the site publishes many client installation properties to Active Directory. If a computer can locate these client installation properties, it can use them during Configuration Manager client deployment. Because the site automatically generates this information, it eliminates the risk of human error associated with manually entering installation properties.

For more information, see [About client installation properties published to Active Directory Domain Services](../about-client-installation-properties-published-to-active-directory-domain-services.md).

### Install client language packs

Before you deploy the client, install any necessary client language packs to enable other languages. If you install client language packs on a site after you install clients, you need to reinstall the clients before they can use the new languages.

For more information, see [Language packs](../../../servers/deploy/install/language-packs.md).

### Configure any required client settings and maintenance windows

Although you can configure client settings and maintenance windows before or after you install clients, it's better to configure required settings before you install clients. Then the client can use them as soon as it installs. For more information about settings download during the client assignment process, see [How to assign clients to a site](../assign-clients-to-a-site.md#download-client-settings).

Configure maintenance windows for servers and for Windows Embedded devices to support business continuity on critical devices. Maintenance windows make sure that required software updates and antimalware software don't restart the computer during business hours.

For more information, see [Configure client settings](../configure-client-settings.md) and [How to use maintenance windows](../../manage/collections/use-maintenance-windows.md).

## Installation

### If you install the client with client.msi properties, use SMSMP and FSP

The **SMSMP** property specifies the initial management point for the client. It removes the dependency on service location solutions such as Active Directory Domain Services and DNS.

Use the FSP property and install a fallback status point. It allows you to better monitor client installation and assignment, and identify any communication problems.

For more information about these options, see [About client installation properties](../about-client-installation-properties.md).

### Use software update-based client installation for Active Directory computers

This client deployment method has the following benefits:

- Uses existing Windows technologies
- Integrates with your Active Directory infrastructure
- Requires the least configuration in Configuration Manager
- Is the easiest to configure for firewalls
- Is the most secure

By using security groups and WMI filtering for the group policy configuration, you also have flexibility to control which computers install the Configuration Manager client.

For more information, see [How to install Configuration Manager clients by using software update-based installation](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### Enable automatic upgrade after your main client deployment finishes

Performance improvements in Configuration Manager can allow you to use automatic upgrades as a primary client upgrade method. However, performance will depend on your hierarchy infrastructure, such as the number of clients.  

If you use another client installation method as the primary upgrade method, use automatic client upgrade to catch computers that it missed. For example, devices that were offline during the main deployment.

For more information, see [Automatic client upgrades](../../manage/upgrade/upgrade-clients-for-windows-computers.md).

### Assign site systems as clients to the same site

<!-- 9606023 -->
If you install the Configuration Manager client on site systems, assign them to the same site. Roles like the management point and distribution point have shared binary files between the role and the client. These collocated clients should always be the same version as the site system role.

For example, for a management point in site XYZ, assign the client installed on this site system server to site XYZ.

## Other device types

### Plan your user enrollment experience for Mac computers and mobile devices

If users will enroll their own macOS computers and mobile devices with Configuration Manager, plan the user experience. For example, you might script the installation and enrollment process by using a web page. Then users only enter the minimum amount of information necessary. You can also send instructions with a link by email.

### Write filters for Windows Embedded devices

Embedded devices that use enhanced write filters (EWF) are likely to experience state message resynchronization. For example, they send full inventory rather than delta inventory. If you have just a few embedded devices that use Enhanced Write Filters, you might not notice anything. However, when you have many embedded devices that resynchronize their information, this behavior can generate a noticeable increase in network packets and higher CPU processing on the site server.

When you have a choice of which type of write filter to enable, choose file-based write filters (FBWF) or unified write filters (UWF). Configure exceptions to persist client state and inventory data between device restarts. These exceptions improve network and CPU efficiency on the Configuration Manager client. For more information, see [Plan for client deployment to Windows Embedded devices](planning-for-client-deployment-to-windows-embedded-devices.md).

For more information about the maximum number of Windows Embedded clients that a primary site can support, see [Supported operating systems for clients and devices](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!IMPORTANT]
> For Windows computers that you plan to protect with a unified write filter (UWF), configure the device for UWF before you install the client. This configuration enables Configuration Manager to install the client with a custom credential provider that locks out low-rights users from signing in to the device during maintenance mode.

## Next steps

[How to deploy clients to Windows computers](../deploy-clients-to-windows-computers.md)
