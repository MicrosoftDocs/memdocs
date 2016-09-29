---
title: "Plan the site database | System Center Configuration Manager"
description: "Consider the site database and the site database server role as you plan your System Center Configuration Manager hierarchy."
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brendunsmanager: angrobe

---
# Plan for the site database for System Center Configuration Manager
The site database server is a computer that runs a supported version of Microsoft SQL Server that stores information for Configuration Manager sites. Each site in a Configuration Manager hierarchy contains a site database and a server that is assigned the site database server role.  

-   For central administration sites and primary sites, you can install SQL Server on the site server, or you can install SQL Server on a computer other than the site server  

-   For secondary sites, you can use SQL Server Express instead of a full SQL Server installation; however, the database server must be run on the secondary site server  

If you use a remote database server computer, ensure the intervening network connection is a high-availability, high-bandwidth network connection. This is because the site server and some site system roles must constantly communicate with the SQL Server that is hosting the site database.  


**Consider the following when you select a remote database server location:**  

-   The amount of bandwidth required for communications to the database server depends upon a combination of many different site and client configurations; therefore, the actual bandwidth required cannot be adequately predicted.  

-   Each computer that runs the SMS Provider and that connects to the site database increases network bandwidth requirements.  

-   The computer that runs SQL Server must be located in a domain that has a two-way trust with the site server and all computers running the SMS Provider.  

-   You cannot use a clustered SQL Server for the site database server when the site database is co-located with the site server.  


Typically, a site system server supports site system roles from only a single Configuration Manager site; however, you can use different instances of SQL Server, on clustered or non-clustered servers running SQL Server, to host a database from different Configuration Manager sites. To support databases from different sites, you must configure each instance of SQL Server to use unique ports for communication.  


**The following SQL Server configurations can be used to host the site database:**  

-   The default instance of SQL Server  

-   A named instance on a single computer running SQL Server  

-   A named instance on a clustered instance of SQL Server  

-   A SQL Server AlwaysOn availability group (beginning with version 1602)


**Prerequisites for the Site Database:**  

-   To host the site database, the SQL Server must meet the requirements detailed in [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  
>>>>>>> ce49567f396c5575aa275603a69aa350aaa73be0
