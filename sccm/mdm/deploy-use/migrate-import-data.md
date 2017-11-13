---
title: "Import data to Microsoft Intune"
titleSuffix: "Configuration Manager"
description:
keywords:
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service:
ms.technology:
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a

---

# Import Configuration Manager data to Microsoft Intune 

*Applies to: System Center Configuration Manager (Current Branch)*    

The recommended first phase in the process to [migrate hybrid MDM users and devices to Intune standalone](migrate-hybridmdm-to-intunesa.md) in the cloud-only configuration is to use the Intune Data Importer tool. If you want, you can skip this phase and move on to the [prepare Intune for user migration](migrate-prepare-intune.md) phase. However, this tool performs the following functions that can save you a lot of time in the next phase: 
1.	Collects data about the objects you select from your Configuration Manager hierarchy. 
2.	Provides details about the objects you can select for import and information about why some objects cannot be imported.
3.	Imports selected objects into your Microsoft Intune tenant. 

The Data Importer tool does not change your Configuration Manager environment in any way, and therefore, you can import objects into Intune and validate that everything works as expected without risk of leaving your hybrid MDM devices in an unmanaged state. 

## What objects can this tool import?
The import tool can collect information about the following object types in Configuration Manager and provides information about whether the collected objects can be imported: 
- Configuration items
- Certificate profiles
- Email profiles
- VPN profiles
- Wi-Fi profiles
- Compliance policies
- Apps
- Deployments

> [!Note]    
> Importing deployments is only useful for other object types you are importing. For example, if you import VPN profiles and deployments, you will only be able to import the deployments for the VPN profiles that you select. Deployments in Intune are called assignments. If you want to import a deployment for a previously imported object, you will need to import that object again or manually create the assignment in Intune on Azure. For example, if you import VPN profiles and not deployments, you will have run the tool again and select VPN profiles and Deployments or manually create the assignment in Intune on Azure.  If you rerun the tool, duplicate objects may be created that you can delete later in Intune on Azure.  

> [!Important]    
> If the collection for a deployment is based on an Active Directory group that has been replicated to Azure Active Directory (AAD), the tool will automatically target migrated objects to the groups if you select the appropriate deployment when running the tool. When you have more complex collections or direct membership collections, you must manually recreate them in AAD and manually target object assignments to them in Intune on Azure.


## Things to know before you run the tool
- Running the tool will not change your Configuration Manager environment in any way.
- We recommend that you first test the data import process using a trial tenant. Then, after you confirm that the data you expect has been imported, you can go through the same process with your production Intune tenant.
- The data importer is meant to only import Configuration Manager data one time. It does not keep track of objects in Configuration Manager or Intune. However, if you run the importer again on the same computer as before, it will tell you which objects you previously imported. The tool will not know if the object still exists in Intune or if an object has changed. If you import data to Intune more than once, you may end up with duplicate objects.
- Not all profile settings can be imported. For example, you cannot import kiosk mode or PFX settings. 
- If you have a Configuration Manager policy with settings that are not applicable to the selected platforms, the tool might ignore these settings during the import. Ignoring the settings help to make sure the policy can be imported and supported by Intune. 
- The tool will attempt to give you a reason for why an object cannot be imported. In some cases, before you import objects to Intune, you can go back to the Configuration Manager console, fix the issue, start the Configuration Manager object discovery scan again, and then import the objects. Sometimes you may need, or may want, to recreate these objects manually in Intune.
- There are some profiles that depend on other objects. If you want to import a profile that depends on another object, like an email profile that depends on a certificate, you must import both objects at the same time unless you have previously imported the other object from the same computer with the same user.  
- After you run the tool, you might need to perform additional manual steps. For example, targeting apps and policies to AAD groups. 

## Prerequisites
- Configuration Manager version 1610 or later.- We recommend that you specify the top-level site and run the tool with a user that has access to all objects in the site hierarchy. The tool only discovers objects accessible by the user running the tool. 
- A Global Administrator must run the Data Importer tool the first time using the following ***intunedataimporter.exe -GlobalConsent*** parameter. Then, a Global Administrator or an Intune Administrator can run the tool.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## Download the Data Importer tool
The Data Importer tool is available to download from the ConfigMgrTools/Intune-Data-Importer repo in GitHub. Use the following procedure to download the tool.

1. Go to the [Intune Data Importer GitHub releases](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases) page.
2. For the latest release, click **Microsoft.Intune.Data.Importer.exe**.
3. Save and run (or just run) the .exe, and then choose a destination folder to extract the Intune Data Importer tool.

## Run the Data Importer tool
The wizard for the Data Importer tool can be divided in three main steps. This section provides information to help you complete each section of the wizard and successfully import Configuration Manager data into Intune. Each step continues where the previous step ended.

### Provide permission for the Data Importer tool to access resources
Before you can run the Data Importer tool, you must use a Global Administrator account to give the Data Importer tool permission in Azure to access resources. Then, you can run the tool by using a Global Administrator or Intune Administrator account.   

1.	A Global Administrator must run the tool the first time using the following parameter:  ***intunedataimporter.exe -GlobalConsent*** 
2. When the tool starts, a login screen displays where you must sign in using an account with the Global Administrator role in Azure. 
3. Click **Accept** to create an application in Azure with appropriate rights in Microsoft Graph. The Data Importer tool needs these rights to import objects into Microsoft Intune.   

   > [!Important]
   > When you click **Accept**, you give the tool permission to do the following:
   > - Read all groups
   > - Sign in and read the user profile
   > - Read and write Intune device configuration and policies
   > - Read and write Intune apps
   > - Read and write Intune role-based administration control policies
   > - Read and write Intune devices
   > - Read and write Intune configuration
1. After you accept consent, any other Global Administrator or Intune Administrator can run the tool to import data from Configuration Manager into Intune on Azure.    
        
    > [!Note]
    > If consent has not first been accepted by a Global Administrator, the tool might display **You can't access this application** after an Intune Administrator runs the Data Importer tool and logs in to the Intune subscription.

### Manually map collections to Azure AD groups
When you run the Data Importer tool, it extracts the AD group name from collections with a single rule that targets a single AD group. When the assignments are created in Intune, the Data Importer looks for an Azure AD group with the same name as the AD group, and if it exists, assigns the imported object to that Azure AD group. You can override the AD group name that the Data Importer finds for a collection and provide one or more Azure AD groups to use for that collection. Using the collection mapping file provides a way for you to map collections that are typically not importable with the Data Importer to Azure AD groups.
#### Find the collections that are not importable
You can get a list of all collections that aren’t importable so you can add them to your collection mapping .csv file. 
1. Run the Data Importer tool and select the objects to import. Use the procedures in [Phase 1: Discover Configuration Manager objects and collect data](#phase-1:-discover-configuration-manager-objects-and-collect-data) and [Phase 2: Resolve issues and select the objects to import](#phase-2:-resolve-issues-and-select-the-objects-to-import) to discover and choose the objects. Then, on the **Summary** page, choose **Export Details** to create a .csv file with details of everything selected for import, including the objects that can't be imported and deployments. 
2. Open the .csv file in Microsoft Excel and filter the data based on the **Deployment** for the **Type** column and **No** for the **Importable** column. The collection name column shows all the collections that need to be added to a collection mapping file in order for those deployments to be importable.

#### Create the collection mapping file
The collection mapping file is a comma-separated values (CSV) file where the first column is the Configuration Manager collection name and the second column is the Azure AD group name to use for that collection. To specify more than one Azure AD group for a single Configuration Manager collection, create multiple rows in the CSV file with that collection name. The following example is a CSV file that contains two collections. The first collection is mapped to a single Azure AD group and the second collection is mapped to two Azure AD groups.

![Example of collection mapping csv file](..\media\migrate-collectionmapping.png)

#### Start the Data Importer tool using collection mapping
To use a collection mapping file, you must start the Data Importer tool using the *-CollectionMappingFile* command-line parameter and full path to the collection mapping .csv file you create. For example:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> The Data Importer does not display anything on any wizard page to indicate that the collection mapping file was loaded. However, the tool displays any errors encountered while reading the .csv file. Also, on the **Summary** page of the wizard you can review **Deployment** types. The tool displays **Yes** in the Importable column and lists the Azure AD groups that it will assign to objects in the **Notes** column.

### Phase 1: Discover Configuration Manager objects and collect data
In phase 1, you select the objects to discover and have the tool collect information about the selected objects. 
1. Open the tool and click **Start**.  
2. Read the information, and then click **Next**. 
3. Choose whether to import a previously exported data set or select the object types to import:
   - **Import previously exported data set**: Choose **Import data set exported from a previous run of Intune Data Importer**, and click **Exported data folder** to select a data set that you previously exported using the Data Importer Tool. The user who imports the data set must be the same user that exported the data. After you import the data, a summary of the objects are listed on the **Summary** page of the wizard. If the summary looks correct, skip to the [Phase 3: Import selected object to Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > After you discover and select the objects in your site to import, you can export the objects to a data set on the **Sign-in to Intune** page of the wizard. You can then import the data set on this page. The data set is encrypted using the Windows user credentials of the logged-in user so only the user that exported the data set can import the data set in the tool. 
   - **Select object types to import**: Choose **Select object types to import** to select object types to import and discover objects in your environment. Provide the following information about your site and the objects you want to import.
      - **Site server name**: Provide the fully qualified domain name of the site server to import objects. The tool only discovers objects accessible by the user running the tool. Typically, you will specify the top-level site and run the tool with a user that has access to all objects in the site hierarchy.
      - **Site code**: Provide the site code for the site server. You can find the three-letter code at the top of the Configuration Manager console.
      - **Object types to import**: Choose the objects that you want the tool to collect. You can choose **Select all** to choose all the objects or select individual object types. 
4.	Click **Next** to start discovering the objects at the site. The tool displays progress for each of the object types. 
    - When the tool discovers no data for a selected object type, the progress bar immediately displays completed for that object type.
    - Objects that you did not select do not display on the **Collect** data page. 
    - You can run the tool again for objects that were not collected or that you cancelled during the collection process.

### Phase 2: Resolve issues and select the objects to import  
In phase 2, you review the objects found by the tool, resolve issues that prevent the object from being imported to Intune, and select the objects to import. If you fix issues, return to the **Discover environment** page of the wizard to re-discover the objects. 
5.	Click **Next** to review the collected objects. An item selection page is available for each collected object type. 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.	On each item selection page, sort the objects by the Importable column and review the objects that are not importable. The information in the Notes column provides details about why the tool cannot import the object. 
7.	Now you must decide whether you want to fix any of the issues for non-importable objects. If you fix one or more issues, click Previous until you get to the Select data from Configuration Manager page and collect the data again to see if you resolved the issue. You can continue to fix issues until you are satisfied with the objects that are importable. 
8.	On each item selection page, select the objects that you want to import. The following columns are listed:
    - **Name**: Name of the Configuration Manager object. 
    - **Importable**: Specifies whether an object can be imported. You can only choose objects that have Yes in the Importable column. 
    - **Platform**: Specifies the platform supported by the object.
    - **Already imported**: Specifies whether the object has already been imported by using the tool on this computer. 
    - **Is superseded** (for apps): Specifies whether the app is superseded by another app. You must check the **Show superseded apps** check box at the top of the page for superseded apps to display.
    - **Notes**: Provides information about why an object can’t be imported. The **Notes** column also displays information about settings that were ignored (for some object types), but the object is still importable without those settings.
    - **Configuration baselines** (for configuration items): Specifies the configuration baselines that are associated with a configuration item.
    - **Required certificate** (for profiles and policies): Specifies whether a certificate is associated with the object. When a certificate is associated with the object, you must import the certificate too.
9.	After you choose the objects to import, they are listed on the Summary page. You have the following actions available: 
    - **Export details**: Creates a .csv file that contains the information displayed on the screen. It also shows objects that are not importable and the reason why it can't be imported. You can keep this file for your records. 
    - **Export error data**: Exports a compressed file that contains information about the data that the tool wasn’t able convert or import. 

### Phase 3: Import selected objects to Intune
In phase 3, you will sign into Intune and import the selected objects. 
10.	Click **Next**, and then click **Sign in to Intune** to sign into the Intune tenant for the data import or choose to export the data.

    - **Export**: After you discover and select the objects in your site to import, you can export the objects to a data set. This allows you to discover objects from a computer that doesn't have Internet access, export the data, and then import the data from a computer that has Internet access. The data set is encrypted using the Windows user credentials of the logged-in user so only the user that exported the data set can import the data set in the tool. When you choose this option, choose the path to the exported data. 
      1. Click **Export** on the **Sign in to Intune** page. 
      2. Click **Start** to export the data, and then click **Close** to complete the wizard.
      3. Start the Data Importer from another computer with Internet access using the same credentials and select **Import previously exported data set** on the second page of the wizard. Once the data is imported, the wizard takes you to the **Sign in to Intune** page. 
    - **Sign in to Intune**: You must sign in with a Global Administrator or Intune Administrator account. After you sign in, the import process starts.
    
      > [!Important]
      > We recommend that you first test the data import process using a trial tenant. Then, after you confirm that the data you expect has been imported, you can go through the same process with your production Intune tenant.
12.	The Progress page provides the progress as the objects are imported. Click **Next** when the import completes. 
13.	On the Completion page, the imported objects are listed. Check the status for any objects that encountered an error during the import process. You have the following actions available: 
    - **Export details**: Creates a .csv file that contains the information displayed on screen. You can keep this file for your records. 
    - **Export error data**: Exports a compressed file that contains information about the data that the tool wasn’t able convert or import.

## Next steps
After you import the data into Intune, you must take steps to [prepare Intune for user migration](migrate-prepare-intune.md). 