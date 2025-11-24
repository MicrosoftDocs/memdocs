---
title: Step 6. Deploy Microsoft Edge security baseline
description: Step 6. Deploy the Microsoft Edge security baseline for rapid Windows security configuration.
ms.date: 11/11/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 6: Microsoft Edge Security Baseline

The Microsoft Edge security baseline provides a preconfigured set of security settings that address core browser security requirements and enable rapid deployment of enterprise browser protection. These baselines represent Microsoft’s recommended configuration based on industry best practices and security frameworks.

> [!NOTE]
> Security baselines are only available for Windows enrolled devices and provide a foundation for Level 2 enhanced security. The baseline can be supplemented with extra Settings Catalog policies for Level 3 high security.

**Applies to:**

- Windows (enrolled devices)

> **Microsoft Documentation:**
>
> - [Security Baselines Overview](../protect/security-baselines.md)
> - [Use security baselines to configure Windows devices](../protect/security-baselines-configure.md)
> - [Microsoft Edge Security Baseline](../protect/security-baseline-settings-edge.md)

**Prerequisites:**

- Windows Enterprise
- Intune enrollment
- Microsoft Edge Stable channel

## Deploy Microsoft Edge security baseline

The security baseline provides a foundation for Level 2 enhanced security with Microsoft-validated settings.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Security baselines** > **Security Baseline for Microsoft Edge** > **Create policy** > **Create**.
3. On the **Basics** tab:
    - **Name**: Microsoft Edge Security Baseline - Level 2
    - **Description**: Microsoft Edge security baseline providing Level 2 enhanced security
4. Select **Next**.
5. In **Configuration settings**, expand **Microsoft Edge** and review the preconfigured settings:

| Category | Setting | Value |
|-----------|----------|--------|
| SmartScreen | Configure Microsoft Defender SmartScreen | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
| Privacy & Data | Allow personalization of ads, search, and news | Disabled |
|  | Block tracking of users' web-browsing activity | Balanced |
|  | Send required and optional diagnostic data | Required diagnostic data |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses | Disabled |
|  | Enable AutoFill for payment instruments | Disabled |
| Content & Cookies | Block third party cookies | Enabled |
|  | Configure cookies | Ask |
|  | Default pop-up window setting | Don't allow popups |
|  | Default notification setting | Ask before sending |
| Browser Features | Show Home button on toolbar | Enabled |
|  | Configure the home page URL | about:blank |
|  | Configure the new tab page URL | about:blank |
|  | Configure InPrivate mode availability | Available |
|  | Force synchronization of browser data | Disabled |
| Extensions | Control which extensions can't be installed | Configured |
| Authentication | Supported authentication schemes | ntlm,negotiate |
|  | Allow Basic authentication for HTTP | Disabled |
|  | Allow user-level native messaging hosts | Disabled |
| Encryption | Enable Application Bound Encryption | Enabled |
| Browser Security | Enable browser legacy extension point blocking | Enabled |
| Site Isolation | Enable site isolation for every site | Enabled |
| Internet Explorer Mode | Allow unconfigured sites to be reloaded in Internet Explorer mode | Disabled |
| HTTPS | Allow users to proceed from the HTTPS warning page | Disabled |

> [!NOTE]
> All settings are preconfigured to Microsoft-recommended values. You can accept the defaults or customize specific settings based on organizational requirements.

6. Select **Next**.
7. For **Scope tags**, select the appropriate scope tag.
8. For **Assignments**, assign to **SEB-Level2-Devices** group.
9. Select **Next** to review the settings. Then choose **Create**.

## Create Level 3 enhancements

For Level 3 high security, supplement the baseline with extra Settings Catalog policies.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Security baselines** > **Security Baseline for Microsoft Edge** > **Create policy** > **Create**.
3. On the **Basics** tab:
    - **Name**: Microsoft Edge Security Baseline - Level 3 Enhancements
    - **Description**: More settings to enhance the security baseline for Level 3 high security
4. Select **Next**.
5. In **Configuration settings**, expand **Microsoft Edge** and modify the following settings:

| Category | Setting | Value |
|-----------|----------|--------|
| SmartScreen | Configure Microsoft Defender SmartScreen | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
| Privacy & Data | Allow personalization of ads, search, and news | Disabled |
|  | Block tracking of users' web-browsing activity | Balanced |
|  | Send required and optional diagnostic data | Required diagnostic data |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses | Disabled |
|  | Enable AutoFill for payment instruments | Disabled |
| Content & Cookies | Block third party cookies | Enabled |
|  | Configure cookies | Ask |
|  | Default pop-up window setting | Don't allow popups |
|  | Default notification setting | Ask before sending |
| Browser Features | Show Home button on toolbar | Enabled |
|  | Configure the home page URL | about:blank |
|  | Configure the new tab page URL | about:blank |
|  | Configure InPrivate mode availability | Disabled |
|  | Force synchronization of browser data | Disabled |
| Extensions | Control which extensions can't be installed | Configured |
| Authentication | Supported authentication schemes | negotiate |
|  | Allow Basic authentication for HTTP | Disabled |
|  | Allow user-level native messaging hosts | Disabled |
| Encryption | Enable Application Bound Encryption | Enabled |
| Browser Security | Enable browser legacy extension point blocking | Enabled |
| Site Isolation | Enable site isolation for every site | Enabled |
| Internet Explorer Mode | Allow unconfigured sites to be reloaded in Internet Explorer mode | Disabled |
| HTTPS | Allow users to proceed from the HTTPS warning page | Disabled |

6. Select **Next**.
7. For **Scope tags**, select the appropriate scope tag.
8. For **Assignments**, assign to **SEB-Level3-Devices** group.
9. Select **Next** to review the settings. Then choose **Create**.

## Validation

After deploying the security baseline:

1. **Policy Deployment**: Check Endpoint security > Security baselines > Monitor > Device status
2. **Endpoint Verification**: On device, open edge://policy and verify baseline settings
3. **Settings Precedence**: Verify Level 3 enhancements override baseline defaults
4. **Framework Compliance**: Confirm alignment with NIST Moderate (Level 2) and NIST High (Level 3) controls

## Framework compliance

> [!IMPORTANT]  
> The Microsoft Edge security baseline and its Level 2 and Level 3 configurations **do not make your organization compliant** with any industry security standard. These configurations include **some settings informed by** frameworks such as DISA STIG, NIST, and CISA, but they are **not designed to implement** or achieve compliance with those frameworks. They were used only as **reference input** when developing Microsoft’s recommended security settings.  

### Compliance considerations

Security baselines help you align with industry-standard security frameworks and reduce configuration complexity, but they **do not guarantee compliance** with any standard or certification. Achieving full compliance requires organizations to implement **additional technical, administrative, and procedural controls** beyond the browser configuration, including network and device policies, documentation, and formal assessment processes.  

For more information related to security baselines and framework alignment, see:

- [Security baselines overview](/mem/intune/protect/security-baselines)
- [Windows security baselines](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines)  
- [Windows security baselines FAQ](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines)

## Next steps

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-07.png" alt-text="Step 2 to create an app protection policy.":::](mamedge-7-end-user-experience.md)

Continue to [Step 7](mamedge-7-end-user-experience.md) to understand the Microsoft Edge for Business end user experience.
