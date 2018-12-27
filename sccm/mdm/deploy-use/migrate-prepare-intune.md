---
title: Prepare Intune for user migration
titleSuffix: "Configuration Manager"
description: Learn how to prepare Intune on Azure for user migration from hybrid MDM.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
---

# Prepare Intune for user migration 

*Applies to: System Center Configuration Manager (Current Branch)*    

Before you migrate users from hybrid MDM (Intune integrated with Configuration Manager) to Intune standalone, you must take steps to prepare Intune. These steps help to ensure that your migrated users and their devices continue to be managed. When you complete these steps and start the migration to Intune, there is no signifcant impact to your users.  

## Fix issues found during data collection and import
If you went through the process to [import Configuration Manager data to Microsoft Intune](migrate-import-data.md), the Intune Data Importer tool provided you with a summary of all the objects that it was not able to import. Some of the typical issues that you likely ran across, as well as steps you can take to fix the issue in Intune, are listed in the following table: 

|Issue  |Fix  |
|---------|---------|
|Collections based on direct membership or on a complex are not be migrated automatically.|You must create Azure Active Directory (AAD) groups in Azure to replace the collection that was not imported. Then, you must assign the object to the group.|
|Policies were not importable |You must recreate the policy in Intune.|
|Deployment for an object not imported|You must assign the object to the group. The group should contain the same users from the collection for the deployment.|

## Create Intune objects 
If you went through the process to [import Configuration Manager data to Microsoft Intune](migrate-import-data.md) and fixed issues during the import process, you should verify the imported objects are correctly configured. In addition, create any additional objects (policies, profiles, apps, etc.) in Intune that you need in your organization. 

## Assign Intune licenses to migrated users
In Configuration Manager, you add a collection to the Intune subscription and the members of the collection have the ability to enroll their devices. While an Intune license is reserved for enrolled devices, these licenses are not specifically associated with the user or device. For example, you wouldn't find an Intune license in AAD for a user that has an enrolled device. However, in Intune standalone you must configure an Intune license for each user. You must do this BEFORE you migrate a user to Intune standalone to ensure that the user and their devices are managed by Intune after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign). 

## Verify Intune user groups
Your users and groups are likely already in AAD because you have directory synchronization configured. To make sure that your users are part of the correct user group, we recommend that you review your Intune user groups. You target policies, profiles, apps, etc. to these groups. Make sure the users you migrate to Intune standalone are part of the correct groups. 

## Configure role-based administration control (RBAC)
As part of the migration, configure all the necessary RBAC roles in Intune and assign users to those roles. Note that there are differences between RBAC in Configuration Manager and Intune, such as scoping of resources. For details, see
[Role-based administration control (RBAC) with Intune](https://docs.microsoft.com/intune/role-based-access-control).

## Assign apps and policies to AAD groups
If you went through the [Import Configuration Manager data to Microsoft Intune](migrate-import-data.md) phase of the migration process to migrate different Configuration Manager objects to Intune, many of your objects might already be assigned to AAD groups. However, you should verify that all objects (apps, policies, profiles, etc.) are assigned to the correct AAD groups. If you assign objects correctly, user’s devices are automatically configured after the user is migrated and the migration should be transparent to users. For details about assigning the objects to an AAD group, see the following: 
- [Assign policies](https://docs.microsoft.com/intune/get-started-policies) 
- [Assign profiles](https://docs.microsoft.com/intune/device-profile-assign) 
- [Assign apps](https://docs.microsoft.com/intune/get-started-apps) 

## Terms and conditions policy
Just like other tenant-level policies, terms and conditions policies are automatically migrated to Intune once mixed authority is enabled for your tenant.  However, you must assign the terms and conditions to a group that contains migrated users to accurately report on acceptance for migrated users and ensure that the terms and conditions are properly targeted for future terms and conditions updates or device enrollments. Users do not have to re-accept the terms and conditions unless there are changes made to the policy in the Configuration Manager console. For details, see [Assign terms and conditions](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## Configure the Exchange Connector
If you use Exchange and have an on-premises Exchange Connector in Configuration Manager, you need to [configure the on-premises Exchange Connector in Intune](https://docs.microsoft.com/intune/exchange-connector-install). Also consider the information in the following sections to help you migrate to the Intune Exchange Connector and to ensure conditional access work properly after migration.

### PowerShell scripts to help you migrate to the Intune Exchange Connector 
PowerShell scripts are available to help you prepare to transition your Exchange devices from the Configuration Manager Exchange Connector to the Intune Exchange Connector. While running these scripts are optional, we recommend that you run them to remove inactive devices from Exchange, which prevents Intune from discovering unnecessary devices. Running the scripts ensure that devices discovered through Exchange can merge with devices enrolled with Intune as smoothly as possible. Run these scripts prior to setting up the Intune Exchange Connector. The PowerShell scripts are part of the Intune Data Importer installation that you use to [import Configuration Manager data to Microsoft Intune](migrate-import-data.md) in the next article. For details and to download the scripts, go to [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer) GitHub page.

### Steps to ensure conditional access works properly after user migration
For conditional access to work properly after you migrate users, and to ensure that your users continue to have access to their email server, ensure the following is true:
- If the Exchange ActiveSync default access level setting (DefaultAccessLevel) is set to Block or Quarantine, devices might lose access to email. 
- If the Exchange Connector is installed in Configuration Manager and the **Access level when a mobile device is not managed by a rule** setting has a value of **Allow access**, you must install the [On-premises Exchange connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) in Intune before you migrate users. Configure the default access level setting in Intune on the **Exchange on-premises** blade in **Advanced Exchange ActiveSync access settings**. For details, see [Configure Exchange on-premises access](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Use the same configuration for both connectors. The last connector that you configure overwrites the ActiveSync organization settings previously written by the other connector. If you configure the connectors differently, it could result in unexpected conditional access changes.
- Remove users from conditional access targeting in Configuration Manager once they are migrated to Intune standalone.

## Configure the Microsoft Intune Certificate Connector
If you use NDES to issue certificates using SCEP, you need to configure the Microsoft Intune Certificate Connector. The computer that hosts the NDES connector in Intune cannot be the same computer that hosts the NDES connector in Configuration Manager. For details, see [Configure and manage SCEP certificates with Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> After you configure the connector, you must modify imported SCEP profiles to reference the new server URL.

## Next step
After you prepare Intune for migration, you are ready to migrate a set of test users to Intune standalone. For details, see [Change the MDM authority for specific users (mixed authority)](migrate-mixed-authority.md).


