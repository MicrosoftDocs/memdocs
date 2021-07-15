---
# required metadata
title: Create a dynamic device group for all level 2 Cloud PCs - Azure | Microsoft Docs
titleSuffix:
description: Learn how to create dynamic device groups all level 2 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/18/2021
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

# Create a dynamic device group containing all level 2 Cloud PCs

You might want to apply the same set of policies to all your Cloud PCs with the same computing power (for example, all Cloud PCs from the same SKU). You can do this by creating a dynamic device group containing all level 2 Cloud PCs provisioned from a specific provisioning policy.

You can follow the below steps and create a dynamic group for any of the listed SKUs for Cloud PC. In these steps, you will use the Device Model device property to create the dynamic device group.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/) > **Groups** > **New Group**.
2. Select the **New Group** page, choose **Security** for **Group type**.
3. Enter the following:
    1. **Group name** = “All Level 2 Cloud PCs.
    2. **Group description** = “A dynamic device group containing all Level 2 Cloud PCs”.
4. For **Membership type**, choose **Dynamic Device**.
5. Select **Add dynamic query**.
6. On the **Dynamic membership rules** page, enter the following:
    1. **Property** = “deviceModel”.
    2. **Operator** = “Contains”.
    3. **Value** = “Cloud PC”.
7. Select **Add expression** and enter the following:
    1. **Property** = “deviceModel”
    2. **Operator** = “Contains”
    3. **Value** = “Level 2”
8. To validate that it works, select **Validate Rules (Preview)** > **Add devices** > select some Cloud PCs that are Level 2 , some Cloud PCs of a different level, and some non-Cloud PC devices.
9. After the validation completes, select **Save** > **Create**.



<!-- ########################## -->
## Next steps

[Create a dynamic device group containing all Cloud PCs from a specific provisioning policy](create-dynamic-device-group-from-specific-policy.md).
