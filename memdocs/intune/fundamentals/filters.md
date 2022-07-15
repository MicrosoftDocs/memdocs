---
# required metadata

title: Create filters in Microsoft Intune
description: Learn more about policy assignment filters, and see the steps to create, update, or delete a filter in Microsoft Endpoint Manager and Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/26/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager

When you create a policy, you can use filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy. For example, use filters to target devices with a specific OS version or a specific manufacturer, target only personal devices or only organization-owned devices, and more.

For example, you can use filters in the following scenarios:

- Deploy a Windows device restriction policy to only the corporate devices in the Marketing department, while excluding personal devices.
- Deploy an iOS/iPadOS app to only the iPad devices in the Finance users group.
- Deploy an Android mobile phone compliance policy to all users in the company, and exclude Android meeting room devices that don't support the mobile phone compliance policy settings.

Filters include the following features and benefits:

- Improve flexibility and granularity when assigning Intune policies and apps.
- Are used when assigning app, policies, and profiles. They dynamically target devices based on device properties you enter.
- Can include or exclude devices in a specific group based on criteria you enter.
- Create a query of device properties based on the device platform, including Android, iOS/iPadOS, macOS, and Windows client.
- Can be used and reused in multiple scenarios in “Include” or “Exclude” mode.

This feature applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10/11


This article describes the filter architecture, and shows you how to create, update, and delete a filter.

## How filters work

:::image type="content" source="./media/filters/admin-creates-filter.png" alt-text="Admin creates a filter, and uses the filter in a policy in Microsoft Endpoint Manager and Microsoft Intune." lightbox="./media/filters/admin-creates-filter.png":::

Before a policy is applied to a device, filters dynamically evaluate applicability. Looking at the image, here's an overview:

1. You create a reusable filter for any platform based on some device properties. In the example, the filter is for personal devices.

2. You assign a policy or app to the group. In the assignment, you add the filter in include or exclude mode. For example, you "include" personal devices, or you "exclude" personal devices from the policy.

3. The filter is evaluated when the device enrolls, checks in with the Intune service, or at any other time a policy evaluates.

4. You see the filter results based on the evaluation. For example, the app or policy applies, or they don't apply.

## Prerequisites

- Sign in as an Intune administrator. For more information on Intune roles, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Create a filter

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters** > **Create**.

    You can also create filters in:

    - **Devices** > **Filters**
    - **Apps** > **Filters**

3. In **Basics**, enter the following properties:

    - **Filter name**: Enter a descriptive name for the filter. Name your filters so you can easily identify them later. For example, a good filter name is **Windows OS version filter**.
    - **Description**: Enter a description for the filter. This setting is optional, but recommended.
    - **Platform**: Select your platform. Your options:
      - Android device administrator
      - Android Enterprise
      - iOS/iPadOS
      - macOS
      - Windows 10 and later

4. Select **Next**.
5. In **Rules**, there are two ways to create a rule: Use the **rule builder**, or use the **rule syntax**.

    **Rule builder**:

    - **And/Or**: After you add an expression, you can add to the expression using the `and` or `or` options.
    - **Property**: Select a property for your rule, such as device or operating system SKU.
    - **Operator**: Select the operator from the list, such as `equals` or `contains`.
    - **Value**: Enter the value in your expression. For example, enter `10.0.18362` for the OS version, or `Microsoft` for the manufacturer.
    - **Add expression**: After you add the property, operator, and value, select **Add expression**:

      :::image type="content" source="./media/filters/rule-builder-example.png" alt-text="Use the rule builder in Microsoft Endpoint Manager and Microsoft Intune to create an expression filter, and assign to your policies.":::

      The expression you created is automatically added to the rule syntax editor.

    **Rule syntax**:

    You can also manually enter your rule expression, and write your own rules in the rule syntax editor. In **Rule syntax**, select **Edit**:

    :::image type="content" source="./media/filters/rule-syntax-edit.png" alt-text="Select rule syntax edit to use the rule builder in Microsoft Endpoint Manager and Microsoft Intune.":::

    The expression builder opens. Manually enter expressions, such as `(device.osVersion -eq "10.0.18362") and (device.manufacturer -eq "Microsoft")`:

    :::image type="content" source="./media/filters/rule-syntax-example.png" alt-text="Use the expression builder to enter your rule syntax in Microsoft Endpoint Manager and Microsoft Intune.":::

    For more information on writing your own expressions, see [Device properties, operators, and rule editing when creating filters](filters-device-properties.md).

    Select **OK** to save your expression.

    > [!TIP]
    > 
    > - When you create a rule, it's validated for the correct syntax, and any errors are shown.
    > - If you enter syntax that's not supported by the basic rule builder, then the rule builder is disabled. For example, using nested parenthesis disables the basic rule builder.

6. Select **Preview devices**. A list of enrolled devices that match your filter criteria is shown.

    In this list, you can also search for devices by the device name, OS version, device model, device manufacturer, the user principal name of the primary user, and device ID:

    :::image type="content" source="./media/filters/preview-search.png" alt-text="In preview devices, search for devices when creating a filter in Microsoft Endpoint Manager and Microsoft Intune.":::

7. Select **Next**.
8. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

9. In **Review + create**, review your settings. When you select **Create**, your changes are saved. The filter is created, and ready to be used. The filter is also shown in the filters list.

## Use a filter

After the filter is created, it's ready to use when assigning your apps or policies.

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to your apps, compliance policies, or configuration profiles. For a list of what's supported, see [Supported workloads when creating filters](filters-supported-workloads.md). Select an existing policy, or create a new policy.

    For example, select **Devices** > **Compliance policies**, and select an existing policy. Select **Properties** > **Assignments** > **Edit**:

    :::image type="content" source="./media/filters/edit-compliance-policy-assignment.png" alt-text="Select a policy or profile, and edit the assignment in Microsoft Endpoint Manager and Microsoft Intune.":::

3. Assign your policy to a users group or a devices group.
4. Select **Edit filter**. Your options:

    - **Do not apply a filter**: All targeted users or devices receive the app or policy without filtering.
    - **Include filtered devices in assignment**: Devices that match the filter conditions receive the app or policy. Devices that don't match the filter conditions don't receive the app or policy.

      A list of filters that match the policy platform is shown.

    - **Exclude filtered devices in assignment**: Devices that match the filter conditions don't receive the app or policy. Devices that don't match the filter conditions receive the app or policy.

      A list of filters that match the policy platform is shown.

5. Select your filter > **Select**.

    For example, select **Include filtered devices in assignment**, and select the filter:

    :::image type="content" source="./media/filters/add-filter-compliance-policy.png" alt-text="Include the filter when assigning a policy in Microsoft Endpoint Manager and Microsoft Intune.":::

6. To save your changes, select **Review + save** > **Save**.

When the device checks in with the Intune service, the properties defined in the filter are evaluated, and determine if the app or policy should be applied.

## Change an existing filter

After a filter is created, it can be changed or updated.

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters**. A list of all the filters is shown.

    You can also update filters in **Devices** > **Filters**, or **Apps** > **Filters**.

3. Select the filter you want to change. Select **Rules** > **Edit**, and make your changes:

    :::image type="content" source="./media/filters/update-existing-filter.png" alt-text="Change or update an existing filter in Microsoft Endpoint Manager and Microsoft Intune.":::

4. To save your changes, select **Review + save** > **Save**.

## Delete a filter

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters**. A list of all the filters is shown.

    You can also delete filters in **Devices** > **Filters**, or **Apps** > **Filters**.

3. Next to the filter, select the ellipses (**...**), and select **Delete**:

    :::image type="content" source="./media/filters/delete-filter.png" alt-text="Delete a filter in Microsoft Endpoint Manager and Microsoft Intune.":::

To delete a filter, you must remove the filter from any policy assignments. Otherwise, when trying to delete the filter, you'll get the following error:

`Unable to delete assignment filter – An assignment filter is associated with existing assignments. Delete all the assignments for the filter and try again.`

## Next steps

- [Device properties, operators, and rule editing when creating filters](filters-device-properties.md)
- [Supported workloads when creating filters](filters-supported-workloads.md)
- [Filter reports and troubleshooting](filters-reports-troubleshoot.md)
