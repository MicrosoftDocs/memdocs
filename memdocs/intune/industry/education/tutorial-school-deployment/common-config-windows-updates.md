---
title: Common Education Windows Update configuration
description: Learn about common Windows Update configuration used by Eduation organizations in Intune
ms.date: 11/09/2023
ms.topic: overview
author: scottbreenmsft
ms.author: scbree
---

# Common Education Windows Update configuration

Create update rings that specify how and when Windows as a Service updates your Windows 10/11 devices with feature and quality updates.

In this article you will find Windows Update ring configuration that is commonly used for 1:1 student and teacher devices.

## Update rings for Windows 10 and later

Additional information:

- [Update rings for Windows 10 and later policy in Intune](https://learn.microsoft.com/mem/intune/protect/windows-10-update-rings)
- [The Windows Update policies you should set and why](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/the-windows-update-policies-you-should-set-and-why/ba-p/3270914)
- [教育機関向け Microsoft Intune を使った Windows Update 管理](https://youtu.be/o6_eGOyv-_g)
- [YouTube: Windows Update for Business Fundamentals](https://www.youtube.com/watch?v=TXwp-jLDcg0&list=PLMuDtq95SdKvpS9zPyFt9fc9HgepQxaw9&index=1)

| **Update settings** | **Value** | **Notes** | **CSP** |
| --- | --- | --- | --- |
| Microsoft product updates | Allow | Do not set to Block. In order to revert the configuration, a PowerShell commands will have to be run on each device. | [AllowMUUpdateService](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#allowmuupdateservice) |
| Windows drivers | Allow |     | [ExcludeWUDriversInQualityUpdate](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#excludewudriversinqualityupdate) |
| Quality update deferral period (days) | 7   |     | [DeferQualityUpdatesPeriodInDays](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#deferqualityupdatesperiodindays) |
| Feature update deferral period (days) | 30  | Select 0 if using a [**Feature update policy**](#windows-update-feature-control) otherwise select 30 days. | [DeferFeatureUpdatesPeriodInDays](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#deferfeatureupdatesperiodindays) |
| Upgrade Windows 10 devices to Latest Windows 11 release | No  |     | [ProductVersion](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#productversion) |
| Set feature update uninstall period (2 - 60 days) | 14  |     | [ConfigureFeatureUpdateUninstallPeriod](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#configurefeatureupdateuninstallperiod) |
| Enable pre-release builds | Not configured |     | [ManagePreviewBuilds](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#managepreviewbuilds) |

| **User experience settings** | **Value** | **Notes** | **CSP** |
| --- | --- | --- | --- |
| Automatic update behavior | Reset to default | Auto install and restart. Updates are downloaded automatically on non-metered networks and installed during "Automatic Maintenance" when the device isn't in use and isn't running on battery power.<br><br>**Note:** If Windows Update policy is configured via the Settings Catalog, the value should be **Auto install and restart**. | [](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#allowautoupdate)[AllowAutoUpdate](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#allowautoupdate) |
| Restart checks (EDU Restart) | Allow | Must not be disable for future compatibility. | [SetEDURestart](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#setedurestart) |
| Option to pause Windows updates | Disable |     | [SetDisablePauseUXAccess](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#setdisablepauseuxaccess) |
| Option to check for Windows updates | Disable |     | [SetDisableUXWUAccess](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#setdisableuxwuaccess) |
| Change notification update level | Turn off all notifications, excluding restart warnings |     | [UpdateNotificationLevel](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#updatenotificationlevel) |
| Use deadline settings | Allow | Only enables the setting configuration. |     |
| Deadline for feature updates | 7   |     | [ConfigureDeadlineForFeatureUpdates](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#configuredeadlineforfeatureupdates) |
| Deadline for quality updates | 3   |     | [ConfigureDeadlineForQualityUpdates](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#configuredeadlineforqualityupdates) |
| Grace period | 2   |     | [ConfigureDeadlineGracePeriod](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiod)<br><br>[ConfigureDeadlineGracePeriodForFeatureUpdates](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiodforfeatureupdates) |
| Auto reboot before deadline | Yes |     | [ConfigureDeadlineNoAutoReboot](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautoreboot) |

## Settings Catalog

Settings described in this section are not shown in an Update ring policy and should be configured as a Settings Catalog type Configuration Profile.

Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
| --- | --- | --- | --- |
| No update notifications during active hours | Enabled |     | [NoUpdateNotificationsDuringActiveHours](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-update#noupdatenotificationsduringactivehours) |

## Windows Update Feature Control

Windows feature updates contain new Windows features to improve the user experience. Windows feature versions are supported differently depending on the edition. It is important to ensure that the Windows version installed remains supported so that it can receive the latest security updates and support required applications such as testing apps.

Below is a list of the support lifecycle websites by Windows operating system version and edition:

- [Windows 10 Home, Pro and Pro Education](https://learn.microsoft.com/lifecycle/products/windows-10-home-and-pro);
- [Windows 10 Enterprise and Education](https://learn.microsoft.com/lifecycle/products/windows-10-enterprise-and-education);
- [Windows 11 Home, Pro and Pro Education](https://learn.microsoft.com/lifecycle/products/windows-11-home-and-pro);
- [Windows 11 Enterprise and Education](https://learn.microsoft.com/lifecycle/products/windows-11-enterprise-and-education).

There are 2 ways to control how and when Windows feature updates are installed on Windows. The table below gives an overview of the advantages and disadvantages of each option.

| Feature update control type | Configuration | Advantages | Disadvantages |
| --- | --- | --- | --- |
| Automatically keep up to date (recommended) | Use only **Update ring policies** and set a feature update deferral to 30 or more days | Devices are always kept up to date and receive access to the latest Windows features | Users may not have had training on new features and some apps may not be compatible with the new feature version |
| Control feature version | Use **feature update policies** to keep devices at a particular version of Windows | Devices are kept at a particular Windows version until the policy is changed | The policy must be reviewed and changed periodically to ensure Windows remains supported |

### Automatically keep Windows up to date

Using the **update ring** you configured earlier, set the **Feature update deferral period (days)** to **30** days. The deferral period can be increased or decreased based on the needs of the based on school needs.

### Control feature version

A [Feature update policy](https://learn.microsoft.com/mem/intune/protect/windows-10-feature-updates) can be configured to set devices to a particular version of Windows. If the devices targeted are running an older version they will update to the specified version. If devices are running the specified version or newer, they will not perform any feature updates.

To set a feature update policy:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Windows** > **Feature updates for Windows 10 and later** > **Create profile**.
3. Under **Deployment settings**:
    - Specify a name, a description (optional), and for **Feature update to deploy**, select the version of Windows with the feature set you want, and then select **Next**.
    - Configure **Rollout options** to **As soon as possible**.
4. Under **Assignments**, choose **\+ Select groups to include** and then assign the feature updates deployment to one or more device groups. Select **Next** to continue.
5. Under **Review + create**, review the settings. When ready to save the Feature updates policy, select **Create**.

> [!WARNING]
> If you don’t review the feature update version at least every 18 months, your Windows devices may no longer receive security updates. Ensure you review and update the feature version to stay supported. |