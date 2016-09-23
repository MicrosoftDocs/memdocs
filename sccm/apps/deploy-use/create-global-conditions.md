---
title: "Create global conditions | System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft

---
# How to create global conditions in System Center Configuration Manager
In System Center Configuration Manager, global conditions are rules that represent business or technical conditions that you can use to specify how an application is provided and deployed to client devices. Global conditions are accessed from the **Requirements** page of the Create Deployment Type Wizard.  
  
> [!NOTE]  
>  You can only edit global conditions from the site where they were created.  
  
 Use the following procedures to create Configuration Manager global conditions.  
  
## Provide basic information about the global condition  
 Several different types of global conditions are available. Different options are associated with the different global condition types. When you select a specific global condition type, Configuration Manager displays the options that apply to your selection.  
  
1.  In the Configuration Manager console, click **Software Library** > **Application Management** > **Global Conditions**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Global Condition**.  
  
4.  In the **Create Global Condition** dialog box, provide a name and an optional description for the global condition.  
  
5.  In the **Device type** drop-down list, choose whether the global condition is for a **Windows** computer or a **Windows Mobile** device.  
  
6.  In the **Condition Type** drop-down list, choose one of the following options:  
  
    -   **Setting** – This option checks for the existence of one or more items on client devices. For example, you can check that a particular file, folder, or registry key value exists on a client device.  
  
    -   **Expression** – This option allows you to configure more complex rules to determine if the condition is satisfied on client devices. For example, you can determine if the physical memory on a computer is between 2 GB and 4 GB or to determine if a mobile device uses touch screen input.  
  
## Configure rules for the global condition  
 The procedure for defining the global condition rules is different depending on whether you are configuring a setting or an expression. Use the applicable procedure here to configure a setting or an expression for the global condition.  
  
#### To configure a setting for the global condition  
  
1.  In the **Condition Type** drop-down list, choose **Setting**.  
  
2.  In the **Setting type** drop-down list, choose the item to use as the condition for which requirements will be checked. The following setting types and configurations are available.  
  
    -   **Active Directory query**  
  
        -   **LDAP prefix** - Specify a valid LDAP prefix to the Active Directory Domain Services query to assess compliance on client computers. You can use either **LDAP://** or **GC://**.  
  
        -   **Distinguished Name (DN)** - Specify the distinguished name of the Active Directory Domain Services object that will be assessed for compliance on client computers.  
  
        -   **Search filter** - Specify an optional LDAP filter to refine the results from the Active Directory Domain Services query to assess compliance on client computers.  
  
        -   **Search scope** - Specify the search scope in Active Directory Domain Services:  
  
            -   **Base** - Queries only the object specified.  
  
            -   **One Level** - This option is not used in this version of Configuration Manager.  
  
            -   **Subtree** -  Queries the object specified and its complete subtree in the directory.  
  
        -   **Property** - Specify the property of the Active Directory Domain Services object that will be used to assess compliance on client computers.  
  
        -   **Query** - Displays the LDAP query that is constructed from the entries in **LDAP prefix**, **Distinguished name (DN)**, **Search Filter** if specified and **Property**. This query will be used to assess compliance on client computers.  
  
    -   **Assembly**  
  
        -   **Assembly name** - Specifies the name of the assembly object to search for. The name cannot be the same as any other assembly object of the same type and the name must be registered in the Global Assembly Cache. The assembly name can be a maximum of 256 characters long.  
  
        > [!NOTE]  
        >  An assembly is a piece of code that can be shared between applications. Assemblies can have the file name extension .dll or .exe. The Global Assembly Cache is a folder named *%systemroot%\assembly* on client computers in which all shared assemblies are stored.  
  
    -   **File system**  
  
        -   **Type** – From the drop-down list, select whether you want to search for a **File** or a **Folder**.  
  
        -   **Path** - Specify the path to the specified file or folder on client computers. You can specify system environment variables and the *%USERPROFILE%* environment variable in the path.  
  
            > [!NOTE]  
            >  If you use the *%USERPROFILE%* environment variable in the **Path** or **File or folder name** fields, all user profiles on the client computer will be searched. This could result in the discovery of multiple instances of the file or folder.  
  
        -   **File or folder name** - Specify the name of the file or folder object that will be searched for. You can specify system environment variables and the *%USERPROFILE%* environment variable in the file or folder name. You can also use the wildcards * and ? in the filename.  
  
            > [!NOTE]  
            >  If you specify a file or folder name and use wildcards, this might produce a high numbers of results. This could result in high resource use on the client computer and also high network traffic when reporting results to Configuration Manager.  
  
        -   **Include subfolders** – Enable this option if you also want to search any subfolders under the specified path.  
  
        -   **This file or   folder is associated with a 64-bit application** - Choose whether the 64-bit system file location (*%windir%*\system32) should be searched in addition to the 32-bit system file location (*%windir%*\syswow64) on Configuration Manager clients that run a 64-bit version of Windows.  
  
            > [!NOTE]  
            >  If the same file or folder exists in both the 64-bit and 32-bit system file locations on the same 64-bit computer, multiple files will be discovered by the global condition.  
  
         The **File system** setting type does not support specifying a UNC path to a network share in the **Path** field.  
  
    -   **IIS metabase**  
  
        -   **Metabase path** - Specify a valid path to the IIS Metabase.  
  
        -   **Property ID** - Specify the numeric property of the IIS Metabase setting.  
  
    -   **Registry key**  
  
        -   **Hive** – From the drop-down list, select the registry hive that you want to search in.  
  
        -   **Key** - Specify the registry key name that you want to search for. The format used should be *key\subkey*.  
  
        -   **This registry key is associated with a 64-bit application** - Specifies whether the 64-bit registry keys should be searched in addition to the 32-bit registry keys on clients that run a 64-bit version of Windows.  
  
            > [!NOTE]  
            >  If the same registry key exists in both the 64-bit and 32-bit registry locations on the same 64-bit computer, both registry keys will be discovered by the global condition.  
  
    -   **Registry value**  
  
        -   **Hive** - From the drop-down list, select the registry hive that you want to search in.  
  
        -   **Key** - Specify the registry key name that you want to search for. The format used should be *key\subkey*.  
  
        -   **Value** – Specify the value that must be contained within the specified registry key.  
  
        -   **This registry key is associated with a 64-bit application** - Specifies whether the 64-bit registry keys should be searched in addition to the 32-bit registry keys on clients that run a 64-bit version of Windows.  
  
            > [!NOTE]  
            >  If the same registry key exists in both the 64-bit and 32-bit registry locations on the same 64-bit computer, both registry keys will be discovered by the global condition.  
  
    -   **Script**  
  
        -   **Discovery script** – Click **Add** to enter, or browse to the script to use. You can use Windows PowerShell, VBScript or JScript scripts.  
  
        -   **Run scripts by using the logged on user credentials** – If you enable this option, the script will run on client computers by using the logged on users credentials.  
  
            > [!NOTE]  
            >  The value returned by the script will be used to assess the compliance of the global condition. For example, when you use VBScript, you could use the command **WScript.Echo Result** to return the Result variable value to the global condition.  
            >   
            >  If your script returns multiple values, these values must be on a single line, separated with a semi-colon. If each value is on a separate line, the evaluation will fail.  
  
    -   **SQL query**  
  
        -   **SQL Server instance** – Choose whether you want the SQL query to run on the default instance, all instances, or a specified database instance name.  
  
            > [!NOTE]  
            >  The instance name must refer to a local instance of SQL Server. To refer to a clustered SQL server instance, you should use a script setting.  
  
        -   **Database** - Specify the name of the Microsoft SQL Server database for which the SQL query will be run.  
  
        -   **Column** - Specify the column name returned by the Transact-SQL statement to use to assess the compliance of the global condition.  
  
        -   **Transact-SQL statement** – Specify the full SQL query to use for the global condition. You can also click **Open** to open an existing SQL query.  
  
    -   **WQL query**  
  
        -   **Namespace** - Specify the WMI namespace that will be used to build a WQL query that will be assessed for compliance on client computers. The default value is Root\cimv2.  
  
        -   **Class** - Specifies the WMI class that will be used to build a WQL query that will be assessed for compliance on client computers.  
  
        -   **Property** - Specifies the WMI property that will be used to build a WQL query that will be assessed for compliance on client computers.  
  
        -   **WQL query WHERE clause** - You can use the **WQL query WHERE clause** item to specify a WHERE clause to be applied to the specified namespace, class, and property on client computers.  
  
    -   **XPath query**  
  
        -   **Path** - Specify the path to the XML file on client computers that will be used to assess compliance. Configuration Manager supports the use of all Windows system environment variables and the *%USERPROFILE%* user variable in the path name.  
  
        -   **XML file name** - Specify the file name containing the XML query to use to assess compliance on client computers.  
  
        -   **Include subfolders** - Enable this option if you also want to search any subfolders under the specified path.  
  
        -   **This file is associated with a 64-bit application** - Choose whether the 64-bit system file location (*%windir%*\system32) should be searched in addition to the 32-bit system file location (*%windir%*\syswow64) on Configuration Manager clients that run a 64-bit version of Windows.  
  
        -   **XPath query** - Specify a valid full XML path language (XPath) query to use to assess compliance on client computers.  
  
        -   **Namespaces** - Opens the **XML Namespaces** dialog box to identify namespaces and prefixes to use during the XPath query.  
  
3.  In the **Data type** drop-down list, choose the format in which data will be returned by the condition before it is used to check requirements.  
  
    > [!NOTE]  
    >  The **Data type** drop-down list is not displayed for all setting types.  
  
4.  Configure further details about this setting below the **Setting type** drop-down list. The items you can configure will vary depending on the setting type you have selected.  
  
5.  Click **OK** to save the rule and to close the **Create Global Condition** dialog box.  
  
#### To configure an expression for the global condition  
  
1.  In the **Condition Type** drop-down list, choose **Expression**.  
  
2.  Click **Add Clause** to open the **Add Clause** dialog box.  
  
3.  From the **Select category** drop-down list, select whether this expression is for a device or a user. Alternatively, select **Custom** to use a previously configured global condition.  
  
4.  From the **Select a condition** drop-down list, select the condition to use to assess whether the user or device meets the rule requirements. The contents of this list will vary depending on the selected category.  
  
5.  From the **Choose operator** drop-down list, choose the operator that will be used to compare the selected condition to the specified value to assess whether the user or device meets the rule requirements. The available operators will vary depending on the selected condition.  
  
6.  In the **Value** field, specify the values that will be used with the selected condition and operator to assess whether the user or device meets the rule requirements. The available values will vary depending on the selected condition and the selected operator.  
  
7.  Click **OK** to save the expression and to close the **Add Clause** dialog box.  
  
8.  When you have finished adding clauses to the global condition, click **OK** to close the **Create Global Condition** dialog box and to save the global condition.  
  
## See Also  
 [Application management technical reference for System Center Configuration Manager](../Topic/Application%20management%20technical%20reference%20for%20System%20Center%20Configuration%20Manager.md)

