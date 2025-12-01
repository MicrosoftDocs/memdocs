---
title: Create assignment filters in Microsoft Intune
description: Create assignment filters in Microsoft Intune to target policies based on device properties like OS version or manufacturer. Learn to create, update, and delete filters for managed devices and apps.
author: MandiOhlinger
ms.author: mandia
ms.date: 11/19/2025
ms.topic: how-to
ms.reviewer: mattcall
ms.collection:
- M365-identity-device-management
---

# Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune

Assignment filters in Microsoft Intune let you assign policies based on rules you create. Use filters to narrow policy scope by targeting devices with specific OS versions, manufacturers, or ownership types (personal vs. organization-owned). This targeting capability helps you apply the right policies to the right devices automatically.

Assignment filters are available for:

- Devices enrolled in Intune, which are **managed devices**.
- Apps that are managed by Intune, which are **managed apps**.

  Managed apps are used in mobile application management (MAM) scenarios. MAM involves managing apps on devices that aren't enrolled in Intune, which is common with personally owned devices. For more information on MAM in Intune, go to [What is Microsoft Intune app management?](../apps/app-management.md).

Use assignment filters in the following scenarios:

- Deploy a Windows device restriction policy to only the corporate devices in the Marketing department, while excluding personal devices.
- Deploy an iOS/iPadOS app to only the iPad devices in the Finance users group.
- Deploy an Android mobile phone compliance policy to all users in the company, and exclude Android meeting room devices that don't support the mobile phone compliance policy settings.
- On personally owned devices, deploy an app configuration policy for a specific app manufacturer or an app protection policy that runs a specific OS version.

Assignment filters include the following features and benefits:

- Improve flexibility and granularity when assigning Intune policies and apps.
- Are used when assigning apps, policies, and profiles. They dynamically target managed devices based on device properties and target managed apps based on app properties you enter.
- Can include or exclude devices or apps in a specific group based on criteria you enter.
- Can create a query of device or app properties based on different properties, like device platform or application version.
- Can be used and reused in multiple scenarios in "Include" or "Exclude" mode.

This feature applies to:

- **Managed devices** on the following platforms:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **Managed apps** on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

This article describes the filter architecture, and shows you how to create, update, and delete a filter.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## How assignment filters work

:::image type="content" source="./media/filters/admin-creates-filter.png" alt-text="Screenshot that shows how an admin creates a filter, and uses the filter in a policy in Microsoft Intune." lightbox="./media/filters/admin-creates-filter.png":::

Before you apply a policy to an app or device, assignment filters dynamically evaluate applicability. Here's an overview of the image:

1. You create a reusable filter based on an app or device property. In the example, the device filter is for iPhone XR devices.

2. You assign a policy to the group. In the assignment, you add the filter in include or exclude mode. For example, you "include" iPhone XR devices, or you "exclude" iPhone XR devices from the policy.

3. The filter is evaluated when the device enrolls, checks in with the Intune service, or at any other time a policy evaluates.

4. You see the filter results based on the evaluation. For example, the app or policy applies, or it doesn't apply.

### Restrictions

There are some general restrictions when creating assignment filters:

- You can have up to 200 assignment filters for each tenant.
- Each filter is limited to 3,072 characters.
- For managed devices, the devices must be enrolled in Intune.
- For managed apps, assignment filters apply to app protection policies and app configuration policies. They don't apply to other policies, like compliance or device configuration profiles.

## Prerequisites

- Sign in as an Intune administrator. For more information on Intune roles, go to [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Create a filter

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Assignment filters** > **Create**.

    You can also create assignment filters in:

    - **Devices** > **Organize devices** > **Assignment filters**
    - **Apps** > **Organize devices** > **Assignment filters**

3. Select **Managed devices** or **Managed apps**:

    :::image type="content" source="./media/filters/managed-apps-managed-devices.png" alt-text="Screenshot that shows selecting Managed apps or Managed devices when creating a filter in the Microsoft Intune admin center.":::

    Remember, managed devices are devices enrolled in Intune and are typically owned by the organizations. Managed apps are for devices that aren't enrolled in Intune and are typically owned by end users.

4. In **Basics**, enter the following properties:

    - **Filter name**: Enter a descriptive name for the filter. Name your assignment filters so you can easily identify them later. For example, a good filter name is **Windows OS version filter**.
    - **Description**: Enter a description for the filter. This setting is optional, but recommended.
    - **Platform**: Select your platform. Your options:

      - **Managed devices**:
        - Android device administrator
        - Android Enterprise
        - Android (AOSP)
        - iOS/iPadOS
        - macOS
        - Windows 10 and later

      - **Managed apps**:
        - Android
        - iOS/iPadOS
        - Windows

5. Select **Next**.
6. In **Rules**, there are two ways to create a rule: Use the **rule builder**, or use the **rule syntax**.

    **Rule builder**:

    - **And/Or**: After you add an expression, you can add to the expression using the `and` or `or` options.
    - **Property**: Select a property for your rule, like device or operating system SKU.
    - **Operator**: Select the operator from the list, like `equals` or `contains`.
    - **Value**: Enter the value in your expression. For example, enter `10.0.18362` for the OS version, or `Microsoft` for the manufacturer.
    - **Add expression**: After you add the property, operator, and value, select **Add expression**:

      :::image type="content" source="./media/filters/rule-builder-example.png" alt-text="Screenshot that shows how to use the rule builder in Microsoft Intune to create an expression filter, and assign to your policies.":::

      The expression you created is automatically added to the rule syntax editor.

    **Rule syntax**:

    You can also manually enter your rule expression, and write your own rules in the rule syntax editor. In **Rule syntax**, select **Edit**:

    :::image type="content" source="./media/filters/rule-syntax-edit.png" alt-text="Screenshot that shows how to select rule syntax editor to use the rule builder in Microsoft Intune.":::

    The expression builder opens. Manually enter expressions, like `(device.osVersion -eq "10.0.18362") and (device.manufacturer -eq "Microsoft")`:

    :::image type="content" source="./media/filters/rule-syntax-example.png" alt-text="Screenshot that shows how to use the expression builder to enter your rule syntax in Microsoft Intune.":::

    For more information on writing your own expressions, see [Device and app properties, operators, and rule editing when creating filters](filters-device-properties.md).

    Select **OK** to save your expression.

    > [!TIP]
    >
    > - When you create a rule, the system validates it for the correct syntax and shows any errors.
    > - If you enter syntax that's not supported by the basic rule builder, then the rule builder is disabled. For example, using nested parenthesis disables the basic rule builder.

7. Select **Preview devices**. A list of enrolled devices that match your filter criteria is shown.

    In this list, you can also search for devices by the device name, OS version, device model, device manufacturer, and more:

    :::image type="content" source="./media/filters/preview-search.png" alt-text="Screenshot that shows how to search for devices when creating a filter in Microsoft Intune.":::

    > [!NOTE]
    >
    > When you select **Preview devices** for a property that's in preview, you get a `You cannot use Filter preview with experimental properties` message. Even though you can't preview the property, you can continue to use the property in your assignment filters.
    >
    > :::image type="content" source="./media/filters/filter-preview.png" alt-text="Screenshot that shows cannot use filter preview message when clicking Preview devices with a preview property in filter rule syntax in Microsoft Intune.":::

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved. The assignment filter is created and ready to be used. The filter is also shown in the assignment filters list.

## Use a filter

After the filter is created, it's ready to use when assigning your apps or policies.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to your apps, compliance policies, or configuration profiles. For a list of supported workloads, see [Supported workloads when creating assignment filters](filters-supported-workloads.md). Select an existing policy, or create a new policy.

    For example, select **Devices** > **Compliance**, and select an existing policy. Select **Properties** > **Assignments** > **Edit**:

    :::image type="content" source="./media/filters/edit-compliance-policy-assignment.png" alt-text="Screenshot that shows how to select a policy or profile, and edit the assignment in Microsoft Intune.":::

2. Assign your policy to a users group or a devices group.
3. Select **Edit filter**. Your options:

    - **Do not apply a filter**: All targeted users or devices receive the app or policy without filtering.
    - **Include filtered devices in assignment**: Devices that match the filter conditions receive the app or policy. Devices that don't match the filter conditions don't receive the app or policy.

      A list of assignment filters that match the policy platform is shown.

    - **Exclude filtered devices in assignment**: Devices that match the filter conditions don't receive the app or policy. Devices that don't match the filter conditions receive the app or policy.

      A list of assignment filters that match the policy platform is shown.

4. Select your existing filter > **Select**.

    For example, select **Include filtered devices in assignment**, and select the filter:

    :::image type="content" source="./media/filters/add-filter-compliance-policy.png" alt-text="Screenshot that shows how to include the filter when assigning a policy in Microsoft Intune.":::

5. To save your changes, select **Review + save** > **Save**.

When the device checks in with the Intune service, the properties defined in the filter are evaluated, and determine if the app or policy should be applied.

## Filter your existing assignment filters

After you create an assignment filter, you can filter the existing list of assignment filters by platform and by profile type (**Managed devices** or **Managed apps**).

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Assignment filters**. You see a list of all the assignment filters.

    You can also go to **Devices** > **Organize devices** > **Assignment filters**, or **Apps** > **Assignment filters**.

2. Select **Add filters**:

    :::image type="content" source="./media/filters/add-filter.png" alt-text="Screenshot that shows how to add a filter to filter the existing filter list in Microsoft Intune.":::

3. You can filter the list by the **Filter type** or by **Platform**:

    :::image type="content" source="./media/filters/add-filter-profile-type-platform.png" alt-text="Screenshot that shows to filter the existing filter list by platform and profile type in Microsoft Intune.":::

4. Select **Filter type** > **Apply**. Then select **Managed devices** or **Managed apps** > **Apply**. The list of assignment filters is filtered based on your selection.

    :::image type="content" source="./media/filters/filter-type-managed-devices.png" alt-text="Screenshot that shows the filtered list of assignment filters by managed devices in Microsoft Intune.":::

5. Add another filter, select **Platform** > **Apply**. Select your platform from the list, like **Windows 10 and later** > **Apply**. The list of assignment filters is filtered based on your selection.

    :::image type="content" source="./media/filters/filter-platform.png" alt-text="Screenshot that shows the filtered list of assignment filters by platform in Microsoft Intune.":::

    :::image type="content" source="./media/filters/filter-platform-list.png" alt-text="Screenshot that shows the filtered list of assignment filters and all the available platform options in Microsoft Intune.":::

## Review the assignments

After you assign the filter to your policies, you can see all the policies that use the filter.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Assignment filters**. You see a list of all the assignment filters.

    You can also go to **Devices** > **Organize devices** > **Assignment filters**, or **Apps** > **Assignment filters**.

2. Select the filter you want to review > **Associated Assignments** tab.

    The page shows all the apps and policies that use the filter, the groups that receive the filter assignments, and the filter mode (**Include** or **Exclude**):

    :::image type="content" source="./media/filters/associated-assignments-filter-mode.png" alt-text="Screenshot that shows associated assignment tabs for an existing filter in Microsoft Intune.":::

## Change an existing filter

After you create a filter, you can change or update it.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Assignment filters**. You see a list of all the assignment filters.

    You can also update filters in **Devices** > **Organize devices** > **Assignment filters**, or **Apps** > **Assignment filters**.

2. To update an existing filter, select the filter you want to change. Select **Rules** > **Edit**, and make your changes:

    :::image type="content" source="./media/filters/update-existing-filter.png" alt-text="Screenshot that shows how to change or update an existing filter in Microsoft Intune.":::

3. To save your changes, select **Review + save** > **Save**.

## Delete a filter

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Assignment filters**. You see a list of all the assignment filters.

    You can also delete filters in **Devices** > **Organize devices** > **Assignment filters**, or **Apps** > **Assignment filters**.

2. Next to the filter, select the ellipses (**...**), and select **Delete**:

    :::image type="content" source="./media/filters/delete-filter.png" alt-text="Screenshot that shows how to delete a filter in Microsoft Intune.":::

    To delete a filter, you must remove the filter from any policy assignments. Otherwise, when you try to delete the filter, the following error is shown:
    
    `Unable to delete assignment filter – An assignment filter is associated with existing assignments. Delete all the assignments for the filter and try again.`

## Related content

- [Device properties, operators, and rule editing when creating assignment filters](filters-device-properties.md)
- [Supported workloads when creating assignment filters](filters-supported-workloads.md)
- [Filter performance recommendations](filters-performance-recommendations.md)
- [Filter reports and troubleshooting](filters-reports-troubleshoot.md)
