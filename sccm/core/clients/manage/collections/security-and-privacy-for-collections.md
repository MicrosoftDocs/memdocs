---
title: "Collections security and privacy"
titleSuffix: "Configuration Manager"
description: "Get best practices for security and privacy in collections in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7 
ms.author: andredm 
manager: angrobe

---
# Security and privacy for collections in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic contains security best practices and privacy information for collections in System Center Configuration Manager.  

 There is no privacy information specifically for collections in Configuration Manager. Collections are containers for resources, such as users and devices. Collection membership often depends on the information that Configuration Manager collects during standard operation. For example, by using resource information that has been collected from discovery or inventory, a collection can be configured to contain the devices that meet specified criteria. Collections might also be based on the current status information for client management operations, such as deploying software and checking for compliance. In addition to these query-based collections, administrative users can also add resources to collections.  

 For more information about collections, see [Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md). For more information about any security best practices and privacy information for Configuration Manager operations that can be used to configure collection membership, see [Security best practices and privacy information for System Center Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## Security Best Practices for Collections  
 Use the following security best practice for collections.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|When you export or import a collection by using a Managed Object Format (MOF) file that is saved to a network location, secure the location, and secure the network channel.|Restricts who can access the network folder.<br /><br /> Use Server Message Block (SMB) signing or Internet Protocol security (IPsec) between the network location and the site server to prevent an attacker from tampering with the exported collection data. Use IPsec to encrypt the data on the network to prevent information disclosure.|  

### Security Issues for Collections  
 Collections have the following security issues:  

-   If you use collection variables, local administrators can read potentially sensitive information.  

     Collection variables can be used when you deploy an operating system.  
