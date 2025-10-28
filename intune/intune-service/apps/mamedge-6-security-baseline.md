---
title: Step 6. Deploy Microsoft Edge security baseline
description: Step 6. Deploy the Microsoft Edge security baseline for rapid Windows security configuration.
ms.date: 10/28/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 6: Microsoft Edge Security Baseline

The Microsoft Edge security baseline provides a preconfigured set of 23 security settings that enable rapid deployment of enterprise browser security. Security baselines represent Microsoft's recommended security configuration based on industry best practices and security frameworks.

**Applies to:**
- Windows (enrolled devices)

> [!NOTE]
> Security baselines are only available for Windows enrolled devices and provide a foundation for Level 2 enhanced security. The baseline can be supplemented with extra Settings Catalog policies for Level 3 high security.

## Overview

The Microsoft Edge security baseline includes 23 preconfigured settings that address core browser security requirements. Deploying the baseline provides immediate security hardening without requiring individual setting configuration.

> **Microsoft Documentation:**
> - [Security Baselines Overview](../../protect/security-baselines.md)
> - [Use security baselines to configure Windows devices](../../protect/security-baselines-configure.md)
> - [Microsoft Edge Security Baseline](../../protect/security-baseline-settings-edge.md)

**Prerequisites:**
- Windows 10/11 Enterprise
- Intune enrollment
- Microsoft Edge Stable channel
- Administrative access

## Deploy Microsoft Edge security baseline

The security baseline provides a foundation for Level 2 enhanced security with Microsoft-validated settings.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines**.

3. Select **Microsoft Edge version xxx** (latest available baseline).

4. Select **Create profile**.

5. On the **Basics** tab:
    - **Name**: Microsoft Edge Security Baseline - Level 2
    - **Description**: Microsoft Edge security baseline providing Level 2 enhanced security

6. Select **Next**.

7. On **Configuration settings**, review the 23 preconfigured settings:

    **SmartScreen Protection:**
    - Configure Microsoft Defender SmartScreen: Enabled
    - Configure Microsoft Defender SmartScreen to block potentially unwanted apps: Enabled

    **Privacy & Data:**
    - Allow personalization of ads, search, and news: Disabled
    - Block tracking of users' web-browsing activity: Balanced
    - Send required and optional diagnostic data: Required diagnostic data
    - Enable saving passwords to the password manager: Disabled
    - Enable AutoFill for addresses: Disabled
    - Enable AutoFill for payment instruments: Disabled

    **Content & Cookies:**
    - Block third party cookies: Enabled
    - Configure cookies: Ask
    - Default pop-up window setting: Don't allow popups
    - Default notification setting: Ask before sending

    **Browser Features:**
    - Show Home button on toolbar: Enabled
    - Configure the home page URL: about: blank
    - Configure the new tab page URL: about: blank
    - Configure InPrivate mode availability: Available
    - Force synchronization of browser data: Disabled

    **Extensions:**
    - Control which extensions can't be installed: Configured

    > [!NOTE]
    > All settings are preconfigured to Microsoft-recommended values. You can accept the defaults or customize specific settings based on organizational requirements.

8. Select **Next**.

9. For **Scope tags**, select the appropriate scope tag.

10. For **Assignments**, assign to **SEB-Level2-Devices** group.

11. Select **Next**.

12. On **Review + create**, review the configuration, and select **Create**.

## Create Level 3 enhancements

For Level 3 high security, supplement the baseline with extra Settings Catalog policies.

1. Navigate to **Endpoint security** > **Security baselines** > **Microsoft Edge**.

2. Select the baseline profile you created.

3. Select **Duplicate**.

4. On the **Basics** tab:
    - **Name**: Microsoft Edge Security Baseline - Level 3 Enhancements
    - **Description**: More settings to enhance the security baseline for Level 3 high security

5. Select **Next**.

6. On **Configuration settings**, modify the following settings for Level 3:

    **Enhanced Security:**
    - Configure InPrivate mode availability: Change to **Disabled** (1)

    **Authentication:**
    - Supported authentication schemes: Change from **ntlm,negotiate** to **negotiate** (remove NTLM)

    **Additional Level 3 Controls (keep unchanged from baseline):**
    - Allow unconfigured sites to be reloaded in Internet Explorer mode: Disabled
    - Allow users to proceed from the HTTPS warning page: Disabled
    - Allow Basic authentication for HTTP: Disabled
    - Allow user-level native messaging hosts: Disabled
    - Enable Application Bound Encryption: Enabled
    - Enable browser legacy extension point blocking: Enabled
    - Enable site isolation for every site: Enabled

7. For **Assignments**, assign to **SEB-Level3-Devices** group with **higher priority** than the baseline.

8. Select **Next** and **Create**.

## Validation

After deploying the security baseline:

1. **Policy Deployment**: Check Endpoint security > Security baselines > Monitor > Device status
2. **Endpoint Verification**: On device, open edge://policy and verify baseline settings
3. **Settings Precedence**: Verify Level 3 enhancements override baseline defaults
4. **Framework Compliance**: Confirm alignment with NIST Moderate (Level 2) and NIST High (Level 3) controls

## Benefits of security baselines

**Rapid Deployment:**
- 23 settings configured in under 30 minutes
- No manual configuration required
- Production-ready security

**Best Practices:**
- Microsoft-validated security settings
- Industry framework alignment
- Regular updates from Microsoft

**Consistency:**
- Standardized security posture
- Predictable configuration
- Reduced configuration errors

**Maintenance:**
- Automatic updates when Microsoft releases new baseline versions
- Simplified compliance reporting
- Reduced administrative overhead

## Framework compliance

**Level 2 Baseline:**
- DISA STIG: CAT II/III requirements
- NIST: Moderate controls
- CISA: Enhanced protections

**Level 3 Enhanced:**
- DISA STIG: CAT I compliance
- NIST: High-impact controls
- CISA: Maximum protections

## Next steps

Continue to [Step 7](mamedge-7-end-user-experience.md) to understand the Microsoft Edge for Business end user experience.
