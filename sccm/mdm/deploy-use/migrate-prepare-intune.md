---
# required metadata

title: Prepare Intune for user migration 
description:
keywords:
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service:
ms.technology:
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4

---

# Prepare Intune for user migration 

*Applies to: System Center Configuration Manager (Current Branch)*

Before you migrate users from hybrid MDM (Intune integrated with Configuration Manager) to Intune standalone, you must take steps to prepare Intune. These steps will help to ensure that your migrated users and their devices will continue to be managed. When you complete these steps and start the migration to Intune, it should be transparent to your users.  

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
Your users and groups are likely already in AAD because you have directory synchronization configured. To make sure that your users are part of the correct user group, we recommend that you review your Intune user groups. You will target policies, profiles, apps, etc. to these groups. Make sure the users you migrate to Intune standalone are part of the correct groups. 

## Configure role-based administration control (RBAC)
As part of the migration, configure all the necessary RBAC roles in Intune and assign users to those roles. Note that there are differences between RBAC in Configuration Manager and Intune, such as scoping of resources. For details, see
[Role-based administration control (RBAC) with Intune](https://docs.microsoft.com/en-us/intune/role-based-access-control).

## Target apps and policies to AAD groups
If you went through the [Import Configuration Manager data to Microsoft Intune](migrate-import-data.md) phase of the migration process to migrate different Configuration Manager objects to Intune, many of your objects might already be assigned to AAD groups. However, you should verify that all objects (apps, policies, profiles, etc.) are assigned to the correct AAD groups. If you assign objects correctly, user’s devices are automatically configured after the user is migrated and the migration should be transparent to users. For more information about assigning the objects to an AAD group, see the following: 
- [Assign policies](https://docs.microsoft.com/intune/get-started-policies) 
- [Assign profiles](https://docs.microsoft.com/intune/device-profile-assign) 
- [Assign apps](https://docs.microsoft.com/intune/get-started-apps) 

## Configure the Exchange Connector
If you use Exchange and have an Exchange Connector in Configuration Manager, you need to configure the on-premises Exchange Connector in Intune. The computer that will host the connector for the Exchange Connector in Intune cannot be the same computer that hosts the Exchange Connector in Configuration Manager. For details, see [Set up the Intune on-premises Exchange Connector in Microsoft Intune Azure](https://docs.microsoft.com/intune/exchange-connector-install)

> [!Important]    
> For conditional access to work properly after you migrate users, and to ensure that your users continue to have access to their email server, you must perform the following steps:
> 1. Configure the default access level for your Exchange connectors to **Allow**. Or, you can decide not to configure the default access level for the connectors in both Intune and Configuration Manager.    
>    
>     Devices may lose access to Exchange if the default access level for your Exchange connector is configured as **Block** or **Quarantine** and you configure the Intune Exchange Connector.
> 2. Use the same configuration for both connectors. The last connector that you configure overwrites the ActiveSync organization settings previously written by the other connector. Configuring the connectors differently could result in unexpected conditional access changes.
> 3. Remove users from conditional access targeting in Configuration Manager once they are migrated to Intune standalone.

## Configure the Microsoft Intune Certificate Connector
If you use NDES to issue certificates using SCEP, you need to configure the Microsoft Intune Certificate Connector. The computer that hosts the NDES connector in Intune cannot be the same computer that hosts the NDES connector in Configuration Manager. For details, see [Configure and manage SCEP certificates with Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> After you configure the connector, you must modify imported SCEP profiles to reference the new server URL.

## Next step
After you prepare Intune for migration, you are ready to migrate a set of test users to Intune standalone. For details, see [Change the MDM authority for specific users (mixed authority)](migrate-mixed-authority.md).


