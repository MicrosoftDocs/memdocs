---
title: "Configure clients find management points DNS publishing"
description: "Set client computers to find management points by using DNS publishing in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: 6
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to configure client computers to find management points by using DNS publishing in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Clients in System Center Configuration Manager must locate a management point to complete site assignment and as an on-going process to remain managed. Active Directory Domain Services provides the most secure method for clients on the intranet to find management points. However, if clients cannot use this service location method (for example, you have not extended the Active Directory schema, or clients are from a workgroup), use DNS publishing as the preferred alternative service location method.  

> [!NOTE]  
>  When you install the client for Linux and UNIX, you must specify a management point to use as an initial point of contact. For information about how to install the client for Linux and UNIX, see  [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Before you use DNS publishing for management points, make sure that DNS servers on the intranet have service location resource records (SRV RR) and corresponding host (A or AAA) resource records for the site's management points. The service location resource records can be created automatically by Configuration Manager or manually, by the DNS administrator who creates the records in DNS.  

 For more information about DNS publishing as a service location method for Configuration Manager clients, see [Understand how clients find site resources and services for System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 By default, clients search DNS for management points in their DNS domain. However, if there are no management points published in the clients' domain, you must manually configure clients with a management point DNS suffix. You can configure this DNS suffix on clients either during or after client installation:  

-   To configure clients for a management point suffix during client installation, configure the CCMSetup Client.msi properties.  

-   To configure clients for a management point suffix after client installation, in Control Panel, configure the **Configuration Manager Properties**.  

#### To configure clients for a management point suffix during client installation  

-   Install the client with the following CCMSetup Client.msi property:  

    -   **DNSSUFFIX=** *&lt;management point domain\>*  

         If the site has more than one management point and they are in more than one domain, specify just one domain. When clients connect to a management point in this domain, they download a list of available management points, which will include the management points from the other domains.  

     For more information about the CCMSetup command-line properties, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### To configure clients for a management point suffix after client installation  

1.  In Control Panel of the client computer, navigate to **Configuration Manager**, and then double-click **Properties**.  

2.  On the **Site** tab, specify the DNS suffix of a management point, and then click **OK**.  

     If the site has more than one management point and they are in more than one domain, specify just one domain. When clients connect to a management point in this domain, they download a list of available management points, which will include the management points from the other domains.
