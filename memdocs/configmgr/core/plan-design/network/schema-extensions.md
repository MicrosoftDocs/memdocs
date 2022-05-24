---
title: About schema extensions
titleSuffix: Configuration Manager
description: Understand the benefits of extending the Active Directory schema to support Configuration Manager.
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# About schema extensions for Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can extend the Active Directory schema to support Configuration Manager. This action edits a forest's Active Directory schema to add a new container and several attributes. Configuration Manager sites use these extensions to publish key information in Active Directory where clients can securely access it. This information can simplify the deployment and configuration of clients. It also helps clients locate site resources like servers with deployed content or that provide different services to clients.

Microsoft recommends that you extend your Active Directory schema for Configuration Manager, but it's not required.

Before you [extend the Active Directory schema](extend-the-active-directory-schema.md), you should be familiar with Active Directory Domain Services and comfortable with modifying the [Active Directory schema](/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).

## Considerations

- There are no new Active Directory schema extensions for Configuration Manager current branch. They haven't changed since Configuration Manager 2007. If you previously extended the schema an earlier version, you don't have to extend the schema again.

- Extending the schema is a forest-wide, one-time, irreversible action.

- Only a member of the **Schema Admins** group can extend the schema. It can also be a user with delegated permissions to change the schema.

- You can extend the schema before or after you install a Configuration Manager site. However, it's best to extend the schema before you start to configure your sites and hierarchy settings. This action can simplify many of the later configuration steps.

- After you extend the schema, the Active Directory global catalog replicates throughout the forest. Plan to extend the schema when the replication traffic won't adversely affect other network-dependent processes. Active Directory only replicates the newly added attributes.

### Devices and clients that don't use the Active Directory schema

- Mobile devices that are managed by the Exchange Server connector

- The client for macOS computers

- Mobile devices that are enrolled by Configuration Manager on-premises MDM

- Windows clients that you configure for internet-only client management

- Windows clients that Configuration Manager detects to be on the internet

## Features that benefit

The following Configuration Manager features benefit from extending the Active Directory schema.

### Client computer installation and site assignment

When you install a new client on a Windows computer, it searches Active Directory Domain Services for installation properties.

If you don't extend the schema, use one of the following options to provide configuration details:

- Use [client push installation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation). This method uses the client installation properties that you configure in the Configuration Manager console.

- Use [manual installation](../../clients/deploy/plan/client-installation-methods.md#manual-installation). Provide at least the following client installation properties on the command line:

  - Specify a management point or source path from which the computer can download the installation files. Use the CCMSetup property `/mp` or `/source`.

  - Specify a list of initial management points for the client to use. It uses this initial management point to assign to the site and download client policy and site settings. Use the CCMSetup Client.msi property `SMSMP`.

  For more information, see [About client installation parameters and properties](../../clients/deploy/about-client-installation-properties.md).

- [Publish the management point in DNS](../hierarchy/understand-how-clients-find-site-resources-and-services.md#dns). Configure clients to use this service location method.

### Port configuration for client-to-server communication

When a client installs, it uses the port information from Active Directory. If you later change the client-to-server communication port for a site, clients get this new port setting from Active Directory.

If you don't extend the schema, use one of the following options to provide new port configurations to existing clients:

- Reinstall clients. Use options that configure the new port.

- Deploy a custom script to clients that updates the communication port. If clients can't communicate with a site because of a port change, you can't use Configuration Manager to deploy this script. For example, you could use group policy.

### Content deployment scenarios

When you create content at one site, and then deploy that content to another site in the hierarchy, the receiving site tries to verify the signature of the signed content data. This behavior requires access to the public key of the source site where you create this content. When you extend the Active Directory schema for Configuration Manager, a site's public key is available to all sites in the hierarchy.

If you don't extend the schema, use the [hierarchy maintenance tool](../../servers/manage/hierarchy-maintenance-tool-preinst.exe.md), **preinst.exe**, to exchange the secure key information between sites.

For example, you plan to create content at a primary site and then deploy that content to a secondary site below a different primary site. If you extend the Active Directory schema, the secondary site automatically gets the source primary site's public key. Otherwise, use preinst.exe to share keys between the two sites directly.

## Active Directory attributes and classes

When you extend the schema for Configuration Manager, the following classes and attributes are added to the schema and available to all Configuration Manager sites in that Active Directory forest.  

| Attributes | Classes |
|---------|---------|
| cn=mS-SMS-Assignment-Site-Code</br>cn=mS-SMS-Capabilities</br>cn=MS-SMS-Default-MP</br>cn=mS-SMS-Device-Management-Point</br>cn=mS-SMS-Health-State</br>cn=MS-SMS-MP-Address</br>cn=MS-SMS-MP-Name</br>cn=MS-SMS-Ranged-IP-High</br>cn=MS-SMS-Ranged-IP-Low</br>cn=MS-SMS-Roaming-Boundaries</br>cn=MS-SMS-Site-Boundaries</br>cn=MS-SMS-Site-Code</br>cn=mS-SMS-Source-Forest</br>cn=mS-SMS-Version | cn=MS-SMS-Management-Point</br>cn=MS-SMS-Roaming-Boundary-Range</br>cn=MS-SMS-Server-Locator-Point</br>cn=MS-SMS-Site |

> [!NOTE]
> The schema extensions might include attributes and classes from previous versions of the product but not used by the latest version. For example:
>
> - Attribute: cn=MS-SMS-Site-Boundaries
> - Class: cn=MS-SMS-Server-Locator-Point

You can view these settings in the **ConfigMgr_ad_schema.LDF** file from the **\SMSSETUP\BIN\x64** folder of the Configuration Manager installation media.

## Next steps

[Prepare Active Directory for site publishing](extend-the-active-directory-schema.md)
