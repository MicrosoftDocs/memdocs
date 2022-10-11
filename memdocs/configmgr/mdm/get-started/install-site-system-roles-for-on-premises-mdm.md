---
title: Install roles for on-premises MDM
titleSuffix: Configuration Manager
description: Install the required site system roles for on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Install site system roles for on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager on-premises mobile device management (MDM) requires the following site system roles in your Configuration Manager site:

- Enrollment point

- Enrollment proxy point

- Distribution point

- Device management point, which is a management point that you allow for mobile devices

## Requirements and limitations

- On-premises MDM requires that you enable site system roles for HTTPS communications. For more information, see [Set up certificates for trusted communications in on-premises MDM](set-up-certificates-on-premises-mdm.md).

- The current branch of Configuration Manager only supports *intranet* connections from devices to the distribution points and device management points for on-premises MDM. However, if you also manage macOS computers, those clients require *internet* connections to those same roles. When you configure the distribution point and the device management point, use the option to **Allow intranet and internet connections**.

- Distribution points that you configure for intranet connections require that you configure site boundaries for them. Configuration Manager only supports IPv4 range boundaries for on-premises MDM. For more information, see [Define site boundaries and boundary groups](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- If you use [database replicas](../../core/servers/deploy/configure/database-replicas-for-management-points.md) with your device management point, newly enrolled devices will initially fail to connect. This connection failure occurs because the database replica doesn't have the information about the newly enrolled device necessary for a successful connection. Replicas synchronize every five minutes. Devices will fail to connect for the first five minutes after enrollment, which is usually two connection attempts. Then devices will connect successfully.

## Add roles

If you're adding on-premises MDM to a site that has most devices managed with the Configuration Manager client, you might already have some of these roles installed in the site. For example, the distribution point is a common role, and the device management point is required to manage macOS devices.

For more information on how to add roles to your site, see [Add site system roles](../../core/servers/deploy/configure/install-site-system-roles.md).

## Configure roles

Configure new or existing roles to manage mobile devices. Follow the steps below to configure the distribution point and device management point to function correctly for on-premises MDM:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node.

1. Select the site system server with the distribution point or device management point that you want to configure. Select the server in the list, then select the **Site system** role in the Site System Roles details pane. In the ribbon, on the **Site Role** tab, select **Properties**.

    > [!TIP]
    > In a large site, you can scope the view to only show servers with specific roles. When you select the **Servers and Site System Roles** node, in the ribbon, on the Home tag, select **Servers with Role**. Then select the role you want from the list of roles currently available in the site.

    On the **General** tab of the **Site system properties**, make sure the **Name** is a fully qualified domain name (FQDN). Close the properties.

1. In the console list, select a server with an on-premises distribution point role. Select the **Distribution point** role in the Site System Roles details pane. In the ribbon, on the **Site Role** tab, select **Properties**. On the **Communication** tab of the **Distribution point Properties**:

    1. Select **HTTPS**, and select **Allow intranet-only connections**.

        > [!IMPORTANT]
        > If you're also managing macOS computers with the Configuration Manager client, use **Allow intranet and internet connections** instead.

    1. Enable the option to **Allow mobile devices to connect to this distribution point**, then close the properties.

1. Open properties for the **Management point** site system role.

    1. On the **General** tab, select **HTTPS**, and select **Allow intranet-only connections**.

        > [!IMPORTANT]
        > If you're also managing macOS computers with the Configuration Manager client, use **Allow intranet and internet connections** instead.

    1. Enable the option to **Allow mobile devices and Mac Computer to use this management point**, then close the properties.

        > [!NOTE]
        > This option effectively turns the management point into a *device* management point.  

## Next step

After you add and configure the roles for managing mobile devices, configure the servers as trusted endpoints. This trust enables the roles to communicate with and enroll managed devices.

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
