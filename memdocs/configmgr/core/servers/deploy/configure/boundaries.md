---
title: Define boundaries
titleSuffix: Configuration Manager
description: Understand how to define network locations on your intranet that can contain devices you want to manage.
ms.date: 12/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Define network locations as boundaries for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager boundaries are locations on your network that contain devices that you want to manage. You can create different types of boundaries, for example, an Active Directory site or network IP address. When the Configuration Manager client identifies a similar network location, that device is a part of the boundary.

Configuration Manager supports the following boundary types:

- IP subnet
- Active Directory site
- IPv6 prefix
- IP address range
- VPN (starting in version 2006)

You can manually create individual boundaries or use [Active Directory forest discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest). This discovery method automatically finds and creates boundaries for IP subnets and Active Directory sites. When Active Directory forest discovery identifies a supernet for an Active Directory site, Configuration Manager converts the supernet into an IP address range boundary.

If a device isn't in the boundary you expect, it may because you haven't defined its network location as a boundary. When the network location of a device is in doubt, use the following Windows commands on the device to confirm:

- IP address: `ipconfig`
- Active Directory site: `nltest /dsgetsite`
- VPN: `ipconfig /all`

## Boundary types

### IP subnet

The IP subnet boundary type requires a **Subnet ID**. For example, `169.254.0.0`. If you provide the **Network** (default gateway) and **Subnet mask** values, Configuration Manager automatically calculates the **Subnet ID**. When you save the boundary, Configuration Manager only saves the Subnet ID value.

> [!NOTE]
> Configuration Manager doesn't support the direct entry of a supernet as a boundary. Instead, use the IP address range boundary type.

### Active Directory site

For the **Active Directory site** boundary type, you specify the site name. You can type the name or browse the local forest of the site server.

When you specify an Active Directory site for a boundary, the boundary includes each IP subnet that's a member of that Active Directory site. If the configuration of the Active Directory site changes in Active Directory, the network locations included in this boundary also change.  

Active Directory site boundaries don't work for pure Microsoft Entra devices, also called cloud domain-joined devices. If they roam on-premises, and you only create Active Directory site type boundaries, these devices won't be in a boundary.

> [!TIP]
> Use the following Windows command to see a device's current Active Directory site: `nltest /dsgetsite`.
>
> To determine if a client is cloud domain-joined, use the following Windows command: `dsregcmd /status`. For more information, see [dsregcmd command - device state](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### IPv6 prefix

For the **IPv6 prefix** boundary type, you specify a **Prefix**. For example, `2001:1111:2222:3333`.

### IP address range

For the **IP address range** boundary type, specify the **Starting IP address** and **Ending IP address** for the range. The range can include part of an IP subnet or multiple IP subnets. Use an IP address range boundary type to support a supernet.

You can also use this type to define a boundary for a single IP address. Set both the starting and ending IP addresses as the same value. This configuration may be useful for unique devices or test environments.

### VPN

<!--7020519-->

Starting in version 2006, to simplify managing remote clients, create a boundary type for VPNs. When a client sends a location request, it includes additional information about its network configuration. Based upon this information, the server determines whether the client is on a VPN. For Configuration Manager to associate the client in the boundary, connect the device to the VPN.

You can configure a VPN boundary in several ways:

- **Auto detect VPN**: Configuration Manager detects any VPN solution that uses the point-to-point tunneling protocol (PPTP). If it doesn't detect your VPN, use one of the other options. The boundary value in the console list will be `Auto:On`.

- **Connection name**: Specify the name of the VPN connection on the device. It's the name of the network adapter in Windows for the VPN connection. Configuration Manager matches the first 250 characters of the string, but doesn't support wildcard characters or partial strings. The boundary value in the console list will be `Name:<name>`, where `<name>` is the connection name that you specify.

  For example, you run the `ipconfig` command on the device, and one of the sections starts with: `PPP adapter ContosoVPN:`. Use the string `ContosoVPN` as the **Connection name**. It displays in the list as `Name:CONTOSOVPN`.

- **Connection description**: Specify the description of the VPN connection. Configuration Manager matches the first 243 characters of the string, but doesn't support wildcard characters or partial strings. The boundary value in the console list will be `Description:<description>`, where `<description>` is the connection description that you specify.

  For example, you run the `ipconfig /all` command on the device, and one of the connections includes the following line: `Description . . . . . . . . . . . : ContosoMainVPN`. Use the string `ContosoMainVPN` as the **Connection description**. It displays in the list as `Description:CONTOSOMAINVPN`.

> [!IMPORTANT]
> To take full advantage of this feature, after you update the site, also update clients to the latest version. New functionality appears in the Configuration Manager console when you update the site and console. The complete scenario isn't functional until the client version is also the latest.
>
> To use this VPN boundary during an OS deployment, make sure to also update the boot image to include the latest client binaries.

Starting in version 2111, you can now match the start of a connection name or description instead of the whole string. Some third-party VPN drivers dynamically create the connection, which starts with a consistent string but also has a unique connection identifier. For example, `Virtual network adapter #19`. When you use the **Connection name** or **Connection description** options, also use the new **Starts with** option.<!--7822886-->

## Create a boundary

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Boundaries** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Boundary**.

1. On the **General** tab of the **Create Boundary** window, specify the following information:

    - **Description**: Identify the boundary by a friendly name or reference.

        > [!NOTE]
        > Configuration Manager automatically names the boundary based on its type and scope. You can't modify the name.

    - **Type**: Select the type of boundary to create. Then specify the additional information that the type requires. For more information, see [Boundary types](#boundary-types).

1. Switch to the **Boundary Groups** tab. If you already have boundary groups in the site, you can immediately add this new boundary to one or more groups.

1. Select **OK** to save the new boundary.

## Configure a boundary

> [!TIP]
> When you create a boundary, Configuration Manager automatically names it based on the type and scope of the boundary. You can't modify this name. To help identify the boundary in the Configuration Manager console, specify a description.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Boundaries** node.

1. Select the boundary you want to modify. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. In the **Properties** window for the boundary, on the **General** tab, you can configure the following settings:

    - Edit the **Description**
    - Change the **Type** for the boundary
    - Change the scope of a boundary by editing its network locations. For example, for an Active Directory site boundary you can specify a new Active Directory site name.

1. To view the site systems that are associated with this boundary, switch to the **Site Systems** tab. You can't change this configuration from the properties of a boundary.

    > [!TIP]
    > For a server to be listed as a site system for a boundary, associate it as a site system server for at least one boundary group that includes this boundary. Make this configuration on the **References** tab of a boundary group. For more information, see [Configure site assignment and select site system servers](boundary-group-procedures.md#configure-site-assignment-and-select-site-system-servers).

1. To modify the boundary group membership for this boundary, select the **Boundary Groups** tab:

    - To add this boundary to one or more boundary groups, select **Add**. Select one or more boundary groups, and then select **OK**.

    - To remove this boundary from a boundary group, choose the boundary group, and then select **Remove**.

1. Select **OK** to close the boundary properties and save the configuration.

## Next steps

Each boundary is available for use by every site in your hierarchy. After you create a boundary, add the boundary to one or more [boundary groups](boundary-groups.md).
