---
# required metadata

title: Create filters in Microsoft Intune - Azure | Microsoft Docs
description: Learn more about policy assignment filters, and see the steps to create, update, or delete a filter in Microsoft Endpoint Manager and Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/04/2021
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

Filters provide improved flexibility for assigning Intune workloads. You can use filters in policy and app assignments to dynamically refine targeting based on device properties.

Filters allow admins to include or exclude devices in a specific group based on a set of admin-defined criteria. 

Allows admins to define a query of device properties based on platform. 

Once created, a filter can be used in multiple scenarios as a re-usable entity in either an “Include” or “Exclude” mode. 

This feature applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and newer

## Example scenarios 

Filters can be used by IT admins for several scenarios. Here are a few examples: 

- Deploy a Windows 10 device restriction policy to just the corporate devices of users in the Marketing department while excluding personal devices.

- Deploy an iOS app to only the iPad devices for users in the Finance group.

- Deploy an Android compliance policy for mobile phones to all users in the company but exclude android-based meeting room devices that do not support the settings in that mobile phone policy.

## How filters work 

Filters work by dynamically evaluating applicability before delivering an app or policy to a device. Here is the high level overview: 

1. Admin creates a re-usable filter for a platform based on device properties.  

1. Admin assigns a Policy or App to a group and adds the Filter in either include or exclude mode. 

1. Filter evaluation is performed at device enrollment, check-in and any other policy evaluation time in the device’s lifecycle. 

1. Admin can see evaluation results (Apply or Don’t apply) based on the evaluation results in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

:::image type="content" source="./media/filters/admin-creates-filter.png" alt-text="Admin creates a filter, and uses the filter in a policy in Microsoft Endpoint Manager and Microsoft Intune.":::

When troubleshooting filters, it helps to understand what happens when you create, update, or delete an association with a policy assignment:

:::image type="content" source="./media/filters/filter-steps-engine.png" alt-text="Admin creates a filter, and uses the filter in a policy in Microsoft Endpoint Manager and Microsoft Intune.":::

## Before you begin

- You must be an Intune administrator. For more information, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Enable filters, and add a filter

### Enable filters

To use filters, you must enable it in your organization tenant.

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters (preview)** > **Try out the filters (preview) feature!**.
3. Set **Filters (preview)** to **On**:

    :::image type="content" source="./media/filters/turn-on-filters.png" alt-text="Turn on or enable the filters features in Microsoft Endpoint Manager and Microsoft Intune.":::

### Create a filter

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters (preview)** > **Create**.

    You can also create filters in **Devices** > **Filters (preview)**, or **Apps** > **Filters (preview)**.

3. In **Basics**, enter the following properties:

    - **Filter name**: Enter a descriptive name for the filter. Name your policies so you can easily identify them later. For example, a good policy name is **Windows OS version filter**.
    - **Description**: Enter a description for the filter. This setting is optional, but recommended.
    - **Platform**: Select your platform. Your options:
      - Android device administrator
      - Android Enterprise
      - iOS/iPadOS
      - macOS
      - Windows 10

4. Select **Next**.
5. In **Rules**, there are two ways to create a rule: Use the **rule builder**, or use the **rule syntax**.

    **Rule builder**:

    - **And/Or**: After you add an expression, you can add to the expression using the **and** or **or** options.
    - **Property**: Select a property for your rule. Your options:
      - Device name
      - Manufacturer
      - Model
      - Device category
      - OS version
      - Device ownership
      - Enrollment profile name
      - OS SKU
    - **Operator**: Select the operator from the list, such as `equals` or `contains`.
    - **Value**: Enter the value in your expression. For example, enter `10.0.18362` for the OS version, or `Microsoft` for the manufacturer.
    - **Add expression**: After you add the property, operator, and value, select **Add expression**:

      :::image type="content" source="./media/filters/rule-builder-example.png" alt-text="Use the rule builder in Microsoft Endpoint Manager and Microsoft Intune to create an expression filter, and assign to your policies.":::

    **Rule syntax**:

    You can also manually enter your rule expression. In **Rule syntax**, select **Edit**:

    :::image type="content" source="./media/filters/rule-syntax-edit.png" alt-text="Select rule syntax edit to use the rule builder in Microsoft Endpoint Manager and Microsoft Intune.":::

    The expression builder opens. You can manually enter expressions, such as `(device.osVersion -eq "10.0.18362") and (device.manufacturer -eq "Microsoft")`:

    :::image type="content" source="./media/filters/rule-syntax-example.png" alt-text="Use the expression builder to enter your rule syntax in Microsoft Endpoint Manager and Microsoft Intune.":::

    Select **OK** to save your expression.

    > [!TIP]
    > When you create a rule, it's validated for the correct syntax, and any errors are shown. If you enter syntax that's not supported, the rule builder is disabled.

6. Select **Next**.
7. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

8. In **Review + create**, review your settings. When you select **Create**, your changes are saved. The filter is created, and ready to be used. The filter is also shown in the filters list.

## Use a filter

After the filter is created, it's ready to be used when assigning your app policies, compliance policies, and configuration profiles.

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to your app policies, compliance policies, or configuration profiles. Select an existing policy.

    For example, select **Devices** > **Compliance policies**, and select an existing policy. Select **Properties** > **Assignments** > **Edit**:

    :::image type="content" source="./media/filters/edit-compliance-policy-assignment.png" alt-text="Select a compliance policy, and edit the assignment in Microsoft Endpoint Manager and Microsoft Intune.":::

3. Select **Edit filter**. You can choose to **include filtered devices** or **exclude filtered devices** when you assign the policy. A list of filters that match the policy platform is shown.

4. Select your filter > **Select**.

    For example, select **Include filtered devices in assignment**, and select the filter:

    :::image type="content" source="./media/filters/add-filter-compliance-policy.png" alt-text="Select a compliance policy, and edit the assignment in Microsoft Endpoint Manager and Microsoft Intune.":::

5. To save your changes, select **Review + save** > **Save**.

## Change an existing filter

After a filter is created, it can be changed or updated.

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters (preview)**. A list of all the filters is shown.

    You can also update filters in **Devices** > **Filters (preview)**, or **Apps** > **Filters (preview)**.

3. Select the filter you want to change. Select **Rules** > **Edit**:

    :::image type="content" source="./media/filters/update-existing-filter.png" alt-text="Delete a filter in Microsoft Endpoint Manager and Microsoft Intune.":::

4. To save your changes, select **Review + save** > **Save**.

## Delete a filter

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Filters (preview)**. A list of all the filters is shown.

    You can also delete filters in **Devices** > **Filters (preview)**, or **Apps** > **Filters (preview)**.

3. Next to the filter, select the ellipses (**...**), and select **Delete**:

    :::image type="content" source="./media/filters/delete-filter.png" alt-text="Delete a filter in Microsoft Endpoint Manager and Microsoft Intune.":::

To delete a filter, you must remove the filter from any policies. Otherwise, when trying to delete the filter, you'll get the following error:

`Unable to delete assignment filter – An assignment filter is associated with existing assignments. Delete all the assignments for the filter and try again.`

## Next steps
