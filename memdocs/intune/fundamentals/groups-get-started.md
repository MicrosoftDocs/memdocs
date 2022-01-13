---
# required metadata

title: Intune classic groups in the Azure portal
titleSuffix: Microsoft Intune
description: Learn what's new with groups in the Microsoft Intune Azure portal.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 03/31/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 323f384d-8a76-4adc-999b-e508d641bfa1

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: scottduf
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Intune classic groups in the Azure portal

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

We've heard your feedback and have made changes to how you work with groups in Microsoft Intune.
If you are using Intune from the Azure portal, your Intune groups have been migrated to Azure Active Directory security groups.

The benefit to you is that you now use the same groups experience across all of your Enterprise Mobility + Security, and Azure AD apps. Additionally, you can use PowerShell and Graph API to extend and customize this new functionality.

Azure AD security groups support all types of Intune deployments to both users and devices. Additionally, you can use Azure AD dynamic groups that automatically update based on the attributes you supply. For example, you could create a group of devices that run iOS 9. Whenever a device running iOS 9 enrolls, the device automatically appears in the dynamic group.

## What is not available?

Some of the Intune groups capabilities you previously might have used are not available in Azure AD:

- The **Ungrouped Users** and **Ungrouped Devices** Intune groups are no longer available.
- The option to **Exclude specific members** from a group does not exist in the Azure portal. You can, however, use an Azure AD security group with advanced rules to replicate this behavior. For example, to create an advanced rule that includes all people in your Sales department in a security group, but excludes those groups with the word "Assistant" in their title, you could use this advanced rule:

  `(user.department -eq "Sales") -and -not (user.jobTitle -contains "Assistant")`.
- The **All Exchange ActiveSync Managed Devices** group in the Intune classic console was not migrated to Azure AD. You can, however, still access information about EAS-managed devices from the Azure portal.

## How to get started?

- Read the following topics to learn about Azure AD security groups and how they work:
  - [Managing access to resources with Azure Active Directory groups](/azure/active-directory/fundamentals/active-directory-manage-groups).
  - [Managing groups in Azure Active Directory](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal).
  - [Using attributes to create advanced rules](/azure/active-directory/users-groups-roles/groups-dynamic-membership).
- Ensure that admins who need to create groups are added to the **Intune Service Administrator** Azure AD role. The Azure AD Service Admin role does not have **Manage Group** permissions.
- If your Intune groups used the **Exclude specific members**  option, decide whether you can redesign these groups without exclusions, or if you need advanced rules to meet business needs.


## What happened to Intune groups?
When groups are migrated from the Azure portal to Intune in the Azure portal, the following rules are applied:

| Groups in Intune|Groups in Azure AD|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|Static user group|Static Azure AD security group|
|Dynamic user group|Static Azure AD security groups with an Azure AD security group hierarchy|
|Static device group|Static Azure AD security group|
|Dynamic device group|Dynamic Azure AD security group|
|A group with an include condition|Static Azure AD security group containing any static or dynamic members from the include condition in Intune|
|A group with an exclude condition|Not migrated|
|The built-in groups:<br>- **All Users**<br>- **Ungrouped Users**<br>- **All Devices**<br>- **Ungrouped devices**<br>- **All Computers**<br>- **All Mobile Devices**<br>- **All-MDM managed devices**<br>- **All EAS-managed devices**|Azure AD security groups|

## Group hierarchy

In the Intune console, all groups had a parent group. Groups could only contain members of their parent group. In Azure AD, child groups can contain members not in their parent group.

## Group attributes
Attributes are device properties that may be used in defining groups. This table describes how those criteria migrate to Azure AD security groups.

| Attribute in Intune|Attribute in Azure AD|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|Organizational Unit (OU) attribute for device groups|OU attribute for dynamic groups.|
|Domain name attribute for device groups|Domain Name attribute for dynamic groups.|
|Security group as an attribute for user groups|Groups cannot be attributes in Azure AD dynamic queries. Dynamic groups can only contain user or device-specific attributes.|
|Manager attribute for user groups|Advanced Rule for *manager* attribute in dynamic groups|
|All users from the parent user group|Static group with that group as a member|
|All mobile devices from the parent device group|Static group with that group as a member|
|All mobile devices managed by Intune|Management Type attribute with 'MDM' as value for dynamic group|
|Nested groups within static groups |Nested groups within static groups|
|Nested groups within dynamic groups|Dynamic group with one level of nesting|

## What happens to policies and apps you previously deployed?

Policies and apps continue to be deployed to groups, just like before. However, you now manage these groups from the Azure portal, instead of the Intune console.