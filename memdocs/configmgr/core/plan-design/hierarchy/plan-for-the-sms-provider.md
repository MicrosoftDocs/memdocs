---
title: Plan for the SMS Provider
titleSuffix: Configuration Manager
description: Learn about the SMS Provider site system role in Configuration Manager.
ms.date: 10/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Plan for the SMS Provider

*Applies to: Configuration Manager (current branch)*

To manage Configuration Manager, you use a Configuration Manager console that connects to an instance of the **SMS Provider**. By default, an SMS Provider installs on the site server when you install a central administration site (CAS) or primary site.

## About

The SMS Provider is a Windows Management Instrumentation (WMI) provider that assigns **read** and **write** access to the Configuration Manager database at a site.

- Each CAS and primary site require at least one SMS Provider. You can install more providers as needed.

- The **SMS Admins** security group provides access to the SMS Provider. Configuration Manager automatically creates this group on the site server, and on each computer where you install an instance of the SMS Provider. For more information, see [SMS Admins](accounts.md#sms-admins).

- Secondary sites don't support the SMS Provider role.

Configuration Manager administrative users use an SMS Provider to access information that's stored in the database. To do so, admins can use the Configuration Manager console, Resource Explorer, tools, and custom scripts. The SMS Provider doesn't interact with Configuration Manager clients. When a Configuration Manager console connects to a site, it queries WMI on the site server to locate an instance of the SMS Provider to use.

The SMS Provider helps enforce Configuration Manager security. It returns only the information that the console user is authorized to view.

The SMS Provider also provides API interoperability access over HTTPS, called the **administration service**. This REST API can be used in place of a custom web service to access information from the site. For more information, see [What is the administration service?](../../../develop/adminservice/overview.md).

> [!IMPORTANT]
> When each instance of the SMS Provider for a site is offline, Configuration Manager consoles can't connect to the site.

For more information about how to manage the SMS Provider, see [Manage the SMS Provider](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).

## Prerequisites

The SMS Provider has the following prerequisites:

- In the same domain as the site server and the site database site systems

- Can't have a site system role from a different site

- Can't already have an SMS Provider from any site

- Run a [supported OS version](../configs/supported-operating-systems-for-site-system-servers.md)

- At least 650 MB of free disk space to support the Windows ADK components. For more information about Windows ADK and the SMS Provider, see [OS deployment requirements](#os-deployment-requirements).

- For the [administration service](../../../develop/adminservice/overview.md) REST API:

  - Starting in version 2107, the SMS Provider requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> In version 2103 and earlier, this role requires .NET 4.5 or later. For more information, [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md#net-version-requirements).

  - In version 2006 and earlier, enable the Windows server role **Web Server (IIS)**. Starting in version 2010, this role is only required if you need to bind a PKI certificate.

    > [!NOTE]
    > Every SMS Provider attempts to install the administration service, which requires a certificate. This service has a dependency on IIS to bind that certificate to HTTPS port 443. If you enable [Enhanced HTTP](enhanced-http.md), then the site binds that certificate using IIS APIs. If your site uses PKI, you need to manually bind a PKI certificate in IIS on the SMS Provider. Unless the server already has a PKI-based certificate, the site automatically uses the site's self-signed certificate.

## Locations

When you install a site, you automatically install the first SMS Provider for the site. You can specify any of the following supported locations for the SMS Provider:

- The site server

- The site database server

- Another server, which meets the [installation prerequisites](#prerequisites)

To view the locations of each SMS Provider for a site:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the **Sites** node.

1. Select a site from the list, and then choose **Properties** in the ribbon.

1. On the **General** tab of the site **Properties**, view the **SMS Provider location** field.

Each SMS Provider supports simultaneous connections from multiple requests. The only limitations on these connections are the number of server connections that are available to Windows, and the available resources on the server to service the connection requests.

After you install a site, you can run Configuration Manager setup on the site server again. Use setup to change the location of an existing SMS Provider, or to install more SMS Providers at that site. Install only one SMS Provider on a computer. A computer can't host an SMS Provider from more than one site.

### Choosing a location

The following sections describe the advantages and disadvantages of installing an SMS Provider on each supported location:

#### Configuration Manager site server

- **Advantages:**

  - The SMS Provider doesn't use the system resources of the site database computer.

  - This location can provide better performance than an SMS Provider located on a computer other than the site server or site database computer.

- **Disadvantages:**

  - The SMS Provider uses system and network resources that could be dedicated to site server operations.

#### SQL Server that hosts the site database

- **Advantages:**

  - The SMS Provider doesn't use system resources on the site server.

  - This location can provide the best performance of the three locations, if sufficient server resources are available.

- **Disadvantages:**

  - The SMS Provider uses system and network resources that could be dedicated to site database operations.

  - When the site database is hosted on a clustered instance of SQL Server, you can't use this location.

#### Computer other than the site server or site database server

- **Advantages:**

  - SMS Provider doesn't use site server or site database system resources.

  - This type of location lets you deploy more SMS Providers to provide high availability for connections.

- **Disadvantages:**

  - The SMS Provider performance might be reduced. This behavior is because of the more network activity that it requires to coordinate with the site server and the site database computer.

  - This server must be always accessible to the site database server, and to all computers with the Configuration Manager console installed.

  - This location can use system resources that would otherwise be dedicated to other services.

## Authentication

[!INCLUDE [SMS Provider authentication](includes/sms-provider-authentication.md)]

## SMS Provider languages

The SMS Provider operates independently of the display language of the server where you install it.

When an administrative user or Configuration Manager process requests data by using the SMS Provider, it attempts to return that data in a format that matches the OS language of the requesting computer.

The way it attempts to match the language is indirect. The SMS Provider doesn't translate information from one language to another. When it returns data for display in the Configuration Manager console, the display language of the data depends on the source of the object and type of storage.

When Configuration Manager stores data for an object in the database, the available languages depend on the following factors:

- Configuration Manager stores objects that it creates by using support for multiple languages. It stores the object in the site database by using the languages that you configure for the site when you run setup. The Configuration Manager console displays these objects in the display language of the requesting computer, when that language is available for the object. If the console can't display the object in the display language of the requesting computer, it displays the object in the default language, which is English.

- Configuration Manager stores objects that an administrative user creates by using the language that was used to create the object. These objects display in the Configuration Manager console in this same language. The SMS Provider can't translate them, and they don't have multiple language options.

## Use multiple SMS Providers

After a site completes installation, you can install more SMS Providers for the site. To install more SMS Providers, run Configuration Manager setup on the site server.

Consider installing more SMS Providers when any of the following are true:

- Many administrative users need to use the Configuration Manager console and connect to a site at the same time.

- You use the Configuration Manager SDK, or other products, that might introduce frequent calls to the SMS Provider.

- You have a business requirement for high availability of the SMS Provider.

When you install multiple SMS Providers at a site, and a connection request is made, the site randomly assigns each new connection request to use an installed SMS Provider. You can't specify the SMS Provider to use with a specific connection session.

> [!NOTE]
> Consider the advantages and disadvantages of each SMS Provider location. For more information, see [Locations](#locations). Balance these considerations with the information that you can't control which SMS Provider is used for each new connection.

When you first connect a Configuration Manager console to a site, the connection queries WMI on the site server. This query identifies an instance of the SMS Provider that the console uses. This specific instance of the SMS Provider remains in use by the console until the session ends. If the session ends because the SMS Provider server is unavailable on the network, when you reconnect the console to the site, it repeats the initial query. It's possible the site assigns the same SMS Provider instance that's not available. If this behavior occurs, attempt to reconnect the console until the site returns an available SMS Provider.

## SMS Provider namespace

The Configuration Manager WMI schema defines the structure of the SMS Provider. Schema namespaces describe the location of Configuration Manager data within the SMS Provider schema. The following table contains some of the common namespaces that the SMS Provider uses:

|Namespace|Description|
|---------|-----------|
|`Root\SMS\site_<site code>`|The SMS Provider, which is extensively used by the Configuration Manager console, Resource Explorer, Configuration Manager tools, and scripts.|
|`Root\SMS\SMS_ProviderLocation`|The location of the SMS Provider computers for a site.|
|`Root\CIMv2`|The location inventoried for WMI namespace information during hardware and software inventory.|
|`Root\CCM`|Configuration Manager client configuration policies and client data.|
|`Root\CIMv2\SMS`|The location of inventory reporting classes that the inventory client agent collects. Clients compile these settings during computer policy evaluation. These settings are based on the client settings configuration for the computer.|

## OS deployment requirements

The computer where you install an instance of the SMS Provider requires a supported version of the Windows ADK.

For more information about this requirement, see [Infrastructure requirements for OS deployment](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk) and [Support for the Windows ADK](../configs/support-for-windows-adk.md).

When you manage OS deployments, the Windows ADK allows the SMS Provider to complete various tasks, such as:

- View WIM file details

- Add driver files to existing boot images

- Create boot ISO files

The Windows ADK installation can require up to 650 MB of free disk space on each computer that installs the SMS Provider. This high disk space requirement is necessary for Configuration Manager to install the Windows PE boot images.

## Administration service

<!--3607711, fka 1321523-->

The SMS Provider provides API interoperability access over an HTTPS OData connection, called the **administration service**. This REST API can be used in place of a custom web service to access information from the site.

For more information, see [What is the administration service?](../../../develop/adminservice/overview.md)

## Next steps

[Manage the SMS Provider](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)

[Configure authentication for the SMS Provider](../security/configure-security.md#sms-provider-authentication)

[Plan for the site database](plan-for-the-site-database.md)
