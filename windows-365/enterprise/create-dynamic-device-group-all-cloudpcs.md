---
# required metadata
title: Create a dynamic device group containing your Cloud PCs
titleSuffix:
description: Learn how to create dynamic device groups containing your Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/09/2023
ms.topic: how-to
ms.service: windows-365
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
ms.collection:
- M365-identity-device-management
- tier1
---

# Create a dynamic device group containing your Cloud PCs

You can create a dynamic device group that contains your Cloud PCs. Policies targeting this device group will target all or some Cloud PCs, depending on the rules you configure. There are three different categories of groups you can create for Cloud PCs:

- [All Cloud PCs](#create-a-dynamic-device-group-for-all-cloud-pcs): This type of group is useful for applying policies and configurations to all Cloud PCs in your organization.
- [All Cloud PCs from a specific provisioning policy](#create-a-dynamic-device-group-for-all-cloud-pcs-from-a-specific-provisioning-policy): This type of group is useful for applying policies and configurations to Cloud PCs based on the same image and location.
- [All Cloud PCs with a specific configuration](#create-a-dynamic-device-group-for-all-cloud-pcs-with-a-specific-configuration): This type of group is useful for applying policies and configurations to Cloud PCs based on computing power (vCPU and RAM) or internal storage.

## Create a dynamic device group for all Cloud PCs

In these steps, you’ll use the Device Model device property to create the dynamic device group.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Groups** > **New Group**.
![Screenshot of delete policy](./media/create-dynamic-device-group-all-cloudpcs/create-group.png)
2. Select **Security** for **Group type**.
3. Enter the following information:
    1. **Group name** = "All Cloud PCs" (or some other name indicating it will contain all Cloud PCs).
    2. **Group description** = "A dynamic device group containing all Cloud PC devices"
4. For **Membership type**, choose **Dynamic Device**.
5. Select **Add dynamic query**.
6. On the **Dynamic membership rules** page, enter the following:
    1. **Property** = "deviceModel"
    2. **Operator** = "Contains"
    3. **Value** = "Cloud PC"
7. To validate that it works, select **Validate Rules (Preview)** > **+Add devices** > select some Cloud PCs and non-Cloud PC devices.
8. After the validation completes, select **Save** > **Create**.

## Create a dynamic device group for all Cloud PCs from a specific provisioning policy

For the example below, we use "UX Engineering" as the name of the provisioning policy. Anywhere you see "UX Engineering" replace it with the name of your provisioning policy.

In these steps, you’ll use the Enrollment Profile Name device property to create the dynamic device group.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Groups** > **New Group**.
![Screenshot of delete policy](./media/create-dynamic-device-group-all-cloudpcs/create-group.png)
2. Select **Security** for **Group type**.
3. Enter the following information:
    1. **Group name** = "All UX Engineering Cloud PC devices"
    2. **Group description** = "A dynamic device group containing all UX Engineering Cloud PC devices."
4. For **Membership type**, choose **Dynamic Device**.
5. Select **Add dynamic query**.
6. On the **Dynamic membership rules** page, enter the following:
    1. **Property** = "enrollmentProfileName"
    2. **Operator** = "Equals"
    3. **Value** = "UX Engineering"
7. To validate that it works, select **Validate Rules (Preview)** > **Add devices** > select some Cloud PCs that were provisioned from the "UX Engineering" provisioning policy, some Cloud PCs that were provisioned from a different provisioning policy, and some non-Cloud PCs.
8. After the validation completes, select **Save** > **Create**.

## Create a dynamic device group for all Cloud PCs with a specific configuration

For the example below, we use 2 vCPU and 4-GB RAM as the configuration. Anywhere you see "2vCPU/4GB" replace it with the desired configuration. You can also target a specific Cloud PC size by adding the OS storage as part of the configuration. You can follow the below steps and create a filter for any of the configurations that make up Cloud PC sizes.

In these steps, you'll use the Device Model device property to create the dynamic device group.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Groups** > **New Group**.
![Screenshot of delete policy](./media/create-dynamic-device-group-all-cloudpcs/create-group.png)
2. Select **Security** for **Group type**.
3. Enter the following information:
    1. **Group name** = “All 2vCPU/4GB RAM Cloud PCs".
    2. **Group description** = “A dynamic device group containing all Cloud PCs with the 2vCPU/4GB RAM configuration.
4. For **Membership type**, choose **Dynamic Device**.
5. Select **Add dynamic query**.
6. On the **Dynamic membership rules** page, enter the following:
    1. **Property** = “deviceModel”
    2. **Operator** = “Contains”
    3. **Value** = “Cloud PC”
7. Select **Add expression** and enter the following:
    1. **Property** = “deviceModel”
    2. **Operator** = “Contains”
    3. **Value** = “2vCPU/4GB”
8. To validate that it works, select **Validate Rules (Preview)** > **Add devices** > select some Cloud PCs that have the 2vCPU/4GB RAM configuration, some Cloud PCs that have a different configuration, and some non-Cloud PC devices.
9. After the validation completes, select **Save** > **Create**.

<!-- ########################## -->
## Next steps

[Create a filter](create-filter.md).
