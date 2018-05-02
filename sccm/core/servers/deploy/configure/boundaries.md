---
title: "Define boundaries"
titleSuffix: "Configuration Manager"
description: "Understand how to define network locations on your intranet that can contain devices you want to manage."
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Define network locations as boundaries for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager boundaries are locations on your network that contain devices that you want to manage. The boundary a device is on is equivalent to the Active Directory site, or network IP address that is identified by the Configuratoin Manager client that is installed on the device.
 - You can manually create individual boundaries. However, Configuration Manager does not support the direct entry of a supernet as a boundary. Instead, use the IP address range boundary type.
 - You can configure the [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) method to auto-discover and create boundaries for each IP Subnet and Active Directory Site it discovers. When Active Directory Forest Discovery identifies a supernet that is assigned to an Active Directory site, Configuration Manager converts the supernet into an IP address range boundary.  

It is not uncommon for a device to use an IP address that the Configuration Manager administrator is not aware of. When the network location of a device is in doubt, confirm what the device reports as its location by using the **IPCONFIG** command on the device.  

When you create a boundary, it automatically receives a name that is based upon the type and scope of the boundary. You cannot modify this name. Instead, you can specify a description to help identify the boundary in the Configuration Manager console.  

Each boundary is available for use by every site in your hierarchy. After a boundary has been created, you can modify its properties to do the following:  
-   Add the boundary to one or more boundary groups.  
-   Change the type or scope of the boundary.  
-   View the boundaries **Site Systems** tab to see which site system servers (distribution points, state migration points, and management  points) are associated with the boundary.  

## To create a boundary  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** > **Boundaries**  

2.  On the **Home** tab, in the **Create** group, click **Create Boundary.**  

3.  On the **General** tab of the Create Boundary dialog box you can specific a **Description** to identify the boundary by a friendly name or reference.  

4.  Select a **Type** for this boundary:  

    -   If you select **IP Subnet**, you must specify a **Subnet ID** for this boundary.  
        > [!TIP]  
        >  You can specify the **Network** and **Subnet mask** to have the **Subnet ID** automatically specified. When you save the boundary, only the Subnet ID value is saved.  

    -   If you select **Active Directory site**, you must specify or **Browse** to an Active Directory site in the local forest of the site server.  

        > [!IMPORTANT]  
        >  When you specify an Active Directory site for a boundary, the boundary includes each IP Subnet that is a member of that Active Directory site. If the configuration of the Active Directory site changes in Active Directory, the network locations included in this boundary also change.  

    -   If you select **IPv6 prefix**, you must specify a **Prefix** in the IPv6 prefix format.  

    -   If you select **IP address range**, you must specify a **Starting IP address** and **Ending IP address** that includes part of an IP Subnet or includes multiple IP Subnets.    

5.  Click **OK** to save the new boundary.  

## To configure a boundary  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** > **Boundaries**  

2.  Select the boundary you want to modify.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the **Properties** dialog box for the boundary, select the **General** tab to edit the **Description** or **Type** for the boundary. You can also change the scope of a boundary by editing the network locations for the boundary. For example, for an Active Directory site boundary you can specify a new Active Directory site name.  

5.  Select the **Site Systems** tab to view the site systems that are associated with this boundary. You cannot change this configuration from the properties of a boundary.  

    > [!TIP]  
    >  For a site system server to be listed as a site system for a boundary, the site system server must be associated as a site system server for at least one boundary group that includes this boundary. This is configured on the **References** tab of a boundary group.  

6.  Select the **Boundary Groups** tab to modify the boundary group membership for this boundary:  

    -   To add this boundary to one or more boundary groups, click **Add**, select the check box for one or more boundary groups, and then click **OK**.  

    -   To remove this boundary from a boundary group, select the boundary group and click **Remove**.  

7.  Click **OK** to close the boundary properties and save the configuration.  
