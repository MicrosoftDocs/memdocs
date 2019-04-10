---
title: Discovery Views in Configuration Manager
TOCTitle: Discovery Views in Configuration Manager
ms:assetid: 06c46d1e-02f3-4cef-9346-02764a27daea
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn581928(v=TechNet.10)
ms:contentKeyID: 60771996
ms.prod: "configuration-manager"
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/30/2019
mtps_version: v=TechNet.10
---

# Discovery Views in Configuration Manager

The Configuration Manager discovery views consist of system resource objects, which include any resources that were discovered on the network. The four main discovery views are **v\_R\_System** for system resources, **v\_R\_User** for user resources, **v\_R\_UserGroup** for user group resources, and **v\_R\_UnknownSystem** for unknown systems.

Each of these discovered resources has a defined resource type, which is stored in the **v\_resourcemap** schema view.

## Discovery Schema Views

The discovery schema views provide information about all resources in a Configuration Manager site. The two discovery schema views are **v\_ResourceMap** and **v\_ResourceAttributeMap**. The **v\_ResourceMap** view contains a list of all the resource types for discovered data. By default, Configuration Manager has the Unknown System, User Group, User, and System Resource types, each of which has its own resource type number and individual view. The view can be joined to other views by using the **ResourceType** column. The following table contains the default data stored in the **v\_ResourceMap** view.

### v_R_System_Valid
Lists information about valid computers. This view is sorted by **ResourceID** and includes the client version, the processor type, the client’s domain, the NetBIOS name, the operating system and more.
This view can be joined to other views by using the **ResourceID** column.

|Resource type|Display name|Resource Class Name|
|--- |--- |--- |
|2|Unknown System|**v_R_UnknownSystem**|
|3|User Group|**v_R_UserGroup**|
|4|User|**v_R_User**|
|5|System|**v_R_System**|
|6|IP Network|**V_R_IPNetwork**|


The **v\_ResourceAttributeMap** contains all of the attributes that will be discovered for each of the resource types, such as NetBIOS name, operating system, user name, user group name, domain name, and so forth. The **v\_ResourceAttributeMap** view can be joined to other views by using the **ResourceType** column. The discovery schema views are also listed and described in the [Schema Views in Configuration Manager](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/dn581997(v%3dtechnet.10)) topic.

## Configuration Manager Discovery Views

The **v\_R\_System** view can be joined with any other view that contains system data (system discovery array views, inventory views, collection views, status views, and so forth) by using the **ResourceID** column. The **v\_R\_System** view will be one of the most often used when joining views. The **v\_R\_UnknownSystem**, **v\_R\_User**, and **v\_R\_UserGroup** views also use the **ResourceID** column to join with views that contain data for their resource type. Most of the remaining discovery views contain data where there can be more than one value for a resource, such as IP address or user organizational unit (OU) name. The discovery views are described in the following table.

### v_AgentDiscoveries

Lists all resources that have been discovered in the Configuration Manager hierarchy and by what discovery agent. The view contains data about the resource type, resource ID, agent that discovered the resource, site code where the agent resides, and time of the discovery.
The view can be joined to other views by using the **ResourceID** column.

### v_ClientMachines

Lists all discovered system resources, by resource ID, that are not in an obsolete or decommissioned state and whether the system resource is a Configuration Manager client.
The view can be joined to other views by using the **ResourceID** column.

### v_ClientMode

Lists all discovered system resources, by resource ID, that are not in an obsolete or decommissioned state and the associated client mode.
The view can be joined to other views by using the **ResourceID** column.

### v_R_System

Lists all discovered system resources by resource ID, resource type, whether the resource is a client, what type of client, client version, NetBIOS name, user name, operating system, unique identifier, and more.
The view can be joined to other views by using the **ResourceID**, **ResourceType**, **Netbios_Name0**, and **SMS_Unique_Identifier0** columns.

### v_RA_System_SMS_Resident

Lists the resident site of discovered devices.
The view can be joined to other views by using the **ResourceID** column.

### v_R_System_Valid

Lists all discovered system resources that are not in an obsolete or decommissioned state. This view is a subset of the **v_R_System** view and includes the resource ID, resource type, whether the resource is a client, what type of client, client version, NetBIOS name, user name, operating system, unique identifier, and so forth.
The view can be joined to other views by using the **ResourceID**, **ResourceType**, and **Netbios_Name0** columns.

### v_R_UnknownSystem

Lists all unknown system resources that have been discovered, including resource ID, resource type, user name, domain, and so forth.
The view can be joined to other views by using the **ResourceID**, **ResourceType**, and **SMS_Unique_Identifier0** columns.

### v_R_User

Lists all discovered user resources by resource ID, resource type, user name, domain, and so forth.
The view can be joined to other views by using the **ResourceID**, **ResourceType**, and **Unique_User_Name0** columns.

### v_R_UserGroup

Lists all disovered user group resources by ID, type, user group name, domain, and more.
The view can be joined to other views by using the **ResourceID** and **ResourceType** columns.

### v_RA_System_IPAddresses

Lists the IP addresses for discovered system resources.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_IPSubnets

Lists the IP subnets for discovered system resources.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_IPv6Addresses

Lists the IPv6 addresses for discovered system resources.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_IPv6Prefixes

Lists the IPv6 prefixes for discovered system resources.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_IPXAddresses

Lists the IPX addresses for discovered system resources.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_MACAddresses

Lists the MAC addresses for discovered system resources.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_ResourceNames

Lists all discovered system resources by resource ID and fully qualified domain name.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_SMSAssignedSites

Lists all system resources, by resource ID, that are assigned to a site, together with the site code.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_SMSInstalledSites

Lists all system resources, by resource ID that have been installed as clients and the site code they belong to.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_SystemContainerName

Lists all system resources, by resource ID, that are in an associated Active Directory container.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_SystemGroupName

Lists all system resources, by resource ID, that are in an associated Active Directory group.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_SystemOUName

Lists all system resources, by resource ID, that and their associated Active Directory OU.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_System_SystemRoles

Lists all system resources, by resource ID, that have an associated site system role (site server, management point, software update point, and so forth).
The view can be joined to other views by using the **ResourceID** column.

### v_RA_User_UserContainerName

Lists all user resources, by resource ID, that are in an associated Active Directory container.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_User_UserGroupName

Lists all user resources, by resource ID, that are in an associated Active Directory group.
The view can be joined to other views by using the **ResourceID** column.

### v_RA_User_UserOUName

Lists all user resources, by resource ID, that are in an associated OU.
The view can be joined to other views by using the **ResourceID** column.

### v_R_IPNetwork

Lists information about IP subnets discovered by Configuration Manager network discovery, sorted by **ResourceID**. This includes information about subnet addresses, masks, names and topology.
This view can be joined to other views by using the **ResourceID** column.

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)  