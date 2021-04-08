---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Learn how to manage and monitor Microsoft Defender Advanced Threat Protection, a new service that helps enterprises respond to advanced attacks.
ms.date: 10/28/2020
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

Endpoint Protection can help manage and monitor [Microsoft Defender Advanced Threat Protection (ATP)](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (formerly known as Windows Defender ATP). Microsoft Defender ATP helps enterprises detect, investigate, and respond to advanced attacks on their networks. Configuration Manager policies can help you onboard and monitor Windows 10 clients.

Microsoft Defender ATP is a service in the [Microsoft Defender Security Center](https://securitycenter.windows.com). By adding and deploying a client onboarding configuration file, Configuration Manager can monitor deployment status and Microsoft Defender ATP agent health. Microsoft Defender ATP is supported on PCs running the Configuration Manager client or [managed by Microsoft Intune](/intune/protect/advanced-threat-protection).

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
- Windows Server 2016, version 1803 or later
- Windows Server 2019

## About onboarding to ATP with Configuration Manager

Different operating systems have different needs for onboarding to ATP. Windows 8.1 and other down-level operating system devices need the **Workspace key** and **Workspace ID** to onboard. Up-level devices, such as Windows Server version 1803, need the onboarding configuration file. Configuration Manager also installs the Microsoft Monitoring Agent (MMA) when needed by onboarded devices but it doesn't update the agent automatically.

Up-level operating systems include:
- Windows 10, version 1607 and later
- Windows Server 2016, version 1803 or later
- Windows Server 2019

Down-level operating systems include:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, version 1709 and earlier

When you onboard devices to ATP with Configuration Manager, you deploy the ATP policy to a target collection or multiple collections. Sometimes the target collection contains devices running any number of the supported operating systems. The instructions for onboarding these devices vary based on if you're targeting a collection containing devices with operating systems that are only up-level or if the collection also includes down-level clients.

- If your target collection contains both up-level and down-level devices, then use the instructions to [onboard devices running any supported operating system](#bkmk_any_os) (recommended).
- If your collection contains only up-level devices, then you can use the [up-level onboarding instructions](#bkmk_uplevel).

> [!Warning]
> - If your target collection contains down-level devices, and you use the instructions for onboarding only up-level devices, then the down-level devices won't be onboarded. The optional **Workspace key** and **Workspace ID** fields are used for onboarding down-level devices, but if they aren't included then the policy will fail on down-level clients.
>
> - In Configuration Manager 2006, or earlier: <!--8715565-->
>   - If you edit an existing policy to add or edit the **Workspace key** and **Workspace ID** fields, you must also provide the configuration file too. If all three items are not provided, the policy will fail on down-level clients. >   - If you need to edit the onboarding file, and also have the **Workspace key** and **Workspace ID** fields populated, provide them again along with the onboarding file. If all three items are not provided, the policy will fail on down-level clients. <!--8715565-->

## <a name="bkmk_any_os"></a> Onboard devices with any supported operating system to ATP (recommended)
 You can onboard devices running any of the [supported operating systems](#bkmk_os) to ATP by providing the configuration file, **Workspace key**, and **Workspace ID** to Configuration Manager.

### Get the configuration file, Workspace ID, and Workspace key

1. Go to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/) and sign in.
1. Select **Settings**, then select **Onboarding** under the **Device management** heading.
1. For the operating system, select **Windows 10**.
1. Choose **Microsoft Endpoint Configuration Manager current branch and later** for the deployment method.
1. Click **Download package**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Onboarding configuration file download" lightbox="media/5229962-onboarding-configuration.png":::
1. Download the compressed archive (.zip) file and extract the contents.
1. Select **Settings**, then select **Onboarding** under the **Device management** heading.
1. For the operating system, select either **Windows 7 SP1 and 8.1** or **Windows Server 2008 R2 Sp1, 2012 R2 and 2016** from the list.
   - The **Workspace key** and **Workspace ID** will be the same regardless of which of these options you choose.
1. Copy the values for the **Workspace key** and **Workspace ID** from the **Configure connection** section.

   > [!IMPORTANT]
   > The Microsoft Defender ATP configuration file contains sensitive information which should be kept secure.


### Onboard the devices

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Microsoft Defender ATP Policies**.
1. Select **Create Microsoft Defender ATP Policy** to open the Microsoft Defender ATP Policy Wizard.
1. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Onboarding**.
1. **Browse** to the configuration file you extracted from the downloaded .zip file.
1. Supply the **Workspace key** and **Workspace ID** then click **Next**.
   - Verify that the **Workspace key** and **Workspace ID** are in the correct fields. The order in the console may vary from the order in Microsoft Defender ATP online service. <!--8538605-->
   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Create Microsoft Defender ATP Policy Wizard" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Specify the file samples that are collected and shared from managed devices for analysis.  
   - **None**
   - **All file types**  
1. Review the summary and complete the wizard.  
1. Right-click on the policy you created, then select **Deploy** to target the Microsoft Defender ATP policy to clients.

> [!IMPORTANT]
> - In Configuration Manager 2006, or earlier: <!--8715565-->
>   - If you edit an existing policy to add or edit the **Workspace key** and **Workspace ID** fields, you must also provide the configuration file too. If all three items are not provided, the policy will fail on down-level clients. >   - If you need to edit the onboarding file, and also have the **Workspace key** and **Workspace ID** fields populated, provide them again along with the onboarding file. If all three items are not provided, the policy will fail on down-level clients. <!--8715565-->
## <a name="bkmk_uplevel"></a> Onboard devices running only up-level operating systems to ATP

Up-level clients require an onboarding configuration file for onboarding to ATP. Up-level operating systems include:
- Windows 10, version 1607 and later 
- Windows Server 2016, version 1803 and later
- Windows Server 2019

If your target collection contains both up-level and down-level devices, or if you're not sure, then use the instructions to [onboard devices running any supported operating system (recommended)](#bkmk_any_os).

### Get an onboarding configuration file for up-level devices

1. Go to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/) and sign in.
1. Select **Settings**, then select **Onboarding** under the **Device management** heading.
1. For the operating system, select **Windows 10**.
1. Choose **Microsoft Endpoint Configuration Manager current branch and later** for the deployment method.
1. Click **Download package**.
1. Download the compressed archive (.zip) file and extract the contents.

> [!IMPORTANT]
> - The Microsoft Defender ATP configuration file contains sensitive information which should be kept secure.
> - If your target collection contains down-level devices, and you use the instructions for onboarding only up-level devices, then the down-level devices won't be onboarded. The optional **Workspace key** and **Workspace ID** fields are used for onboarding down-level devices, but if they aren't included then the policy will fail on down-level clients.


### Onboard the up-level devices

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Microsoft Defender ATP Policies** and select **Create Microsoft Defender ATP Policy**. The Microsoft Defender ATP Policy Wizard opens.  
1. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Onboarding**.
1. **Browse** to the configuration file you extracted from the downloaded .zip file.
1. Specify the file samples that are collected and shared from managed devices for analysis.  
   - **None**
   - **All file types**  
1. Review the summary and complete the wizard.  
1. Right-click on the policy you created, then select **Deploy** to target the Microsoft Defender ATP policy to clients.

## Monitor

1. In the Configuration Manager console, navigate **Monitoring** > **Security** and then select **Microsoft Defender ATP**.  

1. Review the Microsoft Defender Advanced Threat Protection dashboard.  

    - **Microsoft Defender ATP Agent Onboarding Status**: The number and percentage of eligible managed client computers with active Microsoft Defender ATP policy onboarded  

    - **Microsoft Defender ATP Agent Health**: Percentage of computer clients reporting status for their Microsoft Defender ATP agent  

        - **Healthy** - Working properly  

        - **Inactive** - No data sent to service during time period  

        - **Agent state** - The system service for the agent in Windows isn't running  

        - **Not onboarded** - Policy was applied but the agent hasn't reported policy onboard  

## Create an offboarding configuration file  

1. Sign in to the [Microsoft Defender ATP online service](https://securitycenter.windows.com/).
1. Select **Settings**, then select **Offboarding** under the **Device management** heading.
1. Select **Windows 10** for the operating system and **Microsoft Endpoint Configuration Manager current branch and later** for the deployment method.
   - Using the **Windows 10** option ensures that all devices in the collection are offboarded and the MMA is uninstalled when needed.
1. Download the compressed archive (.zip) file and extract the contents. Offboarding files are valid for 30 days.

1. In the Configuration Manager console, navigate to **Assets and Compliance** > **Endpoint Protection** > **Microsoft Defender ATP Policies** and select **Create Microsoft Defender ATP Policy**. The Microsoft Defender ATP Policy Wizard opens.  

1. Type the **Name** and **Description** for the Microsoft Defender ATP policy and select **Offboarding**.

1. **Browse** to the configuration file you extracted from the downloaded .zip file.

1. Review the summary and complete the wizard.  

Select **Deploy** to target the Microsoft Defender ATP policy to clients.  

> [!IMPORTANT]
> The Microsoft Defender ATP configuration files contains sensitive information which should be kept secure.

## Next steps

- [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Troubleshoot Microsoft Defender Advanced Threat Protection onboarding issues](/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
