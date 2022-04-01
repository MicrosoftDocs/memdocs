---
title: Create configuration items for macOS
titleSuffix: Configuration Manager
description: Use the Configuration Manager macOS X configuration item to manage settings for macOS devices.
ms.date: 01/04/2022
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: how-to
author: mestew
manager: dougeby
ms.author: mstewart
ms.localizationpriority: medium
---

# Create configuration items for macOS X devices

> [!IMPORTANT]
> Starting in January 2022, this feature of Configuration Manager is deprecated.<!-- 12927803 --> For more information, see [Mac computers](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

Use the Configuration Manager **Mac OS X (custom)** configuration item to manage settings for macOS X devices that are managed by the Configuration Manager client.  
  
The macOS X operating system uses property list (.plist) files to store application settings. Use compliance settings to evaluate and remediate settings in a property list file. You can also manage macOS X settings by writing a shell script that returns a value that you can evaluate and remediate for compliance.  
  
## Create a custom macOS X configuration item  
  
1. In the Configuration Manager console, select **Assets and compliance**.  
  
2. In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then select **Configuration Items**.  
  
3. On the **Home** tab, in the **Create** group, select **Create Configuration Item**.  
  
4. On the **General** page of the **Create Configuration Item** wizard, specify a name and optional description for the configuration item.  
  
5. Under **Specify the type of configuration item that you want to create**, select **Mac OS X (custom)**.  
  
6. If you create and assign categories to help you search and filter configuration items in the Configuration Manager console, select **Categories**.  
  
7. On the **Supported Platforms** page of the wizard, select the specific macOS X versions that will evaluate the configuration item.  
  
8. On the **Settings** page of the wizard, add new settings that are evaluated for compliance on Mac computers. Select **New** to open the **Create Setting** dialog box.  
  
9. In the **Create Setting** dialog box, enter a unique name and a description for the setting.  
  
10. Choose the **Setting type** you want, and then supply the required information:  
  
    -   **Mac OS X Preferences**  
  
        -   **Application ID**: Specify the application ID of the property list file from which you want to evaluate a key for compliance.  
  
             For example, if you want to edit settings for the Safari Web browser, you might use **com.apple.Safari.plist**.  
  
        -   **Key**: Specify the name of the key that you want to evaluate for compliance on Mac computers. Use the following syntax: */<dictionary\>/<keyname\>*.  
  
            > [!IMPORTANT]  
            >  The key name is case sensitive, and won't be evaluated if it differs from the key name on the Mac computer. Additionally, you can't edit the key name after you have specified it. If you need to edit the key name, delete and then re-create the setting.  
  
    -   **Script**  
  
        -   **Discovery Script**: Select **Add Script**, and then enter a shell script to assess settings on the Mac computer for compliance. Use the **echo** command in the shell script to return values to Configuration Manager for compliance. Configuration Manager uses the results returned in **STDOUT** to evaluate compliance.  
  
            > [!IMPORTANT]  
            >  Don't include the **reboot** command in the discovery script. Because the discovery script runs each time the client restarts, this causes the Mac computer to continually restart.  
  
        -   **Remediation script (optional)**: Optionally, select **Add Script**, and then enter a shell script that is used to remediate any noncompliant settings found on Mac client computers.  
  
            > [!IMPORTANT]  
            >  To ensure that you don't introduce formatting characters that the Mac computer can't interpret, don't use copy and paste. Instead, type in the script.  
  
11. Choose the **Data type**, which is the format in which the condition returns the data before it's used to evaluate the setting.  
  
    > [!NOTE]  
    >  The **Floating point** data type supports only 3 digits after the decimal point.  
    >   
    >  Configuration Manager doesn't support using the **Boolean** data type for Mac configuration item script settings. Instead, set the data type to **Integer**, and ensure that the script returns an integer value.  
  
12. Select **OK** to save the setting and close the **Create Setting** dialog box. Then continue to add as many settings as you require.  
  
13. On the **Compliance Rules** page of the wizard, specify the conditions that define the compliance of a configuration item. Before a setting can be evaluated to compliance, it must have at least one compliance rule. Select **New** to add a new rule.  
  
14. In the **Create Rule** dialog box, provide the following information:  
  
    -   **Name**: Enter a name for the compliance rule.  
  
    -   **Description**: Enter a description for the compliance rule.  
  
    -   **Selected setting**: Select **Browse** to open the **Select Setting** dialog box. Select the setting that you want to define a rule for, or select **New Setting**. When you are finished, choose **Select**.  
  
        > [!TIP]  
        >  You can also select **Properties** to view information about the currently selected setting.  
  
    -   **Rule type**: Select the type of compliance rule that you want to use:  
  
        -   **Value**: Create a rule that compares the value returned by the configuration item against a value that you specify.  
  
        -   **Existential**: Create a rule that evaluates the setting depending on whether it exists on a device.  
  
    -   For a rule type of **Value**, specify the following information:  
  
        -   **The setting must comply with the following rule**: Select an operator and a value that is assessed for compliance with the selected setting. You can use the following operators:  
  
            -   **Equals**  
  
            -   **Not equal to**  
  
            -   **Greater than**  
  
            -   **Less than**  
  
            -   **Between**  
  
            -   **Greater than or equal to**  
  
            -   **Less than or equal to**  
  
            -   **One of**: In the text box, specify one entry on each line.  
  
            -   **None of**: In the text box, specify one entry on each line.  
  
        -   **Remediate noncompliant rules when supported**: Select this option if you want Configuration Manager to automatically remediate noncompliant rules.  
  
            > [!IMPORTANT]  
            >  You can only remediate noncompliant rules when the rule operator is set to **Equals**.  
  
        -   **Report noncompliance if this setting instance is not found**: The configuration item reports noncompliance if this setting isn't found on the Mac computer.  
  
        -   **Noncompliance severity for reports**: Specify the severity level reported if this compliance rule fails. The available severity levels are:  
  
            -   **None**: Computers that fail this compliance rule don't report a failure severity for Configuration Manager reports.  
  
            -   **Information**: Computers that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
            -   **Warning**: Computers that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
            -   **Critical**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
            -   **Critical with event**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. The Mac client computer also logs this severity level.  
  
    -   For a rule type of **Existential**, specify the following information:  
  
        -   Choose either:  
  
            -   **The setting must exist on client devices**  
  
            -   **The setting must not exist on client devices**  
  
        -   **Noncompliance severity for reports**: Specify the severity level that is reported if this compliance rule fails. The available severity levels are:  
  
            -   **None**: Computers that fail this compliance rule don't report a failure severity for Configuration Manager reports.  
  
            -   **Information**: Computers that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
            -   **Warning**: Computers that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
            -   **Critical**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
            -   **Critical with event**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. The Mac client computer also logs this severity level.  
  
        > [!NOTE]  
        >  The options shown might vary, depending on the setting type you are configuring a rule for.  
  
15. Select **OK** to close the **Create Rule** dialog box.  
  
16. On the **Summary** page, confirm the settings for the new configuration item. Then, complete the wizard.  
  
See the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.  
  
If you now want to add this configuration item to a configuration baseline, see [How to create configuration baselines](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## Next steps

 [Configuration items for devices managed with the Configuration Manager client](../../compliance/deploy-use/create-configuration-items.md)
