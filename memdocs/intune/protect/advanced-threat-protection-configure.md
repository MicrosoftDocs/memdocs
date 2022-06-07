---
# required metadata

title: Configure Microsoft Defender for Endpoint in Microsoft Intune
description: Configure Microsoft Defender for Endpoint in Intune, including connecting to Defender for Endpoint, onboarding devices, assigning compliance for risk levels, and conditional access policies.
keywords: configure, manage, capabilities, attack surface reduction, next-generation protection, security controls, endpoint detection and response, auto investigation and remediation, security controls, controls, microsoft defender for endpoint, mde
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 06/06/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.reviewer: aanavath

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Configure Microsoft Defender for Endpoint in Intune

Use the information and procedures in this article to configure integration of Microsoft Defender for Endpoint with Intune. Configuration includes the following general steps:

- Enable Microsoft Defender for Endpoint for your tenant
- Onboard devices that run Android, iOS/iPadOS, and Windows 10/11
- Use compliance policies to set device risk levels
- Use conditional access policies to block devices that exceed your expected risk levels
- Android and iOS/iPadOS, use [app protection policies](../protect/mtd-app-protection-policy.md) that set device risk levels. App protection polices work with both enrolled and unenrolled devices.

Before starting, your environment must meet the [prerequisites](../protect/advanced-threat-protection.md#prerequisites) to use Microsoft Defender for Endpoint with Intune.

In addition to managing settings for Microsoft Defender for Endpoint on devices you manage with Intune, you can manage Defender for Endpoint security configurations on devices that aren’t enrolled with Intune. This scenario is called *Security Management for Microsoft Defender for Endpoint* and requires configuring the *Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations* toggle to *On*. For more information, see [MDE Security Configuration Management](../protect/mde-security-integration.md).

## Enable Microsoft Defender for Endpoint in Intune

The first step you take is to set up the service-to-service connection between Intune and Microsoft Defender for Endpoint. Set up requires administrative access to both the Microsoft Defender Security Center, and to Intune.

You only need to enable Microsoft Defender for Endpoint a single time per tenant.

### To enable Microsoft Defender for Endpoint

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Microsoft Defender for Endpoint**, and then select **Open the Microsoft Defender for Endpoint admin console**. 

   This opens the **Microsoft 365 Defender** portal at *security.microsoft.com*, which [replaces the use of the previous portal](/microsoft-365/security/defender/microsoft-365-defender?view=o365-worldwide&preserve-view=true) at *securitycenter.windows.com*.

   > [!TIP]
   > If the **Connection status** at the top of the page is already set to **Enabled**, the connection to Intune has already been made, and the admin center displays different UI than in the following screen shot. In this event, you can use the link **Open the Microsoft Defender for Endpoint admin console** to open the Microsoft Defender Security Center and use the guidance in the following step to confirm that the **Microsoft Intune connection** is set to **On**.

   :::image type="content" source="./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png" alt-text="Screen shot that shows the patch to open the Microsoft Defender Security Center.":::

3. In **Microsoft 365 Defender**, (previously the *Microsoft Defender Security Center*):
   1. Select [**Settings** > **Endpoints** >**Advanced features**](https://security.microsoft.com/preferences2/integration).
   2. For **Microsoft Intune connection**, choose **On**:

      :::image type="content" source="./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png" alt-text="Screen shot of the Microsoft Intune connection setting.":::

   3. Select **Save preferences**.

   > [!NOTE]
   > Once the connection is established, the services are expected to sync with each other _at least_ once every 24 hours. The number of days without sync until the connection is considered unresponsive is configurable in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Endpoint security** > **Microsoft Defender for Endpoint** > **Number of days until partner is unresponsive**

4. Return to **Microsoft Defender for Endpoint** page in the Microsoft Endpoint Manager admin center.

   1. To use Defender for Endpoint with **compliance policies**, configure the following under **MDM Compliance Policy Settings** for the platforms you support:
      - Set **Connect Android devices** to Microsoft Defender for Endpoint to **On**
      - Set **Connect iOS devices** to Microsoft Defender for Endpoint to **On**
      - Set **Connect Windows devices** to Microsoft Defender for Endpoint to **On**

      When these configurations are *On*, applicable devices that you manage with Intune, and devices you enroll in the future, are connected to Microsoft Defender for Endpoint for compliance.

      For iOS devices, Defender for Endpoint also supports the following settings:

      - **Enable App Sync for iOS Devices**:  Set to **On** to allow Defender for Endpoint to request metadata of iOS applications from Intune to use for threat analysis purposes. The iOS device must be MDM-enrolled and will provide updated app data during device check-in.

      - **Send full application inventory data on personally-owned iOS/iPadOS Devices**: This setting controls the application inventory data that Intune shares with Defender for Endpoint when Defender for Endpoint syncs app data and requests the app inventory list.

        When set to **On**, Defender for Endpoint can request a list of applications from Intune for personally-owned iOS/iPadOS devices. This includes unmanaged apps as well as apps that were deployed through Intune. 

        When set to **Off**, data about unmanaged apps isn’t provided. Intune does share data for the apps that were deployed through Intune.

      For more information, see [Mobile Threat Defense toggle options](../protect/mtd-connector-enable.md#mobile-threat-defense-toggle-options).

   2. To use Defender for Endpoint with **app protection policies**, configure the following under **App Protection Policy Settings** for the platforms you support. These capabilities are available for Android and iOS/iPadOS.
      - Set **Connect Android devices** to Microsoft Defender for Endpoint for app protection policy evaluation to **On**.  
      - Set **Connect iOS devices** to Microsoft Defender for Endpoint for app protection policy evaluation to **On**.  

    For more information about both MDM Compliance Policy Settings and App Protection Policy Settings, see [Mobile Threat Defense toggle options](../protect/mtd-connector-enable.md#mobile-threat-defense-toggle-options).

5. Select **Save**.

> [!TIP]
> When you integrate a new application to Intune Mobile Threat Defense and enable the connection to Intune, Intune creates a classic conditional access policy in Azure Active Directory. Each MTD app you integrate, including [Microsoft Defender for Endpoint](advanced-threat-protection.md) or any of our additional [MTD partners](mobile-threat-defense.md#mobile-threat-defense-partners), creates a new classic conditional access policy. These policies can be ignored, but should not be edited, deleted, or disabled.
>
> If the classic policy is deleted, you will need to delete the connection to Intune that was responsible for its creation, and then set it up again. This recreates the classic policy. It's not supported to migrate classic policies for MTD apps to the new policy type for conditional access.
>
> Classic conditional access policies for MTD apps:
>
> - Are used by Intune MTD to require that devices are registered in Azure AD so that they have a device ID before communicating to MTD partners. The ID is required so that devices and can successfully report their status to Intune.
> - Have no effect on any other Cloud apps or Resources.
> - Are distinct from conditional access policies you might create to help manage MTD.
> - By default, don't interact with other conditional access policies you use for evaluation.
>
> To view classic conditional access policies, in [Azure](https://portal.azure.com/#home), go to **Azure Active Directory** > **Conditional Access** > **Classic policies**.

## Onboard devices

When you enabled support for Microsoft Defender for Endpoint in Intune, you established a service-to-service connection between Intune and Microsoft Defender for Endpoint. You can then onboard devices you manage with Intune to Microsoft Defender for Endpoint. Onboarding enables collection of data about device risk levels.

When onboarding devices, be sure to use most recent version of Microsoft Defender for Endpoint for each platform.

### Onboard Windows devices

After you connect Intune and Microsoft Defender for Endpoint, Intune receives an onboarding configuration package from Microsoft Defender for Endpoint. You use a device configuration profile for Microsoft Defender for Endpoint to deploy the package to your Windows devices.

The configuration package configures devices to communicate with [Microsoft Defender for Endpoint services](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) to scan files and detect threats. The device also reports its risk level to Microsoft Defender for Endpoint based on your compliance policies.

After onboarding a device using the configuration package, you don't need to do it again.

You can also onboard devices using:

- [Endpoint detection and response](../protect/endpoint-security-edr-policy.md) (EDR) policy. Intune EDR policy is part of endpoint security in Intune. Use EDR policies to configure device security without the overhead of the larger body of settings found in device configuration profiles. You can also use EDR policy with tenant attached devices, which are devices you manage with Configuration Manager.

  When you configure EDR policy after connecting Intune and Microsoft Defender for Endpoint, the policy setting *Microsoft Defender for Endpoint client configuration package type* has a new configuration option: **Auto from connector**. With this option, Intune automatically gets the onboarding package (blob) from your Defender for Endpoint deployment, replacing the need to manually configure an *Onboard* package.

- [Group policy or Microsoft Endpoint Configuration Manager](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

> [!TIP]
> When using multiple policies or policy types like *device configuration* policy and *endpoint detection and response* policy to manage the same device settings (such as onboarding to Defender for Endpoint), you can create policy conflicts for devices. To learn more about conflicts, see [Manage conflicts](../protect/endpoint-security-policy.md#manage-conflicts) in the *Manage security policies* article.

### Create the device configuration profile to onboard Windows devices

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.
3. For **Platform**, select **Windows 10 and Later**.
4. For **Profile type**, select **Endpoint detection and response**, and then select **Create**.
5. On the **Basics** page, enter a *Name* and *Description* (optional) for the profile, then choose **Next**.
6. On the **Configuration settings** page, configure the following options for **Endpoint Detection and Response**:

   - **Sample sharing for all files**: Returns or sets the Microsoft Defender for Endpoint Sample Sharing configuration parameter.
   - **Expedite telemetry reporting frequency**: For devices that are at high risk, **Enable** this setting so it reports telemetry to the Microsoft Defender for Endpoint service more frequently.

   [Onboard Windows machines using Microsoft Endpoint Configuration Manager](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) has more details on the Microsoft Defender for Endpoint settings.  

   :::image type="content" source="./media/advanced-threat-protection-configure/automatic-package-configuration.png" alt-text="Screen shot of the configuration options for Endpoint Detection and Response.":::

   > [!NOTE]
   > The preceding screen capture shows your configuration options after you’ve configured a connection between Intune and Microsoft Defender for Endpoint. When connected, the details for the onboarding and offboarding blobs are automatically generated and transferred to Intune.
   >
   > If you haven’t configured this connection successfully, the setting *Microsoft Defender for Endpoint client configuration package type* displays with options to specify onboarding and offboarding blobs.

7. Select **Next** to open the **Scope tags** page. Scope tags are optional. Select **Next** to continue.

8. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   When deploying to user groups, a user must sign in on a device before the policy applies and the device can onboard to Defender for Endpoint.

   Select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.
 **OK**, and then **Create** to save your changes, which creates the profile.

### Onboard macOS devices

After you establish the service-to-service connection between Intune and Microsoft Defender for Endpoint, you can onboard macOS devices to Microsoft Defender for Endpoint. Onboarding configures devices to communicate with Microsoft Defender Endpoint, which then collects data about devices risk level.

For configuration guidance for Intune, see [Microsoft Defender for Endpoint for macOS](../apps/apps-advanced-threat-protection-macos.md).

For more information about Microsoft Defender for Endpoint for Mac, including what's new in the latest release, see [Microsoft Defender for Endpoint for Mac](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-mac?view=o365-worldwide&preserve-view=true) in the Microsoft 365 security documentation.

### Onboard Android devices

After you establish the service-to-service connection between Intune and Microsoft Defender for Endpoint, you can onboard Android devices to Microsoft Defender for Endpoint. Onboarding configures devices to communicate with Defender for Endpoint, which then collects data about the devices risk level.

There isn't a configuration package for devices that run Android. Instead, see [Overview of Microsoft Defender for Endpoint for Android](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) in the Microsoft Defender for Endpoint documentation for the prerequisites and onboarding instructions for Android.

For devices that run Android, you can also use Intune policy to modify Microsoft Defender for Endpoint on Android. For more information, see [Microsoft Defender for Endpoint web protection](../protect/advanced-threat-protection-manage-android.md).

### Onboard iOS/iPadOS devices

After you establish the service-to-service connection between Intune and Microsoft Defender for Endpoint, you can onboard iOS/iPadOS devices to Microsoft Defender for Endpoint. Onboarding configures devices to communicate with Defender for Endpoint, which then collects data about the devices risk level.

There isn't a configuration package for devices that run iOS/iPadOS. Instead, see [Overview of Microsoft Defender for Endpoint for iOS](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-ios) in the Microsoft Defender for Endpoint documentation for prerequisites and onboarding instructions for iOS/iPadOS.

For devices that run iOS/iPadOS (in Supervised Mode), there is specialized ability given the increased management capabilities provided by the platform on these types of devices. To take advantage of these capabilities, the Defender app needs to know if a device is in Supervised Mode. Intune allows you to configure the Defender for iOS app through an App Configuration policy (for managed devices) that should be targeted to all iOS Devices as a best practice.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **App configuration policies** > **Managed devices**.
3. On the **Basics** page, enter a *Name* and *Description* (optional) for the profile, select **Platform** as **iOS/iPadOS** then choose **Next**.
4. Select **Targeted app** as **Microsoft Defender for iOS**.
5. On the **Settings** page, set the **Configuration key** as **issupervised**, then **Value type** as **string** with the **{{issupervised}}** as the **Configuration value**.
6. Select **Next** to open the **Scope tags** page. Scope tags are optional. Select **Next** to continue.
7. On the **Assignments** page, select the groups that will receive this profile. For this scenario, it's a best practice to target **All Devices**. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   When deploying to user groups, a user must sign-in on a device before the policy applies.

   Select **Next**.

8. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list of configuration profiles.

Further, for devices that run iOS/iPadOS (in Supervised Mode), the Defender for iOS team has made available a custom .mobileconfig profile to deploy to iPad/iOS devices. The .mobileconfig profile will be used to analyze network traffic to ensure a safe browsing experience - a feature of Defender for iOS.

1. Download the .mobile profile, which is hosted here: [https://aka.ms/mdatpiossupervisedprofile](https://aka.ms/mdatpiossupervisedprofile).
2. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Devices** > **Configuration profiles** > **Create profile**.
4. For **Platform**, select **iOS/iPadOS**
5. For **Profile type**, select **Custom**, and then select **Create**.
6. On the **Basics** page, enter a *Name* and *Description* (optional) for the profile, then choose **Next**.
7. Enter a *Configuration profile name*, and select a file to .mobileconfig file to Upload.
8. Select **Next** to open the **Scope tags** page. Scope tags are optional. Select **Next** to continue.
9. On the **Assignments** page, select the groups that will receive this profile. For this scenario, it's a best practice to target **All Devices**. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   When deploying to user groups, a user must sign in on a device before the policy applies.

   Select **Next**.

10. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list of configuration profiles.

## Create and assign compliance policy to set device risk level

For Android, iOS/iPadOS, and Windows devices, the compliance policy determines the level of risk that you consider as acceptable for a device.

If you're not familiar with creating compliance policy, reference the [Create a policy](../protect/create-compliance-policy.md#create-the-policy) procedure from the *Create a compliance policy in Microsoft Intune* article. The following information is specific to configuring Microsoft Defender for Endpoint as part of a compliance policy.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance policies** > **Policies** > **Create Policy**.

3. For **Platform**, use the drop-down box to select one of the following options:
   - **Android device administrator**
   - **Android Enterprise**
   - **iOS/iPadOS**
   - **Windows 10 and later**

   Next, select **Create** to open the **Create policy** configuration window.

4. Specify a **Name** that helps you identify this policy later. You can also choose to specify a **Description**.
  
5. On the **Compliance settings** tab, expand the **Microsoft Defender for Endpoint** group and set the option **Require the device to be at or under the machine risk score** to your preferred level.

   Threat level classifications are [determined by Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Clear**: This level is the most secure. The device can't have any existing threats and still access company resources. If any threats are found, the device is evaluated as noncompliant. (Microsoft Defender for Endpoint uses the value *Secure*.)
   - **Low**: The device is compliant if only low-level threats exist. Devices with medium or high threat levels aren't compliant.
   - **Medium**: The device is compliant if the threats found on the device are low or medium. If high-level threats are detected, the device is determined as noncompliant.
   - **High**: This level is the least secure and allows all threat levels. Devices with high, medium, or low threat levels are considered compliant.

6. Complete the configuration of the policy, including assignment of the policy to applicable groups.

## Create and assign app protection policy to set device risk level

Use the procedure to [create an application protection policy for either iOS/iPadOS or Android](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps), and use the following information on the *Apps*, *Conditional launch*, and *Assignments* pages:

- **Apps**: Select the apps you wish to be targeted by app protection policies. For this feature set, these apps are blocked or selectively wiped based on device risk assessment from your chosen Mobile Threat Defense vendor.
- **Conditional launch**:  Below *Device conditions*, use the drop-down box to select **Max allowed device threat level**.

  Options for the threat level **Value**:

  - **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.
  - **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.
  - **High**: This level is the least secure and allows all threat levels, using Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

  Options for **Action**:

  - **Block access**
  - **Wipe data**

- **Assignments**: Assign the policy to groups of users. The devices used by the group's members are evaluated for access to corporate data on targeted apps via Intune app protection.

> [!IMPORTANT]
> If you create an app protection policy for any protected app, the device's threat level is assessed. Depending on the configuration, devices that don’t meet an acceptable level are either blocked or selectively wiped through conditional launch. If blocked, they are prevented from accessing corporate resources until the threat on the device is resolved and reported to Intune by the chosen MTD vendor.

## Create a conditional access policy

Conditional access policies can use data from Microsoft Defender for Endpoint to block access to resources for devices that exceed the threat level you set. You can block access from the device to corporate resources, such as SharePoint or Exchange Online.

> [!TIP]
> Conditional access is an Azure Active Directory (Azure AD) technology. The *Conditional access* node found in the Microsoft Endpoint Manager admin center is the node from *Azure AD*.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Conditional Access** > **New policy**.

3. Enter a policy **Name** and select **Users and groups**. Use the Include or Exclude options to add your groups for the policy, and then select **Done**.

4. Select **Cloud apps**, and then choose which apps to protect. For example, choose **Select apps**, and select **Office 365 SharePoint Online** and **Office 365 Exchange Online**.

   Select **Done** to save your changes.

5. Select **Conditions** > **Client apps** to apply the policy to apps and browsers. For example, select **Yes**, and then enable **Browser** and **Mobile apps and desktop clients**.

   Select **Done** to save your changes.

6. Select **Grant** to apply Conditional Access based on device compliance. For example, select **Grant access** > **Require device to be marked as compliant**.

    Choose **Select** to save your changes.

7. Select **Enable policy**, and then **Create** to save your changes.

## Next steps

- [Configure Microsoft Defender for Endpoint settings on Android](../protect/advanced-threat-protection-manage-android.md)
- [Monitor compliance for risk levels](../protect/advanced-threat-protection-monitor.md)

Learn more from the Intune documentation:

- [Use security tasks with Defender for Endpoints Vulnerability Management to remediate issues on devices](atp-manage-vulnerabilities.md)
- [Get started with device compliance policies](device-compliance-get-started.md)
- [App protection policies overview](../apps/app-protection-policy.md)

Learn more from the Microsoft Defender for Endpoint documentation:

- [Microsoft Defender for Endpoint Conditional Access](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender for Endpoint risk dashboard](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
