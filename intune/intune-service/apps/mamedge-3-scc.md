---
title: Step 3. Integrate Mobile Threat Defense for App Protection Policy
description: Step 3. Integrate Mobile Threat Defense signals with Microsoft Edge for Business app protection policies in Microsoft Intune.
ms.date: 11/07/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---


# Step 3. Integrate Mobile Threat Defense

The Microsoft Mobile Threat Defense (MTD) connector is a feature in Microsoft Intune that creates a channel of communication between Intune and your chosen MTD vendor, regardless of the device’s operating system. There are many supported MTD partners for both Windows and mobile devices. Intune integrates data from an MTD vendor as an information source for device compliance policies, device Conditional Access rules can act on this information to protect corporate resources, such as Exchange and SharePoint online data, by blocking access from compromised devices.

Mobile Application Management (MAM) threat detection can be integrated with various MTD partners, including Windows Security Center. This integration provides a client device health assessment to Intune app protection policies via a service-to-service connector. This assessment supports gating the flow and access to organizational data on personal unmanaged devices.

The health assessment and state includes the following details:

- **User, app, and device identifiers**
- **A predefined health state**
- **The time of last health state update**

Only users enrolled in MAM send health state data. If end users want to stop sending data, they can sign out of their organization account in protected applications. Similarly, administrators can stop data transmission by removing the MTD connector from Microsoft Intune.

## Intune app protection policies

Intune app protection policies help secure organizational data and help ensure client devices are healthy. It also can perform other client health verification via Windows Security Center. This involves designating the Windows Security Center risk level for allowing end users to access corporate resources. In addition, it also involves setting up tenant-based connectors to Microsoft Intune for Windows Security Center.

- **Apps**: Select the apps that you want to target from app protection policies. For this feature set, these apps are blocked or selectively wiped based on device risk assessment from your chosen Mobile Threat Defense vendor.
- **Health Checks**: Under **Device conditions** you can select **Max allowed device threat level**.

> [!IMPORTANT]
> Configure your [Mobile Threat Defense connectors](../protect/mobile-threat-defense.md#mobile-threat-defense-partners) before onboarding users to these policies. If your tenant uses both Microsoft Defender for Endpoint and another MTD partner and you don't designate a primary connector, Intune defaults to Microsoft Defender for Endpoint. For guidance on protecting unenrolled devices, see [Mobile Threat Defense for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md).

### Options for the threat level

You can select one of the following threat level values:

- **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.
- **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
- **Medium**: The device is deemed compliant if the threats found on the device are of low or medium level. If high-level threats are detected, the device is marked as noncompliant.
- **High**: This level is the least secure and allows all threat levels, using Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

### Options for Action

You can select one of the following **Action** options:

- **Block access:** Prevents the users from performing any activity until they're back in compliance.
- **Wipe data:** This removes any information stored in the application related to the corporate data. It doesn't affect personal data on the personal profile.

### Assignments

Assign the policy to groups of users. The devices used by the group's members are evaluated for access to corporate data on targeted apps via Intune app protection.

### Recommended device condition settings

Use the conditional launch settings to maintain progressive security across the Secure Enterprise Browser levels. Configure the following values where the platform supports the setting.

#### Level 1 – Basic

- **Offline grace period (Block access)**: Set to **10080** minutes.
- **Offline grace period (Wipe data)**: Set to **90** days.
- **Max allowed device threat level**: Select **Low**, with the **Block access** action.

#### Level 2 – Enhanced

- **Disabled account**: Set to **Block access**.
- **Min OS version**: Enter **10.0.22621.2506** and select **Block access**.
- **Max allowed device threat level**: Select **Medium**, with the **Block access** action.
- **Offline grace period (Wipe data)**: Set to **30** days.

#### Level 3 – High

App conditions:

- **Offline grace period (Block access)**: Set to **1440** minutes.
- **Offline grace period (Wipe data)**: Set to **30** days.

Device conditions:

- **Min OS version**: Enter **10.0.22621.2506** and select **Block access**.
- **Max OS version**: Enter **10.0.22641** and select **Warn**.
- **Max allowed device threat level**: Select **Secured**, with the **Block access** action.
- **Device threat level**: Select **High**, with the **Block access** action.
- **Mobile Threat Defense apps**: Set to **Enabled/Required**, with the **Block access** action to enforce broker activation.
- **SafetyNet device attestation**: Set to **Pass**, with the **Block access** action. This option appears for Android devices.
- **Require device lockout remediation**: Set to **Enabled**, with the **Block access** action.

> [!TIP]
> These thresholds align with the Secure Enterprise Browser framework's Level 3 (High) posture. Use scope tags and assignments to target the correct Entra ID groups for each level.

> [!IMPORTANT]
> If you create an app protection policy for any protected app, the device's threat level is assessed. Depending on the configuration, devices that don't meet the configured threat level are either blocked or corporate data is selectively wiped through conditional launch. If blocked, they're prevented from accessing corporate resources until the threat on the device is resolved and reported to Intune by the chosen MTD vendor.

## Configure the MTD Connector

Use the following steps to configure the MTD Connector.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant Administrator** > **Connectors and tokens** > **Mobile Threat Defense**.

3. Select **Create** to display the **Add Connector** pane.

4. From the **Select the Mobile Threat Defense connector to setup** dropdown box, select **Windows Security Center**.

    > [!NOTE]
    > In this example, you select **Windows Security Center**. For the full list of MTD Partners, see [Mobile Threat Defense partners](../protect/mobile-threat-defense.md#mobile-threat-defense-partners).

5. Select **Create** to create the connector.

> [!IMPORTANT]
> The connector is now created. It's important to note that the **Connection status** remains **Unavailable** until the first App Protection Policy arrives to the user or the first MAM user is enrolled to your Intune tenant. For more information, see [Connector status](../protect/mobile-threat-defense.md#connector-status).

## Next step

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-04.png" alt-text="Step 2 to create an app protection policy.":::](mamedge-4-app.md)

Continue with [Step 4](mamedge-4-acp-edge.md) to create app configuration policies for Microsoft Edge for Business.
