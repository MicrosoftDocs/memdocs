---
title: Onboard and Configure Devices with Microsoft Defender for Endpoint via Microsoft Intune
description: Integrate Microsoft Defender for Endpoint with Microsoft Intune, including connecting the products, onboarding devices, and assigning policies for compliance and risk level assessment.
author: brenduns
ms.author: brenduns
ms.date: 01/28/2026
ms.topic: how-to

ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- sub-secure-endpoints
---

# Configure Microsoft Defender for Endpoint with Intune and Onboard Devices

This article provides step-by-step instructions to integrate Microsoft Defender for Endpoint with Microsoft Intune. This integration enables real-time threat detection, automated compliance enforcement, and centralized endpoint security management across all your devices.
 
Task-specific requirements are listed throughout this article. Also review [general integration prerequisites](../protect/microsoft-defender-with-intune.md#prerequisites).

## What you'll accomplish

After completing this guide, you'll have completed the following integration workflows:

✅ **Service-to-service connection** between Intune and Microsoft Defender for Endpoint  
✅ **Devices onboarded** to Microsoft Defender for Endpoint (Windows, macOS, Android, iOS/iPadOS)  
✅ **Compliance policies** configured to automatically mark risky devices as noncompliant  
✅ **Conditional Access policies** that block compromised devices from corporate resources

## Quick navigation

- [Connect services](#connect-microsoft-defender-for-endpoint-to-intune)
- [Configure integration settings](#configure-integration-settings)
- [Onboard devices](#onboard-devices)
- [Configure compliance policies](#create-and-assign-compliance-policy-to-set-device-risk-level)
- [Configure app protection policies](#create-and-assign-app-protection-policy-to-set-device-risk-level)
- [Set up Conditional Access](#create-a-conditional-access-policy)

**For mobile environments:** This guide also covers [app protection policies](../protect/mtd-app-protection-policy.md) for Android and iOS/iPadOS devices. These policies set device risk levels and work with both enrolled and unenrolled devices, providing additional protection for mobile apps based on Microsoft Defender for Endpoint threat assessments.

**Additional capabilities:** Beyond enrolled devices, you can also manage Defender for Endpoint security configurations on devices that aren't enrolled with Intune (including Linux devices). This scenario is called *Security Management for Microsoft Defender for Endpoint*. To enable this, set the *Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations* toggle to *On*. For details, see [Microsoft Defender for Endpoint Security Configuration Management](../protect/mde-security-integration.md).

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]   <!-- How long should we persist this note? This dates to June 2024. -->

## Connect Microsoft Defender for Endpoint to Intune

**Prerequisites:**  
- Admin access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with **Endpoint Security Manager** role or equivalent permissions for *Mobile Threat Defense* settings (custom roles require *Read* and *Modify* rights for the *Mobile Threat Defense* permission).
- Admin access to the [Microsoft Defender XDR portal](https://security.microsoft.com) with [Security Administrator](/entra/identity/role-based-access-control/permissions-reference#security-administrator) role in Microsoft Entra ID, or **"Manage security settings in Security Center"** permission in Microsoft Defender for Endpoint.

This one-time setup per tenant establishes the service-to-service connection that enables integration features.

### Enable Intune and Microsoft Defender for Endpoint integration

1. **Check connection status first:** Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Endpoint security** > **Microsoft Defender for Endpoint**.

   - If **Connection status** shows **Enabled**, the services are already connected. Skip to [For app protection policy evaluation](#onboard-devices).
   - If **Connection status** shows **Unavailable**, continue with the next step.

2. **Open Microsoft Defender XDR portal:** From the Intune admin center, scroll to the bottom of the *Microsoft Defender for Endpoint* page and select **Open the Microsoft Defender Security Center** (or navigate directly to [security.microsoft.com](https://security.microsoft.com)).

   > [!TIP]
   > If already connected, the link reads: **Open the Microsoft Defender for Endpoint admin console**.

   :::image type="content" source="./media/microsoft-defender-integrate/open-microsoft-defender.png" alt-text="Screen shot that shows the patch to open the Microsoft Defender Security Center.":::

3. **Enable the connection in Microsoft Defender portal:**

   1. Navigate to **Settings** > **Endpoints** > **General** > **Advanced features**.

      > [!TIP]
      > The location of **Settings** varies depending on your portal layout: **Settings** can appear as a top-level menu item, or you might need to navigate to **System** > **Settings**. If you can't locate **Endpoints**, verify you have the required permissions [listed in the prerequisites for this task](#connect-microsoft-defender-for-endpoint-to-intune).

      :::image type="content" source="./media/microsoft-defender-integrate/defender-console-settings-endpoints.png" alt-text="Screen shot of the Defender console showing the path to Settings and then Endpoints.":::

   2. Locate **Microsoft Intune connection** and toggle it to **On**.

      :::image type="content" source="./media/microsoft-defender-integrate/intune-connection-toggle.png" alt-text="Screen shot of the Microsoft Intune connection setting.":::

   3. Select **Save preferences**.

4. **Validation:** Return to the Intune admin center. The **Connection status** should now show **Enabled** (it can take up to 15 minutes to update). Services sync automatically every 24 hours, and you can adjust monitoring settings under **Endpoint security** > **Microsoft Defender for Endpoint** if needed.

**Congratulations!** The service-to-service connection is now established. Next, configure which platforms and features use this integration.

## Configure integration settings

**Prerequisites:** Admin access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with **Endpoint Security Manager** role or equivalent permissions for *Mobile Threat Defense* settings (custom roles require *Read* and *Modify* rights for the *Mobile Threat Defense* permission).

**What this accomplishes:** Choose which device platforms connect to Microsoft Defender for Endpoint and enable specific integration features like compliance evaluation and app protection policies.

### Configure these settings based on your environment

1. **Navigate to integration settings:** In the Microsoft Intune admin center, go to **Endpoint security** > **Microsoft Defender for Endpoint**. The Connection status should now show **Enabled**.

2. **Configure compliance policy evaluation:** Enable these options under **Compliance policy evaluation** for your supported platforms:

   - **Connect Android devices to Microsoft Defender for Endpoint**: **On**
   - **Connect iOS/iPadOS devices to Microsoft Defender for Endpoint**: **On**  
   - **Connect Windows devices to Microsoft Defender for Endpoint**: **On**

   > [!NOTE]
   > When enabled, all applicable devices you currently manage with Intune, plus future enrollments, will be connected to Microsoft Defender for Endpoint for compliance evaluation.

   > [!TIP]
   > **Additional iOS settings:** For iOS devices, Defender for Endpoint also supports settings that help provide Vulnerability Assessment of apps. You can enable **App Sync for iOS Devices** to allow metadata sharing for threat analysis (requires MDM enrollment), and configure **Send full application inventory data on personally owned iOS/iPadOS Devices** to control what app data is shared with Defender for Endpoint. For details, see [Configure vulnerability assessment of apps](/microsoft-365/security/defender-endpoint/ios-configure-features#configure-vulnerability-assessment-of-apps).

   For more information, see [Mobile Threat Defense toggle options](../protect/mtd-connector-enable.md#mobile-threat-defense-toggle-options).

3. **Configure app protection policy evaluation:** Enable these options under **App protection policy evaluation** for mobile platforms:
   - **Connect Android devices to Microsoft Defender for Endpoint**: **On**
   - **Connect iOS/iPadOS devices to Microsoft Defender for Endpoint**: **On**

   > [!TIP]
   > App protection policies work with both enrolled and unenrolled devices. For details, see [Mobile Threat Defense toggle options](../protect/mtd-connector-enable.md#mobile-threat-defense-toggle-options).

4. **Save your configuration:** Select **Save** to apply all settings.

**What's next:** Your integration is configured! The platforms you enabled will now connect devices to Microsoft Defender for Endpoint for threat assessment and compliance evaluation.

> [!IMPORTANT]
> **Classic Conditional Access cleanup:** As of August 2023, Intune no longer creates classic Conditional Access policies for Microsoft Defender for Endpoint. If your tenant has legacy policies from previous integrations, you can safely delete them. To check: **Azure portal** > **Microsoft Entra ID** > **Conditional Access** > **Classic policies**.

## Onboard devices

**Prerequisites:** Admin access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with **Endpoint Security Manager** role or equivalent permissions for *Endpoint detection and response* policies (custom roles require *Assign*, *Create*, *Delete*, *Read*, *Update*, and *View Reports* rights for the *Endpoint Detection and Response* permission).

**What this accomplishes:** Device onboarding configures your managed devices to communicate with Microsoft Defender for Endpoint, enabling threat detection and risk assessment.

After establishing the service-to-service connection, onboard your devices by platform. This process enrolls devices into the Defender for Endpoint service for threat protection and risk monitoring.

> [!TIP]
> **Version requirement:** Always use the latest Microsoft Defender for Endpoint version for each platform to ensure optimal protection and compatibility.

**Platform-specific onboarding:**

- **Windows**: Automatic onboarding package (recommended)
- **macOS, Android, iOS/iPadOS**: Manual configuration required

### Onboard Windows devices

**What happens:** Intune uses an automatic onboarding package from Microsoft Defender for Endpoint to configure Windows devices for threat detection and compliance reporting.

With the service connection established, Intune automatically receives an onboarding configuration package from Microsoft Defender for Endpoint. This package enables:

- Communication with [Microsoft Defender for Endpoint services](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)
- File scanning and threat detection
- Risk level reporting for compliance policies

> [!NOTE]
> Device onboarding is a one-time action per device.

**Choose your deployment approach:**

- **Quick setup**: Preconfigured policy (deploys to all devices)
- **Custom setup**: Manual policy creation (granular control)

#### Option 1: Quick setup (preconfigured policy)

**Best for:** Fast deployment to all Windows devices

**What's included:**
  
- Automatic onboarding package configuration
- Default scope tag
- Assignment to *All Devices* group
- No additional configuration required

##### Quick setup steps

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Endpoint detection and response** > **EDR Onboarding Status** tab.

2. Select **Deploy preconfigured policy**.

   :::image type="content" source="./media/microsoft-defender-integrate/select-preconfigured-policy.jpg" alt-text="Screen shot that displays the path to the preconfigured policy option.":::

3. Configure the policy:
   - **Platform**: Select **Windows** (for Intune-managed) or **Windows (ConfigMgr)** (for Tenant Attach)
   - **Profile**: Select **Endpoint detection and response**
   - **Name**: Enter a descriptive name (for example, "MDE EDR Onboarding - All Windows Devices")

4. **Review and create**: Verify settings and select **Save**. The policy immediately starts deploying to all Windows devices.

   > [!NOTE]
   > You can edit policy details later, but initial deployment settings can't be changed during creation.

#### Option 2: Custom setup (manual policy creation)

**Best for:** Granular control, specific device groups, or custom settings

**Benefits:**

- Choose specific device groups
- Configure advanced settings
- Set custom scope tags

##### Custom setup steps

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

2. **Platform and profile:**
   - **Platform**: **Windows**
   - **Profile**: **Endpoint detection and response**
   - Select **Create**

3. **Basics:** Enter a descriptive name and optional description, then select **Next**.

4. **Configuration settings:** Configure these options based on your requirements:

   - **Microsoft Defender for Endpoint client configuration package type**:  
     - **Auto from connector** (recommended): Uses the automatic onboarding package from Microsoft Defender for Endpoint.
     - **Onboard**: For disconnected environments - paste the WindowsDefenderATP.onboarding blob content.

   - **Sample Sharing**: Configure whether devices share suspicious file samples with Microsoft for analysis.  
     - **On**: Enables automatic sample sharing for enhanced threat detection
     - **Off**: Disables sample sharing (can reduce detection capabilities).

   > [!NOTE]
   > **Telemetry Reporting Frequency** is deprecated and doesn't affect new devices. The setting remains visible for older policy compatibility.

   :::image type="content" source="./media/microsoft-defender-integrate/automatic-package-configuration.png" alt-text="Screen shot of the configuration options for Endpoint Detection and Response.":::

   > [!NOTE]
   >
   > The preceding screen capture shows your configuration options after a connection between Intune and Microsoft Defender for Endpoint is set up. When connected, the details for the onboarding and offboarding blobs are automatically generated and transfer to Intune.
   >
   > If this connection isn't successfully configured, the setting *Microsoft Defender for Endpoint client configuration package type* only includes options to specify onboard and offboard blobs.

5. **Scope tags** (optional): Add scope tags if needed, then select **Next**.

6. **Assignments**: Select device groups that receive this profile.

   > [!IMPORTANT]
   > - **Device groups**: Recommended for immediate deployment.
   > - **User groups**: Requires user sign-in before policy applies.

   For assignment guidance, see [Assign user and device profiles](../configuration/device-profile-assign.md).

7. **Review + create**: Verify all settings and select **Create**.

##### Validation steps

1. **Check policy deployment**: Navigate to **Endpoint security** > **Endpoint detection and response** > Select your policy > **Device status**.
2. **Verify device onboarding**: After 15-30 minutes, devices should appear in the [Microsoft Defender XDR portal](https://security.microsoft.com) under **Endpoints** > **Device inventory**.

> [!TIP]
> **Avoid policy conflicts:** Multiple policies managing the same settings can cause conflicts. See [Manage policy conflicts](../protect/endpoint-security-policy.md#manage-policy-conflicts) for resolution guidance.

### Onboard macOS devices

**Method:** Manual app deployment and configuration

Unlike Windows devices, macOS requires manual configuration since Intune doesn't provide automatic onboarding packages for macOS.

#### macOS onboarding quick start

1. **Deploy the app**: Follow the [Microsoft Defender for Endpoint for macOS](../apps/apps-advanced-threat-protection-macos.md) deployment guide.
2. **Configure settings**: Use Intune app configuration policies.
3. **Verify onboarding**: Check device appears in Microsoft Defender XDR portal.

**Additional resources:**

- [Microsoft Defender for Endpoint for Mac](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-mac?view=o365-worldwide&preserve-view=true) - Complete feature documentation and release notes.

### Onboard Android devices

**Method:** App deployment with configuration policies

#### Android onboarding quick start

1. **Deploy the app**: Follow [Microsoft Defender for Endpoint for Android](/defender-endpoint/microsoft-defender-atp-android) prerequisites and onboarding instructions.
2. **Configure web protection**: Use [Microsoft Defender for Endpoint web protection](../protect/microsoft-defender-configure-android.md) policies for additional security.
3. **Verify onboarding**: Confirm device registration in Microsoft Defender XDR portal.

**Available configurations:**

- Web protection settings
- VPN-based scanning
- Privacy controls
- Threat detection preferences

### Onboard iOS/iPadOS devices

**Method:** App deployment with device configuration

#### iOS onboarding quick start

1. **Deploy the app**: Follow [Microsoft Defender for Endpoint for iOS](/defender-endpoint/microsoft-defender-atp-ios) prerequisites and onboarding instructions.
2. **Configure supervision detection**: Set up supervised mode detection for enhanced features
3. **Verify onboarding**: Check device registration in Microsoft Defender XDR portal.

**Supervised mode configuration:** - For supervised iOS/iPadOS devices, configure supervision detection to enable advanced management features. See [Complete deployment for supervised devices](/microsoft-365/security/defender-endpoint/ios-install#complete-deployment-for-supervised-devices).

#### Configuration steps for supervised devices

1. **Create app configuration policy:** In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add** > **Managed devices**.

2. **Configure basics:**
   - **Name**: Enter descriptive name (for example, "MDE Supervision Detection - iOS")
   - **Platform**: **iOS/iPadOS**
   - **Targeted app**: **Microsoft Defender for Endpoint**

3. **Configuration settings:**
   - **Configuration key**: `issupervised`
   - **Value type**: **String**
   - **Configuration value**: `{{issupervised}}`

4. **Assignment**: Target **All Devices** or specific supervised device groups.

5. **Review + create**: Complete policy creation.

### Monitor device onboarding status

**Track your progress:** Monitor which devices successfully onboard to Microsoft Defender for Endpoint.

**To view onboarding status:**

1. In the Microsoft Intune admin center, go to **Endpoint security** > **Endpoint detection and response** > **EDR Onboarding Status** tab
2. Review the onboarding status for all platforms

**Required permission:** Your account needs *Read* permission for *Microsoft Defender Advanced Threat Protection* in Intune RBAC.

**Success indicators:**

- Devices appear in the Microsoft Defender XDR portal under **Endpoints** > **Device inventory**
- EDR Onboarding Status shows "Successfully onboarded"
- Risk levels begin appearing in device compliance reports

## Create and assign compliance policy to set device risk level

**Prerequisites:**  
- Admin access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with **Endpoint Security Manager** role or equivalent permissions for *Device compliance policies* (custom roles require *Assign*, *Create*, *Delete*, *Read*, and *Update* rights for the *Device compliance policies* permission).

**Purpose:** Define acceptable device risk levels and automatically mark high-risk devices as noncompliant

**Supported platforms:** Android, iOS/iPadOS, and Windows devices

> [!TIP]
> New to compliance policies? See the [Create a policy](../protect/create-compliance-policy.md#create-the-policy) guide for general instructions. The following steps focus specifically on Microsoft Defender for Endpoint integration.

**What this accomplishes:** Devices exceeding your defined risk threshold are automatically marked as noncompliant, enabling Conditional Access to block them from corporate resources.

### Steps to create the policy

1. **Navigate to compliance policies:** In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Compliance** > **Policies** tab > **Create policy**.

2. **Select platform:** Choose your target platform:
   - **Android device administrator** (limited support)
   - **Android Enterprise** (recommended for Android)
   - **iOS/iPadOS**
   - **Windows 10 and later**

   > [!IMPORTANT]
   > [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

3. **Configure basics:**
   - **Name**: Enter a descriptive name (for example, "MDE Risk Level - Windows Devices")
   - **Description**: Optional details about the policy purpose

4. **Set risk threshold:** On the **Compliance settings** tab, expand **Microsoft Defender for Endpoint** and configure **Require the device to be at or under the machine risk score**:

   **Risk level options** ([determined by Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue)):

   - **Clear (Most Secure)**:
     - **Allows**: No threats
     - **Blocks**: Any detected threats
     - **Use when**: Maximum security required

   - **Low**:
     - **Allows**: Low-level threats only
     - **Blocks**: Medium and high threats
     - **Use when**: Balanced security and productivity

   - **Medium**:
     - **Allows**: Low and medium threats
     - **Blocks**: High-level threats only
     - **Use when**: Moderate security requirements

   - **High (Least Secure)** ⚠️⚠️⚠️
     - **Allows**: All threat levels
     - **Blocks**: None (reporting only)
     - **Use when**: Maximum productivity, minimal blocking

   > [!IMPORTANT]
   > **Recommended setting**: **Low** provides the best balance of security and user productivity for most organizations.

5. **Complete configuration:**
   - **Actions for noncompliance**: Configure notifications and grace periods
   - **Assignments**: Select device or user groups to receive this policy
   - **Review + create**: Verify settings and create the policy

6. **Validation:**:
   - Devices exceeding the risk threshold show as "Not compliant" in **Devices** > **Compliance** > **Device compliance**
   - Check **Reports** > **Device compliance** for compliance trends

## Create and assign app protection policy to set device risk level

**Prerequisites:**  
- Admin access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with **Endpoint Security Manager** role or equivalent permissions for security-related *Mobile apps* policies (custom roles require *Assign*, *Create*, *Delete*, *Read*, *Update*, and *Wipe* rights for the *Managed apps* permission).

**Purpose:** Protect app data based on device threat levels for both enrolled and unenrolled devices

**Platforms:** iOS/iPadOS and Android only

> [!NOTE]
> App protection policies work independently of device enrollment, providing an additional layer of security for mobile applications.

**Quick start:** Follow the [application protection policy creation guide](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps) and configure these Microsoft Defender for Endpoint-specific settings:

- **Apps**: Select apps to be protected by threat-based policies
- **Conditional launch**: Configure threat level and response actions:
  - **Max allowed device threat level**:
    - **Secured**: No threats allowed (most secure)
    - **Low**: Only low-level threats permitted
    - **Medium**: Low and medium threats permitted
    - **High**: All threat levels permitted (reporting only)
  - **Actions** when threshold exceeded:
    - **Block access**: Prevent app access
    - **Wipe data**: Remove corporate data from the app

- **Assignments**: Assign to groups of users, whose devices are evaluated for app-level protection

> [!IMPORTANT]
> App protection policies evaluate all protected apps. Devices exceeding the threshold are blocked or wiped through conditional launch, regardless of enrollment status.

## Create a Conditional Access policy

**Prerequisites:**
- Admin access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
- Permissions equal to the [Conditional Access Administrator](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator) role in Microsoft Entra ID for managing Conditional Access policies.

**Purpose:** Block noncompliant devices from accessing corporate resources automatically

**What this accomplishes:** Devices marked as noncompliant (due to high risk levels) are automatically blocked from accessing corporate resources like SharePoint and Exchange Online.

> [!NOTE]
> Conditional Access is a Microsoft Entra technology. The Intune admin center provides direct access to the same Conditional Access configuration available in the Azure portal.

### Steps to create the policy

1. **Navigate to Conditional Access:** In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Endpoint security** > **Conditional Access** > **Create new policy**.

2. **Basic configuration:**
   - **Name**: Enter descriptive name (for example, "Block Noncompliant Devices - MDE Integration")

3. **User assignment:**
   - **Include**: Select user groups that should be subject to this policy
   - **Exclude**: Optionally exclude specific users (like emergency access accounts)

4. **Resource protection:**
   - **Target resources**: Select **Cloud apps**
   - **Include**: Choose **Select apps** and add:
     - Office 365 SharePoint Online
     - Office 365 Exchange Online
     - Other corporate applications as needed

5. **Client app conditions:**
   - **Conditions** > **Client apps** > **Configure**: **Yes**
   - Select: **Browser** and **Mobile apps and desktop clients**
   - Select **Done**

6. **Access controls:**
   - **Grant** > **Grant access**
   - Select: **Require device to be marked as compliant**
   - **For multiple controls**: **Require all the selected controls**
   - Select **Select**

7. **Enable policy:** Set to **On** and select **Create**.

8. **Validation:**: Test with a noncompliant device to ensure access is properly blocked. Check **Microsoft Entra ID** > **Sign-ins** for policy enforcement logs.

## Next steps

**You've successfully integrated Microsoft Defender for Endpoint with Intune!** 🎉

### Immediate next steps

1. **Monitor deployment**: Check [device onboarding status](#monitor-device-onboarding-status) and compliance reports
2. **Validate protection**: Test with controlled scenarios to ensure policies work as expected
3. **Expand protection**: Consider [vulnerability management](atp-manage-vulnerabilities.md) for proactive threat remediation

### Platform-specific enhancements

- **Android**: [Configure web protection settings](../protect/microsoft-defender-configure-android.md)
- **All platforms**: [Monitor compliance for risk levels](../protect/microsoft-defender-monitor.md)

### Advanced features

**Intune integration:**
- [Security tasks with Vulnerability Management](atp-manage-vulnerabilities.md) - Remediate device vulnerabilities
- [Device compliance policies](device-compliance-get-started.md) - Comprehensive compliance management
- [App protection policies](../apps/app-protection-policy.md) - Mobile app data protection
- [Mobile app protection policies](../protect/mtd-app-protection-policy.md) - For Android and iOS/iPadOS devices, these policies set device risk levels, and work with both enrolled and unenrolled devices
- [Security Management for unenrolled devices](../protect/mde-security-integration.md) - Manage Defender for Endpoint security configurations on devices that aren't enrolled with Intune (including Linux devices)

**Microsoft Defender for Endpoint:**
- [Conditional Access integration](/defender-endpoint/conditional-access) - Advanced access control scenarios
- [Security operations dashboard](/defender-endpoint/security-operations-dashboard) - Threat monitoring and response

### Support resources

- **Integration issues**: Check [troubleshooting guide](../protect/microsoft-defender-monitor.md)
- **Policy conflicts**: See [policy conflict resolution](../protect/endpoint-security-policy.md#manage-policy-conflicts)
- **Updates**: Monitor [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap) for new features
