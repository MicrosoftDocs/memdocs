---
title: "Create configuration items for client-managed Macs - Configuration Manager"
description: "Use the System Center Configuration Manager Mac OS X configuration item to manage settings for Mac OS X devices."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: 8
caps.handback.revision: 0
author: andredm7ms.author: andredmmanager: angrobe

---
# How to create configuration items for Mac OS X devices managed with the System Center Configuration Manager client
Use the System Center Configuration Manager**Mac OS X (custom)** configuration item to manage settings  for Mac OS X devices that are managed by the Configuration Manager client.  
  
 The Mac OS X operating system uses property list (or plist) files to store application settings. Use compliance settings to evaluate and remediate settings in a property list file. You can also manage Mac OS X settings by writing a Shell Script that returns a value that you can evaluate and remediate for compliance.  
  
### To create a custom Mac OS X configuration item  
  
1.  In the Configuration Manager console, click **Assets and compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then click **Configuration Items**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  
  
4.  On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.  
  
5.  Under **Specify the type of configuration item that you want to create**, select **Mac OS X (custom)**.  
  
6.  Click **Categories** if you create and assign categories to help you search and filter configuration items in the Configuration Manager console.  
  
7.  On the **Supported Platforms** page of the wizard, select the specific Mac OS X versions that will evaluate the configuration item.  
  
8.  On the **Settings** page of the wizard, you'll add new settings that will be evaluated for compliance on Mac computers. Click **New** to open the **Create Setting** dialog box.  
  
9. In the **Create Setting** dialog box, enter a unique name and a description for the setting.  
  
10. Choose the **Setting type** you want, then supply the required information as shown in the following table:  
  
    -   **Mac OS X Preferences** -  
  
        -   **Application ID** – Specify the application ID of the property list file from which you want to evaluate a key for compliance.  
  
             For example, if you want to edit settings for the Safari Web browser, you might use **com.apple.Safari.plist**.  
  
        -   **Key** – Specify the name of the key that you want to evaluate for compliance on Mac computers. Use the following syntax: */<dictionary\>/<keyname\>*.  
  
            > [!IMPORTANT]  
            >  The key name is case sensitive and will not be evaluated if it differs from the key name on the Mac computer. Additionally, you cannot edit the key name once you have specified it. If you need to edit the key name, delete and then recreate the setting.  
  
    -   **Script** -  
  
        -   **Discovery Script** – Click **Add Script**, and then enter a shell script to assess settings on the Mac computer for compliance. Use the **echo** command in the shell script to return values to Configuration Manager for compliance. Configuration Manager uses the results returned in **STDOUT** to evaluate compliance.  
  
            > [!IMPORTANT]  
            >  Do not include the **reboot** command in the discovery script. Because the discovery script runs each time the client restarts, this will cause the Mac computer to continually restart.  
  
        -   **Remediation script (optional)** – Optionally, click **Add Script** and then enter a shell script that is used to remediate any noncompliant settings found on Mac client computers.  
  
            > [!IMPORTANT]  
            >  To ensure that you do not introduce formatting characters that the Mac computer cannot interpret, do not use copy and paste but type in the script.  
  
11. Choose the **Data type** which is the format in which the condition returns the data before it is used to evaluate the setting.  
  
    > [!NOTE]  
    >  The **Floating point** data type supports only 3 digits after the decimal point.  
    >   
    >  Configuration Manager does not support using the **Boolean** data type for Mac configuration item script settings. Instead, set the data type to **Integer** and ensure that the script returns an integer value.  
  
12. Click **OK** to save the setting and close the **Create Setting** dialog box, then continue to add as many settings as you require.  
  
13. On the **Compliance Rules** page of the wizard, you'll specify the conditions that define the compliance of a configuration item. Before a setting can be evaluated to compliance, it must have at least one compliance rule. Click **New** to add a new rule.  
  
14. In the **Create Rule** dialog box, provide the following information:  
  
    -   **Name:** Enter a name for the compliance rule.  
  
    -   **Description:** Enter a description for the compliance rule.  
  
    -   **Selected setting:** Click **Browse** to open the **Select Setting** dialog box. Select the setting that you want to define a rule for, or click **New Setting**. When you are finished, click **Select**.  
  
        > [!TIP]  
        >  You can also click **Properties** to view information about the currently selected setting.  
  
    -   **Rule type:** Select the type of compliance rule that you want to use:  
  
        -   **Value:** Create a rule that compares the value returned by the configuration item against a value that you specify.  
  
        -   **Existential** - Create a rule that evaluates the setting depending on whether it exists on a device.  
  
    -   For a rule type of **Value**, specify the following information:  
  
        -   The setting must comply with the following rule – Select an operator and a value which is assessed for compliance with the selected setting. You can use the following operators:  
  
            -   **Equals**  
  
            -   **Not equal to**  
  
            -   **Greater than**  
  
            -   **Less than**  
  
            -   **Between**  
  
            -   **Greater than or equal to**  
  
            -   **Less than or equal to**  
  
            -   **One of** - In the text box, specify one entry on each line.  
  
            -   **None of** - In the text box, specify one entry on each line.  
  
        -   **Remediate noncompliant rules when supported** – Select this option if you want Configuration Manager to automatically remediate noncompliant rules.  
  
            > [!IMPORTANT]  
            >  You can only remediate noncompliant rules when the rule operator is set to **Equals**.  
  
        -   **Report noncompliance if this setting instance is not found** – The configuration item reports noncompliance if this setting is not found on the Mac computer.  
  
    -   **Noncompliance severity for reports** - Specify the severity level that is reported if this compliance rule fails. The available severity levels are the following:  
  
        -   **None** - Computers that fail this compliance rule do not report a failure severity for Configuration Manager reports.  
  
        -   **Information** - Computers that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
        -   **Warning** - Computers that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
        -   **Critical** - Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
        -   **Critical with event** - Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also be logged by the Mac client computer.  
  
    -   For a rule type of **Existential**, specify the following information:  
  
        -   Choose one of:  
  
            -   **The setting must exist on client devices**  
  
            -   **The setting must not exist on client devices**  
  
        -   **Noncompliance severity for reports:** Specify the severity level that is reported if this compliance rule fails. The available severity levels are the following:  
  
            -   **None** - Computers that fail this compliance rule do not report a failure severity for Configuration Manager reports.  
  
            -   **Information** - Computers that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
            -   **Warning** - Computers that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
            -   **Critical** - Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
            -   **Critical with event** - Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also be logged by the Mac client computer.  
  
        > [!NOTE]  
        >  The options shown might vary depending on the setting type you are configuring a rule for.  
  
    -   Click **OK** to close the **Create Rule** dialog box.  
  
15. On the **Summary** page, confirm the settings for the new configuration item then, complete the wizard.  
  
 The new configuration item is displayed in the **Configuration Items** node of the **Assets and Compliance** workspace.  
  
 If you now want to add this configuration item to a configuration baseline, see [How to create configuration baselines in System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## See Also  
 [Configuration items for devices managed with the System Center Configuration Manager client](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
