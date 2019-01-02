---
title: "Asset Intelligence security privacy"
titleSuffix: "Configuration Manager"
description: "Get security and privacy information for Asset Intelligence in System Center Configuration Manager."
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Security and privacy for Asset Intelligence in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic contains security and privacy information for Asset Intelligence in System Center Configuration Manager.  

##  <a name="BKMK_Security_AI"></a> Security best practices for Asset Intelligence  
 Use the following security best practices for when you use Asset Intelligence.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|When you import a license file (Microsoft Volume Licensing file or a General License Statement file), secure the file and communication channel.|Use NTFS file system permissions to ensure that only authorized users can access the license files and use Server Message Block (SMB) signing to ensure the integrity of the data when it is transferred to the site server during the import process.|  
|Use the principle of least permissions to import the license files.|Use role-based administration to grant the Manage Asset Intelligence permission to the administrative user who imports license files. The built-in role of Asset Manager includes this permission.|  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Privacy information for Asset Intelligence  
 Asset Intelligence extends the inventory capabilities of Configuration Manager to provide a higher level of asset visibility in the enterprise. Asset Intelligence information collection is not automatically enabled. You can modify the type of information collected by enabling hardware inventory reporting classes. For more information, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Asset Intelligence information is stored in the Configuration Manager database in the same manner as inventory information. When clients connect to management points by using HTTPS, the data is always encrypted during transfer to the management point. When clients connect by using HTTP, you can configure the inventory data transfer to be signed and encrypted. Inventory data is not stored in encrypted format in the database. Information is retained in the database, until the site maintenance task **Delete Aged Inventory History** deletes it in intervals of every 90 days. You can configure the deletion interval.  

 Asset Intelligence does not send information about users and computers or license usage to Microsoft. You can choose to send System Center Online requests for categorization, which means that you can tag one or more software titles that are uncategorized and send them to System Center Online for research and categorization. After a software title is uploaded, Microsoft researchers identify, categorize, and then make that knowledge available to all customers who use the on-line service. You should be aware of the following privacy implications of submitting information to System Center Online:  

- Upload applies only to generic software title information (name, publisher, and so on) that you choose to send to System Center Online. Inventory information is not sent with an upload.  

- Upload never occurs automatically, and the system is not designed for this task to be automated. You must manually select and approve the upload of each software title.  

- A dialog box shows you exactly what data is going to be uploaded, before the upload process starts.  

- License information is not sent to Microsoft. The license information is stored in a separate area of the Configuration Manager database, and it cannot be sent to Microsoft.  

- Any software title that is uploaded becomes public, in the sense that the knowledge of that given application and its categorization become part of the System Center Online Asset Intelligence catalog, and then is downloaded to other consumers of the catalog.  

- The source of the software title is not recorded in the Asset Intelligence catalog, and it is not made available to other customers. However, you must still verify that you do not load any application titles that contain any private information.  

- Uploaded data cannot be recalled.  

  Before you configure Asset Intelligence data collection and decide whether to submit information to System Center Online, consider the privacy requirements of your organization.  
