---
# required metadata
title: Create device configuration profile for Windows 365
titleSuffix:
description: Learn how to create device configuration profile for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Create device configuration profile

In this example, we’ll apply a **Device restrictions** [device configuration profile](/mem/intune/configuration/device-profile-create) and apply it to **All Cloud PCs**. You'll need either a dynamic device group or a filter to accomplish this task.

> [!NOTE]
> If you haven’t already, follow the steps to either [create a dynamic device group containing all Cloud PCs](create-dynamic-device-group-all-cloudpcs.md#create-a-dynamic-device-group-for-all-cloud-pcs) or [create a filter for all Cloud PCs](create-filter.md#create-a-filter-for-all-cloud-pcs), then return here to create the device configuration profile.

Now that you’ve created a dynamic device group or a filter for all Cloud PCs, you can target policies to apply to all Cloud PCs in the tenant. To do so, follow these steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** > **Create profile**.
![Screenshot of delete policy](./media/create-device-configuration-profile/create-profile.png)
2. On the **Create profile** page, select:
   - **Platform** = **Windows 10 and later**.
   - **Profile Type** = **Templates**, then select **Device restrictions**.
3. Select **Create**.
4. Enter a **Name** for the configuration profile, like "All Cloud PCs – Device restrictions" and a useful **Description**.
5. Select **Next**.
6. On the **Configuration settings** page, select the settings and restrictions that you want applied by this profile.
7. Select **Next**.
8. On the **Assignments** page, choose the following selections based on if you're using a dynamic device group or a filter:
   
   a. **Dynamic device group**: Select **Add groups** > search for and select the dynamic device group for all Cloud PCs > **Select**.
   
   b. **Filter**: Select an existing user group, **Edit filter** > **Include filtered devices in assignment** > search for and select the filter for all Cloud PCs.
   
   c. **Filter**: Select **Add all devices** or **Add all users**, **Edit filter** > **Include filtered devices in assignment** > search for and select the filter for all Cloud PCs.
   
9. Choose **Select** > **Next**.
10. On the **Applicability Rules** page, select **Next**.
11. On the **Review + create** page, review the settings. You’ll see all the settings you selected along with the assignment to “All Cloud PCs”.
12. Select **Create** to deploy the profile.

<!-- ########################## -->
## Next steps

[Assign a user as a local admin](assign-users-as-local-admin.md).
