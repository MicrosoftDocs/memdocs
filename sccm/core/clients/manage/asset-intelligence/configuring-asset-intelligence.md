---
title: "Configure Asset Intelligence"
titleSuffix: "Configuration Manager"
description: "Set up Asset Intelligence in System Center Configuration Manager."
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configure Asset Intelligence in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Asset Intelligence inventories and manages software license usage.   

## Steps to configure Asset Intelligence  
   

- **Step 1**:To collect the inventory data required for Asset Intelligence reports, you have to enable the hardware inventory client agent as described in [How to extend hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Step 2**: [Enable Asset Intelligence Hardware Inventory Reporting Classes](#BKMK_EnableAssetIntelligence).  
- **Step 3**: [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Step 4**: [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents)  
- **Step 5**: [Import Software License Information](#BKMK_ImportSoftwareLicenseInformation)  
- **Step 6**: [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 To enable Asset Intelligence in Configuration Manager sites, you must enable one or more Asset Intelligence hardware inventory reporting classes. You can enable the classes on the **Asset Intelligence** home page, or, in the **Administration** workspace, in the **Client Settings** node, in client settings properties. Use one of the following procedures.  

##### To enable Asset Intelligence hardware inventory reporting classes from the Asset Intelligence home page  

1.  In the Configuration Manager console, choose **Asset and Compliance** > **Asset Intelligence**.  

3.  On the **Home** tab, in the **Asset Intelligence** group, choose **Edit Inventory Classes**.   

4.  To enable Asset Intelligence reporting, select **Enable all Asset Intelligence reporting classes** or  **Enable only the selected Asset Intelligence reporting classes**, and select at least one reporting class from the classes displayed.  

    > [!NOTE]  
    >  Asset Intelligence reports that depend on the hardware inventory classes that you enable by using this procedure do not display data until clients have scanned for and returned hardware inventory.  


##### To enable Asset Intelligence hardware inventory reporting classes from client settings properties  

1.  In the Configuration Manager console, choose **Administration** >  **Client Settings** > **Default Client Agent Settings**. If you have created custom client settings, you can select those instead.  

3.  On the **Home** tab > **Properties** group, choose **Properties**.   

4.  Choose **Hardware Inventory** > **Set Classes**. .  

5.  Choose **Filter by category** > **Asset Intelligence Reporting Classes**. The list of classes is refreshed with only the Asset Intelligence hardware inventory reporting classes.  

6.  Select at least one reporting class from the list.  

    > [!NOTE]  
    >  Asset Intelligence reports that depend on the hardware inventory classes that you enable by using this procedure do not display data until clients have scanned for and returned hardware inventory.  
  

###  <a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

The Asset Intelligence synchronization point site system role is used to connect Configuration Manager sites to System Center Online to synchronize Asset Intelligence catalog information. The Asset Intelligence synchronization point can only be installed  on a site system located at the top-level site of the Configuration Manager hierarchy and requires Internet access to synchronize with System Center Online by using TCP port 443.

In addition to downloading new Asset Intelligence catalog information, the Asset Intelligence synchronization point can upload custom software title information to System Center Online for categorization. Microsoft treats all uploaded software titles as public information. Ensure that your custom software titles do not contain confidential or proprietary information. For more information about requesting software title categorization, see [Request a catalog update for uncategorized software titles](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### To install an Asset Intelligence synchronization point site system role  

1.  In the Configuration Manager console, choose **Administration**> **Site Configuration** > **Servers and Site System Roles**.  

3.  Add the Asset Intelligence synchronization point site system role to a new or existing site system server:  

    -  For a **New site system server**: On the **Home** tab, in the **Create** group, choose **Create Site System Server** to start the wizard.   

        > [!NOTE]  
        >  By default, when Configuration Manager installs a site system role, the installation files are installed on the first available NTFS-formatted hard disk drive that has the most available free hard disk space. To prevent Configuration Manager from installing on specific drives, create an empty file named No_sms_on_drive.sms and copy it to the root folder of the drive before you install the site system server.  

    -  For an **Existing site system server**: Choose the server on which you want to install the Asset Intelligence synchronization point site system role. When you choose a server, a list of the site system roles that are already installed on the server are displayed in the details pane.  

         On the **Home** tab, in the **Server** group, choose **Add Site System Role** to start the wizard.  

4.  Complete the **General** page. When you add the Asset Intelligence synchronization point to an existing site system server, verify the values that were previously configured.  

5.  On the **System Role Selection** page, select **Asset Intelligence Synchronization Point** from the list of available roles.  

6.  On the **Asset Intelligence Synchronization Point Connection Settings** page, choose **Next**.  

     By default, the **Use this Asset Intelligence Synchronization Point** setting is selected and cannot be configured on this page. System Center Online accepts network traffic only over TCP port 443, therefore the **SSL port number** setting cannot be configured on this page of the wizard.  

7.  Optionally, you can specify a path to the System Center Online authentication certificate (.pfx) file. Typically, you do not specify a path for the certificate because the connection certificate is automatically provisioned during site role installation.  

8.  On the **Proxy Server Settings** page, specify whether the Asset Intelligence synchronization point will use a proxy server when connecting to System Center Online to synchronize the catalog and whether to use credentials to connect to the proxy server.  

    > [!WARNING]  
    >  If a proxy server is required to connect to System Center Online, the connection certificate might also be deleted if the user account password expires for the account configured for proxy server authentication.  

9. On the **Synchronization Schedule** page, specify whether to synchronize the Asset Intelligence catalog on a schedule. When you enable the synchronization schedule, you specify a simple or custom synchronization schedule. During scheduled synchronization, the Asset Intelligence synchronization point connects to System Center Online to retrieve the latest Asset Intelligence catalog. You can manually synchronize the Asset Intelligence catalog from the Asset Intelligence node in the Configuration Manager console. For the steps to manually synchronize the Asset Intelligence catalog, see the [To manually synchronize the Asset Intelligence catalog](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) section in the [Operations for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Complete the wizard 

###  <a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Four Asset Intelligence reports display information gathered from the Windows Security event logs on client computers. Here's how to configure computer security policy logon settings to enable auditing of Success logon events.  

##### To enable success logon event logging by using a local security policy  

1.  On a Configuration Manager client computer, choose **Start** > **Administrative Tools** > **Local Security Policy**.  

2.  In the **Local Security Policy** dialog box, under **Security Settings**, expand **Local Policies**, and then choose **Audit Policy**.  

3.  In the results pane, double-click **Audit logon events**, ensure that the **Success** check box is selected, and then choose **OK**.  

##### To enable success logon event logging by using an Active Directory domain security policy  

1.  On a domain controller computer, choose **Start**, point to **Administrative Tools**, and then choose **Domain Security Policy**.  

2.  In the **Local Security Policy** dialog box, under **Security Settings**, expand **Local Policies**, and then choose **Audit Policy**.  

3.  In the results pane, double-click **Audit logon events**, ensure that the **Success** check box is selected, and then choose **OK**.  

###  <a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 The following sections describe the procedures necessary to import both Microsoft and general software licensing information into the Configuration Manager site database by using the Import Software License Wizard. When you import software license information into the site database from license statement files, the site server computer account requires **Full Control** permissions for the NTFS file system to the file share that is used to import software license information.  

> [!IMPORTANT]  
>  When software license information is imported into the site database, existing software license information is overwritten. Ensure that the software license information file that you use with the Import Software License Wizard contains a complete listing of all necessary software license information.  

##### To import software license information into the Asset Intelligence catalog  

1.  In the **Asset and Compliance** workspace, choose **Asset Intelligence**.  

2.  On the **Home** tab, in the **Asset Intelligence** group, choose **Import Software Licenses**.   

4.  On the **Import** page, specify whether you are importing a Microsoft Volume Licensing (MVLS) file (.xml or .csv) or a General License Statement file (.csv). For more information about creating a General License Statement file, see [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) later in this topic.  

    > [!WARNING]  
    >  To download an MVLS file in .csv format that you can import to the Asset Intelligence catalog, see [Microsoft Volume Licensing Service Center](http://go.microsoft.com/fwlink/p/?LinkId=226547). To access this information, you must have a registered account on the website. You must contact your Microsoft account representative for information about how to get your MVLS file in .xml format.  

5.  Enter the UNC path to the license statement file or choose **Browse** to select a network shared folder and file.  

    > [!NOTE]  
    >  The shared folder should be correctly secured to prevent unauthorized access to the licensing information file, and the computer account of the computer that the wizard is being run on must have Full Control permissions to the share that contains the license import file.  

6. Complete the wizard.  

###  <a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 A general license statement can also be imported into the Asset Intelligence catalog by using a manually created license import file in comma delimited (.csv) file format.  

> [!NOTE]  
>  While only the **Name**, **Publisher**, **Version**, and **EffectiveQuantity** fields are required to contain data, all fields must be entered on the first row of the license import file. All date fields should be displayed in the following format: Month/Day/Year, for example, 08/04/2008.  

Asset Intelligence matches the products that you specify in the general license statement by using the product name and product version, but not publisher name. You must use a product name in the general license statement that is an exact match with the product name stored in the site database. Asset Intelligence takes the **EffectiveQuantity** number given in the general license statement and compares the number with the number of installed products found in Configuration Manager inventory.  

> [!TIP]  
>  To get a complete list of the product names stored in the Configuration Manager site database, you can run the following query on the site database: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 You can specify exact versions for a product or specify part of the version, such as only the major version. The following examples provide the resulting version matches for a general license statement version entry for a specific product.  

|General license statement entry|Matching site database entries|  
|-------------------------------------|------------------------------------|  
|Name: "MySoftware", ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Name: "MySoftware", Version "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Name: "Mysoftware", Version "2"<br /><br /> Name: "Mysoftware", Version "2.05"|Error during import. The import fails when more than one entry matches the same product version.|  
  

##### To create a general license statement import file by using Microsoft Excel  

1.  Open Microsoft Excel and create a new spreadsheet.  

2.  On the first row of the new spreadsheet, enter all software license data field names.  

3.  On the second and subsequent rows of the new spreadsheet, enter software license information as required. Ensure that at least all of the required software license data fields are entered on subsequent rows for each software license to be imported. The software title name entered in the spreadsheet must be the same as the software title that is displayed in Resource Explorer for a client computer after hardware inventory has run.  

4.  Save the file in .csv format.  

5.  Copy the .csv file to the file share that is used to import software license information into the Asset Intelligence catalog.  

6.  In the Configuration Manager console, use the Import Software License Wizard to import the newly created .csv file.  

7.  Run the Asset Intelligence **License 15A - Third Party Software Reconciliation Report** to verify that the licensing information has been successfully imported into the Asset Intelligence catalog.  

> [!NOTE]  
>  For an example of a general software license file that you can use for testing purposes, see [Example Asset Intelligence general license import file in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### Sample table to describe software licenses  
 When creating a general license statement import file, the information in the following table can be used to describe software licenses to be imported into the Asset Intelligence catalog.  

|Column name|Data type|Required|Example|  
|-----------------|---------------|--------------|-------------|  
|Name|Up to 255 characters|Yes|Software title|  
|Publisher|Up to 255 characters|Yes|Software publisher|  
|Version|Up to 255 characters|Yes|Software title version|  
|Language|Up to 255 characters|Yes|Software title language|  
|EffectiveQuantity|Integer value|Yes|Number of licenses purchased|  
|PONumber|Up to 255 characters|No|Purchase order information|  
|ResellerName|Up to 255 characters|No|Reseller information|  
|DateOfPurchase|Date value in the following format: MM/DD/YYYY|No|Date of license purchase|  
|SupportPurchased|Bit value|No|0 or 1: Enter 0 for Yes, or 1 for No|  
|SupportExpirationDate|Date value in the following format: MM/DD/YYYY|No|End date of purchased support|  
|Comments|Up to 255 characters|No|Optional comments|  

###  <a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 The following maintenance tasks are available for Asset Intelligence:  

-   **Check Application Title with Inventory Information**: Checks that the software title that is reported in software inventory is reconciled with the software title in the Asset Intelligence catalog. By default, this task is enabled and scheduled to run on Saturday after 12:00 A.M. and before 5:00 A.M. This maintenance task is only available at the top-level site in your Configuration Manager hierarchy.  

-   **Summarize Installed Software Data**: Provides the information that is displayed in the **Assets and Compliance** workspace, in the **Inventoried Software** node, under the **Asset Intelligence** node. When the task runs, Configuration Manager gathers a count for all inventoried software titles at the primary site. By default, this task is enabled and scheduled to run every day after 12:00 A.M. and before 5:00 A.M. This maintenance task is available only on primary sites.  

##### To configure Asset Intelligence maintenance tasks  

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites**.  

3.  Select the site on which to configure the Asset Intelligence maintenance task.  

4.  On the **Home** tab, in the **Settings** group, choose **Site Maintenance**. Select a task, and choose **Edit** to modify the settings. 

  	We recommend that you set the time period to off-peak hours of the site. The time period is the time interval in which the task can run. It is defined by the **Start after** and **Latest start time** specified in the **Task Properties** dialog box.  

    You can initiate the task right away by selecting the current day and setting the **Start after** time to a couple minutes after the present time.  

7.  Choose **OK** to save your settings. The task now runs according to its schedule.  

    > [!NOTE]  
    >  If a task fails to run on the first attempt, Configuration Manager attempts to rerun the task until either the task runs successfully or until the time period in which the task can run has passed.  
