---
# required metadata

title: Use group policy analytics to import and analyze GPOs in Microsoft Intune
description: Import and analyze your group policy objects in Microsoft Intune and Endpoint Manager. See the policies that are supported and aren't supported in cloud MDM providers.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 05/05/2022
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
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Analyze your on-premises GPOs using Group Policy analytics in Microsoft Endpoint Manager (public preview)

> [!TIP]
> Looking for information on ADMX templates? See [Use Windows 10/11 Administrative Templates to configure group policy settings in Microsoft Endpoint Manager](administrative-templates-windows.md).

Microsoft Intune has many of the same settings as your on-premises GPOs. **Group Policy analytics** is a tool in Microsoft Endpoint Manager that:

- Analyzes your on-premises GPOs.
- Shows the settings that are supported by cloud-based MDM providers, including Microsoft Intune.
- Shows any deprecated settings, or settings not available.
- Can [migrate your imported GPOs to a settings catalog policy](group-policy-analytics-migrate.md) that can be deployed to your devices.

If your organization uses on-premises GPOs to manage Windows 10/11 devices, then Group Policy analytics will help. With Group Policy analytics, it's possible Intune can replace your on-premises GPOs. Windows 10/11 devices are inherently cloud native. So depending on your configuration, these devices might not require access to an on-premises Active Directory.

If you're ready to remove the dependency to on on-premises AD, then analyzing your GPOs with **Group Policy analytics** is a good first step. Some older settings aren't supported, or don't apply to cloud native Windows devices. After you analyze your GPOs, you'll know which settings might still be valid.

This feature applies to:

- Windows 11
- Windows 10

This article shows you how export your GPOs, import the GPOs into Endpoint Manager, and review the analysis and results. To migrate or transfer your imported GPOs to an Intune policy, go to [Create a Settings Catalog policy using your imported GPOs in Microsoft Endpoint Manager (public preview)](group-policy-analytics-migrate.md).

## Before you begin

- In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in as the Intune administrator or with a role that has the **Security Baselines** permission.

  For example, the **Endpoint Security Manager** role has the **Security Baselines** permission. For more information on the built-in roles, see [role-based access control](../fundamentals/role-based-access-control.md).

- This feature is in public preview. For more information, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

## Export GPO as an XML file

1. On your on-premises computer, open the `Group Policy Management` console (GPMC.msc).
2. In the manageent console, expand your **domain name**.
3. Then expand **Group Policy Objects** to see all the available GPOs.
4. Right-click the GPO you want to migrate and choose **Save report**:

    :::image type="content" source="./media/group-policy-analytics/sample-group-policy-object-save-report.png" alt-text="Open Group Policy management and save a GPO as an XML file report.":::

4. Select an easily accessible folder for your export and choose "Save as type" **XML File**. You'll add this file in Endpoint Manager group policy analytics.

Be sure the file is less than 4 MB and has a proper unicode encoding. 
If the exported file is greater than 4 MB, then you must reduce the amount of settings within the selected group policy object.

## Import GPOs and run analytics

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Group Policy analytics (preview)**.
2. Select **Import**, and then select your saved XML file (you can select multiple files at once). When you select the XML file, Intune automatically analyzes the GPO in the XML file.

    Check the sizes of your individual GPO XML files. A single GPO can't be bigger than 4 MB. If a single GPO is larger than 4 MB, then the import will fail. XML files without the appropriate unicode ending will also fail.

3. After the analysis runs, the GPO you imported is listed with the following information:

    - **Group Policy name**: The name is automatically generated using information in the GPO.
    - **Active Directory Target**: The target is automatically generated using the organizational unit (OU) target information in the GPO.
    - **MDM Support**: Shows the percentage of group policy settings in the GPO that have the same setting in Intune.  

        > [!NOTE]
        > Whenever the Microsoft Intune product team makes changes to the mapping in Intune, the percentage under MDM Support automatically updates to reflect those changes.

    - **Unknown Settings**: There are some CSPs that can't be analyzed. **Unknown Settings** lists the GPOs that can't be analyzed.
    - **Targeted in AD**: **Yes** means the GPO is linked to an OU in on-premises group policy. **No** means the GPO isn't linked to an on-premises OU.
    - **Last imported**: Shows the date of the last import.

    You can **Import** more GPOs for analysis, **Refresh** the page, and **Filter** the output. You can also **Export** this view to a `.csv` file:

    :::image type="content" source="./media/group-policy-analytics/import-refresh-filter-options.png" alt-text="Import, refresh, filter, or export a group policy object (GPO) to a CSV file in Microsoft Intune and Endpoint Manager admin center.":::

4. Select the **MDM Support** percentage for a listed GPO. More detailed information about the GPO is shown:  

    - **Setting Name**: The name is automatically generated using information in the GPO setting.
    - **Group Policy Setting Category**: Shows the setting category for ADMX settings, such as Internet Explorer and Microsoft Edge. Not all settings have a setting category.
    - **MDM Support**: 

      - **Yes** means there's a matching setting available in Endpoint Manager. You can configure this setting in the Settings Catalog.
      - **No** means there isn't a matching setting available to MDM providers, including Intune.

    - **Value**: Shows the value imported from the GPO. It shows different values, such `true`, `900`, `Enabled`, `false`, and so on.
    - **Scope**: Shows if the imported GPO targets users or targets devices.
    - **Min OS Version**: Shows the minimum Windows OS version build numbers that the GPO setting applies. It may show `18362` (1903), `17130` (1803), and other Windows client versions.

      For example, if a policy setting shows `18362`, then the setting supports build `18362` and newer builds.

    - **CSP Name**: A Configuration Service Provider (CSP) exposes device configuration settings in Windows client. This column shows the CSP that includes the setting. For example, you may see Policy, BitLocker, PassportforWork, and so on.

      The [CSP reference](/windows/client-management/mdm/configuration-service-provider-reference) lists the available CSPs, shows the supported OS editions, and more.

    - **CSP Mapping**: Shows the OMA-URI path for the on-premises policy. You can use the OMA-URI in a [custom device configuration profile](custom-settings-configure.md). For example, you may see `./Device/Vendor/MSFT/BitLocker/RequireDeviceEnryption`.

5. For the settings that have MDM support, you can create a Settings Catalog policy with these settings. For the specific steps, go to [Create a Settings Catalog policy using your imported GPOs in Microsoft Endpoint Manager (public preview)](group-policy-analytics-migrate.md).

## Supported CSPs and group policies

Group Policy analytics can parse the following CSPs:

- [Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider)
- [PassportForWork CSP](/windows/client-management/mdm/passportforwork-csp)
- [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp)
- [Firewall CSP](/windows/client-management/mdm/firewall-csp)
- [AppLocker CSP](/windows/client-management/mdm/applocker-csp)
- [Group Policy Preferences](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn581922(v=ws.11)#group-policy-preferences-1)

If your imported GPO has settings that aren't in the supported CSPs and Group Policies, then the settings may be listed in the **Unknown Settings** column. This behavior means the settings were identified in your GPO.

## Group Policy migration readiness report

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Group policy analytics (preview)**:

    :::image type="content" source="./media/group-policy-analytics/policy-analytics-reports.png" alt-text="Review the report and output of imported GPOs using Group Policy analytics in Microsoft Intune and Endpoint Manager admin center.":::

2. In the **Summary** tab, a summary of the GPO and its policies are shown. Use this information to determine the status of the policies in your GPO:

    - **Ready for migration**: The policy has a matching setting in Intune, and is ready to be migrated to Intune.
    - **Not supported**: The policy doesn't have a matching setting. Typically, policy settings that show this status aren't exposed to MDM providers, including Intune.
    - **Deprecated**: The policy may apply to older Windows versions, older Microsoft Edge versions, and more policies that aren't used anymore.

      > [!NOTE]
      > When the Microsoft Intune product team updates the mapping logic, your imported GPOs are automatically updated. You don't need to reimport your GPOs.

3. Select the **Reports** tab > **Group policy migration readiness**. In this report, you can:

    - See the number of settings in your GPO that can be configured in a device configuration profile. It also shows if the settings can be in a custom profile, aren't supported, or are deprecated.
    - Filter the report output using the **Migration Readiness**, **Profile type**, and **CSP Name** filters.
    - Select **Generate report** or **Generate again** to get current data.
    - See the list of settings in your GPO.
    - Use the search bar to find specific settings.
    - Get a time stamp of when the report was last generated. 

    > [!NOTE]
    > After you add or remove your imported GPOs, it can take about 20 minutes to update the Migration Readiness reporting data.

## Known issues

Currently, the Group Policy analytics (preview) tool only supports non-ADMX settings in the English language. If you import a GPO with settings in languages other than English, then your **MDM Support** percentage will be inaccurate.

## Send product feedback

You can provide feedback on Group Policy Analytics. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Group Policy analytics (preview)** > **Got feedback**.

Examples of feedback areas:

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

- [Create a Settings Catalog policy using your imported GPOs in Microsoft Endpoint Manager (public preview)](group-policy-analytics-migrate.md)

- [Use Windows 10/11 Administrative Templates to configure group policy settings in Microsoft Endpoint Manager](administrative-templates-windows.md)

## See also

Learn more about [Configuration Service Providers (CSP)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).
