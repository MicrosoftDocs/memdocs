---
title: "Extend hardware inventory | System Center Configuration Manager"
description: "Learn ways to extend hardware inventory in System Center Configuration Manager."
ms.custom: na
ms.date: 04/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigmanms.author: nbigmanmanager: angrobe

---
# How to extend hardware inventory in System Center Configuration Manager
System Center Configuration Manager hardware inventory reads information about devices from Windows PCs by using Windows Management Instrumentation (WMI). WMI is the Microsoft implementation of web-based Enterprise Management (WBEM), which is an industry standard for accessing management information in an enterprise environment. In previous versions of Configuration Manager, you could extend hardware inventory by modifying the file sms_def.mof on the site server. This file contained a list of WMI classes that could be read by Configuration Manager hardware inventory. If you edited this file, you could enable and disable existing classes, and also create new classes to inventory.  

 The Configuration.mof file is used to define the data classes to be inventoried by hardware inventory on the client and is unchanged from Configuration Manager 2012. You can create data classes to inventory existing or custom WMI repository data classes or registry keys present on client systems.  

 The Configuration.mof file also defines and registers the WMI providers that access device information during hardware inventory. Registering providers defines the type of provider to be used and the classes that the provider supports.  

 When Configuration Manager clients request policy, for example, during their standard client policy polling interval, the Configuration.mof is attached to the policy body. This file is then downloaded and compiled by clients. When you add, modify, or delete data classes from the Configuration.mof file, clients automatically compile these changes that are made to inventory-related data classes. No further action is necessary to inventory new or modified data classes on Configuration Manager clients. This file is located  in **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** on primary site servers.  

 In Configuration Manager, you no longer edit the sms_def.mof file as you did in Configuration Manager 2007. Instead, you can enable and disable WMI classes, and add new classes to collect by hardware inventory by using client settings. Configuration Manager provides the following methods to extend hardware inventory.  

> [!NOTE]  
>  If you have manually changed the Configuration.mof file to add custom inventory classes, these changes will be overwritten when you update  to the 1602 release. To keep using custom classes after you update, you must add these to the "Added extensions" section of the Configuration.mof file after you update to 1602.  
> However, you must not modify anything above this section, as these sections are reserved for  modification by Configuration Manager. A backup of your custom Configuration.mof can be found in:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Method|More information|  
|------------|----------------------|  
|Enable or disable existing inventory classes|You can enable or disable the default inventory classes used by Configuration Manager or you can create custom client settings that allow you to collect different hardware inventory classes from specified collections of clients. For more information, see the [To enable or disable existing inventory classes](#BKMK_Enable) procedure in this topic.|  
|Add a new inventory class|You can add a new inventory class from the WMI namespace of another device. For more information, see the [To add a new inventory class](#BKMK_Add) procedure in this topic.|  
|Import and export hardware inventory classes|You can import and export Managed Object Format (MOF) files that contain inventory classes from the Configuration Manager console. For more information, see the [To import hardware inventory classes](#BKMK_Import) and [To export hardware inventory classes](#BKMK_Export) procedures in this topic.|  
|Create NOIDMIF Files|Use NOIDMIF files to collect information about client devices that cannot be inventoried by Configuration Manager. For example, you might want to collect device asset number information that exists only as a label on the device. NOIDMIF inventory is automatically associated with the client device that it was collected from. For more information, see [To create NOIDMIF files](#BKMK_NOIDMIF) in this topic.|  
|Create IDMIF Files|Use IDMIF files to collect information about assets in your organization that are not associated with a Configuration Manager client, for example, projectors, photocopiers and network printers. For more information, see [To create IDMIF files](#BKMK_IDMIF) in this topic.|  

## Procedures to extend hardware inventory  
 Use the following procedures to extend hardware inventory, as described in the preceding table.  

 These procedures help you to configure the default client settings for hardware inventory and they apply to all the clients in your hierarchy. If you want these settings to apply to only some clients, create a custom client device setting and assign it to a collection that contains the devices that you want to inventory. For more information about how to create custom client settings, see [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> To enable or disable existing inventory classes  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Client Settings** dialog box, click **Hardware Inventory**.  

6.  In the **Device Settings** list, click **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, select or clear the classes and class properties to be collected by hardware inventory. You can expand classes to select or clear individual properties within that class. Use the **Search for inventory classes** field to search for individual classes.  

    > [!IMPORTANT]  
    >  When you add new classes to Configuration Manager hardware inventory, the size of the inventory file that is collected and sent to the site server will increase. This might negatively affect the performance of your network and Configuration Manager site. Enable only the inventory classes that you want to collect.  

8.  Click **OK** to save your changes and close the **Hardware Inventory Classes** dialog box.  

###  <a name="BKMK_Add"></a> To add a new inventory class  

1.  In the Configuration Manager console, click **Administration**.  

    > [!IMPORTANT]  
    >  You can only add inventory classes from the top level server in the hierarchy and by modifying the default client settings. This option is not available when you create custom device settings.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Client Settings** dialog box, click **Hardware Inventory**.  

6.  In the **Device Settings** list, click **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, click **Add**.  

8.  In the **Add Hardware Inventory Class** dialog box, click **Connect**.  

9. In the **Connect to Windows Management Instrumentation (WMI)** dialog box, specify the name of the computer from which you will retrieve the WMI classes and the WMI namespace to use for retrieving the classes. If you want to retrieve all classes below the WMI namespace that you specified, click **Recursive**. If the computer you are connecting to is not the local computer, supply login credentials for an account that has permission to access WMI on the remote computer.  

10. Click **Connect**.  

11. In the **Add Hardware Inventory Class** dialog box, in the **Inventory classes** list, select the WMI classes that you want to add to Configuration Manager hardware inventory.  

12. If you want to edit information about the selected WMI class, click **Edit**, and in the **Class qualifiers** dialog box, provide the following information:  

    -   **Display name** - Specify a friendly name for the class that will be displayed in Resource Explorer.  

    -   **Properties** - Specify the units in which each property of the WMI class will be displayed.  

     You can also designate properties as a key property to help uniquely identify each instance of the class. If no key is defined for the class and multiple instances of the class are reported from the client, only the latest instance that is found is stored in the database.  

     When you have finished configuring the properties, click **OK** to close the **Class qualifiers** dialog box.  

13. Click OK to close the **Add Hardware Inventory Class** dialog box.  

14. Click **OK** to close the **Hardware Inventory Classes** dialog box.  

15. Click **OK** to close the **Default Client Settings** dialog box.  

###  <a name="BKMK_Import"></a> To import hardware inventory classes  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

    > [!IMPORTANT]  
    >  You can only import inventory classes when you modify the default client settings. However, you can use custom client settings to import information that does not contain a schema change, such as changing the property of an existing class from **True** to **False**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Client Settings** dialog box, click **Hardware Inventory**.  

6.  In the **Device Settings** list, click **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, click **Import**.  

8.  In the **Import** dialog box, select the Managed Object Format (MOF) file that you want to import, and then click **OK**.  

9. In the **Import Summary** dialog box, review the items that will be imported, and then click **Import**.  

###  <a name="BKMK_Export"></a> To export hardware inventory classes  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Client Settings** dialog box, click **Hardware Inventory**.  

6.  In the **Device Settings** list, click **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, click **Export**.  

    > [!NOTE]  
    >  When you export classes, all currently selected classes will be exported.  

8.  In the **Export** dialog box, specify the Managed Object Format (MOF) file that you want to export the classes to, and then click **Save**.  

## How to Use Management Information Files (MIF Files) to extend hardware inventory  
 Use Management Information Format (MIF) files to extend hardware inventory information collected from clients by Configuration Manager. During hardware inventory, the information stored in MIF files is added to the client inventory report and stored in the site database, where you can use the data in the same ways that you use default client inventory data. There are two types of MIF files, NOIDMIF and IDMIF.  

> [!IMPORTANT]  
>  Before you can add information from MIF files to the Configuration Manager database, you must create or import class information for them. For more information, see the sections [To add a new inventory class](#BKMK_Add) and [To import hardware inventory classes](#BKMK_Import) in this topic.  

###  <a name="BKMK_NOIDMIF"></a> To create NOIDMIF files  
 NOIDMIF files can be used to add information to a client hardware inventory that cannot normally be collected by Configuration Manager and is associated with a particular client device. For example, many companies label each computer in the organization with an asset number and then catalogue these by hand. When you create a NOIDMIF file, this information can be added to the Configuration Manager database and be used for queries and reporting. For information about creating NOIDMIF files, see the Configuration Manager SDK documentation.  

> [!IMPORTANT]  
>  When you create a NOIDMIF file, this must be saved in an ANSI encoded format. NOIDMIF files saved in UTF-8 encoded format cannot be read by Configuration Manager.  

 After you create a NOIDMIF file, store this in the folder *%Windir%***\System32\CCM\Inventory\Noidmifs** folder on each client. Configuration Manager will collect information from NODMIF files in this folder during the next scheduled hardware inventory cycle.  

###  <a name="BKMK_IDMIF"></a> To create IDMIF files  
 IDMIF files can be used to add information about assets to the Configuration Manager database that could not normally be inventoried by Configuration Manager and is not associated with a particular client device. For example, you could use IDMIFS to collect information about projectors, DVD players, photocopiers, or other equipment that does not contain a Configuration Manager client. For information about creating IDMIF files, see the Configuration Manager SDK documentation.  

 After you create an IDMIF file, store this in the folder *%Windir%***\System32\CCM\Inventory\Idmifs** folder on client computers. Configuration Manager will collect information from this file during the next scheduled hardware inventory cycle. You must declare new classes for information contained in the file by adding or importing them.  
