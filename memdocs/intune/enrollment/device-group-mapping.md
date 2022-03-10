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

#ms.reviewer: jieyang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Categorize devices into groups

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To make managing devices easier, you can use Microsoft Intune device categories to automatically add devices to groups based on categories that you define.

Device categories use the following workflow:
1. Create categories that users can choose from when they enroll their device.
2. When users of iOS/iPadOS and Android devices enroll a device, they must choose a category from the list of categories you configured. To assign a category to a Windows device, users must use the Company Portal website.
3. You can then deploy policies and apps to these groups.

You can create any device categories you want. For example:
- Point-of-sale device
- Demonstration device
- Sales
- Accounting
- Manager

## How to configure device categories

You need to be a Global Administrator or Intune Administrator to perform these steps.

### Step 1: Create device categories in Intune
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **Device categories** > **Create device category** to add a new category.
3. On the **Create device category** pane, enter a **Name** for the new category, and an optional **Description**.
4. When you are done, select **Create**. You can see the new category in the list of categories.

You'll use the device category name when you create Azure Active Directory (Azure AD) security groups in step 2.

### Step 2: Create Azure Active Directory security groups
In this step, you'll create dynamic groups in the Azure portal, based on the device category and device category name.

To continue, refer to [Using attributes to create advanced rules](/azure/active-directory/users-groups-roles/groups-dynamic-membership#using-attributes-to-create-rules-for-device-objects) in the Azure AD documentation.

Use the information in this section to create a device group with an advanced rule, by using the **deviceCategory** attribute. For example: **device.deviceCategory -eq** "*the device category name you got from the Azure portal*".

After you configure device groups, and users enroll their device, they are presented with a list of the categories you configured. After they choose a category and finish enrollment, their device is added to the Active Directory security group that corresponds with the category they chose.

### View the categories of devices that you manage

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **All devices**.

2. In the list of devices, examine the **Device category** column.

If the **Device category** column isn't shown, select **Columns** > **Category** > **Apply**.

### Change the category of a device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **All devices** > choose the device you want > **Properties**.
2. On the next blade, you can change the **Device category** of the selected device to any of the category names you previously configured.

## After you configure device groups

When users of iOS/iPadOS and Android devices enroll their device, they must choose a category from the list of categories you configured. After they choose a category and finish enrollment, their device is added to the Intune device group, or the Active Directory security group that corresponds with the category they chose.

Windows users should use the Company Portal website or the Company Portal app to select a category.

Regardless of platform, your users can always go to portal.manage.microsoft.com after enrolling the device. Have the user access the Company Portal website, and go to **My Devices**. The user can choose an enrolled device listed on the page, and then select a category.

After choosing a category, the device is automatically added to the corresponding group you created. If a device is already enrolled before you configure categories, the user sees a notification about the device on the Company Portal website. This lets the user know to select a category the next time they access the Company Portal app on iOS/iPadOS or Android.

## Further information
- You can edit a device category in the Azure portal, but you must manually update any Azure AD security groups that reference this category.

- If you delete a category, devices assigned to it display the category name **Unassigned**.
