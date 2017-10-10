---
title: "Hardware inventory | Linux UNIX "
description: "Learn how use hardware inventory for Linux and UNIX in System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
caps.latest.revision: 6
author: andredm7ms.author: andredmmanager: angrobe

---
# Hardware inventory for Linux and UNIX in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
The System Center Configuration Manager client for Linux and UNIX supports hardware inventory. After you collect hardware inventory you can run view inventory in the resource explorer or Configuration Manager reports, and use this information to create queries and collections that enable the following operations:  

-   Software deployment  

-   Enforce maintenance windows  

-   Deploy custom client settings  

 Hardware inventory for Linux and UNIX servers uses a standards based Common Information Model (CIM) server. The CIM server runs as a software service (or daemon) and provides a management infrastructure that is based on Distributed Management Task Force (DMTF) standards. The CIM server provides functionality that is similar to the Windows Management Infrastructure (WMI) CIM capabilities that are available on Windows-based computers.  

 Beginning with cumulative update 1, the client for Linux and UNIX uses the open source **omiserver** version 1.0.6 from the **Open Group**. (Prior to cumulative update 1, the client used **nanowbem** as its CIM server).  

 The CIM server installs as part of the client for Linux and UNIX. The client for Linux and UNIX communicates directly with the CIM server and does not use the WS-MAN interface of the CIM server. The WS-MAN port on the CIM server is disabled when the client installs. Microsoft developed the CIM server that is now available as open source through the Open Management Infrastructure (OMI) project. For more information about the Open Management Infrastructure project, see [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) website.  

 Hardware Inventory on Linux and UNIX servers operates by mapping existing Win32 WMI classes and properties to equivalent classes and properties for Linux and UNIX servers. This one-to-one mapping of classes and properties enables the Linux and UNIX hardware inventory to integrate with Configuration Manager. Inventory data from Linux and UNIX servers displays along with inventory from Windows-based computers in the Configuration Manager console and reports. This provides a consistent heterogeneous management experience.  

> [!TIP]  
>  You can use the **Caption** value for the **Operating System** class to identify different Linux and UNIX operating systems in queries and collections.  

##  <a name="BKMK_ConfigHardwareforLnU"></a> Configuring hardware inventory for Linux and UNIX servers  
 You can use the default client settings or create custom client device settings to configure hardware inventory. When you use custom client device settings you can configure the classes and properties you want to collect from only your Linux and UNIX servers. You can also specify custom schedules for when to collect full and delta inventories from your Linux and UNIX servers.  

 The client for Linux and UNIX supports the following hardware inventory classes that are available on Linux and UNIX servers:  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 Not all properties for these inventory classes are enabled for Linux and UNIX computers in Configuration Manager.  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> Operations for hardware inventory  
 After you collect hardware inventory from your Linux and UNIX servers, you can view and use this information the same way you view inventory you collect from other computers:  

-   Use Resource Explorer to view detailed information about the hardware inventory from Linux and UNIX servers  

-   Create queries based on specific hardware configurations  

-   Create query-based collections that are based on specific hardware configurations  

-   Run reports that display specific details about hardware configurations  

 Hardware inventory on a Linux or UNIX server runs according to the schedule you configure in client settings. By default, this is every seven days. The client for Linux and UNIX supports both full inventory cycles and delta inventory cycles.  

 You can also force the client on a Linux or UNIX server to immediately run hardware inventory. To run hardware inventory, on a client use **root** credentials to run the following command to start a hardware inventory cycle: **/opt/microsoft/configmgr/bin/ccmexec -rs hinv**  

 Actions for hardware inventory are entered into the client log file, **scxcm.log**.  

##  <a name="BKMK_CustomHINVforLinux"></a> How to use Open Management Infrastructure to create custom hardware inventory  
 The client for Linux and UNIX supports custom hardware inventory that you can create by using the Open Management Infrastructure (OMI). To do so you use the following steps:  

1.  Create a custom inventory provider by using the OMI source  

2.  Configure computers to use the new provider to report inventory  

3.  Enable Configuration Manager to support the new provider  

###  <a name="BKMK_LinuxProvider"></a> Create a custom hardware inventory provider for Linux and UNIX computers:  
 To create a custom hardware inventory provider for the Configuration Manager client for Linux and UNIX, use **OMI Source - v.1.0.6** and follow the instructions from the OMI Getting Started Guide. This process includes creating a Managed Object Format (MOF) file that defines the schema of the new provider. Later, you import the MOF file to Configuration Manager to enable support of the new custom inventory class.  

 Both the OMI Source - v.1.0.6, and the OMI Getting Started Guide are available for download from [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) website. You can locate these downloads on the **Documents** tab at the following web page on the OpenGroup.org website: [Open Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="BKMK_AddProvidertoLinux"></a> Configure each computer that runs Linux or UNIX with the custom hardware inventory provider:  
 After you create a custom inventory provider, you must copy and then register the provider library file on each computer that has inventory you want to collect.  

1.  Copy the provider library to each Linux and UNIX computer from which you want to collect inventory. The name of the provider library resembles the following: **XYZ_MyProvider.so**  

2.  Next, on each Linux and UNIX computer, register the provider library with the OMI server. The OMI server installs on the computer when you install the Configuration Manager client for Linux and UNIX but you must manually register custom providers. Use the following command line to register the provider: **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  After you register the new provider, test the provider by using the **omicli** tool. The **omicli** tool is installed on each Linux and UNIX computer when you install the Configuration Manager client for Linux and UNIX. For example, where **XYZ_MyProvider** is the name of the provider you created, run the following command on the computer: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     For information about **omicli** and testing custom providers, see the OMI Getting Started Guide.  

> [!TIP]  
>  Use software distribution to deploy custom providers and to register custom providers on each Linux and UNIX client computer.  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> Enable the new inventory class in Configuration Manager:  
 Before Configuration Manager can report on inventory that is reported by the new provider on Linux and UNIX computers, you must import the Managed Object Format (MOF) file that defines the schema of your custom provider.  

 To import a custom MOF file into Configuration Manager, see [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
