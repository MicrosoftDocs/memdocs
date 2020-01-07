---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Learn how to manage and monitor Microsoft Defender Advanced Threat Protection, a new service that helps enterprises respond to advanced attacks.
ms.date: 01/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---
# Microsoft Defender Advanced Threat Protection

*Applies to: Configuration Manager (current branch)*

Endpoint Protection can help manage and monitor [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (formerly known as Windows Defender ATP). Microsoft Defender ATP helps enterprises detect, investigate, and respond to advanced attacks on their networks. Configuration Manager policies can help you onboard and monitor Windows 10 clients.

Microsoft Defender ATP is a service in the [Windows Defender Security Center](https://securitycenter.windows.com). By adding and deploying a client onboarding configuration file, Configuration Manager can monitor deployment status and Microsoft Defender ATP agent health. Microsoft Defender ATP is supported on PCs running the Configuration Manager client or [managed by Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## Prerequisites

- Subscription to the Microsoft Defender Advanced Threat Protection online service  
- Clients computers running Windows 10, version 1607 and later  
- Clients computers running the Configuration Manager client

## Create an onboarding configuration file  

1. Go to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/) and sign in.

2. Select **Machine Management** under **Settings**, and then select **Onboarding**.

3. Select **Configuration Manager (current branch) version 1606** and select  **Download package**.

4. Download the compressed archive (.zip) file and extract the contents.

> [!IMPORTANT]
> The Microsoft Defender ATP configuration file contains sensitive information which should be kept secure.

## Onboard devices

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Windows Defender ATP Policies** and select **Create Windows Defender ATP Policy**. The Microsoft Defender ATP Policy Wizard opens.  

2. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Onboarding**.

3. **Browse** to the Configuration file provided by your organization’s Microsoft Defender ATP cloud service tenant.

4. Specify the file samples that are collected and shared from managed devices for analysis.  

   - **None**

   - **All file types**  

5. Review the summary and complete the wizard.  

Select **Deploy** to target the Microsoft Defender ATP policy to clients.

## Monitor

1. In the Configuration Manager console, navigate **Monitoring** > **Security** and then select **Windows Defender ATP**.  

2. Review the Microsoft Defender Advanced Threat Protection dashboard.  

    - **Windows Defender Agent Deployment Status**: The number and percentage of eligible managed client computers with active Microsoft Defender ATP policy onboarded  

    - **Windows Defender ATP Agent Health**: Percentage of computer clients reporting status for their Microsoft Defender ATP agent  

        - **Healthy** - Working properly  

        - **Inactive** - No data sent to service during time period  

        - **Agent state** - The system service for the agent in Windows isn't running  

        - **Not onboarded** - Policy was applied but the agent has not reported policy onboard  

## Create an offboarding configuration file  

1. Sign in to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/).

2. Select **Machine Management** under **Settings**, and then select **Onboarding**.  

3. Select **Configuration Manager (current branch) version 1606** and select **Endpoint offboarding**.  

4. Download the compressed archive (.zip) file and extract the contents. Offboarding files are valid for 30 days.

5. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Windows Defender ATP Policies** and select **Create Windows Defender ATP Policy**. The Microsoft Defender ATP Policy Wizard opens.  

6. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Offboarding**.

7. **Browse** to the Configuration file provided by your organization’s Microsoft Defender ATP cloud service tenant.

8. Review the summary and complete the wizard.  

Select **Deploy** to target the Microsoft Defender ATP policy to clients.  

> [!IMPORTANT]
> The Microsoft Defender ATP configuration files contains sensitive information which should be kept secure.

## Next steps

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Troubleshoot Microsoft Defender Advanced Threat Protection onboarding issues](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
