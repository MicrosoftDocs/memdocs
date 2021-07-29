---
# required metadata

title: Use group policy analytics to import GPOs in Microsoft Intune
description: Import and analyze your group policy objects in Microsoft Intune and Endpoint Manager. See the policies that have the same Configuration Service Provider (CSP) setting in the cloud, and assign to your Windows 10 users and devices.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 05/18/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview

Group policy objects (GPOs) are used on-premises to configure settings on personal computers, and other on-premises devices. In device management, GPOs help control security and features in the Windows OS, Internet Explorer, Office apps, and more.

Many organizations are looking at cloud solutions to support the growing remote workforce. **Group Policy analytics** is a tool and feature in Microsoft Endpoint Manager that analyzes your on-premises GPOs. It helps you determine how your GPOs translate in the cloud. The output shows which settings are supported in MDM providers, including Microsoft Intune. It also shows any deprecated settings, or settings not available to MDM providers.

If your organization uses GPOs, and you want to move some workloads to Microsoft Endpoint Manager and Intune, then Group Policy analytics will help.

This feature applies to:

- Windows 10 and newer

This article shows you how export your GPOs, import the GPOs into Endpoint Manager, and review the analysis and results. 

## Prerequisites

Sign in as the Intune administrator with a role that has the **Security Baselines** permission. For example, the **Endpoint Security Manager** role has the **Security Baselines** permission. For more information on the built-in roles, see [role-based access control](../fundamentals/role-based-access-control.md).

## Export GPOs as an XML file

1. On your on-premises computer, open the `Group Policy Management` app (GPMC.msc).
2. Expand your domain to see all the GPOs.
3. Right-click any GPO > **Save report**:

    :::image type="content" source="./media/group-policy-analytics/sample-group-policy-object-save-report.png" alt-text="Open Group Policy management and save a GPO as an XML file report.":::

4. Save the file to an easily accessible folder, and save it as an XML file. You'll add this file in Endpoint Manager.

Be sure the file is less than 750 kB and has a proper unicode encoding. If the exported file is greater than 750 kB, then include fewer GPOs when you save your report from the GPMC.msc tool.

## Use Group Policy analytics

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Group Policy analytics (preview)**.
2. Select **Import**, and then select your saved XML file. When you select the XML file, Intune automatically analyzes the GPO in the XML file.

    Check the sizes of your individual GPO XML files. A single GPO can't be bigger than 750 kB. If a single GPO is larger than 750 kB, then the import will fail. XML files without the appropriate unicode ending will also fail.

3. After the analysis runs, the GPO you imported is listed with the following information:

    - **Group Policy name**: The name is automatically generated using information in the GPO.
    - **Active Directory Target**: The target is automatically generated using the organizational unit (OU) target information in the GPO.
    - **MDM Support**: Shows the percentage of group policy settings in the GPO that have the same setting in Intune.
    - **Targeted in AD**: **Yes** means the GPO is linked to an OU in on-premises group policy. **No** means the GPO isn't linked to an on-premises OU.
    - **Last imported**: Shows the date of the last import.

    You can **Import** more GPOs for analysis, **Refresh** the page, and **Filter** the output. You can also **Export** this view to a `.csv` file:

    :::image type="content" source="./media/group-policy-analytics/import-refresh-filter-options.png" alt-text="Import, refresh, filter, or export a group policy object (GPO) to a CSV file in Microsoft Intune and Endpoint Manager admin center.":::

4. Select the **MDM Support** percentage for a listed GPO. More detailed information about the GPO is shown:

    - **Setting Name**: The name is automatically generated using information in the GPO setting.
    - **Group Policy Setting Category**: Shows the setting category for ADMX settings, such as Internet Explorer and Microsoft Edge. Not all settings have a setting category.
    - **ADMX Support**: **Yes** means there's an ADMX template for this setting. **No** means there isn't an ADMX template for the specific setting.

      For more information on ADMX templates, see [Administrative Templates in Microsoft Intune](administrative-templates-windows.md).

    - **MDM Support**: **Yes** means there's a matching setting available in Endpoint Manager. You can configure this setting in a device configuration profile. Settings in device configuration profiles are mapped to Windows CSPs.

      **No** means there isn't a matching setting available to MDM providers, including Intune.

      For more information on device configuration profiles, see [Apply features and settings on your devices using device profiles](device-profiles.md).

    - **Value**: Shows the value imported from the GPO. It shows different values, such `true`, `900`, `Enabled`, `false`, and so on.
    - **Scope**: Shows if the imported GPO targets users or targets devices.
    - **Min OS Version**: Shows the minimum Windows OS version build numbers that the GPO setting applies. It may show `18362` (1903), `17130` (1803), and other Windows 10 versions.

      For example, if a policy setting shows `18362`, then the setting supports build `18362` and newer builds.

    - **CSP Name**: A Configuration Service Provider (CSP) exposes device configuration settings in Windows 10. This column shows the CSP that includes the setting. For example, you may see Policy, BitLocker, PassportforWork, and so on.

      For more information on CSPs, see the [CSP reference](/windows/client-management/mdm/configuration-service-provider-reference).

    - **CSP Mapping**: Shows the OMA-URI path for the on-premises policy. You can use the OMA-URI in a [custom device configuration profile](custom-settings-configure.md). For example, you may see `./Device/Vendor/MSFT/BitLocker/RequireDeviceEnryption`.

## Supported CSPs

Group Policy analytics can parse the following CSPs:

- [Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider)
- [PassportForWork CSP](/windows/client-management/mdm/passportforwork-csp)
- [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp)
- [Firewall CSP](/windows/client-management/mdm/firewall-csp)
- [AppLocker CSP](/windows/client-management/mdm/applocker-csp)

## Group Policy migration readiness report

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Group policy analytics (preview)**:

    :::image type="content" source="./media/group-policy-analytics/policy-analytics-reports.png" alt-text="Review the report and output of imported GPOs using Group Policy analytics in Microsoft Intune and Endpoint Manager admin center.":::

2. In the **Summary** tab, a summary of the GPO and its policies are shown. Use this information to determine the status of the policies in your GPO:

    - **Ready for migration**: The policy has a matching setting in Intune, and is ready to be migrated to Intune.
    - **Not supported**: The policy doesn't have a matching setting. Typically, policy settings that show this status aren't exposed to MDM providers, including Intune.
    - **Deprecated**: The policy may apply to older Windows versions, and no longer used in Windows 10 and newer.

3. Select the **Reports** tab > **Group policy migration readiness**. In this report, you can:

    - See the number of settings in your GPO that are available in a device configuration profile, if they can be in a custom profile, aren't supported, or are deprecated.
    - Filter the report output using the **Migration Readiness**, **Profile type**, and **CSP Name** filters.
    - Select **Generate report** or **Generate again** to get current data.
    - See the list of settings in your GPO.
    - Use the search bar to find specific settings.
    - Get a time stamp of when the report was last generated. 

    > [!NOTE]
    > After you add or remove your imported GPOs, it can take about 20 minutes to update the Migration Readiness reporting data.


## Send product feedback

You can provide feedback on Group Policy Analytics when you select **Got feedback**. Examples of feedback areas:

- You received errors during GPO import or analytics, and you need more specific information.
- How easy is it to use Group Policy analytics to find the supported group policies in Microsoft Intune?
- Will this tool help you move some workloads to Endpoint Manager? If yes, what workloads are you considering?

To get information on the customer experience, the feedback is aggregated, and sent to Microsoft. Entering an email is optional, and may be used to get more information.

## Privacy and security

Any use of customer data, such as which GPOs are used in your organization, is aggregated. It's not sold to any third parties. This data might be used to make business decisions within Microsoft. Your customer data is stored securely.

At any time, you can delete imported GPOs:

1. Go to **Devices** > **Group Policy analytics (preview)**.
2. Select the context menu > **Delete**:

    :::image type="content" source="./media/group-policy-analytics/delete-imported-gpo.png" alt-text="Delete or remove the group policy object (GPO) you imported in the Group Policy analyzer in Microsoft Intune and Endpoint Manager admin center.":::

## Next steps

- [Use Windows 10 Administrative Templates to configure group policy settings in Microsoft Endpoint Manager](administrative-templates-windows.md)

- [Add endpoint protection settings in Microsoft Endpoint Manager](../protect/endpoint-protection-configure.md)

## See also

Learn more about [Configuration Service Providers (CSP)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).
