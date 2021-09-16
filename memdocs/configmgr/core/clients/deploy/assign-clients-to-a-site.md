---
title: Assign clients to a site
titleSuffix: Configuration Manager
description: Before you can manage a client, it needs to assign to a primary site.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# How to assign clients to a site in Configuration Manager

*Applies to: Configuration Manager (current branch)*

After you install the Configuration Manager client, before you can manage the client, it needs to join a Configuration Manager primary site. The site that a client joins is called its _assigned site_. You can't assign a client to a central administration site or a secondary site.

The assignment process happens after you successfully install the client and it determines which site manages the computer. You can either directly assign the client to a site, or use automatic site assignment. With automatic assignment, the client finds an appropriate site based on its current network location. The client may assign to a fallback site, if you configure it for the hierarchy.

> [!NOTE]
> Always assign clients to sites running the same version of Configuration Manager. Avoid assigning a client from a later release to a site on an earlier release. If necessary, update the primary site to the same Configuration Manager version that you use for the clients.

After the client assigns to a site, it remains assigned to that site, even if it changes its IP address or roams to another site. Only an administrator can manually assign the client to another site or remove the client assignment.

> [!WARNING]
> An exception to a client remaining assigned to a site is if you assign the client on a Windows Embedded device with write filters enabled. If you don't first disable write filters before you assign the client, the site assignment status of the client reverts to its original state when the device next restarts. For example, if you configure the client for automatic site assignment, it reassigns on startup and might assign to a different site. If the client requires manual site assignment, you have to manually reassign it before you can manage it.
>
> To avoid this behavior, disable the write filters before you assign the client on embedded devices. Then enable the write filters after you have verified that site assignment was successful.

If assignment fails, the client remains installed, but you can't manage it. A client is considered _unmanaged_ when it's installed but not assigned to a site. It's also unmanaged when it's assigned to a site but it can't communicate with a management point.

## Manual site assignment

You can manually assign client computers to a site by using the following two methods:

- Use a client installation property that specifies the site code. For more information, see [Client installation properties - SMSSITECODE](about-client-installation-properties.md#smssitecode).

- In the Windows Control Panel for **Configuration Manager**, specify the site code.

> [!NOTE]
> If you manually assign a client to a site code that doesn't exist, the site assignment fails.

## Automatic site assignment

Automatic site assignment typically happens during client deployment. To manually start automatic site assignment, select **Find Site** on the **Advanced** tab of the **Configuration Manager** control panel. The Configuration Manager client compares its network location with the boundaries for the hierarchy. When the network location of the client falls within a boundary group you enabled for site assignment, or the hierarchy is configured for a fallback site, the client is automatically assigned to that site. This behavior lets clients easily assign to a site and you don't have to specify a site code.

> [!NOTE]
> If a client computer has multiple network adapters and multiple IP addresses, the IP address used to evaluate client site assignment is assigned randomly.

For more information about how to configure boundary groups for site assignment, see [Define site boundaries and boundary groups](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

Configuration Manager clients that use automatic site assignment attempt to find site boundary groups that you publish to Active Directory Domain Services. If this process fails, clients can get boundary group information from a management point. This process can fail if you don't extend the Active Directory schema for Configuration Manager, or clients are workgroup computers.

When you install the client, you can specify a management point for it to use, or the client can locate a management point automatically. For more information, see [How clients find site resources and services](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).

If the client can't find a site in a boundary group for its network location, and the hierarchy doesn't have a fallback site, the client retries every 10 minutes. It repeats this process until it assigns to a site.

Configuration Manager clients can't automatically assign to a site if any of the following conditions apply:

- They are currently assigned to a site.

- They are on the internet or configured as internet-only clients.

- Their network location doesn't fall within one of the boundary groups in the hierarchy, and there's no fallback site.

If any of these conditions apply, you have to manually assign the client.

## Check site compatibility

After a client has found its assigned site, the site checks the version of the Configuration Manager client and OS. This check is to make sure that the site can manage the client. For example, a current branch site can't manage a Configuration Manager 2007 client, or a client that runs Windows 2000.

If you try to assign a client that runs a legacy OS version, site assignment fails. When you assign a Configuration Manager 2007 client or a System Center 2012 Configuration Manager client to a current branch site, assignment succeeds to support automatic client upgrade. However, until you upgrade the older generation clients, you can't manage it.

> [!NOTE]
> To support the site assignment of a Configuration Manager 2007 or a System Center 2012 Configuration Manager client to a current branch site, configure automatic client upgrade for the hierarchy. For more information, see the [How to upgrade clients for Windows computers](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

Configuration Manager also checks that you've assigned the current branch client to a site that supports it.

The site compatibility check requires one of the following conditions:  

- The client can access site information published to Active Directory Domain Services.

- The client can communicate with a management point in the site.

If the site compatibility check fails to finish successfully, the site assignment fails. The client remains unmanaged until the site compatibility check runs again and succeeds.

An exception to this site compatibility check is when you configure a client for an internet-based management point. In this case, Configuration Manager doesn't check site compatibility. If you assign clients to a site that contains internet-based site systems, and you specify an internet-based management point, make sure that you assign the client to the correct site.

### Scenarios for assignment of legacy clients

The following scenarios might occur during migration from previous versions of Configuration Manager:

#### You use automatic site assignment and boundaries overlap between versions of Configuration Manager

In this case, the client automatically tries to find a current branch site.  

The client first checks Active Directory Domain Services. If it finds a current branch site published, site assignment succeeds. If this check fails, the client then checks for site information from its assigned management point.

> [!NOTE]
> You can specify an initial management point for the client during client installation. For more information, see [Client installation properties - SMSMP](about-client-installation-properties.md#smsmp).

If both these methods fail, site assignment fails. You need to manually assign the client.

#### Accidental manual assignment to a legacy site version

For example, you assign a current branch client with a specific site code, and mistakenly specify a site code for a version of Configuration Manager earlier than System Center 2012 R2 Configuration Manager.

In this case, site assignment fails. Manually reassign the client to a current branch site.

## Locate a management point

After the client assigns to a site, it then tries to locate a management point. This process in itself can be complex, depending upon the situation. For more information about how the client locates management points and other site resources, see [How clients find site resources and services](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).

## Download site settings

After the client finds a management point, it needs to get client-related site settings. These settings include:

- The client certificate selection criteria
- Whether to use a certificate revocation list
- The client request port numbers

The client continues to check these settings on a periodic basis.

Clients get these settings from one of the following methods:

- If the client used Active Directory Domain Services for its site compatibility check, it downloads these settings for its assigned site from the domain.

- When clients can't get site settings from Active Directory, they download them from the management point.

- You specify the settings during client installation. For more information, see [About client installation properties](about-client-installation-properties.md).

## Download client settings

All clients download the **default client settings** policy and any applicable custom client settings policies. For more information, see [About client settings](about-client-settings.md).

Software Center relies on these client configuration policies. It notifies users that it can't run until the client downloads the configuration information. Depending on the client settings that you configure, the initial download of client settings might take a while. Some client management tasks might not run until this process is complete.

## Verify site assignment

You can verify site assignment success by any of the following methods:

- For clients on Windows computers, use the **Configuration Manager** control panel. Verify that it shows the correct site code on the **Site** tab.

- In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Devices** node. Verify that the computer shows **Yes** in the **Client** column and the correct primary site code in the **Site Code** column.

- Use the [reports for client assignment](../../servers/manage/list-of-reports.md#site---client-information).

- Use the **LocationServices.log** file on the client.

## Roaming to other sites

A client on the internal network is assigned to a primary site. You change the client computer's network location. It's now in a boundary group for another site. In this scenario, the client is _roaming_ in the other site. When this site is a secondary site for the client's assigned site, the client can use a management point in the secondary site to download policy and upload data. This behavior avoids sending this data over a potentially slow network. If the client roams into the boundary of another primary site, it still uses a management point in its assigned site to download policy and upload data.

Clients that roam to other sites can always use management points in other sites for [content location requests](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Management points in the current site can give clients a list of distribution points that have the requested content.

When you configure clients for internet-only client management, they only communicate with management points in their assigned site. These clients never communicate with management points in secondary sites or with management points in other primary sites. This behavior is the same for macOS and on-premises MDM devices that you enroll to Configuration Manager.

## Next steps

[How to monitor client deployment status](monitor-client-deployment-status.md)

[Monitor and manage clients](../manage/monitor-and-manage-clients.md)
