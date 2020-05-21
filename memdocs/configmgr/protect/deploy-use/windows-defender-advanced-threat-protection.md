---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Learn how to manage and monitor Microsoft Defender Advanced Threat Protection, a new service that helps enterprises respond to advanced attacks.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby


---
# Microsoft Defender Advanced Threat Protection

*Applies to: Configuration Manager (current branch)*

Endpoint Protection can help manage and monitor [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (formerly known as Windows Defender ATP). Microsoft Defender ATP helps enterprises detect, investigate, and respond to advanced attacks on their networks. Configuration Manager policies can help you onboard and monitor Windows 10 clients.

Microsoft Defender ATP is a service in the [Windows Defender Security Center](https://securitycenter.windows.com). By adding and deploying a client onboarding configuration file, Configuration Manager can monitor deployment status and Microsoft Defender ATP agent health. Microsoft Defender ATP is supported on PCs running the Configuration Manager client or [managed by Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## Prerequisites

- Subscription to the Microsoft Defender Advanced Threat Protection online service  
- Clients computers running the Configuration Manager client
- Clients using an OS listed in the [Supported client operating systems](#bkmk_os) section below.

### <a name="bkmk_os"></a> Supported client operating systems
Based on the version of Configuration Manager you're running, the following client operating systems can be onboarded:

#### Configuration Manager version 1910 and prior

- Clients computers running Windows 10, version 1607 and later

#### Configuration Manager version 2002 and later
<!--5229962-->
Starting in Configuration Manager version 2002, you can onboard the following operating systems:

- Windows 8.1
- Windows 10, version 1607 or later
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, version 1803
- Windows Server 2019

## Create an onboarding configuration file

1. Go to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/) and sign in.
1. Select **Machine Management** under **Settings**, and then select **Onboarding**.
1. Select the operating systems you'd like to onboard from the list.
   - If you're onboarding Windows 10, Windows Server 1803, and Windows Server 2019:
      1. Select **Configuration Manager (current branch) version 1606** and select **Download package**.
      1. Download the compressed archive (.zip) file and extract the contents.
   - If you're onboarding another Windows operating system:
      1. Select the operating systems you'd like to onboard from the list presented in the Microsoft Defender ATP online service.
      1. Copy the values for the **Workspace key** and **Workspace ID** from the **Configure connection** section once the process completes.

> [!IMPORTANT]
> - The Microsoft Defender ATP configuration file contains sensitive information which should be kept secure.

## Onboard devices

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Windows Defender ATP Policies** and select **Create Windows Defender ATP Policy**. The Microsoft Defender ATP Policy Wizard opens.  
1. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Onboarding**.
1. **Browse** to the Configuration file provided by your organization's Microsoft Defender ATP cloud service tenant.
   - For Windows 8.1 or Windows Server 2012 R2 and 2016, provide the **Workspace key** and **Workspace ID**.
   - For Configuration Manager version 2002, you'll need the **Workspace key** and **Workspace ID** even if you're onboarding only Windows Server 2019 and Windows Server 1803 or later devices. Get these values by selecting **Settings** > **Onboarding** > **Windows 7 and 8.1** from the [Microsoft Defender ATP online service](https://securitycenter.windows.com/). <!--7054188-->
1. Specify the file samples that are collected and shared from managed devices for analysis.  

   - **None**

   - **All file types**  
1. Review the summary and complete the wizard.  

Select **Deploy** to target the Microsoft Defender ATP policy to clients.

## Monitor

1. In the Configuration Manager console, navigate **Monitoring** > **Security** and then select **Windows Defender ATP**.  

1. Review the Microsoft Defender Advanced Threat Protection dashboard.  

    - **Windows Defender Agent Deployment Status**: The number and percentage of eligible managed client computers with active Microsoft Defender ATP policy onboarded  

    - **Windows Defender ATP Agent Health**: Percentage of computer clients reporting status for their Microsoft Defender ATP agent  

        - **Healthy** - Working properly  

        - **Inactive** - No data sent to service during time period  

        - **Agent state** - The system service for the agent in Windows isn't running  

        - **Not onboarded** - Policy was applied but the agent hasn't reported policy onboard  

## Create an offboarding configuration file  

1. Sign in to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/).

1. Select **Machine Management** under **Settings**, and then select **Onboarding**.  

1. Select **Configuration Manager (current branch) version 1606** and select **Endpoint offboarding**.  

1. Download the compressed archive (.zip) file and extract the contents. Offboarding files are valid for 30 days.

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Windows Defender ATP Policies** and select **Create Windows Defender ATP Policy**. The Microsoft Defender ATP Policy Wizard opens.  

1. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Offboarding**.

1. **Browse** to the Configuration file provided by your organization's Microsoft Defender ATP cloud service tenant.

1. Review the summary and complete the wizard.  

Select **Deploy** to target the Microsoft Defender ATP policy to clients.  

> [!IMPORTANT]
> The Microsoft Defender ATP configuration files contains sensitive information which should be kept secure.

## Next steps

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Troubleshoot Microsoft Defender Advanced Threat Protection onboarding issues](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
