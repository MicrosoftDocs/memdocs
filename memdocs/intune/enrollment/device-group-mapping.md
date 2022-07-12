---
# required metadata

title: Categorize devices into groups in Intune
titleSuffix: Microsoft Intune
description: Learn how to categorize devices into groups for easier management.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/10/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7b668c37-40b9-4c69-8334-5d8344e78c24

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jieyang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# Categorize devices into groups

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Device categories allow you to easily manage and group devices in Microsoft Intune. Assign a category, such as *sales* or *accounting*, to a device and Intune will automatically add the device to the corresponding Intune device group or Active Directory security group.   

To enable categories in your tenant, you must create a category in the Microsoft Endpoint Manager admin center and set up a dynamic group for it in Azure AD. 

This article describes how to configure and edit device categories.   

## Configure device categories

You must be a Global Administrator or Intune Administrator to perform these steps.

### Step 1: Create device category in Intune  
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **Device categories**.
3. Select **Create device category** to add a new category.
4. Enter the name of the new category, such as `HR` and an optional description.
5. Select **Next**.  
6. Optionally, assign a scope tag, like `US-NC IT Team` or `JohnGlenn_ITDepartment`, to limit management of the category to specific IT groups. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).  
7. Select **Next**.  
8. Select **Create**. The new category is added to your **Device categories** list.   

You'll use the device category name when you create Azure Active Directory (Azure AD) security groups in the next step.  

### Step 2: Create Azure Active Directory security groups 

To enable automatic grouping, you must create a dynamic group using the attribute-based rules in Azure AD. For instructions, see [Using attributes to create advanced rules](/azure/active-directory/users-groups-roles/groups-dynamic-membership#using-attributes-to-create-rules-for-device-objects) in the Azure AD documentation. Create an advaced rule for your group using the **deviceCategory** attribute and the category name you created in step 1. For example: `device.deviceCategory -eq "HR"`   

### View categories of all devices 
 Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices** for a list of all devices. The **Device category** column shows the category assigned to each device. 
 
 If the **Device category** column isn't visible in the table, select **Columns**  and then choose **Category** > **Apply**.  

### Change the category of a device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. Select a device.
4. On the device details page, select **Properties**.  
5. Change your selection in the **Device category** field.  

## Best practices  
Device categories are supported on devices running Android, iOS/iPadOS, or Windows. People with Windows devices must use the Company Portal website to select their category. Regardless of platform, any device user can sign in to portal.manage.microsoft.com at anytime and go to **My devices** to select a category. 

If a device is already enrolled before you configure categories, the user will receive a notification about the device on the Company Portal website informing them to select a category the next time they access the Company Portal app on iOS/iPadOS or Android.  

You can edit a device category in the Azure portal, but you must manually update any Azure AD security groups that reference this category.  

If you delete a category, devices assigned to it display the category name **Unassigned**.  
