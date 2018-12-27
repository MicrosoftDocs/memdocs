---
title: Prepare Intune for user migration
titleSuffix: Configuration Manager
description: Learn how to prepare Intune on Azure for user migration from hybrid MDM.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
---

# Prepare Intune for user migration 

*Applies to: System Center Configuration Manager (Current Branch)*    

Before you migrate users from hybrid MDM to Intune standalone, take steps to prepare Intune. These steps help to make sure that your migrated users and their devices continue to be managed. When you complete these steps and start the migration to Intune, there's no signifcant impact to your users.  

## Fix issues found during data collection and import
If you used the Intune Data Importer tool to [import Configuration Manager data to Microsoft Intune](migrate-import-data.md), it summarized the objects that it couldn't import. Some of the typical issues, and steps to fix them in Intune, are listed in the following table: 

|Issue  |Fix  |
|---------|---------|
|Collections based on direct membership or on a complex aren't automatically migrated.|Create Azure Active Directory (Azure AD) groups in Azure to replace the collection that wasn't imported. Then, assign the object to the group.|
|Policies weren't importable |Recreate the policy in Intune.|
|Deployment for an object not imported|Assign the object to the group. The group should include the same users from the collection for the deployment.|

## Create Intune objects 
If you [imported Configuration Manager data to Microsoft Intune](migrate-import-data.md) and fixed issues during the process, verify the imported objects are correctly configured. Also create any additional objects (policies, profiles, and apps) in Intune that you need in your organization. 

## Assign Intune licenses to migrated users
In Configuration Manager, you add a collection to the Intune subscription and the members of the collection can enroll their devices. While an Intune license is reserved for enrolled devices, these licenses aren't associated with the user or device. For example, you wouldn't find an Intune license in Azure AD for a user that has an enrolled device. 

In Intune standalone, configure an Intune license for each user. Configure the license *before* you migrate a user to Intune standalone. This action makes sure that the user and their devices are managed by Intune after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign). 

## Verify Intune user groups
Your users and groups are likely already in Azure AD because you have directory synchronization configured. To make sure that your users are part of the correct user group, we recommend that you review your Intune user groups. You target policies, profiles, and apps to these groups. Make sure the users you migrate to Intune standalone are part of the correct groups. 

## Configure role-based administration control (RBAC)
As part of the migration, configure all the necessary RBAC roles in Intune and assign users to those roles. There are differences between RBAC in Configuration Manager and Intune, such as scoping of resources. For more information, see
[Role-based administration control (RBAC) with Intune](https://docs.microsoft.com/intune/role-based-access-control).

## Assign apps and policies to AAD groups
If you [imported Configuration Manager data to Microsoft Intune](migrate-import-data.md), many of your objects might already be assigned to Azure AD groups. Verify that all objects (apps, policies, and profiles) are assigned to the correct Azure AD groups. If you assign objects correctly, user’s devices are automatically configured after the user is migrated and the migration should be transparent to users. For more information about assigning the objects to an Azure AD group, see the following articles: 
- [Assign policies](https://docs.microsoft.com/intune/get-started-policies) 
- [Assign profiles](https://docs.microsoft.com/intune/device-profile-assign) 
- [Assign apps](https://docs.microsoft.com/intune/get-started-apps) 

## Terms and conditions policy
Just like other tenant-level policies, terms and conditions policies are automatically migrated to Intune once mixed authority is enabled for your tenant.  However, you must assign the terms and conditions to a group that contains migrated users to accurately report on acceptance for migrated users and make sure that the terms and conditions are properly targeted for future terms and conditions updates or device enrollments. Users don't have to reaccept the terms and conditions unless there are changes made to the policy in the Configuration Manager console. For more information, see [Assign terms and conditions](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## Configure the Exchange Connector
If you use Exchange and have an on-premises Exchange Connector in Configuration Manager, you need to [configure the on-premises Exchange Connector in Intune](https://docs.microsoft.com/intune/exchange-connector-install). Also consider the information in the following sections to help you migrate to the Intune Exchange Connector and to make sure conditional access works properly after migration.

### PowerShell scripts to help you migrate to the Intune Exchange Connector 
PowerShell scripts are available to help you prepare to transition your Exchange devices from the Configuration Manager Exchange Connector to the Intune Exchange Connector. While running these scripts are optional, we recommend that you run them to remove inactive devices from Exchange, which prevents Intune from discovering unnecessary devices. Running the scripts ensure that devices discovered through Exchange can merge with devices enrolled with Intune as smoothly as possible. Run these scripts prior to setting up the Intune Exchange Connector. The PowerShell scripts are part of the Intune Data Importer installation that you use to [import Configuration Manager data to Microsoft Intune](migrate-import-data.md) in the next article. For details and to download the scripts, go to [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer) GitHub page.

### Steps to make sure conditional access works properly after user migration
For conditional access to work properly after you migrate users, and to make sure that your users continue to have access to their email server, make sure the following configurations are set:
- If the Exchange ActiveSync default access level setting (DefaultAccessLevel) is set to Block or Quarantine, devices might lose access to email. 
- If the Exchange Connector is installed in Configuration Manager and the **Access level when a mobile device is not managed by a rule** setting has a value of **Allow access**, install the [On-premises Exchange connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) in Intune before you migrate users. Configure the default access level setting in Intune on the **Exchange on-premises** page in **Advanced Exchange ActiveSync access settings**. For more information, see [Configure Exchange on-premises access](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Use the same configuration for both connectors. The last connector that you configure overwrites the ActiveSync organization settings previously written by the other connector. If you configure the connectors differently, it could result in unexpected conditional access changes.
- Remove users from conditional access targeting in Configuration Manager once they are migrated to Intune standalone.

## Configure the Microsoft Intune Certificate Connector
If you use NDES to issue certificates using SCEP, you need to configure the Microsoft Intune Certificate Connector. The computer that hosts the NDES connector in Intune can't be the same computer that hosts the NDES connector in Configuration Manager. For more information, see [Configure and manage SCEP certificates with Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> After you configure the connector, modify imported SCEP profiles to reference the new server URL.

## Next step
After you prepare Intune for migration, you're ready to migrate a set of test users to Intune standalone. For more information, see [Change the MDM authority for specific users (mixed authority)](migrate-mixed-authority.md).


