---
title: Deploy Microsoft Edge policy using settings catalog in Microsoft Intune
description: Add or create settings using the settings catalog to configure Microsoft Edge on Windows and macOS devices. Using Microsoft Intune, you can configure group policy settings, and deploy these settings to Microsoft Edge users.
ms.author: mandia
author: MandiOhlinger
ms.date: 08/25/2025
ms.topic: how-to

ms.reviewer: mayurjadhav
ms.collection:
- M365-identity-device-management
---

# Configure Microsoft Edge policy settings in Microsoft Intune

Using the [settings catalog](settings-catalog.md) in Microsoft Intune, you can create and manage Microsoft Edge policy settings on your Windows and macOS devices. The Microsoft Edge settings are ADMX-backed policy settings, similar to on-premises Group Policy Objects (GPO).

With these settings, you can control how Microsoft Edge works and configure Microsoft Edge features for users in your organization. For example, you can:

- Allow specific extensions
- Add download restrictions
- Use autofill
- Show the favorites bar
- And more...

These settings are created in an Intune policy, and then deployed to devices in your organization.

This article shows you how to configure Microsoft Edge policy settings using the [settings catalog](settings-catalog.md) in Microsoft Intune.

This article applies to:

- Windows
- macOS
- Microsoft Edge version 77 and newer

  For Microsoft Edge version 45 and earlier, go to [Microsoft Edge Browser device restrictions](device-restrictions-windows-10.md#microsoft-edge-legacy-version-45-and-older).

> [!TIP]
>
> - For information on adding the Microsoft Edge version 77+ app on Windows client, go to [Add Microsoft Edge app on Windows client devices](../apps/apps-windows-edge.md).
> - For information on adding and configuring Microsoft Edge version 77+ app on macOS, go to [Add Microsoft Edge app](../apps/apps-edge-macos.md), and [Configure Microsoft Edge app using plist](/DeployEdge/configure-microsoft-edge-on-mac).
> - For a list of the Microsoft Edge updates, including new policies, go to the [Release notes for Microsoft Edge](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

## Prerequisites

- To configure the settings catalog policy, at a minimum, sign into the Intune admin center with the **Policy and Profile manager** role. For information on the built-in roles in Intune, and what they can do, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Create a policy for Microsoft Edge

This section shows you how to create, search, and configure Microsoft Edge settings using the settings catalog.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **macOS** or **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Edge on Windows client devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**, and search for Edge:

    :::image type="content" source="./media/settings-catalog-configure-edge/settings-catalog-search-edge.png" alt-text="Screenshot that shows Microsoft Edge settings in the settings catalog in Microsoft Intune and Intune admin center." lightbox="./media/settings-catalog-configure-edge/settings-catalog-search-edge.png":::

    Select the **Microsoft Edge** category. The settings with `(User)` in the name apply to all users signed into the device. The other settings apply to the device, even if no one is signed in.

    :::image type="content" source="./media/settings-catalog-configure-edge/settings-catalog-edge-user-device.png" alt-text="Screenshot that shows Microsoft Edge user and device settings in the settings catalog in Microsoft Intune and Intune admin center." lightbox="./media/settings-catalog-configure-edge/settings-catalog-edge-user-device.png":::

8. In search, find a specific Microsoft Edge setting you want to configure. For example, search for `home page`, and select the **Configure the home page URL** setting:

    :::image type="content" source="./media/settings-catalog-configure-edge/settings-catalog-edge-home-page-url.png" alt-text="Screenshot that shows home page URL settings in the settings catalog in Microsoft Intune and Intune admin center." lightbox="./media/settings-catalog-configure-edge/settings-catalog-edge-home-page-url.png":::

   > [!NOTE]
   > For a list of the available settings, go to [Microsoft Edge – Policies](/DeployEdge/microsoft-edge-policies) and [Microsoft Edge – Update policies](/DeployEdge/microsoft-edge-update-policies).

9. Close the settings picker. Set the **Configure the home page URL** setting to **Enabled**, and set its value to a URL, like `https://www.bing.com`:

    :::image type="content" source="./media/settings-catalog-configure-edge/settings-catalog-edge-home-page-url-enabled.png" alt-text="Screenshot of the Microsoft Edge home page URL set to a web site using the settings catalog in Microsoft Intune and Intune admin center." lightbox="./media/settings-catalog-configure-edge/settings-catalog-edge-home-page-url-enabled.png":::

10. Select **Next**. In **Scope tags**, select **Next**.

    Scope tags are optional, and this example doesn't use them. To learn more about scope tags, and what they do, go to [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

11. In **Assignments**, select **Next**.

    Assignments are optional, and this example doesn't use them. In production, select **Add groups**. Select a Microsoft Entra group that includes users or devices that should receive this policy. For information and guidance on assigning policies, go to [Assign user and device profiles in Intune](device-profile-assign.md).

    :::image type="content" source="./media/settings-catalog-configure-edge/add-entra-group-assign-policy.png" alt-text="Screenshot of Assign or deploy the ADMX policy template to users or groups in Microsoft Intune and Intune admin center." lightbox="./media/settings-catalog-configure-edge/add-entra-group-assign-policy.png":::

12. In **Review + create**, the summary of your changes is shown. Select **Create**.

    When you create the profile, your policy is automatically assigned to the users or groups you chose. If you didn't choose any users or groups, then your policy is created, but it isn't deployed.

    In **Devices** > **Configuration**, your new Microsoft Edge policy is shown in the list.

## Related content

- [Download Microsoft Edge for your business](https://aka.ms/EdgeEnterprise)
- [Manage web access by using Microsoft Edge with Microsoft Intune](../apps/manage-microsoft-edge.md)
- [Deploy Microsoft Edge app using Microsoft Intune](../apps/apps-windows-edge.md)
