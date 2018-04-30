---
title: "Extend hardware inventory"
titleSuffix: "Configuration Manager"
description: "Learn ways to extend hardware inventory in System Center Configuration Manager."
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to extend hardware inventory in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Hardware inventory reads information from Windows PCs by using Windows Management Instrumentation (WMI). WMI is the Microsoft implementation of web-based Enterprise Management (WBEM), an industry standard for accessing management information in an enterprise. In previous versions of Configuration Manager, you extended hardware inventory by modifying the file sms_def.mof on the site server. This file contained a list of WMI classes that could be read by hardware inventory. Editing this file, you could enable and disable existing classes, and also create new classes to inventory.  

The Configuration.mof file is used to define the data classes to be inventoried by hardware inventory on the client and is unchanged from Configuration Manager 2012. You can create data classes to inventory existing or custom WMI repository data classes or registry keys present on client systems.  

 The Configuration.mof file also defines and registers the WMI providers that access device information during hardware inventory. Registering providers defines the type of provider to be used and the classes that the provider supports.  

 When Configuration Manager clients request policy, the Configuration.mof is attached to the policy body. This file is then downloaded and compiled by clients. When you add, modify, or delete data classes from the Configuration.mof file, clients automatically compile these changes that are made to inventory-related data classes. No further action is necessary to inventory new or modified data classes on Configuration Manager clients. This file is located  in **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** on primary site servers.  

 In Configuration Manager, you no longer edit the sms_def.mof file as you did in Configuration Manager 2007. Instead, you can enable and disable WMI classes, and add new classes to collect by hardware inventory by using client settings. Configuration Manager provides the following methods to extend hardware inventory.  

> [!NOTE]  
>  If you've manually changed the Configuration.mof file to add custom inventory classes, these changes will be overwritten when you update to version 1602. To keep using custom classes after you update, you must add them to the "Added extensions" section of the Configuration.mof file after you update to 1602.  
> However, you must not modify anything above this section, as these sections are reserved for modification by Configuration Manager. A backup of your custom Configuration.mof can be found in:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Method|More information|  
|------------|----------------------|  
|Enable or disable existing inventory classes|Enable or disable the default inventory classes or create custom client settings that allow you to collect different hardware inventory classes from specified collections of clients. See the [To enable or disable existing inventory classes](#BKMK_Enable) procedure in this article.|  
|Add a new inventory class|Add a new inventory class from the WMI namespace of another device. See the [To add a new inventory class](#BKMK_Add) procedure in this article.|  
|Import and export hardware inventory classes|Import and export Managed Object Format (MOF) files that contain inventory classes from the Configuration Manager console. See the [To import hardware inventory classes](#BKMK_Import) and [To export hardware inventory classes](#BKMK_Export) procedures in this article.|  
|Create NOIDMIF Files|Use NOIDMIF files to collect information about client devices that cannot be inventoried by Configuration Manager. For example, you might want to collect device asset number information that exists only as a label on the device. NOIDMIF inventory is automatically associated with the client device that it was collected from. See [To create NOIDMIF files](#BKMK_NOIDMIF) in this article.|  
|Create IDMIF Files|Use IDMIF files to collect information about assets in your organization that are not associated with a Configuration Manager client, for example, projectors, photocopiers and network printers. See [To create IDMIF files](#BKMK_IDMIF) in this article.|  

## Procedures to extend hardware inventory  
These procedures help you to configure the default client settings for hardware inventory and they apply to all the clients in your hierarchy. If you want these settings to apply to only some clients, create a custom client device setting and assign it to a collection of specific clients. See [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> To enable or disable existing inventory classes  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Default Client Settings** dialog box, choose **Hardware Inventory**.  

6.  In the **Device Settings** list, click **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, select or clear the classes and class properties to be collected by hardware inventory. You can expand classes to select or clear individual properties within that class. Use the **Search for inventory classes** field to search for individual classes.  

    > [!IMPORTANT]  
    >  When you add new classes to Configuration Manager hardware inventory, the size of the inventory file that is collected and sent to the site server will increase. This might negatively affect the performance of your network and Configuration Manager site. Enable only the inventory classes that you want to collect.  


###  <a name="BKMK_Add"></a> To add a new inventory class  

You can only add inventory classes from the hierarchy's top level server by modifying the default client settings. This option is not available when you create custom device settings.

1.  In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Default Client Settings** dialog box, choose **Hardware Inventory**.  

6.  In the **Device Settings** list, choose **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, choose **Add**.  

8.  In the **Add Hardware Inventory Class** dialog box, click **Connect**.  

9. In the **Connect to Windows Management Instrumentation (WMI)** dialog box, specify the name of the computer from which you will retrieve the WMI classes and the WMI namespace to use for retrieving the classes. If you want to retrieve all classes below the WMI namespace that you specified, click **Recursive**. If the computer you are connecting to is not the local computer, supply login credentials for an account that has permission to access WMI on the remote computer.  

10. Choose **Connect**.  

11. In the **Add Hardware Inventory Class** dialog box, in the **Inventory classes** list, select the WMI classes that you want to add to Configuration Manager hardware inventory.  

12. If you want to edit information about the selected WMI class, choose **Edit**, and in the **Class qualifiers** dialog box, provide the following information:  

    -   **Display name** - This name will be displayed in Resource Explorer.  

    -   **Properties** - Specify the units in which each property of the WMI class will be displayed.  

     You can also designate properties as a key property to help uniquely identify each instance of the class. If no key is defined for the class and multiple instances of the class are reported from the client, only the latest instance that is found is stored in the database.  

     When you've finished configuring the properties, click **OK** to close the **Class qualifiers** dialog box and the other open dialogs. 

###  <a name="BKMK_Import"></a> To import hardware inventory classes  

You can only import inventory classes when you modify the default client settings. However, you can use custom client settings to import information that doesn't include a schema change, such as changing the property of an existing class from **True** to **False**.  

1.  In the Configuration Manager console, choose **Administration** >  **Client Settings** > **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Default Client Settings** dialog box, choose **Hardware Inventory**.  

6.  In the **Device Settings** list, choose **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, choose **Import**.  

8.  In the **Import** dialog box, select the Managed Object Format (MOF) file that you want to import, and then choose **OK**. Review the items that will be imported, and then click **Import**.  

###  <a name="BKMK_Export"></a> To export hardware inventory classes  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Default Client Settings** dialog box, choose **Hardware Inventory**.  

6.  In the **Device Settings** list, choose **Set Classes**.  

7.  In the **Hardware Inventory Classes** dialog box, choose **Export**.  

    > [!NOTE]  
    >  When you export classes, all currently selected classes will be exported.  

8.  In the **Export** dialog box, specify the Managed Object Format (MOF) file that you want to export the classes to, and then choose **Save**.  

### <a name="bkmk_GreaterThan255"></a> Configure hardware inventory to collect strings larger than 255 characters
Beginning in Configuration Manager 1802, you can specify the length of strings to be greater than 255 characters for hardware inventory properties. This change applies only to newly added classes and for hardware inventory properties that aren't keys. <!-- 1357389 -->

1. In the **Administration** workspace, click on **Client Settings** highlight a client device setting to edit, right-click then select **Properties**.

2. Select **Hardware Inventory**, then **Set Classes**, and **Add**.

3. Click the **Connect** button.

4. Fill in **Computer Name**, **WMI namespace**, select **recursive** if needed. Provide credentials if necessary to connect. Click **Connect** to view the namespace classes.

5. Select a new class then click **Edit**.

6. Change the **Length** of your property that is a string, other than the key, to be greater than 255. Click **OK**. 

7. Ensure that the edited property is selected for **Add Hardware Inventory Class** and click **OK**. 


## How to Use Management Information Files (MIF Files) to extend hardware inventory  
 Use Management Information Format (MIF) files to extend hardware inventory information collected from clients by Configuration Manager. During hardware inventory, the information stored in MIF files is added to the client inventory report and stored in the site database, where you can use the data in the same ways that you use default client inventory data. There are two types of MIF files, NOIDMIF, and IDMIF.

> [!IMPORTANT]  
>  Before you can add information from MIF files to the Configuration Manager database, you must create or import class information for them. For more information, see the sections [To add a new inventory class](#BKMK_Add) and [To import hardware inventory classes](#BKMK_Import) in this article.  

###  <a name="BKMK_NOIDMIF"></a> To create NOIDMIF files  
 NOIDMIF files can be used to add information to a client hardware inventory that can't normally be collected by Configuration Manager and is associated with a particular client device. For example, many companies label each computer in the organization with an asset number and then catalog these numbers manually. When you create a NOIDMIF file, this information can be added to the Configuration Manager database and be used for queries and reporting. For information about creating NOIDMIF files, see the Configuration Manager SDK documentation.  

> [!IMPORTANT]  
>  When you create a NOIDMIF file, it must be saved in an ANSI encoded format. NOIDMIF files saved in UTF-8 encoded format cannot be read by Configuration Manager.  

 After you create a NOIDMIF file, store it in the *%Windir%***\CCM\Inventory\Noidmifs** folder on each client. Configuration Manager will collect information from NODMIF files in this folder during the next scheduled hardware inventory cycle.  

###  <a name="BKMK_IDMIF"></a> To create IDMIF files  
 IDMIF files can be used to add information about assets that couldn't normally be inventoried by Configuration Manager and isn't associated with a particular client device, to the Configuration Manager database. For example, you could use IDMIFS to collect information about projectors, DVD players, photocopiers, or other equipment that doesn't have a Configuration Manager client. For information about creating IDMIF files, see the Configuration Manager SDK documentation.  

 After you create an IDMIF file, store it in the *%Windir%***\CCM\Inventory\Idmifs** folder on client computers. Configuration Manager will collect information from this file during the next scheduled hardware inventory cycle. You must declare new classes for information contained in the file by adding or importing them.  

> [!NOTE]
> MIF files could contain large amounts of data and collecting this data could negatively affect the performance of your site. Enable MIF collection only when required and configure the option **Maximum custom MIF file size (KB)** in the hardware inventory settings. For more information, see [Introduction to hardware inventory in System Center Configuration Manager](introduction-to-hardware-inventory.md).
