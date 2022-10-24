---
title: Site system roles for clients
titleSuffix: Configuration Manager
description: Determine site system roles for clients in Configuration Manager.
ms.date: 01/04/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Determine the site system roles for Configuration Manager clients

*Applies to: Configuration Manager (current branch)*

This article can help you determine the site system roles that you need to deploy Configuration Manager clients.

For more information about where to install these roles in the hierarchy, see [Design a hierarchy of sites](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

For more information about how to install and configure these roles, see [Install site system roles](../../../servers/deploy/configure/install-site-system-roles.md).  

## Management point

By default, all Windows client computers use a distribution point to install the Configuration Manager client. They can fall back to a management point when a distribution point is unavailable. However, you can install Windows clients on computers from an alternative source when you use the CCMSetup command-line property `/source:<Path>`. For example, you might do this action if you install clients on the internet. Another scenario is when you want to avoid sending network packets between the computer and the management point during client installation. This scenario is because a firewall blocks the required ports or because you have a low-bandwidth connection. However, all clients must communicate with a management point to assign to a site and to be managed by Configuration Manager.  

For more information about client command-line properties, see [About client installation properties](../about-client-installation-properties.md).  

When you install more than one management point in the hierarchy, clients automatically connect to one point based on their forest membership and network location. You can't install more than one management point in a secondary site.  

Mac computer clients and mobile device clients that you enroll with Configuration Manager always require a management point for client installation. This management point must be in a primary site, must be configured to support mobile devices, and must accept client connections from the Internet. These clients can't use management points in secondary sites or connect to management points in other primary sites.  

## Distribution point

You don't need a distribution point to install Configuration Manager clients on Windows computers. By default, Configuration Manager uses a distribution point to install the client source files on Windows computers. It can fall back to downloading these files from a management point. Distribution points aren't used to install mobile device clients that are enrolled by Configuration Manager, but are used if you install the mobile device legacy client. If you install the Configuration Manager client as part of an OS deployment, the OS image is stored and retrieved from a distribution point.

Although you might not need distribution points to install most Configuration Manager clients, you'll need them to install software such as applications and software updates on the clients.  

## Fallback status point

You can use a fallback status point to monitor client deployment for Windows computers. You can also identify the Windows computer clients that are unmanaged because they can't communicate with a management point.

The following client types don't use a fallback status point:

- Mac computers
- Mobile devices that are enrolled by Configuration Manager
- Mobile devices that are managed by using the Exchange Server connector

A fallback status point isn't required to monitor client activity and client health.  

The fallback status point always communicates with clients over HTTP, which uses unauthenticated connections and sends data in clear text. This behavior makes the fallback status point vulnerable to attack, particularly when it's used with internet-based client management. To help reduce the attack surface, always dedicate a server to running the fallback status point. Don't install other site system roles on the same server in a production environment.  

Install a fallback status point if all the following conditions apply:  

- You want client communication errors from Windows computers to be sent to the site, even if these client computers can't communicate with a management point.  

- You want to use the Configuration Manager client deployment reports, which display the data that's sent by the fallback status point.  

- You have a dedicated server for this site system role and have additional security measures to help protect the server from attack.  

- The benefits of using a fallback status point outweigh any security risks associated with unauthenticated connections and clear text transfers over HTTP traffic.  

Don't install a fallback status point if the security risks of running a website with unauthenticated connections and clear text transfers outweigh the benefits of identifying client communication problems.  

## Reporting services point

Configuration Manager provides many reports to help you monitor the installation, assignment, and management of clients in the Configuration Manager console. Some of the client deployment reports require that clients are assigned to a fallback status point.  

The reports aren't needed to deploy clients. You can see some deployment information in the Configuration Manager console or use the client log files for detailed information. However, the client reports provide valuable information to help monitor and troubleshoot client deployment.  

## Enrollment point and enrollment proxy point

> [!IMPORTANT]
> With the deprecation of on-premises MDM and the Configuration Manager client for macOS, these site system roles are also deprecated. For more information, see [Removed and deprecated features for Configuration Manager](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->

Configuration Manager requires the enrollment point and the enrollment proxy point to enroll mobile devices and to enroll certificates for Mac computers. You don't need these site system roles in the following situations:

- You plan to manage mobile devices by using the Exchange Server connector
- You install the mobile device legacy client
- You request and install the client certificate on Mac computers independently from Configuration Manager

## Cloud management gateway connector point

You need a cloud management gateway connector point if you're setting up a [cloud management gateway](../../manage/cmg/overview.md) to manage clients on the internet.
