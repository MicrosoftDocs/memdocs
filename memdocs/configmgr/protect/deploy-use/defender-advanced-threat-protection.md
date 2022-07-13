---
title: Microsoft Defender for Endpoint
titleSuffix: Configuration Manager
description: Learn how to manage and monitor Microsoft Defender for Endpoint, a new service that helps enterprises respond to advanced attacks.
ms.date: 12/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Microsoft Defender for Endpoint

*Applies to: Configuration Manager (current branch)*

Endpoint Protection can help manage and monitor [Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection). Microsoft Defender for Endpoint helps enterprises detect, investigate, and respond to advanced attacks on their networks. Configuration Manager policies can help you onboard and monitor Windows 10 or later clients.

Microsoft Defender for Endpoint's cloud-based portal is [Microsoft Defender Security Center](https://securitycenter.windows.com). By adding and deploying a client onboarding configuration file, Configuration Manager can monitor deployment status and Microsoft Defender for Endpoint agent health. Microsoft Defender for Endpoint is supported on PCs running the Configuration Manager client or [managed by Microsoft Intune](/intune/protect/advanced-threat-protection).

## Prerequisites

- Subscription to the Microsoft Defender for Endpoint online service  
- Clients computers running the Configuration Manager client
- Clients using an OS listed in the [Supported client operating systems](#bkmk_os) section below.
- Your administrative user account needs the **Endpoint Protection Manager** security role.<!-- MEMDocs#698 -->

### <a name="bkmk_os"></a> Supported client operating systems

<!--5229962-->
You can onboard the following operating systems:

- Windows 8.1
- Windows 10, version  1709 or later
- Windows 11
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server Semi-Annual Channel (SAC), version 1803 or later
- Windows Server 2019
- Windows Server 2022<!-- 10200029 -->

## About onboarding to Microsoft Defender for Endpoint with Configuration Manager

Different operating systems have different needs for onboarding to Microsoft Defender for Endpoint. Windows 8.1 and other down-level operating system devices need the **Workspace key** and **Workspace ID** to onboard. Up-level devices, such as Windows Server version 1803, need the onboarding configuration file. Configuration Manager also installs the Microsoft Monitoring Agent (MMA) when needed by onboarded devices but it doesn't update the agent automatically.

Up-level operating systems include:
- Windows 10, version 1607 and later
- Windows 11
- Windows Server Semi-Annual Channel (SAC), version 1803 or later
- Windows Server 2019
- Windows Server 2022

Down-level operating systems include:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016

> [!Note]
> Currently, the [modern, unified Microsoft Defender for Endpoint for Windows Server 2012 R2 & 2016](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/defending-windows-server-2012-r2-and-2016/bc-p/2904464) is in public preview. Configuration Manager version 2107 with the update rollup supports configuration using Endpoint Protection policies, including those policies created in the Microsoft Endpoint Manager admin center using tenant attach. For more information on how to deploy the preview, see [Server migration scenarios](/microsoft-365/security/defender-endpoint/server-migration).

When you onboard devices to Microsoft Defender for Endpoint with Configuration Manager, you deploy the Defender policy to a target collection or multiple collections. Sometimes the target collection contains devices running any number of the supported operating systems. The instructions for onboarding these devices vary based on if you're targeting a collection containing devices with operating systems that are only up-level or if the collection also includes down-level clients.

- If your target collection contains both up-level and down-level devices, then use the instructions to [onboard devices running any supported operating system](#bkmk_any_os) (recommended).
- If your collection contains only up-level devices, then you can use the [up-level onboarding instructions](#bkmk_uplevel).

> [!Warning]
> - If your target collection contains down-level devices, and you use the instructions for onboarding only up-level devices, then the down-level devices won't be onboarded. The optional **Workspace key** and **Workspace ID** fields are used for onboarding down-level devices, but if they aren't included then the policy will fail on down-level clients.
>
> - In Configuration Manager 2006, or earlier: <!--8715565-->
>   - If you edit an existing policy to add or edit the **Workspace key** and **Workspace ID** fields, you must also provide the configuration file too. If all three items are not provided, the policy will fail on down-level clients. >   - If you need to edit the onboarding file, and also have the **Workspace key** and **Workspace ID** fields populated, provide them again along with the onboarding file. If all three items are not provided, the policy will fail on down-level clients. <!--8715565-->

## <a name="bkmk_any_os"></a> Onboard devices with any supported operating system to Microsoft Defender for Endpoint (recommended)
 You can onboard devices running any of the [supported operating systems](#bkmk_os) to Microsoft Defender for Endpoint by providing the configuration file, **Workspace key**, and **Workspace ID** to Configuration Manager.

### Get the configuration file, workspace ID, and workspace key

1. Go to the [Microsoft Defender for Endpoint online service](https://security.microsoft.com/) and sign in.
1. Select **Settings**, then select **Onboarding** under the **Endpoints** heading.
1. For the operating system, select **Windows 10 and 11**.
1. Choose **Microsoft Endpoint Configuration Manager current branch and later** for the deployment method.
1. Click **Download package**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Onboarding configuration file download" lightbox="media/5229962-onboarding-configuration.png":::
1. Download the compressed archive (.zip) file and extract the contents.
1. Select **Settings**, then select **Onboarding** under the **Device management** heading.
1. For the operating system, select either **Windows 7 SP1 and 8.1** or **Windows Server 2008 R2 Sp1, 2012 R2 and 2016** from the list.
   - The **Workspace key** and **Workspace ID** will be the same regardless of which of these options you choose.
1. Copy the values for the **Workspace key** and **Workspace ID** from the **Configure connection** section.

   > [!IMPORTANT]
   > The Microsoft Defender for Endpoint configuration file contains sensitive information which should be kept secure.


### Onboard the devices

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Microsoft Defender ATP Policies**.
1. Select **Create Microsoft Defender ATP Policy** to open the policy wizard.
1. Type the **Name** and **Description** for the Microsoft Defender for Endpoint policy and select **Onboarding**.
1. **Browse** to the configuration file you extracted from the downloaded .zip file.
1. Supply the **Workspace key** and **Workspace ID** then click **Next**.
   - Verify that the **Workspace key** and **Workspace ID** are in the correct fields. The order in the console may vary from the order in Microsoft Defender for Endpoint online service. <!--8538605-->
   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Create Microsoft Defender for Endpoint Policy Wizard" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Specify the file samples that are collected and shared from managed devices for analysis.  
   - **None**
   - **All file types**  
1. Review the summary and complete the wizard.  
1. Right-click on the policy you created, then select **Deploy** to target the Microsoft Defender for Endpoint policy to clients.

> [!IMPORTANT]
> - In Configuration Manager 2006, or earlier: <!--8715565-->
>   - If you edit an existing policy to add or edit the **Workspace key** and **Workspace ID** fields, you must also provide the configuration file too. If all three items are not provided, the policy will fail on down-level clients. >   - If you need to edit the onboarding file, and also have the **Workspace key** and **Workspace ID** fields populated, provide them again along with the onboarding file. If all three items are not provided, the policy will fail on down-level clients. <!--8715565-->
## <a name="bkmk_uplevel"></a> Onboard devices running only up-level operating systems to Microsoft Defender for Endpoint

Up-level clients require an onboarding configuration file for onboarding to Microsoft Defender for Endpoint. Up-level operating systems include:
- Windows 11
- Windows 10, version 1607 and later 
- Windows Server Semi-Annual Channel (SAC), version 1803 and later
- Windows Server 2019
- Windows Server 2022

If your target collection contains both up-level and down-level devices, or if you're not sure, then use the instructions to [onboard devices running any supported operating system (recommended)](#bkmk_any_os).

### Get an onboarding configuration file for up-level devices

1. Go to the [Microsoft Defender Security Center](https://securitycenter.windows.com/) and sign in.
1. Select **Settings**, then select **Onboarding** under the **Endpoint** heading.
1. For the operating system, select **Windows 10 and 11**.
1. Choose **Microsoft Endpoint Configuration Manager current branch and later** for the deployment method.
1. Click **Download package**.
1. Download the compressed archive (.zip) file and extract the contents.
> [!Note]
> The steps have you download the onboarding file for Windows 10 and 11 but this file is also used for up-level Server operating systems. 

> [!IMPORTANT]
> - The Microsoft Defender for Endpoint configuration file contains sensitive information which should be kept secure.
> - If your target collection contains down-level devices, and you use the instructions for onboarding only up-level devices, then the down-level devices won't be onboarded. The optional **Workspace key** and **Workspace ID** fields are used for onboarding down-level devices, but if they aren't included then the policy will fail on down-level clients.


### Onboard the up-level devices

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Microsoft Defender ATP Policies** and select **Create Microsoft Defender ATP Policy**. The policy wizard opens.  
1. Type the **Name** and **Description** for the Microsoft Defender for Endpoint policy and select **Onboarding**.
1. **Browse** to the configuration file you extracted from the downloaded .zip file.
1. Specify the file samples that are collected and shared from managed devices for analysis.  
   - **None**
   - **All file types**  
1. Review the summary and complete the wizard.  
1. Right-click on the policy you created, then select **Deploy** to target the Microsoft Defender for Endpoint policy to clients.

## Monitor

1. In the Configuration Manager console, navigate **Monitoring** > **Security** and then select **Microsoft Defender ATP**.  

1. Review the Microsoft Defender for Endpoint dashboard.  

    - **Microsoft Defender ATP Agent Onboarding Status**: The number and percentage of eligible managed client computers with active Microsoft Defender for Endpoint policy onboarded  

    - **Microsoft Defender ATP Agent Health**: Percentage of computer clients reporting status for their Microsoft Defender for Endpoint agent  

        - **Healthy** - Working properly  

        - **Inactive** - No data sent to service during time period  

        - **Agent state** - The system service for the agent in Windows isn't running  

        - **Not onboarded** - Policy was applied but the agent hasn't reported policy onboard  

## Create an offboarding configuration file  

1. Sign in to the [Microsoft Defender Security Center](https://securitycenter.windows.com/).
1. Select **Settings**, then select **Offboarding** under the **Endpoint** heading.
1. Select **Windows 10 and 11** for the operating system and **Microsoft Endpoint Configuration Manager current branch and later** for the deployment method.
   - Using the **Windows 10 and 11** option ensures that all devices in the collection are offboarded and the MMA is uninstalled when needed.
1. Download the compressed archive (.zip) file and extract the contents. Offboarding files are valid for 30 days.

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Microsoft Defender ATP Policies** and select **Create Microsoft Defender ATP Policy**. The policy wizard opens.  

1. Type the **Name** and **Description** for the Microsoft Defender for Endpoint policy and select **Offboarding**.

1. **Browse** to the configuration file you extracted from the downloaded .zip file.

1. Review the summary and complete the wizard.  

Select **Deploy** to target the Microsoft Defender for Endpoint policy to clients.  

> [!IMPORTANT]
> The Microsoft Defender for Endpoint configuration files contains sensitive information which should be kept secure.

## Next steps

- [Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Troubleshoot Microsoft Defender for Endpoint onboarding issues](/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
