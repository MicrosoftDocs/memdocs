---
# required metadata
title: Create a filter for your Cloud PCs
titleSuffix:
description: Learn how to create a filter for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/03/2021
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
# Create a filter for Cloud PCs

You can create a filter to use when creating Intune policies and configurations. The filter you create can target all or some Cloud PCs, depending on the rules you configure. You can also use the filter that you create to exclude Cloud PCs from existing policies that are intended for physical devices only. There are three different categories of filters you can create for Cloud PCs:

- [All Cloud PCs](#create-a-filter-for-all-cloud-pcs): This type of filter is useful for applying policies and configurations to all Cloud PCs in your organization.
- [All Cloud PCs from a specific provisioning policy](#create-a-filter-for-all-cloud-pcs-from-a-specific-provisioning-policy): This type of filter is useful for applying policies and configurations to Cloud PCs based on the same image and location.
- [All Cloud PCs with a specific configuration](#create-a-filter-for-all-cloud-pcs-with-a-specific-configuration): This type of filter is useful for applying policies and configurations to Cloud PCs based on computing power (vCPU and RAM) or internal storage.

## Create a filter for all Cloud PCs

In these steps, you’ll use the Model device property to create the filter.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant Administration** > **Filters**.
2. Select **Create**, then enter the following:
    1. **Filter name** = "All Cloud PCs" (or some other name indicating it will contain all Cloud PCs)
    2. **Description** = "A filter containing all Cloud PC devices"
    3. **Platform** = "Windows 10 and later"
3. On the **Rules** page, enter the following:
    1. **Property** = "model (Model)"
    2. **Operator** = "Contains"
    3. **Value** = "Cloud PC"
4. To validate that it works, select **Preview devices**.
5. After the validation completes, select **Next**.
6. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.
7. On the **Review + create** page, select **Create**.

## Create a filter for all Cloud PCs from a specific provisioning policy

For the example below, we use "UX Engineering" as the name of the provisioning policy. Anywhere you see "UX Engineering" replace it with the name of your provisioning policy.

In these steps, you’ll use the Enrollment Profile Name and Device Model device property to create the filter.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant Administration** > **Filters**.
2. Select **Create**, then enter the following:
    1. **Filter name** = "All UX Engineering Cloud PC devices"
    2. **Description** = "A filter containing all UX Engineering Cloud PC devices"
    3. **Platform** = "Windows 10 and later"
3. On the **Rules** page, enter the following:
    1. **Property** = "enrollmentProfileName (Enrollment profile name)"
    2. **Operator** = "Equals"
    3. **Value** = "UX Engineering"
4. To validate that it works, select **Preview devices**.
5. After the validation completes, select **Next**.
6. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.
7. On the **Review + create** page, select **Create**.

## Create a filter for all Cloud PCs with a specific configuration

For the example below, we use 2 vCPU and 4 GB RAM as the configuration. Anywhere you see "2vCPU/4GB" replace it with the desired configuration. You can also target a specific Cloud PC size by adding the OS storage as part of the configuration. You can follow the below steps and create a filter for any of the configurations that make up Cloud PC sizes.

In these steps, you'll use the Model device property to create the filter.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant Administration** > **Filters**.
2. Select **Create**, then enter the following:
    1. **Filter name** = "All 2vCPU/4GB RAM Cloud PCs"
    2. **Description** = "A filter containing all Cloud PCs with the 2vCPU/4GB RAM configuration"
    3. **Platform** = "Windows 10 and later"
3. On the **Rules** page, enter the following:
    1. **Property** = "model (Model)"
    2. **Operator** = "Contains"
    3. **Value** = "2vCPU/4GB"
4. To validate that it works, select **Preview devices**.
5. After the validation completes, select **Next**.
6. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.
7. On the **Review + create** page, select **Create**.

Once you've created the filter, you can use the filter in the assignment page in [supported policies](/mem/intune/fundamentals/filters-supported-workloads).

For more information on using filters in Intune, see the following how-to guides:

- [Create a filter (Intune how-to guide)](/mem/intune/fundamentals/filters)
- [Supported filter properties](/mem/intune/fundamentals/filters-device-properties)
- [Filter reporting and troubleshooting](/mem/intune/fundamentals/filters-reports-troubleshoot)

<!-- ########################## -->
## Next steps

[Create device configuration profile](create-device-configuration-profile.md).
