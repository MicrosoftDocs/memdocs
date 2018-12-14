---
title: "Import configuration data"
titleSuffix: "Configuration Manager"
description: "Import configuration data if it's contained in a cabinet file format and adheres to the supported Service Modeling Language schema."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Import configuration data with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In addition to creating configuration baselines and configuration items in the System Center Configuration Manager console, you can import configuration data if it is contained in a cabinet (.cab) file format and adheres to the supported Service Modeling Language (SML) schema. You can import configuration data from:  

- Best practice configuration data (Configuration Packs) that has been downloaded from Microsoft or from other software vendor sites.  

- Configuration data that has been exported from System Center 2012 Configuration Manager and later.  

- Configuration data that was externally authored and that conforms to the SML schema.  

  For an example Configuration Pack that helps you manage compliance for System Center 2012 Configuration Manager site server roles, see [System Center 2012 Configuration Manager Configuration Pack](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

When you import a configuration baseline, some or all of the configuration items that are referenced in the configuration baseline might also be included in the cabinet file. During the import process, Configuration Manager verifies that all of the configuration items that are referenced in the configuration baseline are either also included in the cabinet file or already exist in the Configuration Manager site. The import process fails if you attempt to import a configuration baseline that references configuration data that Configuration Manager cannot locate.  

Other scenarios where the import process might fail include the following:  

-   The configuration data references configuration data that Configuration Manager cannot locate, either in its database or in the cabinet file itself.  

-   The configuration data is already present in the Configuration Manager database with the same name and configuration data version, but the content version differs.  

-   The configuration data is already present in the Configuration Manager database with the same content version, but the hash calculation identifies it as being different.  

-   A newer version of the configuration data with same name is already present or has recently been deleted in the Configuration Manager database.  

-   In a multi-site Configuration Manager hierarchy, the configuration data was originally imported from a parent site. You must update it from the same site and not a child site.  

### Import configuration data  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Configuration Items** or **Configuration Baselines**
2.  In the **Home** tab, in the **Create** group, click **Import Configuration Data**.  
3.  On the **Select Files** page of the **Import Configuration Data Wizard**, click **Add**, and then in the **Open** dialog box, select the .cab files you want to import.  
4.  Select the **Create a new copy of the imported configuration baselines and configuration items** check box if you want the imported configuration data to be editable in the Configuration Manager console.  
5.  On the **Summary** page, review the actions that will be taken, and then complete the wizard.  

The imported configuration data displays in the **Compliance Settings** node of the **Assets and Compliance** workspace.  
