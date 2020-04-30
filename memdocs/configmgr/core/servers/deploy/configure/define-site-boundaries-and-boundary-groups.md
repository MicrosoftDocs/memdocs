---
title: Use boundaries and boundary groups
titleSuffix: Configuration Manager
description: Use boundaries and boundary groups to define network locations and accessible site systems for devices you manage.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby


---

# Define site boundaries and boundary groups

*Applies to: Configuration Manager (current branch)*

*Boundaries* in Configuration Manager define network locations on your intranet. These locations include devices that you want to manage. *Boundary groups* are logical groups of boundaries that you configure.

A hierarchy can include any number of boundary groups. Each boundary group can contain any combination of the following boundary types:  

- IP subnet  
- Active Directory site name  
- IPv6 prefix  
- IP address range  

Clients on the intranet evaluate their current network location and then use that information to identify boundary groups to which they belong.  

Clients use boundary groups to:  

- **Find an assigned site:** Boundary groups enable clients to find a primary site for client assignment. This behavior is also known as *automatic site assignment*.  

- **Find certain site system roles they can use:** Associate a boundary group with certain site system roles. Then the site provides clients with that list of site systems in the boundary group. Clients use these site systems for actions such as finding content or a nearby management point.  

Clients that are on the internet or configured as internet-only clients don't use boundary information. These clients can't use automatic site assignment. They can download content from an internet-based distribution point from their assigned site or a cloud-based distribution point.  

Starting in version 1902, you can associate a cloud management gateway (CMG) with a boundary group. For more information, see [CMG hierarchy design](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="BKMK_BoundaryBestPractices"></a> Recommendations

### Use a mix of the fewest boundaries that meet your needs

Use whichever boundary type or types you choose that work for your environment. To simplify your management tasks, use boundary types that let you use the fewest number of boundaries you can.

### Avoid overlapping boundaries for automatic site assignment

Although each boundary group supports both site assignment and site system reference, create a separate set of boundary groups to use only for site assignment. Make sure that each boundary in a boundary group isn't a member of another boundary group with a different site assignment.

- A single boundary can be included in multiple boundary groups  

- Each boundary group can be associated with a different primary site for site assignment  

- For a boundary that's a member of two different boundary groups with different site assignments, clients randomly select a site to join. This behavior might not be for the site you want the client to join. This configuration is called *overlapping boundaries*.  

    Overlapping boundaries isn't a problem for content location. It can be a useful configuration that provides clients additional resources or content locations they can use.  


## Next steps

- [Define network locations as boundaries](boundaries.md)

- [Configure boundary groups](boundary-groups.md)
