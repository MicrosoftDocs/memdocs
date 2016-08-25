---
title: "How to manage clients for Linux and UNIX servers in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: Mtillman
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to manage clients for Linux and UNIX servers in System Center Configuration Manager
When you manage Linux and UNIX servers with System Center Configuration Manager, you can configure collections, maintenance windows, and client settings to help manage the servers. In addition, although the Configuration Manager client for Linux and UNIX does not have a user interface, you can force the client to manually poll for client policy. The following sections provide more information about these configurations.  
  
-   [Collections of Linux and UNIX servers](#BKMK_CollectionsforLnU)  
  
-   [Maintenance windows for Linux and UNIX servers](#BKMK_MaintenanceWindowsforLnU)  
  
-   [Client settings for Linux and UNIX servers](#BKMK_ClientSettingsforLnU)  
  
-   [Computer policy for Linux and UNIX servers](#BKMK_PolicyforLnU)  
  
-   [How to manage certificates on the client for Linux and UNIX](#BKMK_ManageLinuxCerts)  
  
##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 You use collections to manage groups of Linux and UNIX servers in the same way you use collections to manage other client types. Collections can be direct membership collections or query based collections that identify client operating systems, hardware configurations, or other details about the client that are stored in the site database. For example, you can use collections that include Linux and UNIX servers to manage the following:  
  
-   Client settings  
  
-   Software deployments  
  
-   Enforce maintenance windows  
  
 Before you can identify a Linux or UNIX client by its operating system or distribution, you must successfully collect hardware inventory from the client. For information about collecting hardware inventory, see [Hardware inventory for Linux and UNIX in System Center Configuration Manager](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  
  
 The default client settings for hardware inventory include information about a client computer’s operating system. You can use the **Caption** property of the **Operating System** class to identify the operating system of a Linux or UNIX server.  
  
 You can view details about computers that run the Configuration Manager client for Linux and UNIX in the Devices node of the Assets and Compliance workspace in the Configuration Manager console. In the Asset and Compliance workspace of the Configuration Manager console, you can view the name of each computer’s operating system in the **Operating System** column.  
  
 By default, Linux and UNIX servers are members of the **All Systems** collection. It is recommended that you build custom collections that include only Linux and UNIX servers, or a subset of them. This enables you to manage operations such as deploying software or assigning client settings to groups of applicable computers. For example, if you deploy software for RHEL6 x64 computers to a collection that contains both Windows and Linux computers, the status for the deployment will show partial success. Instead, when you deploy software to a collection that contains only RHEL6 x64 computers, you can use status messages and reports to accurately identify the success of the deployment.  
  
 When you build a custom collection for Linux and UNIX servers, include membership rule queries that include the Caption attribute for the Operating System attribute. For information about creating collections, see [How to create collections in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  
  
##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 The Configuration Manager client for Linux and UNIX servers supports the use of maintenance windows. This support is unchanged from that for Windows-based clients.  
  
 For more information about how to use maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  
  
##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 You can configure client settings that apply to Linux and UNIX servers the same way you configure settings for other clients.  
  
 By default, the **Default Client Agent Settings** apply to Linux and UNIX servers. You can also create custom client settings and deploy them to collections that contain specific client operating systems, or a mix of client operating systems.  
  
 There are no additional client settings that apply only to Linux and UNIX clients. However, there are default client settings that do not apply to Linux and UNIX clients. The client for Linux and UNIX only applies settings for functionality that it supports, and any configurations for unsupported functionality are ignored.  
  
 For example, you create custom client device setting that specify a hardware inventory schedule and then assign it to a collection that includes Linux computers. The result is that the hardware inventory schedule is enforced on the Linux and UNIX servers. Next, you create a custom client device setting that enables and configures remote control settings, and assign it to that same collection. The result is that the remote control settings are ignored by the Linux and UNIX servers. This is because the client for Linux and UNIX does not support remote control in Configuration Manager.  
  
 For information about configuring client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  
  
##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 The Configuration Manager client for Linux and UNIX servers periodically polls its site for computer policy to learn about requested configurations, and to check for deployments.  
  
 You can also force the client on a Linux or UNIX server to immediately poll for computer policy. To poll immediately, use **root** credentials on the server to run the following command: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  
  
 Details about the computer policy poll are entered into the shared client log file, **scxcm.log**.  
  
> [!NOTE]  
>  The Configuration Manager client for Linux and UNIX never requests nor processes user policy.  
  
##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 After you install the client for Linux and UNIX, you can use the **certutil** tool to update the client with a new PKI certificate, and to import a new Certificate Revocation list (CRL). When you install the client for Linux and UNIX, this tool is placed in the following location: **/opt/microsoft/configmgr/bin/certutil**  
  
 To manage certificates, on each client run certutil with one of the following options:  
  
|Option|More information|  
|------------|----------------------|  
|importPFX|Use this option to specify a certificate to replace the certificate that is currently used by a client.<br /><br /> When you use **-importPFX**, you must also use the **–password** command line parameter to  supply the password associated with the PKCS#12 file.<br /><br /> Use **-rootcerts** to specify any additional root certificate requirements.<br /><br /> Example:  **certutil -importPFX <Path to the PKCS#12 certificate> -password <Certificate password\> [-rootcerts <comma-separated list of certificates>]**|  
|-importsitecert|Use this option to update the site server signing certificate that is on the management server.<br /><br /> Example: **certutil -importsitecert <Path to the DER certificate\>**|  
|-importcrl|Use this option to update the CRL on the client with one or more CRL file paths.<br /><br /> Example: **certutil -importcrl <comma separated CRL file paths\>**|  
  
## See Also  
 [Monitor and manage clients in System Center Configuration Manager](../../../core/clients/manage/monitor-and-manage-clients.md)