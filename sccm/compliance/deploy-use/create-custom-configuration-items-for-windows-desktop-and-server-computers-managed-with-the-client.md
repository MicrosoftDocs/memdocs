---
title: "Create configuration items for client-managed Windows computers "
titleSuffix: "Configuration Manager"
description: "Manage settings for Windows computers and servers with a custom Windows Desktops and Servers configuration item."
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to create custom configuration items for Windows desktop and server computers managed with the System Center Configuration Manager client

*Applies to: System Center Configuration Manager (Current Branch)*


Use the System Center Configuration Manager **custom Windows Desktops and Servers** configuration item to manage settings  for Windows computers and servers that are managed by the Configuration Manager client.  

## Start the create configuration item wizard

1.  In the Configuration Manager console, click **Assets and compliance** > **Compliance Settings** > **Configuration Items**.  

3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  

4.  On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.  

5.  Under **Specify the type of configuration item that you want to create**, select **Windows Desktops and Servers (custom)**.  

    > [!TIP]  
    >  If you want to supply detection method settings that check for the existence of an application, select **This configuration file contains application settings**.  

6.  Click **Categories** if you create and assign categories to help you search and filter configuration items in the Configuration Manager console.  

## Provide detection method information  
 Use this procedure to provide detection method information for the configuration item.  

> [!NOTE]  
>  Applies only if you selected **This configuration item contains application settings** on the **General** page of the wizard.  

 A detection method in Configuration Manager contains rules that are used to detect whether an application is installed on a computer. This detection occurs before the configuration item is assessed for compliance. To detect whether an application is installed, you can detect the presence of a Windows Installer file for the application, use a custom script, or select **Always assume application is installed** to assess the configuration item for compliance regardless of whether the application is installed.  

 Use these procedures to configure detection methods in System Center Configuration Manager.  

### To detect an application installation by using the Windows Installer File  

1.  On the **Detection Methods** page of the **Create Configuration Item Wizard**, select the **Use Windows Installer detection** check box.  

2.  Click **Open**, browse to the Windows Installer (.msi) file that you want to detect, and then click **Open**.  

3.  The **Version** box is automatically populated with the version number of the Windows Installer file that you selected. You can enter a new version number in this box if the displayed value is incorrect.  

4.  Select the **This application is installed for one or more users** check box if you want to detect each user profile on the computer.  

### To detect a specific application and deployment type  

1.  On the **Detection Methods** page of the **Create Configuration Item Wizard**, select the **Detect a specific application and deployment type** check box, then click **Select**.  

2.  In the **Specify Application** dialog box, select the application and an associated deployment type that you want to detect.  

### To detect an application installation by using a custom script  

1.  On the **Detection Methods** page of the **Create Configuration Item Wizard**, select the **Use a custom script to detect this application** check box.  

2.  In the list, select the language of the script you want to open. Choose from the following scripts:  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Click **Open**, browse to the script that you want to use, and then click **Open**.  

##  Configure settings  
 Use this procedure to configure the settings in the configuration item.  

 Settings represent the business or technical conditions that are used to assess compliance on client devices. You can configure a new setting or browse to an existing setting on a reference computer.  

1. On the **Settings** page of the **Create Configuration Item Wizard**, click **New**.  

2. On the **General** tab of the **Create Setting** dialog box, provide the following information:  

   - **Name:** Enter a unique name for the setting. You can use a maximum of 256 characters.  

   - **Description:** Enter a description for the setting. You can use a maximum of 256 characters.  

   - **Setting type:** In the list, choose and configure one of the following setting types to use for this setting:  

     - **Active Directory query**  

        **LDAP prefix** - Specify a valid prefix to the Active Directory Domain Services query to assess compliance on client computers. You can use either **LDAP://** for a or **GC://** to perform a global catalog search..  

        **Distinguished Name (DN)** - Specify the distinguished name of the Active Directory Domain Services object that is assessed for compliance on client computers.  

        For example, if you want to evaluate a value related to a user named John Smith in the corp.contoso.com domain, enter the following:  

       - **Search filter** - Specify an optional LDAP filter to refine the results from the Active Directory Domain Services query to assess compliance on client computers.  

          To return all results from the query, enter **(objectclass=\*)**.  

       - **Search scope** - Specify the search scope in Active Directory Domain Services/ You can choose from:  

         -   **Base** - Queries only the object that is specified.  

         -   **One Level** - This option is not used in this version of Configuration Manager.  

         -   **Subtree** - Queries the object that is specified and its complete subtree in the directory.  

       - **Property** - Specify the property of the Active Directory Domain Services object that is used to assess compliance on client computers.  

          For example, if you want to query the Active Directory property **badPwdCount**, which stores the number of times a user incorrectly enters a password, enter **badPwdCount** in this field.  

       - **Query** - Displays the query constructed from the entries in **LDAP prefix**, **Distinguished name (DN)**, **Search Filter** (if specified), and **Property**, which are used to assess compliance on client computers.  

         For more information about constructing LDAP queries, see your Windows Server documentation.  

     - **Assembly**  

        Configure the following for this setting type:  

       - **Assembly name:** Specifies the name of the assembly object that you want to search for. The name cannot be the same as other assembly objects of the same type and must be registered in the Global Assembly Cache. The assembly name can be up to 256 characters long.  

         An assembly is a piece of code that can be shared between applications. Assemblies can have the file name extension .dll or .exe. The Global Assembly Cache is a folder named *%systemroot%\Assembly* on client computers where all shared assemblies are stored.  

     - **File system**  

       - **Type** – In the list, select whether you want to search for a **File** or a **Folder**.  

       - **Path** - Specify the path of the specified file or folder on client computers. You can specify system environment variables and the *%USERPROFILE%* environment variable in the path.  

         > [!NOTE]  
         >  If you use the *%USERPROFILE%* environment variable in the **Path** or **File or folder name** boxes, all user profiles on the client computer are searched, which could result in multiple instances of the file or folder that is found.  
         >   
         >  If compliance settings do not have access to the specified path, a discovery error is generated. Additionally, if the file you are searching for is currently in use, a discovery error is generated.  

       - **File or folder name** - Specify the name of the file or folder object to search for. You can specify system environment variables and the *%USERPROFILE%* environment variable in the file or folder name. You can also use the wildcards * and ? in the file name.  

         > [!NOTE]  
         >  If you specify a file or folder name and use wildcards, this combination might produce a high numbers of results and could result in high resource use on the client computer and high network traffic when reporting results to Configuration Manager.  

       - **Include subfolders** – Enable this option if you also want to search any subfolders under the specified path.  

       - **This file or folder is associated with a 64-bit application** - If enabled, only 64-bit file locations (such as *%ProgramFiles%*) will be checked on 64-bit computers. If this option is not enabled, both 32-bit (such as *%ProgramFiles(x86)%*) and 64-bit locations will be checked.  

         > [!NOTE]  
         >  If the same file or folder exists in both the 64-bit and 32-bit system file locations on the same 64-bit computer, multiple files are discovered by the global condition.  

         The **File system** setting type does not support specifying a UNC path to a network share in the **Path** box.  

     - **IIS metabase**  

       -   **Metabase path** - Specify a valid path to the Internet Information Services (IIS) Metabase.  

       -   **Property ID** - Specify the numeric property of the IIS Metabase setting.  

     - **Registry key**  

       -   **Hive** – In the list, select the registry hive that you want to search in.  

       -   **Key** - Specify the registry key name that you want to search for. Use the format *key\subkey*.  

       -   **This registry key is associated with a 64-bit application** - Specifies whether the 64-bit registry keys should be searched in addition to the 32-bit registry keys on clients that are running a 64-bit version of Windows.  

           > [!NOTE]  
           >  If the same registry key exists in both the 64-bit and 32-bit registry locations on the same 64-bit computer, both registry keys are discovered by the global condition.  

     - **Registry value**  

       - **Hive** - In the list, select the registry hive that you want to search in.  

       - **Key** - Specify the registry key name that you want to search for. Use the format *key\subkey*.  

       - **Value** – Specify the value that must be contained within the specified registry key.  

       - **This registry key is associated with a 64-bit application** - Specifies whether the 64-bit registry keys should be searched in addition to the 32-bit registry keys on clients that are running a 64-bit version of Windows.  

         > [!NOTE]  
         >  If the same registry key exists in both the 64-bit and 32-bit registry locations on the same 64-bit computer, both registry keys are discovered by the global condition.  

         You can also click **Browse** to browse to a registry location on the computer or on a remote computer. To browse a remote computer, you must have administrator rights on the remote computer and the remote computer must be running the remote registry service.  

     - **Script**  

       -   **Discovery script** – Click **Add** to enter, or browse to the script you want to use. You can use Windows PowerShell, VBScript, or Microsoft JScript scripts.  

       -   **Run scripts by using the logged on user credentials** – If you enable this option, the script runs on client computers that use the credentials of the logged-on users.  

           > [!NOTE]  
           >  The value returned by the script is used to assess the compliance of the global condition. For example, when using VBScript, you could use the command **WScript.Echo Result** to return the *Result* variable value to the global condition.  

     - **SQL query**  

       -   **SQL Server instance** – Choose whether you want the SQL query to run on the default instance, all instances, or a specified database instance name.  

           > [!NOTE]  
           >  The instance name must refer to a local instance of SQL Server. To refer to a clustered SQL server instance, you should use a script setting.  

       -   **Database** - Specify the name of the Microsoft SQL Server database against which you want to run the SQL query.  

       -   **Column** - Specify the column name returned by the Transact-SQL statement that is used to assess the compliance of the global condition.  

       -   **Transact-SQL statement** – Specify the full SQL query you want to use for the global condition. You can also click **Open** to open an existing SQL query.  

           > [!IMPORTANT]  
           >  SQL Query settings do not support any SQL commands that modify the database. You can only use SQL commands that read information from the database.  

     - **WQL query**  

       -   **Namespace** - Specify the Windows Management Instrumentation (WMI) namespace which is used to build a WQL query that is assessed for compliance on client computers. The default value is Root\cimv2.  

       -   **Class** - Specifies the WMI class which is used to build a WQL query that is assessed for compliance on client computers.  

       -   **Property** - Specifies the WMI property which is used to build a WQL query that is assessed for compliance on client computers.  

       -   **WQL query WHERE clause** - You can use the **WQL query WHERE clause** item to specify a WHERE clause to be applied to the specified namespace, class, and property on client computers.  

     - **XPath query**  

       - **Path** - Specify the path of the .xml file on client computers that is used to assess compliance. Configuration Manager supports the use of all Windows system environment variables and the *%USERPROFILE%* user variable in the path name.  

       - **XML file name** - Specify the file name containing the XML query that is used to assess compliance on client computers.  

       - **Include subfolders** - Enable this option if you also want to search any subfolders under the specified path.  

       - **This file is associated with a 64-bit application** - Choose whether the 64-bit system file location (*%windir%*\System32) should be searched in addition to the 32-bit system file location (*%windir%*\Syswow64) on Configuration Manager clients that are running a 64-bit version of Windows.  

       - **XPath query** - Specify a valid full XML path language (XPath) query that is used to assess compliance on client computers.  

       - **Namespaces** - Opens the **XML Namespaces** dialog box to identify namespaces and prefixes to be used during the XPath query.  

         If you attempt to discover an encrypted .xml file, compliance settings find the file, but the XPath query produces no results, and no error is generated.  

         If the XPath query is not valid, the setting is evaluated as noncompliant on client computers.  

   - **Data type:** In the list, choose the format in which the condition returns the data before it is used to assess the setting. The **Data type** list is not displayed for all setting types.  

     > [!NOTE]  
     >  The **Floating point** data type supports only 3 digits after the decimal point.  

3. Configure additional details about this setting under the **Setting type** list. The items you can configure vary depending on the setting type you have selected.  

   > [!NOTE]  
   >  When you create settings of the type **File system**, **Registry key**, and **Registry value**, you can click **Browse** to configure the setting from values on a reference computer. To browse to a registry key or value on a remote computer, the remote computer must have the Remote Registry service enabled.  

4. Click **OK** to save the setting and close the **Create Setting** dialog box.  

##  Configure compliance rules  
 Use the following procedure to configure compliance rules for the configuration item.  

 Compliance rules specify the conditions that define the compliance of a configuration item. Before a setting can be evaluated for compliance, it must have at least one compliance rule. WMI, registry, and script settings let you remediate values that are found to be noncompliant. You can create new rules or browse to an existing setting in any configuration item to select rules in it.  

### To create a compliance rule  

1.  On the **Compliance Rules** page of the **Create Configuration Item Wizard**, click **New**.  

2.  In the **Create Rule** dialog box, provide the following information:  

    -   **Name:** Enter a name for the compliance rule.  

    -   **Description:** Enter a description for the compliance rule.  

    -   **Selected setting:** Click **Browse** to open the **Select Setting** dialog box. Select the setting that you want to define a rule for, or click **New Setting**. When you are finished, click **Select**.  

        > [!NOTE]  
        >  You can also click **Properties** to view information about the currently selected setting.  

    -   **Rule type:** Select the type of compliance rule that you want to use:  

        -   **Value** Create a rule that compares the value returned by the configuration item against a value that you specify.  

        -   **Existential** Create a rule that evaluates the setting depending on whether it exists on a client device or on the number of times it is found.  

    -   For a rule type of **Value**, specify the following information:  

        -   **The setting must comply with the following rule** – Select an operator and a value which is assessed for compliance with the selected setting. You can use the following operators:  

            |Operator|More information|  
            |--------------|----------------------|  
            |Equals|No additional information|  
            |Not equal to|No additional information|  
            |Greater than|No additional information|  
            |Less than|No additional information|  
            |Between|No additional information|  
            |Greater than or equal to|No additional information|  
            |Less than or equal to|No additional information|  
            |One of|In the text box, specify one entry on each line.|  
            |None of|In the text box, specify one entry on each line.|  

        -   **Remediate noncompliant rules when supported** – Select this option if you want Configuration Manager to automatically remediate noncompliant rules. Configuration Manager can automatically remediate the following rule types:  

            -   **Registry value** – The registry value is remediated if it is noncompliant, and created if it does not exist.  

            -   **Script** (by automatically running a remediation script).  

            -   **WQL Query**  

            > [!IMPORTANT]  
            >  You can only remediate noncompliant rules when the rule operator is set to **Equals**.  

        -   **Report noncompliance if this setting instance is not found** – The configuration item reports noncompliance if this setting is not found on client computers.  

        -   **Noncompliance severity for reports:** Specify the severity level that is reported (in Configuration Manager reports) if this compliance rule fails. The available severity levels are the following:  

            -   **None** Computers that fail this compliance rule do not report a failure severity.  

            -   **Information** Computers that fail this compliance rule report a failure severity of **Information**.  

            -   **Warning** Computers that fail this compliance rule report a failure severity of **Warning**.  

            -   **Critical** Computers that fail this compliance rule report a failure severity of **Critical**.  

            -   **Critical with event** Computers that fail this compliance rule report a failure severity of **Critical**. This severity level is also logged as a Windows event in the application event log.  

        -   For a rule type of **Existential**, specify the following information:  

            > [!NOTE]  
            >  The options shown might vary depending on the setting type you are configuring a rule for.  

            -   **The setting must exist on client devices**  

            -   **The setting must not exist on client devices**  

            -   **The setting occurs the following number of times:**  

        -   **Noncompliance severity for reports:** Specify the severity level that is reported (in Configuration Manager reports) if this compliance rule fails. The available severity levels are the following:  

            -   **None** Computers that fail this compliance rule do not report a failure severity.  

            -   **Information** Computers that fail this compliance rule report a failure severity of **Information**.  

            -   **Warning** Computers that fail this compliance rule report a failure severity of **Warning**.  

            -   **Critical** Computers that fail this compliance rule report a failure severity of **Critical**.  

            -   **Critical with event** Computers that fail this compliance rule report a failure severity of **Critical**. This severity level is also logged as a Windows event in the application event log.  

3.  Click **OK** to close the **Create Rule** dialog box.  

##  Specify supported platforms  
 Supported platforms are the operating systems on which a configuration item is assessed for compliance.  

On the **Supported Platforms** page of the **Create Configuration Item Wizard**, in the list, select the Windows versions on which you want the configuration item to be assessed for compliance, or click **Select all**.  

## Complete the wizard  
 On the **Summary** page of the Wizard, review the actions that will be taken, and then complete the wizard. The new configuration item is displayed in the **Configuration Items** node in the **Assets and Compliance** workspace.  
