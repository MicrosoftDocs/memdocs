---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Tables and Views in the MDT DB
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Tables and Views in the MDT DB
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: frankroj,mstewart,aaroncz
---

# Tables and Views in the MDT DB

In MDT, many property settings can be stored (typically configured in the CustomSettings.ini file) in a database. Configuring the properties in a database helps create a generic CustomSettings.ini file that requires fewer modifications and allows one CustomSettings.ini file to be used in more images (because the file is more generic).

Customize the database in the Database node in the Deployment Workbench. Using the Deployment Workbench, the deployment settings can be configured and saved in tables.

However, queries about the information in the tables are done using views. Views help simplify the queries by joining results from multiple tables. ZTIGather.wsf queries the views to return the result set that the **Parameters** and **ParameterCondition** properties specify.

## Tables in the MDT DB

The following table lists the database tables that Deployment Workbench creates and manages.

|**Table**|**Description**|
|-|-|
|ComputerIdentity|Used to identify a specific computer using any combination of the **AssetTag, UUID, SerialNumber**, and **MACAddress** properties. The table includes a **Description** column to provide a user-friendly method of describing the computer (usually the computer name).|
|Descriptions|Contains descriptions of all properties configurable via the database.|
|LocationIdentity|Used to identify geographic locations using the **Location** property. The values for this property are stored in a corresponding column in the table.|
|LocationIdentity_DefaultGateway|Relates the default gateway values with a location identified in the LocationIdentity table. There is a one-to-many relationship between this table and the LocationIdentity table.|
|MakeModelIdentity|Used to identify a specific make and model of a computer using the **Make** and **Model** properties. The values for these properties are stored in corresponding columns in the table.|
|PackageMapping|Used to associate the name presented in the Add or Remove Programs Control Panel item with a Configuration Manager package and program to be deployed in place of the application in Add or Remove Programs. For more information on this table, see the section, "Deploying Applications Based on Earlier Application Versions", in the MDT document *Microsoft Deployment Toolkit Samples Guide.*|
|RoleIdentity|Used to identify the purpose of a computer or the users of a computer using the **Role** property. The values for this property are stored in a corresponding column in the table.|
|Settings|Identifies the settings that are applied to an individual computer or a group of computers based on the settings in the Computers, Roles, Locations, and Make and Model nodes in the Database node in the Deployment Workbench.|
|Settings_Administrators|Identifies the user accounts to be added to the local Administrator group on the target computer based on the settings in the Computers, Roles, Locations, and Make and Model nodes in the Database node in the Deployment Workbench.|
|Settings_Applications|Identifies the applications to be deployed to the target computer based on the settings in the Computers, Roles, Locations, and Make and Model nodes in the Database node in the Deployment Workbench.|
|Settings_Packages|Identifies the packages to be deployed to the target computer based on the settings in the Computers, Roles, Locations, and Make and Model nodes in the Database node in the Deployment Workbench.|
|Settings_Roles|Identifies the roles to be associated with the target computer based on the settings in the Computers, Locations, and Make and Model nodes in the Database node in the Deployment Workbench.|

## Views in the MDT DB

The following table lists and describes the database views that are used when querying configuration information in the MDT DB.

|**View**|**Description**|
|-|-|
|ComputerAdministrators|Used to find all accounts to be made members of the local Administrators group on the target computer. The view is a join of the ComputerIdentity and Settings_Administrators tables.|
|ComputerApplications|Used to find all applications to be deployed to the target computer. The view is a join of the ComputerIdentity and Settings_Applications tables.|
|ComputerPackages|Used to find all packages to be deployed to the target computer. The view is a join of the ComputerIdentity and Settings_Packages tables.|
|ComputerRoles|Used to find all roles to be associated with the target computer. The view is a join of the ComputerIdentity and Settings_Roles tables.|
|ComputerSettings|Used to find all property settings to be configured for the target computer. The view is a join of the ComputerIdentity and Settings tables.|
|LocationAdministrators|Used to find all the accounts to be made a member of the local Administrators group on the target computers within a location. The view is a join of the LocationIdentity, LocationIdentity_DefaultGateway, and Settings_Administrators tables.|
|LocationApplications|Used to find all the applications to be deployed to the target computers within a location. The view is a join of the LocationIdentity, LocationIdentity_DefaultGateway, and Settings_Applications tables.|
|LocationPackages|Used to find all the packages to be deployed to the target computers within a location. The view is a join of the LocationIdentity, LocationIdentity_DefaultGateway, and Settings_Packages tables.|
|LocationRoles|Used to find all the roles to be associated with the target computers within a location. The view is a join of the LocationIdentity, LocationIdentity_DefaultGateway, and Settings_Roles tables.|
|Locations|Used to find the IP addresses for the default gateways within a location or for all the locations that contain a specified IP address for a default gateway. The view is a join of the LocationIdentity and LocationIdentity_DefaultGateway tables.|
|LocationSettings|Used to find all the property settings to be configured for the target computers within a location. The view is a join of the LocationIdentity, LocationIdentity_DefaultGateway, and Settings tables.|
|MakeModelAdministrators|Used to find all accounts to be made members of the local Administrators group on the target computers with a given make and model. The view is a join of the MakeModelIdentity and Settings_Administrators tables.|
|MakeModelApplications|Used to find all applications to be deployed to the target computers with a given make and model. The view is a join of the MakeModelIdentity and Settings_Applications tables.|
|MakeModelPackages|Used to find all packages to be deployed to the target computers with a given make and model. The view is a join of the MakeModelIdentity and Settings_Applications tables.|
|MakeModelRoles|Used to find all roles associated with the target computers with a given make and model. The view is a join of the MakeModelIdentity and Settings_Roles tables.|
|MakeModelSettings|Used to find all property settings to be configured for the target computers with a given make and model. The view is a join of the MakeModelIdentity and Settings tables.|
|RoleAdministrators|Used to find all accounts to be made members of the local Administrators group on the target computers with a given role. The view is a join of the RoleIdentity and Settings_Administrators tables.|
|RoleApplications|Used to find all applications to be deployed to the target computers with a given role. The view is a join of the RoleIdentity and Settings_Applications tables.|
|RolePackages|Used to find all packages to be deployed to the target computers with a given role. The view is a join of the RoleIdentity and Settings_Packages tables.|
|RoleSettings|Used to find all property settings to be configured for the target computers with a given role. The view is a join of the RoleIdentity and Settings tables.|

## Related articles

- [Task Sequence Steps](task-sequence-steps.md).
- [Properties](properties.md).
- [Scripts](scripts.md).
- [Support Files](support-files.md).
- [Utilities](utilities.md).
- [MDT Windows PowerShell Cmdlets](mdt-windows-powershell-cmdlets.md).
- [Windows 7 Feature Dependency Reference](windows-7-feature-dependency.md).
- [UDI Reference](udi-reference.md).