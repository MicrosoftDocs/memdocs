---
# required metadata

title: Update Microsoft 365 using administrative templates in Microsoft Intune
description: Use Administrative templates in Microsoft Intune to update Microsoft 365 apps to the latest version, and choose how frequently Office checks for updates. See the device registry keys that are updated when an Intune policy to Office update is applied.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/18/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use Update Channel and Target Version settings to update Microsoft 365 with Microsoft Intune Administrative Templates

In Intune, you can use [Windows client templates to configure group policy settings](administrative-templates-windows.md). This article shows you how to update Microsoft 365 using an administrative template in Intune. It also gives guidance on confirming your policies apply successfully. This information also helps when troubleshooting.

In this scenario, you create an administrative template in Intune that updates Microsoft 365 on your devices.

For more information on administrative templates, see [Windows client templates to configure group policy settings](administrative-templates-windows.md).

Applies to:

- Windows 11
- Windows 10
- Microsoft 365

## Prerequisites

Be sure to [enable Microsoft 365 Apps Automatic Updates](/deployoffice/configure-update-settings-for-office-365-proplus) for your Office apps. You can do this using group policy, or the Intune Office 2016 ADMX template:

:::image type="content" source="./media/administrative-templates-update-office/admx-enable-automatic-updates.png" alt-text="In Microsoft Intune and Intune admin center, create an administrative ADMX template to Enable Automatic Updates for Office.":::

## Set the Update Channel in the Intune administrative template

1. In your [Intune administrative template](administrative-templates-windows.md#create-the-template), go to the **Update Channel** setting, and enter the channel you want. For example, choose `Semi-Annual Channel`:

    :::image type="content" source="./media/administrative-templates-update-office/admx-enable-update-channel-setting.png" alt-text="In Microsoft Intune and Intune admin center, create an administrative ADMX template that sets the Update Channel setting for Office.":::

    > [!NOTE]
    > It's recommended to update more frequently. Semi-annually is only used as an example.

2. Be sure to [assign the policy](device-profile-assign.md) to your Windows client devices. To test your policy sooner, you can also sync the policy:

    - [Sync the policy in Intune](../remote-actions/device-sync.md)
    - [Manually sync the policy on the device](../user-help/sync-your-device-manually-windows.md#sync-from-settings-app)

## Check the Intune registry keys

After you assign the policy and the device syncs, you can confirm the policy is applied:

1. On the device, open the **Registry Editor** app.
2. Go to the Intune policy path: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`.

    > [!TIP]
    > The `<Provider ID>` in the registry key changes. To find the provider ID for your device, open the **Registry Editor** app, and go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\AdmxInstalled`. The provider ID is shown.

    When the policy is applied, you see the following registry keys:

    - `L_UpdateBranch`
    - `L_UpdateTargetVersion`

    Looking at the following example, you see `L_UpdateBranch` has a value similar to `<enabled /><data id="L_UpdateBranchID" value="Deferred" />`. This value means it's set to Semi-Annual Channel:

    :::image type="content" source="./media/administrative-templates-update-office/admx-update-branch-registry-key.png" alt-text="Administrative template L_Updatebranch registry key example for Microsoft Office":::

    > [!TIP]
    > [Manage Microsoft 365 Apps with Configuration Manager](../../configmgr/sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) lists the values, and what they mean. The registry values are based on the distribution channel selected:
    >
    >- Monthly Channel                - value="Current"
    >- Monthly Channel (Targeted)     - value="Current"
    >- Semi-Annual Channel            - value="Current"
    >- Semi-Annual Channel (Targeted) - value="FirstReleaseDeferred"
    >- Insider Fast                   - value="InsiderFast"

At this point, the Intune policy is successfully applied to the device.

## Check the Office registry keys

1. On the device, open the **Registry Editor** app.
2. Go to the Office policy path: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration`.

    You see the following registry keys:

    - `UpdateChannel`: A dynamic key that changes, depending on the configured settings.
    - `CDNBaseUrl`: Set when Microsoft 365 installs on the device.

3. Look at the `UpdateChannel` value. The value tells you how frequently Office is updated. [Manage Microsoft 365 Apps with Configuration Manager](../../configmgr/sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) lists the values, and what they're set to.

    Looking at the following example, you see `UpdateChannel` is set to `http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60`, which is **monthly**:

    :::image type="content" source="./media/administrative-templates-update-office/admx-update-channel-office-registry-key.png" alt-text="Administrative template Office UpdateChannel registry key example":::

    This example means the policy isn't applied yet, as it's still set to **monthly**, instead of **semi-annual**.

This registry key is updated when the **Task Scheduler** > **Office Automatic Updates 2.0** runs, or when a user signs into the device. To confirm, open the **Office Automatic Updates 2.0** task > **Triggers**. Depending on your triggers, it can take at least a day and more before the `UpdateChannel` registry key is updated.

## Force Office automatic updates to run

To test your policy, you can force the policy settings on the device. The following steps update the registry. As always, be careful when updating the registry.

1. Clear the registry key:

    1. Go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Updates`.
    2. Double-select the `UpdateDetectionLastRunTime` key, delete the value data > **OK**.

2. Run the Office Automatic Updates task:

    1. Open the **Task Scheduler** app on the device.
    2. Expand **Task Scheduler Library** > **Microsoft** > **Office**.
    3. Select **Office Automatic Updates 2.0** > **Run**:

        :::image type="content" source="./media/administrative-templates-update-office/admx-task-scheduler-office-automatic-updates.png" alt-text="Open Task Schedule, and run Office Automatic Updates using the task scheduler.":::

        Wait for the task to finish, which can take several minutes.

3. In the **Registry Editor** app, go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration`. Check the `UpdateChannel` value.

    It should be updated with the value set in the policy. In our example, the value should be set to `http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114`.

At this point, the Office update channel is successfully changed on the device. You can open a Microsoft 365 app for a user that receives this update to check status.

## Force the Office synchronization to update account information  

If you want to do more, you can force Office to get the latest version update. The following steps should only be done as a confirmation, or if you need the devices to get the latest version update from that channel quickly. Otherwise, let Office do its job, and update automatically.

### Step 1: Force the Office version to update

1. Confirm the Office version supports the update channel you're choosing. [Update history for Microsoft 365 Apps](/officeupdates/update-history-office365-proplus-by-date) lists the build numbers that support the different update channels.

2. In your [Intune administrative template](administrative-templates-windows.md#create-the-template), go to the **Target Version** setting, and enter the version you want.

    Your **Target version** setting looks similar to the following setting:

    :::image type="content" source="./media/administrative-templates-update-office/admx-enable-target-version-setting.png" alt-text="In a Microsoft Intune ADMX administrative template, set the Target Version setting for Office.":::

> [!IMPORTANT]
>
> - Be sure to assign the policy.
> - If you change an existing policy, your changes affect all assigned users.
> - If you're testing this feature, it's recommended to create a test policy, and assign the policy to a test group of users.

### Step 2: Check the Office version

Consider using the following steps to test your policy before deploying the policy to all users:

1. In the **Registry Editor** app, go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`.

2. Look at the `L_UpdateTargetVersion` value. Once the policy applies, the value is set to the version you entered, such as `<enabled /><data id="L_UpdateTargetVersionID" value="16.0.10730.20344" />`.

    At this point, the Intune policy is successfully applied to the device.

3. Next, you can force Office to update. Open an Office app, such as Excel. Choose to update now (possibly in the **Account** menu).

    The update takes several minutes. You can confirm Office is trying to get the version you enter:

      1. On the device, go to `C:\Program Files (x86)\Microsoft Office\Updates\Detection\Version`.
      2. Open the `VersionDescriptor.xml` file, and go to the `<Version>` section. The available version should be the same version you entered in the Intune policy, such as:

          :::image type="content" source="./media/administrative-templates-update-office/office-version-descriptor-xml-example.png" alt-text="Check the version section in the version descriptor Office XML file.":::

4. After the update is installed, the Office app should show the new version (for example, on the **Account** menu)

## Next steps

[Update channel values for Microsoft 365 clients](../../configmgr/sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel)

[Overview of the Office cloud policy service for Microsoft 365 Apps](/deployoffice/overview-office-cloud-policy-service)

[Use Windows 10/11 templates to configure group policy settings (ADMX templates) in Microsoft Intune](administrative-templates-windows.md)