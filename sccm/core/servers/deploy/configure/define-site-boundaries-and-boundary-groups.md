---
title: "Use Boundaries and boundary groups"
titleSuffix: "Configuration Manager"
description: "Use boundaries and boundary groups to define network locations and accessible site systems for devices you manage."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Define site boundaries and boundary groups for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Boundaries for System Center Configuration Manager define network locations on your intranet that can contain devices that you want to manage. Boundary groups are logical groups of boundaries that you configure.

 A  hierarchy can include any number of boundary groups, and each boundary group can contain any combination of the following boundary types:  

-   IP subnet,  
-   Active Directory site name  
-   IPv6 Prefix  
-   IP address range  

Clients on the intranet evaluate their current network location and then use that information to identify boundary groups to which they belong.  

 Clients use boundary groups to:  
-   **Find an assigned site:** Boundary groups enable clients to find a primary site for client assignment (automatic site assignment).  
-   **Find certain site system roles they can use:** When you associate a boundary group with certain site system roles, the boundary group provides clients that list of site systems for use during content location and as  preferred management points.  

Clients that are on the Internet or configured as Internet-only clients do not use boundary information. These clients cannot use automatic site assignment and can always download content from any distribution point from their assigned site when the distribution point is configured to allow client connections from the Internet.  

**To get started:**
- First, [define network locations as boundaries](/sccm/core/servers/deploy/configure/boundaries).
- Then continue by [configuring boundary groups](/sccm/core/servers/deploy/configure/boundary-groups) to associate clients in those boundaries to the site system servers they can use.



##  <a name="BKMK_BoundaryBestPractices"></a> Best practices for boundaries and boundary groups  

-   **Use a mix of the fewest boundaries that meet your needs:**  
   In the past, we recommended the use of some boundary types over others. With changes to improve performance, we now recommend you use whichever boundary type or types you choose that work for your environment, and that let you use the fewest number of boundaries you can to simplify your management tasks.      

-   **Avoid overlapping boundaries for automatic site assignment:**  
     Although each boundary group supports both site assignment configurations and those for content location, it is a best practice to create a separate set of  boundary groups to use only for site assignment. Meaning: ensure that each boundary in a boundary group is not a member of another boundary group with a different site assignment. This is because:  

    -   A single  boundary can be included in multiple boundary groups  

    -   Each boundary group can be associated with a different primary site for site assignment  

    -   A client on a boundary that is a member of two different boundary groups with different site assignments will randomly select a site to join, which might not be the site you intend the client to join.  This configuration is called overlapping boundaries.  

     Overlapping boundaries is not a problem for content location, and instead is often a desired  configuration that provides clients additional resources or content locations they can use.  
