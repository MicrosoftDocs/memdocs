---

title: Tutorial-Get started with cloud-native Windows endpoints
description: Set up secure cloud-native Windows endpoints that are Microsoft Entra joined, enrolled in Intune, and then deploy at scale with Windows Autopilot.
author: scottbreenmsft
ms.author: scbree
ms.date: 07/24/2025
ms.topic: get-started
ms.reviewer: scbree;rogerso
ms.collection:
  - M365-identity-device-management
  - highpri
  - highseo
  - intune-scenario
  - graph-interactive
---

# Tutorial: Set up and configure a cloud-native Windows endpoint with Microsoft Intune

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](../../includes/cloud-native-endpoints-definitions.md)]

This guide walks you through the steps to create a cloud-native Windows endpoint configuration for your organization. For an overview of cloud-native endpoints, and their benefits, see [What are cloud-native endpoints](cloud-native-endpoints-overview.md).

This feature applies to:

- Windows cloud-native endpoints

> [!TIP]
> If you want a Microsoft recommended, standardized solution to build on top of, then you might be interested in [Windows in cloud configuration](https://www.microsoft.com/microsoft-365/windows/cloud-configuration). For an Intune [Guided Scenario](../../intune-service/fundamentals/guided-scenarios-overview.md), see [Windows in cloud configuration](../../intune-service/fundamentals/cloud-configuration.md).
>
> The following table describes the key difference between this guide and *Windows in cloud configuration*:
>
> ---
> | Solution | Objective |
> | --- | --- |
> | **Tutorial: Get started with cloud-native Windows endpoints** (this guide) | Guides you through creating your own configuration for your environment, based on Microsoft recommended settings, and helps you start testing. |
> | [**Windows in cloud configuration**](https://www.microsoft.com/microsoft-365/windows/cloud-configuration) | A guided scenario experience that creates and applies a pre-built configuration based on Microsoft best practices for frontline, remote, and other workers with more focused needs. |
>
> ---
>
> You can use this guide combined with *Windows in cloud configuration* to customize the pre-built experience even more.

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../../intune-service/includes/windows-10-support.md)]

## How to get started

Use the five ordered phases in this guide, which build on each other to help you prepare your cloud-native Windows endpoint configuration. By completing these phases in order, you see tangible progress and are ready to provision new devices.

**Phases**:

:::image type="content" source="../media/cloud-native-windows-endpoints/phases.png" alt-text="Five phases for setting up cloud-native Windows endpoints using Microsoft Intune and Windows Autopilot.":::

- [Phase 1](#phase-1--set-up-your-environment) – Set up your environment
- [Phase 2](#phase-2---build-a-cloud-native-windows-endpoint) – Build your first cloud-native Windows endpoint
- [Phase 3](#phase-3--secure-your-cloud-native-windows-endpoint) – Secure your cloud-native Windows endpoint
- [Phase 4](#phase-4--apply-customizations-and-review-your-on-premises-configuration) – Apply your custom settings and applications
- [Phase 5](#phase-5--deploy-at-scale-with-windows-autopilot) – Deploy at scale with Windows Autopilot

At the end of this guide, you have a cloud-native Windows endpoint ready to start testing in your environment. Before you get started, you might want to check out the Microsoft Entra join planning guide at [How to plan your Microsoft Entra join implementation](/entra/identity/devices/device-join-plan).

## Phase 1 – Set up your environment

:::image type="content" source="../media/cloud-native-windows-endpoints/phase-1.png" alt-text="Image that shows phase 1, set up your environment for cloud native endpoints with Microsoft Intune":::

Before you build your first cloud-native Windows endpoint, there are some key requirements and configuration that need to be checked. This phase walks you through checking the requirements, configuring [Windows Autopilot](/autopilot/overview), and creating some settings and applications.

### Step 1 - Network requirements

Your cloud-native Windows endpoint needs access to several internet services. Start your testing on an open network. Or, use your corporate network after providing access to all the endpoints that are listed at [Windows Autopilot networking requirements](/autopilot/requirements?tabs=networking#networking-requirements).

If your wireless network requires certificates, you can start with an Ethernet connection during testing while you determine the best approach for wireless connections for device provisioning.

### Step 2 - Enrollment and Licensing

Before you can join Microsoft Entra and enroll in Intune, there are a few things you need to check. You could create a new Microsoft Entra group, such as the name **Intune MDM Users**. Then, add specific test user accounts and target each of the following configurations at that group to limit who can enroll devices while you set up your configuration. To create a Microsoft Entra group, go to [Manage Microsoft Entra groups and group membership](/entra/fundamentals/how-to-manage-groups).

- **Enrollment restrictions**
Enrollment restrictions allow you to control what types of devices can enroll into management with Intune. For this guide to be successful, make sure *Windows (MDM)* enrollment is allowed, which is the default configuration.

  For information on configuring Enrollment Restrictions, go to [Set enrollment restrictions in Microsoft Intune](../../intune-service/enrollment/enrollment-restrictions-set.md).

- **Microsoft Entra Device MDM settings**
  When you join a Windows device to Microsoft Entra, Microsoft Entra can be configured to tell your devices to automatically enroll with an MDM. This configuration is required for Windows Autopilot to work.

  To check your Microsoft Entra Device MDM settings are enabled properly, go to [Quickstart - Set up automatic enrollment in Intune](../../intune-service/enrollment/quickstart-setup-auto-enrollment.md).

- **Microsoft Entra company branding**
  Adding your corporate logo and images to Microsoft Entra ensures that users see a familiar and consistent look-and-feel when they sign-in to Microsoft 365. This configuration is required for Windows Autopilot to work.

  For information on configuring custom branding in Microsoft Entra, go to [Add branding to your organization's Microsoft Entra sign-in page](/entra/fundamentals/how-to-customize-branding).

- **Licensing**
  Users enrolling Windows devices from the Out Of Box Experience (OOBE) into Intune require two key capabilities.

  Users require the following licenses:
  - A **Microsoft Intune** or **Microsoft Intune for Education** license
  - A license like one of the following options that allows for automatic MDM enrollment:
    - **Microsoft Entra Premium P1**
    - **Microsoft Intune for Education**

  To assign licenses, go to [Assign Microsoft Intune licenses](../../intune-service/fundamentals/licenses-assign.md).

  > [!NOTE]
  > Both types of licenses are typically included with licensing bundles, like Microsoft 365 E3 (or A3) and higher. View comparisons of Microsoft 365 licensing [here](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans).

### Step 3 - Import your test device

To test the cloud-native Windows endpoint, we need to start by getting a virtual machine or physical device ready for testing. The following steps get the device details and upload them into the Windows Autopilot service, which are used later in this article.

> [!NOTE]
> While the following steps provide a way to import a device for testing, Partners and OEMs can import devices into Windows Autopilot on your behalf as part of purchasing. There's more information about Windows Autopilot in [Phase 5](#phase-5--deploy-at-scale-with-windows-autopilot).

1. Install Windows (preferably 20H2 or later) in a virtual machine or reset physical device so that it's waiting at the OOBE setup screen. For a virtual machine, you can optionally create a checkpoint.

2. Complete the necessary steps to connect to the Internet.

3. Open a command prompt by using the **Shift + F10** keyboard combination.

4. Verify that you have internet access by pinging bing.com:
   - `ping bing.com`

5. Switch into PowerShell by running the command:
   - `powershell.exe`

6. Download the *Get-WindowsAutopilotInfo* script by running the following commands:
   - `Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process`
   - `Install-Script Get-WindowsAutopilotInfo`

7. When prompted, enter **Y** to accept.

8. Type the following command:
   - `Get-WindowsAutopilotInfo.ps1 -GroupTag CloudNative -Online`

   > [!NOTE]
   > Group Tags allow you to create dynamic Microsoft Entra groups based on a subset of devices. Group Tags can be set when importing devices or changed later in the Microsoft Intune admin center. We use the Group Tag *CloudNative* in Step 4. You can set the tag name to something different for your testing.

9. When prompted for credentials, sign in with your Intune Administrator account.

10. Leave the computer at the out of box experience until [Phase 2](#phase-2---build-a-cloud-native-windows-endpoint).

### Step 4 - Create Microsoft Entra dynamic group for the device

To limit the configurations from this guide to the test devices that you import to Windows Autopilot, create a dynamic Microsoft Entra group. This group should automatically include the devices that import to Windows Autopilot and have the Group Tag *CloudNative*. You can then target all your configurations and applications at this group.

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Groups** > **New group**. Enter the following details:

   - **Group type**: Select **Security**.
   - **Group Name**: Enter **Autopilot Cloud-Native Windows Endpoints**.
   - **Membership type**: Select **Dynamic Device**.

3. Select **Add dynamic query**.

4. In the **Rule Syntax** section, select **Edit.**

5. Paste the following text:

    `(device.devicePhysicalIds -any (_ -eq "[OrderID]:CloudNative"))`

6. Select **OK** > **Save** > **Create**.

> [!TIP]
> Dynamic groups take a few minutes to populate after changes occur. In large organizations, it [can take longer](/entra/identity/users/groups-troubleshooting#troubleshooting-dynamic-memberships-for-groups). After creating a new group, wait a few minutes before you check to confirm the device is now a member of the group.
>
> For more information about dynamic groups for devices, go to [Rules for devices](/entra/identity/users/groups-dynamic-membership#rules-for-devices).

### Step 5 - Configure the Enrollment Status Page

The enrollment status page (ESP) is the mechanism an IT pro uses to control the end-user experience during endpoint provisioning. See [Set up the Enrollment Status Page](../../intune-service/enrollment/windows-enrollment-status.md). To limit the scope of the enrollment status page, you can create a new profile and target the **Autopilot Cloud-Native Windows Endpoints** group created in the previous step, *Create Microsoft Entra dynamic group for the device*.

- For the purposes of testing, we recommend the following settings, but feel free to adjust them as required:
  - **Show app and profile configuration progress** - Yes
  - **Only show page to devices provisioned by out-of-box experience (OOBE)** – Yes (*default*)

### Step 6 - Create and assign the Windows Autopilot profile

Now we can create the Windows Autopilot profile and assign it to our test device. This profile tells your device to join Microsoft Entra and what settings to apply during OOBE.

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Device onboarding** > **Enrollment** > **Windows** > **Windows Autopilot** > **Deployment profiles**.

3. Select **Create profile** > **Windows PC**.

1. Enter the name **Autopilot Cloud Native Windows Endpoint**, and then select **Next**.

5. Review and leave the default settings and select **Next**.

6. Leave the scope tags and select **Next**.

7. Assign the profile to the Microsoft Entra group you created called **Autopilot Cloud-Native Windows Endpoint**, select **Next**, and then select **Create**.

### Step 7 - Sync Windows Autopilot devices

The Windows Autopilot service synchronizes several times a day. You can also trigger a sync immediately so that your device is ready to test. To synchronize immediately:

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Device onboarding** > **Enrollment** > **Windows** > **Windows Autopilot** > **Devices**.

3. Select **Sync**.

The sync takes several minutes and continues in the background. When the sync is complete, the profile status for the imported device displays **Assigned**.

### Step 8 - Configure settings for an optimal Microsoft 365 experience

We've selected a few settings to configure. These settings demonstrate an optimal Microsoft 365 end-user experience on your Windows cloud-native device. These settings are configured using a device configuration settings catalog profile. For more information, go to [Create a policy using the settings catalog in Microsoft Intune](../../intune-service/configuration/settings-catalog.md).

After you created the profile and added your settings, assign the profile to the **Autopilot Cloud-Native Windows Endpoints** group created previously.

- **Microsoft Outlook**
  To improve the first run experience for Microsoft Outlook, the following setting automatically configures a profile when Outlook is opened for the first time.

  - Microsoft Outlook 2016\Account Settings\Exchange (User setting)
    - Automatically configure only the first profile based on Active Directory primary SMTP address - **Enabled**

- **Microsoft Edge**
  To improve the first run experience for Microsoft Edge, the following settings configure Microsoft Edge to sync the user's settings and skip the first run experience.

  - Microsoft Edge
    - Hide the first-run experience and splash screen - **Enabled**
    - Force synchronization of browser data and do not show the sync consent prompt - **Enabled**

- **Microsoft OneDrive**

  To improve the first sign-in experience, the following settings configure Microsoft OneDrive to automatically sign in and redirect Desktop, Pictures, and Documents to OneDrive. Files On-Demand (FOD) is also recommended. It's enabled by default and isn't included in the following list. For more information on the recommended configuration for the OneDrive sync app, go to [Recommended sync app configuration for Microsoft OneDrive](/onedrive/ideal-state-configuration).

  - OneDrive
    - Silently sign in users to the OneDrive sync app with their Windows credentials - **Enabled**
    - Silently move Windows known folders to OneDrive – **Enabled**

    > [!NOTE]
    > For more information, go to [Redirect Known Folders](/onedrive/redirect-known-folders).

The following screenshot shows an example of a settings catalog profile with each of the suggested settings configured:

:::image type="content" source="../media/cloud-native-windows-endpoints/settings-catalog-example.png" alt-text="Screenshot that shows an example of a settings catalog profile in Microsoft Intune.":::

### Step 9 - Create and assign some applications

Your cloud-native endpoint needs some applications. To get started, we recommend configuring the following applications and targeting them at the **Autopilot Cloud-Native Windows Endpoints** group created previously.

- **Microsoft 365 Apps** (formerly Office 365 ProPlus)
  Microsoft 365 Apps such as Word, Excel, and Outlook can easily be deployed to devices using the built-in *Microsoft 365 apps for Windows* app profile in Intune.

  - Select **configuration designer** for the settings format, as opposed to XML.
  - Select **Current Channel** for the update channel.

  To deploy Microsoft 365 Apps, go to [Add Microsoft 365 apps to Windows devices using Microsoft Intune](../../intune-service/apps/apps-add-office365.md)

- **Company Portal app**
  Deploying the Intune *Company Portal* app to all devices as a required application is recommended. Company Portal app is the self-service hub for users that they use to install applications from multiple sources, like Intune, Microsoft Store, and Configuration Manager. Users also use the Company Portal app to sync their device with Intune, check compliance status, and so on.

  To deploy **Company Portal** as required, see [Add and assign the Windows Company Portal app for Intune managed devices](../../intune-service/apps/store-apps-company-portal-autopilot.md).

- **Microsoft Store App** (Whiteboard)
  While Intune can deploy a wide variety of apps, we deploy a store app (Microsoft Whiteboard) to help keep things simple for this guide. Follow the steps in [Add Microsoft Store apps to Microsoft Intune](../../intune-service/apps/store-apps-microsoft.md) to install **Microsoft Whiteboard**.

## Phase 2 - Build a cloud-native Windows endpoint

:::image type="content" source="../media/cloud-native-windows-endpoints/phase-2.png" alt-text="Phase 2.":::

To build your first cloud-native Windows endpoint, use the same virtual machine or physical device that you gathered and then uploaded the hardware hash to the Windows Autopilot service in [Phase 1 > Step 3](#phase-1--set-up-your-environment). With this device, go through the Windows Autopilot process.

1. Resume (or reset if necessary) your Windows PC to the Out of Box Experience (OOBE).
   > [!NOTE]
   > If you're prompted to choose setup for personal or an organization, then the Windows Autopilot process hasn't triggered. In that situation, restart the device and ensure it has internet access. If it still doesn't work, try resetting the PC or reinstalling Windows.

2. Sign in with Microsoft Entra credentials (*UPN* or *AzureAD\username*).
3. The enrollment status page shows the status of the device configuration.

**Congratulations!** You've provisioned your first cloud-native Windows endpoint!

Some things to check out on your new cloud-native Windows endpoint:

- The OneDrive folders are redirected. When Outlook opens, it's configured automatically to connect to Office 365.
- Open the **Company Portal** app from the **Start Menu** and notice that **Microsoft Whiteboard** is available for installation.
- Consider testing access from the device to on-premises resources like file shares, printers, and intranet sites.

  > [!NOTE]
  > If you haven't set up [Windows Hello for Business Hybrid](/windows/security/identity-protection/hello-for-business/hello-identity-verification#hybrid-deployments), you might be prompted on Windows Hello logons to enter passwords to access on-premises resources. To continue testing single sign on access, you can configure Windows Hello for Business Hybrid or logon to the device with username and password rather than Windows Hello. To do so, select the key shaped icon on the logon screen.

## Phase 3 – Secure your cloud-native Windows endpoint

:::image type="content" source="../media/cloud-native-windows-endpoints/phase-3.png" alt-text="Phase 3.":::

This phase is designed to help you build out security settings for your organization. This section draws your attention to the various Endpoint Security components in Microsoft Intune including:

- [Microsoft Defender Antivirus (MDAV)](#microsoft-defender-antivirus-mdav)
- [Microsoft Defender Firewall](#microsoft-defender-firewall)
- [BitLocker Encryption](#bitlocker-encryption)
- [Windows Local Administrator Password Solution (LAPS)](#windows-local-administrator-password-solution-laps)
- [Security baselines](#security-baselines)
- [Windows Update client policies](#windows-update-for-business)

### Microsoft Defender Antivirus (MDAV)

The following settings are recommended as a minimum configuration for Microsoft Defender Antivirus, a built-in OS component of Windows. These settings don't require any specific licensing agreement such as E3 or E5, and can be enabled in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

#### [:::image type="icon" source="../../intune-service/media/icons/intune.svg"::: **Intune Admin Console**](#tab/intuneadminconsole)

In the admin center, go to **Endpoint Security** > **Antivirus** > **Create Policy** > **Windows and later** > **Profile type** = **Microsoft Defender Antivirus**.

**Defender**:

- Allow Behavior Monitoring: **Allowed. Turns on real-time behavior monitoring.**
- Allow Cloud Protection: **Allowed. Turns on Cloud Protection.**
- Allow Email Scanning: **Allowed. Turns on email scanning.**
- Allow scanning of all downloaded files and attachments: **Allowed.**
- Allow Realtime Monitoring: **Allowed. Turns on and runs the real-time monitoring service.**
- Allow Scanning Network Files: **Allowed. Scans network files.**
- Allow Script Scanning: **Allowed.**
- Cloud Extended Timeout: **50**
- Days To Retain Cleaned Malware: **30**
- Enable Network Protection: **Enabled (audit mode)**
- PUA Protection: **PUA Protection on. Detected items are blocked. They will show in history along with other threats.**
- Real Time Scan Direction: **Monitor all files (bi-directional).**
- Submit Samples Consent: **Send safe samples automatically.**
- Allow On Access Protection: **Allowed.**
- Remediation action for Severe threats: **Quarantine. Moves files to quarantine.**
- Remediation action for Low severity threat: **Quarantine. Moves files to quarantine.**
- Remediation action for Moderate severity threats: **Quarantine. Moves files to quarantine.**
- Remediation action for High severity threats: **Quarantine. Moves files to quarantine.**

#### [:::image type="icon" source="../../intune-service/media/icons/graph.svg"::: **Microsoft Graph**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../../intune-service/includes/graph-explorer-intro.md)]

This creates a policy in your tenant with the name **_MSLearn_Example_Windows - Defender Antivirus** under **Endpoint Security** > **Antivirus**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_Windows - Defender Antivirus","description":"","settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"905921da-95e2-4a10-9e30-fe5540002ce1"},"value":"device_vendor_msft_policy_config_defender_allowbehaviormonitoring_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowbehaviormonitoring","settingInstanceTemplateReference":{"settingInstanceTemplateId":"8eef615a-1aa0-46f4-a25a-12cbe65de5ab"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"16fe8afd-67be-4c50-8619-d535451a500c"},"value":"device_vendor_msft_policy_config_defender_allowcloudprotection_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowcloudprotection","settingInstanceTemplateReference":{"settingInstanceTemplateId":"7da139f1-9b7e-407d-853a-c2e5037cdc70"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"fdf107fd-e13b-4507-9d8f-db4d93476af9"},"value":"device_vendor_msft_policy_config_defender_allowemailscanning_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowemailscanning","settingInstanceTemplateReference":{"settingInstanceTemplateId":"b0d9ee81-de6a-4750-86d7-9397961c9852"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"df4e6cbd-f7ff-41c8-88cd-fa25264a237e"},"value":"device_vendor_msft_policy_config_defender_allowioavprotection_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowioavprotection","settingInstanceTemplateReference":{"settingInstanceTemplateId":"fa06231d-aed4-4601-b631-3a37e85b62a0"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"0492c452-1069-4b91-9363-93b8e006ab12"},"value":"device_vendor_msft_policy_config_defender_allowrealtimemonitoring_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowrealtimemonitoring","settingInstanceTemplateReference":{"settingInstanceTemplateId":"f0790e28-9231-4d37-8f44-84bb47ca1b3e"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"7b8c858c-a17d-4623-9e20-f34b851670ce"},"value":"device_vendor_msft_policy_config_defender_allowscanningnetworkfiles_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowscanningnetworkfiles","settingInstanceTemplateReference":{"settingInstanceTemplateId":"f8f28442-0a6b-4b52-b42c-d31d9687c1cf"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"ab9e4320-c953-4067-ac9a-be2becd06b4a"},"value":"device_vendor_msft_policy_config_defender_allowscriptscanning_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowscriptscanning","settingInstanceTemplateReference":{"settingInstanceTemplateId":"000cf176-949c-4c08-a5d4-90ed43718db7"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_defender_cloudextendedtimeout","settingInstanceTemplateReference":{"settingInstanceTemplateId":"f61c2788-14e4-4e80-a5a7-bf2ff5052f63"},"simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","settingValueTemplateReference":{"settingValueTemplateId":"608f1561-b603-46bd-bf5f-0b9872002f75"},"value":50}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_defender_daystoretaincleanedmalware","settingInstanceTemplateReference":{"settingInstanceTemplateId":"6f6d741c-1186-42e2-b2f2-8582febcfd60"},"simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","settingValueTemplateReference":{"settingValueTemplateId":"214b6feb-c9b2-4a17-af54-d51c805473e4"},"value":30}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"ee58fb51-9ae5-408b-9406-b92b643f388a"},"value":"device_vendor_msft_policy_config_defender_enablenetworkprotection_2"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_enablenetworkprotection","settingInstanceTemplateReference":{"settingInstanceTemplateId":"f53ab20e-8af6-48f5-9fa1-46863e1e517e"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"2d790211-18cb-4e32-b8cc-97407e2c0b45"},"value":"device_vendor_msft_policy_config_defender_puaprotection_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_puaprotection","settingInstanceTemplateReference":{"settingInstanceTemplateId":"c0135c2a-f802-44f4-9b71-b0b976411b8c"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"6b4e3497-cfbb-4761-a152-de935bbf3f07"},"value":"device_vendor_msft_policy_config_defender_realtimescandirection_0"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_realtimescandirection","settingInstanceTemplateReference":{"settingInstanceTemplateId":"f5ff00a4-e5c7-44cf-a650-9c7619ff1561"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"826ed4b6-e04f-4975-9d23-6f0904b0d87e"},"value":"device_vendor_msft_policy_config_defender_submitsamplesconsent_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_submitsamplesconsent","settingInstanceTemplateReference":{"settingInstanceTemplateId":"bc47ce7d-a251-4cae-a8a2-6e8384904ab7"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"ed077fee-9803-44f3-b045-aab34d8e6d52"},"value":"device_vendor_msft_policy_config_defender_allowonaccessprotection_1"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_allowonaccessprotection","settingInstanceTemplateReference":{"settingInstanceTemplateId":"afbc322b-083c-4281-8242-ebbb91398b41"}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"settingValueTemplateReference":{"settingValueTemplateId":"764256b4-e4d7-46d9-bbc8-003bf23591a1"},"value":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_highseveritythreats_quarantine"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_highseveritythreats","settingInstanceTemplateReference":{"settingInstanceTemplateId":"f55b8c9c-d831-460e-a041-e47e29f2aa17"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_severethreats","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"value":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_severethreats_quarantine"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_lowseveritythreats","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"value":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_lowseveritythreats_quarantine"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_moderateseveritythreats","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","children":[],"value":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction_moderateseveritythreats_quarantine"}}]}],"settingInstanceTemplateReference":{"settingInstanceTemplateId":"f6394bc5-6486-4728-b510-555f5c161f2b"},"settingDefinitionId":"device_vendor_msft_policy_config_defender_threatseveritydefaultaction"}}],"roleScopeTagIds":["0"],"platforms":"windows10","technologies":"mdm,microsoftSense","templateReference":{"templateId":"804339ad-1553-4478-a742-138fb5807418_1"}}
```
[!INCLUDE [graph-explorer-steps](../../intune-service/includes/graph-explorer-steps.md)]

---

For more information on Windows Defender configuration, including Microsoft Defender for Endpoint for customer's licensed for E3 and E5, go to:

- [Next-generation protection in Windows, Windows Server 2016, and Windows Server 2019](/windows/security/threat-protection/microsoft-defender-antivirus/microsoft-defender-antivirus-in-windows-10)
- [Evaluate Microsoft Defender Antivirus](/windows/security/threat-protection/microsoft-defender-antivirus/evaluate-microsoft-defender-antivirus)

### Microsoft Defender Firewall

Use Endpoint Security in Microsoft Intune to configure the firewall and firewall rules. For more information, go to [Firewall policy for endpoint security in Intune](../../intune-service/protect/endpoint-security-firewall-policy.md).

Microsoft Defender Firewall can detect a trusted network using the [NetworkListManager CSP](/windows/client-management/mdm/policy-csp-networklistmanager). And, it can switch to the *domain* firewall profile on endpoints running Windows.

Using the *domain* network profile allows you to separate firewall rules based on a trusted network, a private network, and a public network. These settings can be applied using a Windows custom profile.

> [!NOTE]
> Microsoft Entra joined endpoints can't use LDAP to detect a domain connection in the same way that domain-joined endpoints do. Instead, use the [NetworkListManager CSP](/windows/client-management/mdm/policy-csp-networklistmanager) to specify a TLS endpoint that when accessible, switches the endpoint to the *domain* firewall profile.

### BitLocker Encryption

Use Endpoint Security in Microsoft Intune to configure encryption with BitLocker.

- For more information about managing BitLocker, go to [Encrypt Windows devices with BitLocker in Intune](../../intune-service/protect/encrypt-devices.md).
- Check out our blog series on BitLocker at [Enabling BitLocker with Microsoft Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/enabling-bitlocker-with-microsoft-endpoint-manager-microsoft/ba-p/2149784).

These settings can be enabled in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). In the admin center, go to **Endpoint Security** > **Manage** > **Disk encryption** > **Create Policy** > **Windows and later** > **Profile** = **BitLocker**.

When you configure the following BitLocker settings, they silently enable 128-bit encryption for standard users, which is a common scenario. However, your organization might have different security requirements, so use the [BitLocker documentation](../../intune-service/protect/encrypt-devices.md) for more settings.

**BitLocker**:

- Require Device Encryption: **Enabled**
- Allow Warning For Other Disk Encryption: **Disabled**
  - Allow Standard User Encryption: **Enabled**
- Configure Recovery Password Rotation: **Refresh on for Azure AD-joined devices**

**BitLocker Drive Encryption**:

- Choose drive encryption method and cipher strength: **Not Configured**
- Provide the unique identifiers for your organization: **Not Configured**

**Operating System Drives**:

- Enforce drive encryption type on operating system drives: **Enabled**
  - Select the encryption type (Device): **Used Space Only encryption**
- Require additional authentication at startup: **Enabled**
  - Allow BitLocker without a compatible TPM (requires a password or a startup key on a USB flash drive): **False**
  - Configure TPM startup key and PIN: **Allow startup key and PIN with TPM**
  - Configure TPM startup key: **Allow startup key with TPM**
  - Configure TPM startup PIN: **Allow startup PIN with TPM**
  - Configure TPM startup: **Require TPM**
  - Configure minimum PIN length for startup: **Not configured**
  - Allow enhanced PINs for startup: **Not configured**
- Disallow standard users from changing the PIN or password: **Not configured**
- Allow devices compliant with InstantGo or HSTI to opt out of pre-boot PIN: **Not configured**
- Enable use of BitLocker authentication requiring preboot keyboard input on slates: **Not configured**
- Choose how BitLocker-protected operating system drives can be recovered: **Enabled**
  - Configure user storage of BitLocker recovery information: **Require 48-digit recovery password**
  - Allow data recovery agent: **False**
  - Configure storage of BitLocker recovery information to AD DS: **Store recovery passwords and key packages**
  - Do not enable BitLocker until recovery information is stored to AD DS for operating system drives: **True**
  - Omit recovery options from the BitLocker setup wizard: **True**
  - Save BitLocker recovery information to AD DS for operating system drives: **True**
- Configure pre-boot recovery message and URL: **Not configured**

**Fixed Data Drives**:

- Enforce drive encryption type on fixed data drives: **Enabled**
  - Select the encryption type: (Device):  **Allow user to choose (default)**
- Choose how BitLocker-protected fixed drives can be recovered: **Enabled**
  - Configure user storage of BitLocker recovery information: **Require 48-digit recovery password**
  - Allow data recovery agent: **False**
  - Configure storage of BitLocker recovery information to AD DS: **Backup recovery passwords and key packages**
  - Do not enable BitLocker until recovery information is stored to AD DS for fixed data drives: **True**
  - Omit recovery options from the BitLocker setup wizard: **True**
  - Save BitLocker recovery information to AD DS for fixed data drives: **True**
- Deny write access to fixed drives not protected by BitLocker: **Not configured**

**Removable Data Drives**:

- Control use of BitLocker on removable drives: **Enabled**
  - Allow users to apply BitLocker protection on removable data drives (Device): **False**
  - Allow users to suspend and decrypt BitLocker protection on removable data drives (Device): **False**
- Deny write access to removable drives not protected by BitLocker: **Not configured**


### Windows Local Administrator Password Solution (LAPS)

By default, the built-in local administrator account ([well known SID](/windows-server/identity/ad-ds/manage/understand-security-identifiers#well-known-sids) S-1-5-500) is disabled. There are some scenarios where a local administrator account can be beneficial, such as troubleshooting, end-user support, and device recovery. If you decide to enable the built-in administrator account, or create a new local administrator account, it's important to secure the password for that account.

Windows Local Administrator Password Solution (LAPS) is one of the features you can use to randomize and securely store the password in Microsoft Entra. If you're using Intune as your MDM service, then use the following steps to enable [Windows LAPS](/windows-server/identity/laps/laps-overview).

> [!IMPORTANT]
> Windows LAPS assumes that the default local administrator account is enabled, even if it's renamed or if you create another local admin account. Windows LAPS doesn't create or enable any local accounts for you unless you configure [Automatic account management mode](/windows-server/identity/laps/laps-concepts-account-management-modes#automatic-account-management-mode).
>
> You need to create or enable any local accounts separately from configuring Windows LAPS. You can script this task or use the Configuration Service Providers (CSPs), such as the [Accounts CSP](/windows/client-management/mdm/accounts-csp) or [Policy CSP](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions).

1. Make sure your Windows devices have the April 2023 (or later) security update installed.

    For more information, go to [Microsoft Entra operating system updates](/entra/identity/devices/howto-manage-local-admin-passwords#operating-system-updates).

2. Enable Windows LAPS in Microsoft Entra:

    1. Sign in to [Microsoft Entra](https://aka.ms/aaddevice).
    2. For the **Enable Local Administrator Password Solution (LAPS)** setting, select **Yes** > **Save** (top of the page).

    For more information, go to [Enabling Windows LAPS with Microsoft Entra](/entra/identity/devices/howto-manage-local-admin-passwords#enabling-windows-laps-with-microsoft-entra-id).

3. In Intune, create an endpoint security policy:

    1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
    2. Select **Endpoint Security** > **Account Protection** > **Create Policy** > **Windows** > **Local admin password solution (Windows LAPS)** > **Create**.

    For more information, go to [Create a LAPS policy in Intune](../../intune-service/protect/windows-laps-policy.md#create-a-laps-policy).

### Security Baselines

You can use security baselines to apply a set of configurations that are known to increase the security of a Windows endpoint. For more information about security baselines, go to [Windows MDM security baseline settings for Intune](../../intune-service/protect/security-baseline-settings-mdm-all.md).

Baselines can be applied using the suggested settings and customized as per your requirements. Some settings within baselines might cause unexpected results or be incompatible with apps and services running on your Windows endpoints. As a result, baselines should be tested in isolation. Only apply the baseline to a selective group of test endpoints without any other configuration profiles or settings.

#### Security Baselines Known Issues

The following settings in the **Windows security baseline** can cause issues with Windows Autopilot or attempting to install apps as a standard user:

- Local Policies Security Options\Administrator elevation prompt behavior (default = Prompt for consent on the secure desktop)
- Standard user elevation prompt behavior (default = Automatically deny elevation requests)

For more information, see [Troubleshooting policy conflicts with Windows Autopilot](/autopilot/troubleshooting-faq#troubleshooting-policy-conflicts-with-windows-autopilot).

### Windows Update client policies
<a name="windows-update-for-business"></a>

*Windows Update client policies* is the cloud technology for controlling how and when updates are installed on devices. In Intune, Windows Update client policies can be configured using:

- [Windows update rings](../../intune-service/protect/windows-10-update-rings.md)
- [Windows Feature Updates](../../intune-service/protect/windows-10-feature-updates.md)

For more information, go to:

- [Learn about using Windows Update client policies in Microsoft Intune](../../intune-service/protect/windows-update-for-business-configure.md)
- [Module 4.2 - Windows Update for Business Fundamentals](https://www.youtube.com/watch?v=TXwp-jLDcg0&list=PLMuDtq95SdKsEc_BmAbvwI5l6RPQ2Y2ak&index=6&t=5s) from the Intune for Education Deployment Workshop video series

If you'd like more granular control for Windows Updates and you use Configuration Manager, consider [co-management](../../configmgr/comanage/overview.md).

## Phase 4 – Apply customizations and review your on-premises configuration

:::image type="content" source="../media/cloud-native-windows-endpoints/phase-4.png" alt-text="Phase 4.":::

In this phase, you apply organization-specific settings, apps, and review your on-premises configuration. The phase helps you build any customizations specific to your organization. Notice the various components of Windows, how you can review existing configurations from an on-premises AD Group Policy environment, and apply them to cloud-native endpoints. There are sections for each of the following areas:

- [Microsoft Edge](#microsoft-edge)
- [Start and Taskbar layout](#start-and-taskbar-layout)
- [Settings catalog](#settings-catalog)
- [Device Restrictions](#device-restrictions)
- [Delivery Optimization](#delivery-optimization)
- [Local Administrators](#local-administrators)
- [Group Policy to MDM Setting Migration](#group-policy-to-mdm-setting-migration)
- [Scripts](#scripts)
- [Mapping Network Drives and Printers](#mapping-network-drives-and-printers)
- [Applications](#applications)

### Microsoft Edge

#### Microsoft Edge Deployment

Microsoft Edge is included on devices that run:

- Windows

After users sign in, Microsoft Edge updates automatically. To trigger an update for Microsoft Edge during deployment, you can run the following command:

```powershell
Start-Process -FilePath "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" -argumentlist "/silent /install appguid={56EB18F8-B008-4CBD-B6D2-8C97FE7E9062}&appname=Microsoft%20Edge&needsadmin=True"
```

To deploy Microsoft Edge to previous versions of Windows, go to [Add Microsoft Edge for Windows to Microsoft Intune](../../intune-service/apps/apps-windows-edge.md).

#### Microsoft Edge Configuration

Two components of the Microsoft Edge experience, which apply when users sign in with their Microsoft 365 credentials, can be configured from the Microsoft 365 Admin Center.

- The start page logo in Microsoft Edge can be customized by configuring the *Your organization* section within the Microsoft 365 admin center. For more information, go to [Customize the Microsoft 365 theme for your organization](/microsoft-365/admin/setup/customize-your-organization-theme).

- The default new tab page experience in Microsoft Edge includes Office 365 information and personalized news. How this page is displayed can be customized from the Microsoft 365 admin center at **Settings** > **Org settings** > **News** > **Microsoft Edge new tab page**.

You can also set other settings for Microsoft Edge using settings catalog profiles. For example, you might want to configure specific sync settings for your organization.

- **Microsoft Edge**
  - Configure the list of types that are excluded from synchronization - **passwords**

### Start and Taskbar layout

You can customize and set a standard start and taskbar layout using Intune.

- **For Windows 11**:

  - To create and apply a Start menu layout, go to [Customize the Start menu layout on Windows 11](/windows/configuration/customize-start-menu-layout-windows-11).
  - To create and apply a Taskbar layout, go to [Customize the Taskbar on Windows 11](/windows/configuration/taskbar/configure).

- **For Windows 10**:

  - For more information about start and taskbar customization, go to [Manage Windows Start and taskbar layout (Windows)](/windows/configuration/windows-10-start-layout-options-and-policies).
  - To create a start and taskbar layout, go to [Customize and export Start layout (Windows)](/windows/configuration/customize-and-export-start-layout).

  After the layout is created, it can be uploaded to Intune by configuring a [Device Restrictions](../../intune-service/configuration/device-restrictions-configure.md) profile. The setting is under the *Start* category.

  > [!IMPORTANT]
  > [!INCLUDE [windows-10-support](../../intune-service/includes/windows-10-support.md)]

### Settings catalog

The settings catalog is a single location where all configurable Windows settings are listed. This feature simplifies how you create a policy, and how you see all the available settings. For more information, go to [Create a policy using the settings catalog in Microsoft Intune](../../intune-service/configuration/settings-catalog.md).

> [!TIP]
> Many of the settings you're familiar with from group policy are built into the settings catalog. If settings aren't available in the settings catalog, then check the device configuration profiles templates.

Following are some settings available in the settings catalog that might be relevant to your organization:

- **Azure Active Directory preferred tenant domain**
  This setting configures the preferred tenant domain name to be appended to a user's username. A preferred tenant domain allows users to sign in to Microsoft Entra endpoints with only their username rather than their whole UPN so long as the user's domain name matches the preferred tenant domain. For users that have different domain names, they can type their whole UPN.

  The setting can be found in:
  - Authentication
    - Preferred AAD Tenant Domain Name - Specify domain name, like `contoso.onmicrosoft.com`.

- **Windows Spotlight**
  By default, several consumer features of Windows are enabled which results in selected Store apps installing and third-party suggestions on the lock screen. You can control this using the Experience section of the settings catalog.

  - Experience > Allow Windows Spotlight
    - Allow Windows Consumer Features - **Block**
    - Allow Third-Party Suggestions in Windows Spotlight (user) - **Block**

- **Microsoft Store**
  Organizations typically want to restrict the applications that can install on endpoints. Use this setting if your organization wants to control which applications can install from the Microsoft Store. This setting prevents users from installing applications unless they're approved.
  - Microsoft App Store
    - Require Private Store Only - **Only Private store is enabled**

      > [!NOTE]
      > This setting applies to Windows 10. On Windows 11, this setting blocks access to the public Microsoft store. For more information, go to:
      >
      > - [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-endpoint-manager-integration-with-the-microsoft-store/ba-p/3585077)
      > - [FAQ: Supporting Microsoft Store experiences on managed devices](https://techcommunity.microsoft.com/t5/windows-management/faq-supporting-microsoft-store-experiences-on-managed-devices/m-p/3585286)

- **Block Gaming**
  Organizations might prefer that corporate endpoints can't be used to play games. The Gaming page within the Settings app can be hidden entirely using the following setting.
  For additional information on the settings page visibility, go to the [CSP documentation](/windows/client-management/mdm/policy-csp-settings#settings-pagevisibilitylist) and the ms-settings [URI scheme reference](/windows/uwp/launch-resume/launch-settings-app#ms-settings-uri-scheme-reference).
  - Settings
    - Page Visibility List – **hide:gaming-gamebar;gaming-gamedvr;gaming-broadcasting;gaming-gamemode;gaming-trueplay;gaming-xboxnetworking;quietmomentsgame**

- **Control which tenants the Teams desktop client can sign in to**

  When this policy is configured on a device, users can only sign in with accounts homed in a Microsoft Entra tenant that is included in the "Tenant Allow List" defined in this policy. The "Tenant Allow List" is a comma separated list of Microsoft Entra tenant IDs. By specifying this policy and defining a Microsoft Entra tenant, you also block sign in to Teams for personal use. For more information, go to [How to restrict sign in on desktop devices](/microsoftteams/sign-in-teams#how-to-restrict-sign-in-on-desktop-devices).

  - Microsoft Teams
    - Restrict sign in to Teams to accounts in specific tenants (User) - **Enabled**

### Device Restrictions

Windows Device restrictions templates contain many of the settings required to secure and manage a Windows endpoint using Windows Configuration Service Providers (CSPs). More of these settings will be made available in the settings catalog over time. For more information, go to [Device Restrictions](../../intune-service/configuration/device-restrictions-configure.md).

To create a profile that uses the Device restrictions template, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > Select **Windows 10 and later** for platform > **Templates** **Device restrictions** for profile type.

- **Desktop background picture URL (Desktop only)**
  Use this setting to set a wallpaper on Windows Enterprise or Windows Education SKUs. You host the file online or reference a file that's copied locally. To configure this setting, on the *Configuration settings* tab in the *Device restrictions* profile, expand *Personalization*, and configure **Desktop background picture URL (Desktop only)**.

- **Require users to connect to a network during device setup**
  This setting reduces the risk that a device can skip Windows Autopilot if the computer is reset. This setting requires devices to have a network connection during the out of box experience phase. To configure this setting, on the *Configuration settings* tab in the *Device restrictions* profile, expand *General*, and configure **Require users to connect to network during device setup**.

  > [!NOTE]
  > The setting becomes effective the next time the device is wiped or reset.

### Delivery Optimization

Delivery Optimization is used to reduce bandwidth consumption by sharing the work of downloading supported packages among multiple endpoints. Delivery Optimization is a self-organizing distributed cache that enables clients to download those packages from alternate sources, like peers on the network. These peer sources supplement the traditional Internet-based servers. You can find out about all the settings available for Delivery Optimization and what types of downloads are supported at [Delivery Optimization for Windows updates](/windows/deployment/update/waas-delivery-optimization).

To apply Delivery Optimization settings, create an Intune [Delivery Optimization profile](../../intune-service/configuration/delivery-optimization.md) or a settings catalog profile.

Some settings that are commonly used by organizations are:

- **Restrict peer selection – Subnet**. This setting restricts peer caching to computers on the same subnet.
- **Group ID**. Delivery Optimization clients can be configured to only share content with devices in the same group. Group IDs can be configured directly by sending a GUID through policy or using DHCP options in DHCP scopes.

Customers using Microsoft Configuration Manager can deploy connected cache servers that can be used to host Delivery Optimization content. For more information, go to [Microsoft Connected Cache in Configuration Manager](../../configmgr/core/plan-design/hierarchy/microsoft-connected-cache.md).

### Local Administrators

If there's only one user group that needs local administrator access to all Microsoft Entra joined Windows devices, then you can add them to the [Microsoft Entra Joined Device Local Administrator](/entra/identity/role-based-access-control/permissions-reference#microsoft-entra-joined-device-local-administrator).

You might have a requirement for IT helpdesk or other support staff to have local admin rights on a select group of devices. You can meet this requirement by using the following Configuration Service Providers (CSPs).

- [Local Users and Groups CSP](/windows/client-management/mdm/policy-csp-localusersandgroups) (preferred)
- [Restricted Groups CSP](/windows/client-management/mdm/policy-csp-restrictedgroups) (no update action, only replace)

For more information, go to [How to manage the local administrators group on Microsoft Entra joined devices](/entra/identity/devices/assign-local-admin)

### Group Policy to MDM Setting Migration

There are several options for creating your device configuration when considering a migration from Group Policy to cloud-native device management:

- Start fresh and apply custom settings as required.
- Review existing Group Policies and apply required settings. You can use tools to help, like [Group Policy analytics](../../intune-service/configuration/group-policy-analytics.md).
- Use Group Policy analytics to create Device Configuration profiles directly for supported settings.

The transition to a cloud-native Windows endpoint represents an opportunity to review your end-user computing requirements and establish a new configuration for the future. Wherever possible, start fresh with a minimal set of policies. Avoid carrying forward unnecessary or legacy settings from a domain-joined environment or older operating systems, like Windows 7 or Windows XP.

To start fresh, review your current requirements and implement a minimal collection of settings to meet these requirements. Requirements might include regulatory or mandatory security settings and settings to enhance the end-user experience. The business creates a list of requirements, not IT. Every setting should be documented, understood, and should serve a purpose.

Migrating settings from existing Group Policies to MDM (Microsoft Intune) isn't the preferred approach. When you transition to cloud-native Windows, the intention shouldn't be to lift and shift existing group policy settings. Instead, consider the target audience and what settings they require. It's time consuming and likely impractical to review each group policy setting in your environment to determine its relevance and compatibility with a modern managed device. Avoid trying to assess every group policy and individual setting. Instead, focus on assessing those common policies that cover most devices and scenarios.

Instead, identify the group policy settings that are mandatory and review those settings against available MDM settings. Any gaps would represent blockers that can prevent you from moving forward with a cloud-native device if unresolved. Tools such as [Group Policy analytics](../../intune-service/configuration/group-policy-analytics.md) can be used to analyze group policy settings and determine if they can be migrated to MDM policies or not.

### Scripts

You can use PowerShell scripts for any settings or customizations that you need to configure outside of the in-built configuration profiles. For more information, go to [Add PowerShell scripts to Windows devices in Microsoft Intune](../../intune-service/apps/intune-management-extension.md).

### Mapping Network Drives and Printers

Cloud-native scenarios have no built-in solution for mapped network drives. Instead, we recommend that users migrate to Teams, SharePoint, and OneDrive. If migration isn't possible, consider the use of scripts if necessary.

For personal storage, in [Step 8 - Configure settings for an optimal Microsoft 365 experience](#step-8---configure-settings-for-an-optimal-microsoft-365-experience), we configured OneDrive Known Folder move. For more information, go to [Redirect Known Folders](/onedrive/redirect-known-folders).

For document storage, users can also benefit from SharePoint integration with File Explorer and the ability to sync libraries locally, as referenced here: [Sync SharePoint and Teams files with your computer](https://support.microsoft.com/office/sync-sharepoint-and-teams-files-with-your-computer-6de9ede8-5b6e-4503-80b2-6190f3354a88).

If you use corporate Office document templates, which are typically on internal servers, consider the newer cloud-based equivalent that allows users to access the templates from anywhere.

- [Create an organization assets library](/sharepoint/organization-assets-library)

For printing solutions, consider Universal Print. For more information, go to:

- [What is Universal Print?](/universal-print/fundamentals/universal-print-whatis)
- [Announcing general availability of Universal Print](https://techcommunity.microsoft.com/t5/universal-print-blog/announcing-general-availability-of-universal-print/ba-p/2176759)
- [Tasks you can complete using the Settings Catalog in Intune](../../intune-service/configuration/settings-catalog-common-features.md)

### Applications

Intune supports the deployment of many different Windows application types.

- Windows Installer (MSI) – [Add a Windows line-of-business app to Microsoft Intune](../../intune-service/apps/lob-apps-windows.md)
- MSIX – [Add a Windows line-of-business app to Microsoft Intune](../../intune-service/apps/lob-apps-windows.md)
- Win32 apps (MSI, EXE, script installers) – [Win32 app management in Microsoft Intune](../../intune-service/apps/apps-win32-app-management.md)
- Store apps – [Add Microsoft Store apps to Microsoft Intune](../../intune-service/apps/store-apps-windows.md)
- Web links – [Add web apps to Microsoft Intune](../../intune-service/apps/web-app.md)

If you have applications that use MSI, EXE, or script installers, you can deploy all of these applications using *Win32 app management in Microsoft Intune*. Wrapping these installers in the Win32 format provides more flexibility and benefits, including notifications, delivery optimization, dependencies, detection rules, and support for the Enrollment Status Page in Windows Autopilot.

> [!NOTE]
> To prevent conflicts during installation, we recommend that you stick to using the Windows line-of-business apps or Win32 apps features exclusively. If you have applications that are packaged as `.msi` or `.exe`, then they can be converted to Win32 apps (`.intunewin`) using the *[Microsoft Win32 Content Prep Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool)* available on GitHub.

## Phase 5 – Deploy at scale with Windows Autopilot

:::image type="content" source="../media/cloud-native-windows-endpoints/phase-5.png" alt-text="Phase 5.":::

Now that you configured your cloud-native Windows endpoint and provisioned it with Windows Autopilot, consider how you can import more devices. Also consider how you can work with your partner or hardware supplier to start provisioning new endpoints from the cloud. Review the following resources to determine the best approach for your organization.

- [Overview of Windows Autopilot](/autopilot/overview)
- [Module 6.4 - Windows Autopilot Fundamentals - YouTube](https://www.youtube.com/watch?v=wNmLvqZ21AE)

If for some reason Windows Autopilot isn't the right option for you, there are other enrollment methods for Windows. For more information, go to [Intune enrollment methods for Windows devices](../../intune-service/fundamentals/deployment-guide-enroll.md).

## Follow the cloud-native endpoints guidance

1. [Overview: What are cloud-native endpoints?](cloud-native-endpoints-overview.md)
2. 🡺 **Tutorial: Get started with cloud-native Windows endpoints** (*You are here*)
3. [Concept: Microsoft Entra joined vs. Hybrid Microsoft Entra joined](azure-ad-joined-hybrid-azure-ad-joined.md)
4. [Concept: Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
5. [High level planning guide](cloud-native-endpoints-planning-guide.md)
6. [Known issues and important information](cloud-native-endpoints-known-issues.md)

## Helpful online resources

- [Co-management for Windows devices](../../configmgr/comanage/overview.md)
- [Windows Subscription Activation](/windows/deployment/windows-10-subscription-activation)
- Configure an Intune [device compliance policy](../../intune-service/protect/compliance-policy-create-windows.md) that can allow or deny access to resources based on a Microsoft Entra [Conditional Access policy](/entra/identity/conditional-access/howto-conditional-access-policy-compliant-device)
- Add [Store Apps](../../intune-service/apps/store-apps-microsoft.md)
- Add [Win32 apps](../../intune-service/apps/apps-win32-app-management.md)
- [Use certificates for authentication in Intune](../../intune-service/protect/certificates-configure.md)
- Deploy network profiles, including [VPN](../../intune-service/configuration/vpn-settings-windows-10.md) and [Wi-Fi](../../intune-service/configuration/wi-fi-settings-windows.md)
- Deploy [multifactor authentication](/entra/identity/authentication/concept-mfa-howitworks)
- Security baseline for [Microsoft Edge](../../intune-service/protect/security-baseline-settings-edge.md)
