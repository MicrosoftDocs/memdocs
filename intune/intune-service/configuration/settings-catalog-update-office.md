---
title: Update Microsoft 365 apps with the settings catalog in Microsoft Intune
description: Use settings catalog in Microsoft Intune to update Microsoft 365 apps to the latest version, and choose how frequently Office checks for updates. See the device registry keys that are updated when an Intune policy to Office update is applied.
author: MandiOhlinger
ms.author: mandia
ms.date: 08/28/2025
ms.topic: how-to
ms.reviewer: mayurjadhav
ms.collection:
- M365-identity-device-management
---

# Set the Microsoft 365 apps update channel using the Microsoft Intune settings catalog

Admins must keep Microsoft 365 Apps up-to-date so users have access to the latest security updates and performance improvements. In Intune, you can use the [settings catalog](settings-catalog.md) to update Microsoft 365 apps on your Windows devices, including setting the update channel.

This article shows you how to use the settings catalog to manage Microsoft 365 app updates. It also provides guidance on confirming your policies apply successfully, which can help when troubleshooting.

In this scenario, you create a settings catalog policy in Intune that updates Microsoft 365 on your devices. For more information on settings catalog, go to [Use the Intune settings catalog to configure settings](settings-catalog.md).

This feature applies to:

- Windows
- Microsoft 365

## Prerequisites

- Requires Microsoft Intune and a Microsoft 365 subscription. For information on Intune licensing, go to [Microsoft Intune licensing](../fundamentals/licenses.md).

- To configure the settings catalog policy, at a minimum, sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with the **Policy and Profile manager** role. For information on the built-in roles in Intune, and what they can do, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

- Add and enable [Microsoft 365 Apps Automatic Updates](/deployoffice/configure-update-settings-for-office-365-proplus) for your Office apps. You can enable automatic updates using Group Policy, or the Intune Office settings catalog settings:

  :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-search-enable-automatic-updates.png" alt-text="Screenshot that shows searching for the Enable Office updates using the settings catalog in Microsoft Intune." lightbox="./media/settings-catalog-update-office/settings-catalog-search-enable-automatic-updates.png":::

  :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-enable-automatic-updates.png" alt-text="Screenshot that shows the Enable Office updates setting configured in the settings catalog in Microsoft Intune." lightbox="./media/settings-catalog-update-office/settings-catalog-enable-automatic-updates.png":::

## Set the Update Channel in the Intune settings catalog

Use an Intune policy to set the update channel for Microsoft 365 apps. The update channel determines how frequently Office checks for updates.

1. In your [settings catalog](settings-catalog.md#create-the-policy) policy, search for **Update Channel**, and select it. Close the settings picker.

    :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-update-channel.png" alt-text="In Microsoft Intune and Intune admin center, add the Office Update Channel setting in the settings catalog." lightbox="./media/settings-catalog-update-office/settings-catalog-update-channel.png":::

2. Set the **Update Channel** to **Enabled** and select the channel name. For example, select `Semi-Annual Enterprise Channel`:

    :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-update-channel-semi-annual.png" alt-text="In Microsoft Intune and Intune admin center, enable the Office Update Channel setting and select the channel in the settings catalog." lightbox="./media/settings-catalog-update-office/settings-catalog-update-channel-semi-annual.png":::

    > [!TIP]
    > - It's recommended to update more frequently. Semi-annually is only used as an example.
    > - For information on the different update channels, go to [Overview of update channels for Microsoft 365 Apps](/microsoft-365-apps/updates/overview-update-channels).

3. When the policy is ready, [assign the policy](device-profile-assign.md) to your Windows client devices. To test your policy sooner, you can also sync the policy.

    - [Sync the policy in Intune](../remote-actions/device-sync.md)
    - [Manually sync the policy on the device](../user-help/sync-your-device-manually-windows.md#sync-from-settings-app)

## Check the Intune registry keys

After you assign the policy and the device syncs, you can confirm the Intune policy is applied.

1. On the device, open the **Registry Editor** app.
2. Go to the Intune policy path: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16v2~Policy~L_MicrosoftOfficemachine~L_Updates`.

    The `<Provider ID>` in the registry key changes. To find the provider ID for your device, open the **Registry Editor** app, and go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\AdmxInstalled`. The provider ID is shown.

    When the policy is applied, you see the following registry key:

    - `L_UpdatePath`

    Looking at the following example, you see `L_UpdatePath` has a value similar to `<enabled/><data id="L_UpdatePathID" value="http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114" />`. This value means the update channel is set similar to the following image:

    :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-update-path-registry-key.png" alt-text="Microsoft Intune settings catalog L_UpdatePath registry key example for Microsoft Office" lightbox="./media/settings-catalog-update-office/settings-catalog-update-path-registry-key.png":::

    > [!TIP]
    > [Manage Microsoft 365 Apps with Configuration Manager](../../configmgr/sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) lists the values, and what they mean. The registry values are based on the distribution channel selected:
    >
    >- Current Channel                - value=`http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60`
    >- Current Channel (preview)      - value=`http://officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be`
    >- Monthly Enterprise Channel     - value=`http://officecdn.microsoft.com/pr/55336b82-a18d-4dd6-b5f6-9e5095c314a6`
    >- Semi-Annual Enterprise Channel - value=`http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114`
    >- Semi-Annual Enterprise Channel (preview) - value=`http://officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf`
    >- Beta                   - value=`http://officecdn.microsoft.com/pr/5440fd1f-7ecb-4221-8110-145efaa6372f`

At this point, the Intune policy is successfully applied to the device.

## Check the Office registry keys

1. On the device, open the **Registry Editor** app.
2. Go to the Office policy path: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration`.

    You see the following registry keys:

    - `UpdateChannel`: A dynamic key that changes, depending on the configured settings.
    - `CDNBaseUrl`: Set when Microsoft 365 installs on the device.

3. Look at the `UpdateChannel` value. The value tells you how frequently Office is updated. [Manage Microsoft 365 Apps with Configuration Manager](../../configmgr/sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) lists the values, and what they're set to.

    Looking at the following example, you see `UpdateChannel` is set to `http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60`, which is the **Current Channel** (monthly):

    :::image type="content" source="./media/settings-catalog-update-office/update-channel-office-registry-key.png" alt-text="Office UpdateChannel registry key example" lightbox="./media/settings-catalog-update-office/update-channel-office-registry-key.png":::

    This example means the policy isn't applied yet, as the registry setting is still set to **monthly**, instead of **semi-annual**.

This registry key is updated when the **Task Scheduler** > **Office Automatic Updates 2.0** runs, or when a user signs into the device. To confirm, open the **Task Scheduler app** > **Microsoft** > **Office** > **Office Automatic Updates 2.0** task > **Triggers**. Depending on your triggers, it can take at least a day and more before the `UpdateChannel` registry key is updated.

## Force Office automatic updates to run

To test your policy, you can force the policy settings on the device. The following steps update the registry. As always, be careful when updating the registry.

1. Clear the registry key:

    1. Go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Updates`.
    2. Double-select the `UpdateDetectionLastRunTime` key > delete the value data > **OK**.

2. Run the Office Automatic Updates task:

    1. Open the **Task Scheduler** app on the device.
    2. Expand **Task Scheduler Library** > **Microsoft** > **Office**.
    3. Select **Office Automatic Updates 2.0** > **Run**:

        :::image type="content" source="./media/settings-catalog-update-office/task-scheduler-office-automatic-updates.png" alt-text="Open Task Schedule, and run Office Automatic Updates using the task scheduler." lightbox="./media/settings-catalog-update-office/task-scheduler-office-automatic-updates.png":::

        Wait for the task to finish, which can take several minutes.

3. In the **Registry Editor** app, go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration`. Check the `UpdateChannel` value.

    It should be updated with the value set in the policy. In our example, the value should be set to `http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114`.

At this point, the Office update channel is successfully changed on the device. You can open a Microsoft 365 app for a user that receives this update to check status.

## Force the Office synchronization to update account information

If you want to do more, you can force Office to get the latest version update. The following steps should only be done as a confirmation, or if you need the devices to get the latest version update from that channel quickly. Otherwise, let Office do its job, and update automatically.

### Step 1: Force the Office version to update

1. Confirm the Office version supports the update channel you're choosing. [Update history for Microsoft 365 Apps](/officeupdates/update-history-office365-proplus-by-date) lists the build numbers that support the different update channels.

2. In your settings catalog policy, search for the **Target Version** setting, and close the settings picker:

    :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-search-target-version.png" alt-text="In a Microsoft Intune settings catalog policy, search for the Target Version setting for Office." lightbox="./media/settings-catalog-update-office/settings-catalog-search-target-version.png":::

3. Enter the version you want. Your **Target version** setting looks similar to the following setting:

    :::image type="content" source="./media/settings-catalog-update-office/settings-catalog-enable-target-version-setting.png" alt-text="In the Microsoft Intune settings catalog, set the Target Version setting for Office." lightbox="./media/settings-catalog-update-office/settings-catalog-enable-target-version-setting.png":::

> [!IMPORTANT]
>
> - Be sure to assign the policy.
> - If you change an existing policy, your changes affect all assigned users.
> - If you're testing this feature, it's recommended to create a test policy, and assign the policy to a test group of users.

### Step 2: Check the Office version

Consider using the following steps to test your policy before deploying the policy to all users:

1. In the **Registry Editor** app, go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`.

2. Look at the `L_UpdateTargetVersion` value. Once the policy applies, the value is set to the version you entered, such as `<enabled /><data id="L_UpdateTargetVersionID" value="16.0.19127.20082" />`.

    At this point, the Intune policy is successfully applied to the device.

3. Next, you can force Office to update. Open an Office app, such as Excel. Select to update now (possibly in the **Account** menu).

    The update takes several minutes. You can confirm Office is trying to get the version you enter:

      1. On the device, go to `C:\Program Files (x86)\Microsoft Office\Updates\Detection\Version`.
      2. Open the `VersionDescriptor.xml` file, and go to the `<Version>` section. The available version should be the same version you entered in the Intune policy, such as:

          :::image type="content" source="./media/settings-catalog-update-office/office-version-descriptor-xml-example.png" alt-text="Check the version section in the version descriptor Office XML file." lightbox="./media/settings-catalog-update-office/office-version-descriptor-xml-example.png":::

4. After the update is installed, the Office app should show the new version (for example, on the **Account** menu)

## Related articles

- [Update channel values for Microsoft 365 clients](../../configmgr/sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel)
- [Overview of Cloud Policy service for Microsoft 365](/microsoft-365-apps/admin-center/overview-cloud-policy)
- [Use the Intune settings catalog to configure settings](settings-catalog.md)
