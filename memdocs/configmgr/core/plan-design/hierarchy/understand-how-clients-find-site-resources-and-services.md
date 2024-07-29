---
title: Find site resources
titleSuffix: Configuration Manager
description: Learn how and when Configuration Manager clients use service location to find site resources.
ms.date: 04/05/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How clients find site resources and services

*Applies to: Configuration Manager (current branch)*

Configuration Manager clients use a process called _service location_ to locate site system servers. Clients can communicate with these servers and they  provide services that clients can use. To better configure your sites to successfully support client tasks, you need to understand how and when clients use service location to find site resources. These configurations can require the site to interact with domain and network configurations like Active Directory Domain Services and DNS. They can also require you to configure more complex alternatives.

Some examples of site system roles that provide services include:

- The core site system server for clients.
- The management point.
- Other site system servers that the client can communicate with, like distribution points and software update points.

## Fundamentals of service location

When a client uses service location to find a management point to communicate with, it evaluates the following aspects:

- Current network location
- Communication protocol preference
- Assigned site

### Client communication with a management point

A client communicates with a management point (MP) to:

- Download information about other management points for the site. It then builds a list of known management points for future service location cycles. This list is also known as the *MP list*.

- Upload configuration details, like inventory and status.

- Download a policy that sets configurations on the client, informs it of software to install, and other related tasks.

- Request information about other site system roles that provide services that the client can use. For example, distribution points for software that the client can install, or a software update point for metadata about software updates.

### Client service location requests

A Configuration Manager client makes a service location request:

- Every 25 hours of continuous operation.

- When the client detects a change in its network configuration or location.

- When the **ccmexec.exe** service on the computer starts. This Windows service is the core client service.

- When the client needs to locate a site system role that provides a required service.

### Client requests for site system roles

When a client attempts to find servers that host roles, it uses service location. It tries to find a role that supports its communication protocol, either HTTP or HTTPS. By default, clients use the most secure method available to them.

- To use HTTPS, you need a public key infrastructure (PKI) and install PKI certificates on clients and servers. For more information, see [PKI certificate requirements for Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).

- For roles that use IIS and support client communication, you configure them for HTTP or HTTPS. If you use HTTP, also consider signing and encryption choices. For more information, see [Planning for signing and encryption](../../../core/plan-design/security/plan-for-security.md#signing-and-encryption).

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

## Determine assigned management point

Primary sites support multiple management points. Each client independently identifies a management point as its default. When a client first assigns to a primary site, it selects its default management point. This default management point then becomes that client's _assigned_ management point.

> [!TIP]
> You can use client installation properties to set the assigned management point for a client. For more information, see [Client installation properties](../../clients/deploy/about-client-installation-properties.md#smsmp).

A client selects a management point to communicate with based on the client's current network location and boundary group configurations. Even though it has an assigned management point, this server may not be the management point that the client uses.

> [!NOTE]
> A client always uses the assigned management point for registration messages and certain policy messages. This behavior happens even when other communications are sent to a proxy or local management point.

You can use preferred management points. Preferred management points are management points from a client's assigned site that are associated with a boundary group that the client uses to find site system servers. A preferred management point's association with a boundary group is similar to how distribution points or state migration points are associated with a boundary group. If you enable preferred management points for the hierarchy, when a client uses a management point from its assigned site, it tries to use a preferred management point before using other management points from its assigned site.

> [!TIP]
> You can configure management point affinity with a registry key configuration on the client. Management point affinity overrides the default behavior for assigned management points and lets the client use one or more specific management points. For more information, see [this blog post from a Microsoft Premier engineer](/archive/blogs/jchalfant/management-point-affinity-added-in-configmgr-2012-r2-cu3).

Each time a client needs to contact a management point, it first checks the [MP list](#the-mp-list). The client creates an initial MP list when it installs. The client then periodically updates the list with details about each management point in the hierarchy.

When the client can't find a valid management point in its MP list, it searches the service location sources. It uses the following sources in order, until it finds a management point that it can use:

1. Management point
2. Active Directory Domain Services (AD DS)
3. DNS

After a client successfully locates and contacts a management point, it downloads the current list of available management points. It then updates its own local MP list.

This process is the same for all clients. For example, when a Configuration Manager client that's on the internet connects to an internet-based management point, the management point sends that client a list of available internet-based management points. A client that's not on the internet only gets a list of internal management points.

## The MP list

The MP list is the preferred service location source for a client. It's a prioritized list of management points that the client previously identified. The client sorts its MP list based on its current network location. It stores the list locally in WMI.

### Build the initial MP list

During installation of the client, the client uses the following rules to build its initial MP list:

- Include management points specified during client installation. For example, when you use the `SMSMP` property or `/mp` parameter.

- Query AD DS for published management points. The client identifies management points from AD DS that are in its assigned site and the same product version.

- If it doesn't get any management points from the first two rules, the client checks DNS for published management points.

### MP list categories

Clients organize their list of management points by using the following categories:

- **Proxy**: A management point at a secondary site.

- **Local**: Any management point that's associated with the client's current network location, as defined by site boundaries.

  - When a client belongs to more than one boundary group, it determines the list of local management points from the union of all boundaries that include the current network location of the client.

  - Local management points are typically a subset of a client's assigned management points. Unless the client is in a network location that's associated with another site with management points servicing its boundary groups.

- **Assigned**: Any management point that's in the client's assigned site.

You can use preferred management points. Management points at a site that aren't associated with a boundary group, or that aren't in a boundary group associated with a client's current network location, aren't considered preferred. The client uses these management points when it can't find an available preferred management point.

### Select a management point to use

For typical communications, a client tries to use a management point in the following order, based on the client's network location:

1. Proxy
2. Local
3. Assigned

The client always uses the assigned management point for registration messages and certain policy messages. This behavior happens even when it sends other communication to a proxy or local management point.

Within each [category](#mp-list-categories), the client attempts to use a management point based on preferences, in the following order:

1. When the client is configured for HTTPS communication:
    1. HTTPS-capable in a trusted or local forest
    1. HTTPS-capable not in a trusted or local forest
1. HTTP-capable in a trusted or local forest
1. HTTP-capable not in a trusted or local forest

From the set of management points sorted by preference, the client attempts to use the first management point on the list. This sorted list of management points is otherwise randomized and can't be ordered any further. The order of the list can change each time the client updates its MP list.

When a client can't contact the first management point, it tries each successive management point on its list. It tries each preferred management point in the category before trying the non-preferred management points. If a client can't successfully communicate with any management point in the category, it attempts to contact a preferred management point from the next category, until it finds a management point to use.

After a client establishes communication with a management point, it continues to use that same management point until:

- The client is unable to communicate with the management point for five attempts over a period of 10 minutes.

The client then randomly selects a new management point to use.

## Active Directory

Domain-joined clients can use AD DS for service location. This behavior requires sites to [publish data to Active Directory](../../servers/deploy/configure/publish-site-data.md).

A client can use AD DS for service location when all the following conditions are true:

- You [extended the Active Directory schema](../network/extend-the-active-directory-schema.md).

- You [configured the Active Directory forest for publishing](../../servers/deploy/configure/publish-site-data.md), and you configured the Configuration Manager site to publish.

- The client computer is a member of an Active Directory domain and can access a global catalog server.

If a client can't find a management point to use for service location from AD DS, it attempts to use DNS.

## DNS

Clients on the intranet can use DNS for service location. This behavior requires at least one site in a hierarchy to publish information about management points to DNS.

Consider using DNS for service location when any of the following conditions are true:

- You haven't extended the AD DS schema to support Configuration Manager.

- Clients on the intranet are in a forest that you haven't enabled for Configuration Manager publishing.

- You have clients on workgroup computers, and you haven't configured those clients for internet-only client management. A workgroup client configured for the internet communicates only with internet-facing management points and won't use DNS for service location.

- You can [configure clients to find management points from DNS](../../clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).

When a site publishes service location records for management points to DNS:

- Publishing is applicable only to management points that accept client connections from the intranet.

- Publishing adds a service location resource record (SRV RR) in the DNS zone of the management point server. That server needs a corresponding host entry in DNS.

By default, domain-joined clients search DNS for management point records from the client's local domain. You can configure a [client installation property](../../clients/deploy/about-client-installation-properties.md#dnssuffix) to specify another domain suffix.

For more information, see [How to configure client computers to find management points by using DNS publishing](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).

### Publish management points to DNS

To publish management points to DNS, the following two conditions must be true:  

- Your DNS servers support service location resource records, by using a version of BIND that's at least 8.1.2.

- The specified intranet FQDNs for the management points in Configuration Manager have host entries (A records) in DNS.

> [!IMPORTANT]
> Configuration Manager DNS publishing doesn't support a disjointed namespace. If you have a disjointed namespace, you can manually publish management points to DNS. You can also use one of the other service location methods.

#### DNS configuration scenarios

##### The DNS server supports automatic updates

You can configure Configuration Manager to automatically publish management points on the intranet to DNS, or you can manually publish these records to DNS. When Configuration Manager publishes management points to DNS, it adds their intranet FQDN and port number in the service location (SRV) record. You configure DNS publishing in the site's **Management Point Component Properties**. For more information, see [Site components - Management point](../../../core/servers/deploy/configure/site-components.md#management-point).

##### The DNS zone is set to "Secure only" for dynamic updates

With default permissions, only the first management point can successfully publish to DNS.

If only one management point can successfully publish and change its DNS record, clients can get the full MP list from that management point. As long as that one published management point is healthy, clients can then find their preferred management point.

##### The DNS server doesn't support automatic updates but supports service location records

In this scenario, manually publish management points to DNS. Manually configure the service location resource record (SRV RR). Configuration Manager supports RFC 2782 for service location records. These records have the following format: `_Service._Protocol.Name TTL Class SRV Priority Weight Port Target`

To publish a management point to Configuration Manager, specify the following values:

- **_Service**: `_mssms_mp_<sitecode>`. For example, `_mssms_mp_xyz`
- **._Protocol**: `._tcp`
- **.Name**: Specify the DNS suffix of the management point, for example `contoso.com`
- **TTL**: Use `14400` for four hours.
- **Class**: Specify `IN` for RFC 1035.
- **Priority**: Configuration Manager doesn't use this field.
- **Weight**: Configuration Manager doesn't use this field.
- **Port**: Specify the port number that the management point uses. For example, `443` by default for HTTPS.
- **Target**: Specify the intranet FQDN of the site system server with the management point role.

#### Configure Windows Server DNS

If you use Windows Server DNS, use the following procedures to enter this DNS record for intranet management points.

##### Configure automatic publishing for a site

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select the site to configure publishing. In the ribbon, select **Configure Site Components** and choose **Management Point**.

1. Select the management points that you want to publish. This selection applies to publishing for AD DS and DNS.

1. Enable the option to **Publish selected intranet management points in DNS**.

##### Manually publish management points to DNS on Windows Server

1. In the DNS management console, select the DNS zone for the management point computer.

1. Verify that there's a host record (**A** or **AAAA**) for the intranet FQDN of the site system. If this record doesn't exist, create it.

1. Select **New Other Records**, choose **Service Location (SRV)**, and then choose **Create Record**.

1. Specify the following information, and then select **Done**:

    - **Domain**: If necessary, enter the DNS suffix of the management point, for example `contoso.com`.
    - **Service**: `_mssms_mp_<sitecode>`. For example,  `_mssms_mp_xyz`
    - **Protocol**: `._tcp`
    - **Priority**: Configuration Manager doesn't use this field.
    - **Weight**: Configuration Manager doesn't use this field.
    - **Port**: Specify the port number that the management point uses. For example, `443` by default for HTTPS.
    - **Host offering this service**: Specify the intranet FQDN of the site system server with the management point role.

Repeat these steps for each management point on the intranet that you want to publish to DNS.
