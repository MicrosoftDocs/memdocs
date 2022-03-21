---
title: Hardware inventory security privacy
titleSuffix: Configuration Manager
description: Get security and privacy information for hardware inventory in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Security and privacy for hardware inventory in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This topic contains security and privacy information for hardware inventory in Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Security best practices for hardware inventory  
 Use the following security best practices for when you collect hardware inventory data from clients:  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Sign and encrypt inventory data|When clients communicate with management points by using HTTPS, all data that they send is encrypted by using SSL. However, when client computers use HTTP to communicate with management points on the intranet, client inventory data and collected files can be sent unsigned and unencrypted. Make sure that the site is configured to require signing and use encryption. In addition, if clients can support the SHA-256 algorithm, select the option to require SHA-256.|  
|Do not collect IDMIF and NOIDMIF files in high-security environments|You can use IDMIF and NOIDMIF file collection to extend hardware inventory collection. When necessary, Configuration Manager creates new tables or modifies existing tables in the Configuration Manager database to accommodate the properties in IDMIF and NOIDMIF files. However, Configuration Manager does not validate IDMIF and NOIDMIF files, so these files could be used to alter tables that you do not want altered. Valid data could be overwritten by invalid data. In addition, large amounts of data could be added and the processing of this data might cause delays in all Configuration Manager functions. To mitigate these risks, configure the hardware inventory client setting **Collect MIF files** as **None**.|  

### Security issues for hardware inventory  
 Collecting inventory exposes potential vulnerabilities. Attackers can perform the following:  

- Send invalid data, which will be accepted by the management point even when the software inventory client setting is disabled and file collection is not enabled.  

- Send excessively large amounts of data in a single file and in lots of files, which might cause a denial of service.  

- Access inventory information as it is transferred to Configuration Manager.  

  Because a user with local administrative privileges can send any information as inventory data, do not consider inventory data that is collected by Configuration Manager to be authoritative.  

  Hardware inventory is enabled by default as a client setting.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Privacy information for hardware inventory  
 Hardware inventory allows you to retrieve any information that is stored in the registry and in WMI on Configuration Manager clients. Software inventory allows you to discover all files of a specified type or to collect any specified files from clients. Asset Intelligence enhances the inventory capabilities by extending hardware and software inventory and adding new license management functionality.  

 Hardware inventory is enabled by default as a client setting and the WMI information collected is determined by options that you select. Software inventory is enabled by default but files are not collected by default. Asset Intelligence data collection is automatically enabled, although you can select the hardware inventory reporting classes to enable.  

 Inventory information is not sent to Microsoft. Inventory information is stored in the Configuration Manager database. When clients use HTTPS to connect to management points, the inventory data that they send to the site is encrypted during the transfer. If clients use HTTP to connect to management points, you have the option to enable inventory encryption. The inventory data is not stored in encrypted format in the database. Information is retained in the database until it is deleted by the site maintenance tasks **Delete Aged Inventory History** or **Delete Aged Collected Files** every 90 days. You can configure the deletion interval.  

 Before you configure hardware inventory, software inventory, file collection, or Asset Intelligence data collection, consider your privacy requirements.  
