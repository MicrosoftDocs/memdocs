---
title: "Software inventory security privacy"
description: "Get security and privacy information for software inventory in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe

---
# Security and privacy for software inventory in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic contains security and privacy information for software inventory in System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Security best practices for software inventory  
 Use the following security best practices for when you collect software inventory data from clients:  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Sign and encrypt inventory data|When clients communicate with management points by using HTTPS, all data that they send is encrypted by using SSL. However, when client computers use HTTP to communicate with management points on the intranet, client inventory data and collected files can be sent unsigned and unencrypted. Make sure that the site is configured to require signing and use encryption. In addition, if clients can support the SHA-256 algorithm, select the option to require SHA-256.|  
|Do not use file collection to collect critical files or sensitive information|Configuration Manager software inventory uses all the rights of the LocalSystem account, which has the ability to collect copies of critical system files, such as the registry or security account database. When these files are available at the site server, someone with the Read Resource rights or NTFS rights to the stored file location could analyze their contents and possibly discern important details about the client in order to be able to compromise its security.|  
|Restrict local administrative rights on client computers|A user with local administrative rights can send invalid data as inventory information.|  

### Security issues for software inventory  
 Collecting inventory exposes potential vulnerabilities. Attackers can perform the following:  

-   Send invalid data, which will be accepted by the management point even when the software inventory client setting is disabled and file collection is not enabled.  

-   Send excessively large amounts of data in a single file and in lots of files, which might cause a denial of service.  

-   Access inventory information as it is transferred to Configuration Manager.  

 If users know that they can create a hidden file named **Skpswi.dat** and place it in the root of a client hard drive to exclude it from software inventory, you will not be able to collect software inventory data from that computer.  

 Because a user with local administrative privileges can send any information as inventory data, do not consider inventory data that is collected by Configuration Manager to be authoritative.  

 Software inventory is enabled by default as a client setting.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Privacy information for software inventory  
 Hardware inventory allows you to retrieve any information that is stored in the registry and in WMI on Configuration Manager clients. Software inventory allows you to discover all files of a specified type or to collect any specified files from clients. Asset Intelligence enhances the inventory capabilities by extending hardware and software inventory and adding new license management functionality.  

 Hardware inventory is enabled by default as a client setting and the WMI information collected is determined by options that you select. Software inventory is enabled by default but files are not collected by default. Asset Intelligence data collection is automatically enabled, although you can select the hardware inventory reporting classes to enable.  

 Inventory information is not sent to Microsoft. Inventory information is stored in the Configuration Manager database. When clients use HTTPS to connect to management points, the inventory data that they send to the site is encrypted during the transfer. If clients use HTTP to connect to management points, you have the option to enable inventory encryption. The inventory data is not stored in encrypted format in the database. Information is retained in the database until it is deleted by the site maintenance tasks **Delete Aged Inventory History** or **Delete Aged Collected Files** every 90 days. You can configure the deletion interval.  

 Before you configure hardware inventory, software inventory, file collection, or Asset Intelligence data collection, consider your privacy requirements.  
