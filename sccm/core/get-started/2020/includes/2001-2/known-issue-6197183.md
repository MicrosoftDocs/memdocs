---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 02/03/2020
---

### <a name="ki_coll"></a> Can't create or edit some collections

<!--6197183-->
In this version of the technical preview branch, you can't create a new collection. You also can't edit the properties of an existing user collection.

To work around this issue, use Configuration Manager PowerShell cmdlets to create new collections and edit existing user collections. Some of the available cmdlets for managing collections include:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
