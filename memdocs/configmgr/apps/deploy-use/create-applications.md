---
title: Create applications
titleSuffix: Configuration Manager
description: Create applications with deployment types, detection methods, and requirements to install software.
ms.date: 10/01/2021
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: how-to
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Create applications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

A Configuration Manager application defines the metadata about application. An application has one or more deployment types. These deployment types include the installation files and information that are required to install software on devices. A deployment type also has rules, such as detection methods, and requirements. These rules specify when and how the client installs the software.  

Create applications using the following methods:  

- Automatically create an application and deployment types by reading the application installation files:  
  - [Create an application](#bkmk_create) and [automatically detect](#bkmk_auto-app) application information
  - [Create a deployment type](#bkmk_create-dt) and [automatically identify](#bkmk_auto-dt) deployment type information

- Manually create an application and then add deployment types later:  
  - [Create an application](#bkmk_create) and [manually specify](#bkmk_manual-app) application information
  - [Create a deployment type](#bkmk_create-dt) and [manually specify](#bkmk_manual-dt) deployment type information

- [Import an application](#bkmk_import) from a file  

This article also includes the following information to configure a deployment type:  

- [Content](#bkmk_dt-content)
- [Task Sequence](#bkmk_dt-ts)
- [Detection Method](#bkmk_dt-detect)
- [User Experience](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Return Codes](#bkmk_dt-return)
- [Dependencies](#bkmk_dt-depend)

## <a name="bkmk_create"></a> Create an application  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Application**.  

Next, automatically detect or manually specify application information:  

- [Automatically detect](#bkmk_auto-app) application information to create a basic application with a single deployment type. For example, a Windows Installer file that has no dependencies or requirements. After you create an application by using this procedure, edit it as needed. You can add or change deployment types, and add detection methods, dependencies, or requirements.  

- [Manually specify](#bkmk_manual-app) application information to create more complex applications. Define more than one deployment type, dependencies, detection methods, or requirements.  

### <a name="bkmk_auto-app"></a> Automatically detect application information  

1. On the **General** page of the Create Application wizard, select **Automatically detect information about this application from installation files**.  

2. In the **Type** drop-down list, select the application installation file type that you want to use to detect application information. For more information about the available installation types, see [Deployment types supported by Configuration Manager](create-applications.md#bkmk_deploy-types).  

3. In the **Location** box, specify the application installation file that you want to use to detect application information. This location is either a network path (`\\server\share\filename`) or a store link. You must have access to the network path and any subfolders that include application content.  

    > [!IMPORTANT]  
    > When you select **Windows Installer (\*.msi file)** as an application type, the site imports all of the files in the specified folder. It then sends these files to distribution points. Make sure that the specified folder contains only the files that are necessary to install the application. Microsoft tests Configuration Manager to support up to 20,000 files in the application package. If your application has more files, consider creating multiple applications with less files.  

4. On the **Import Information** page of the Create Application wizard, review the information, and then select **Next**. If necessary, select **Previous** to go back and fix any errors.  

5. On the **General Information** page of the Create Application wizard, specify the following information:  

    > [!NOTE]  
    > If Configuration Manager automatically detects this information from the application installation files, it's already populated here. Additionally, the displayed options might be different depending on the application type that you create.  

    - General information about the application, like the application **Name**, **Administrator comments**, **Publisher**, and **Software version**. To help you find the application in the Configuration Manager console, specify an **Optional reference**, or select **Administrative categories**.  

    - **Installation program**: Specify the installation program and any required properties that are needed to install the application deployment type.  

        > [!TIP]  
        > If the installation program doesn't appear, choose **Browse** and browse to the installation program location.  

    - **Install behavior**: Select one of the three options for how Configuration Manager installs this deployment type. For more information on these options, see [User Experience](#bkmk_dt-ux).  

    - **Use an automatic VPN connection (if configured)**: If you've deployed a VPN profile to the device on which the user launches the app, connect the VPN when the app starts. This option is only for Windows 8.1 and Windows Phone 8.1. On Windows Phone 8.1 devices, if you deploy more than one VPN profile to the device, automatic VPN connections aren't supported. For more information, see [VPN profiles](../../protect/deploy-use/vpn-profiles.md).  

    - **Provision this application for all users on the device**<!--1358310-->: Provision an application with a Windows app package for all users on the device. For more information, see [Create Windows applications](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > If you're modifying an existing application, this setting is on the **User Experience** tab of the Windows app package deployment type properties.  

6. Choose **Next**, review the application information on the **Summary** page, and then finish the Create Application wizard.  

The new application now appears in the **Applications** node of the Configuration Manager console. You've finished creating an application.

To add more deployment types or configure other settings, see [Create deployment types for the application](#bkmk_create-dt).  

### <a name="bkmk_manual-app"></a> Manually specify application information  

1. On the **General** page of the Create Application wizard, select **Manually specify the application information**, and then choose **Next**.  

2. Specify **General Information** about the application:  

    - The application **Name** is required and must be fewer than 256 characters.  

    - **Administrator comments**, **Publisher**, and **Software version** are additional metadata to further describe the application.  

    - To help you find the application in the Configuration Manager console, specify an **Optional reference**, or select **Administrative categories**.  

    - **Date published**  

    - Select users or groups who are responsible for this application as **Owners** and **Support contacts**. By default, these values are set to your username.  

3. On the **Software Center** page of the Create Application wizard, specify the following information:  

    - **Selected language**: In the drop-down list, select the language version of the application that you want to set up. Choose **Add/Remove** to set up more languages for this application.  

    - **Localized application name**: Specify the application name in the selected language.  

        > [!IMPORTANT]  
        > A localized application name is required for each language version that you set up.  

    - **User categories**: Choose **Edit** to specify application categories in the selected language. Users of Software Center use these categories to help filter and sort the applications.  

        > [!NOTE]
        > User categories for device-targeted application deployments show as filters in Software Center. These deployments can be either available or required.
        >
        > <!-- 4726793 -->Renaming or deleting a category doesn't automatically apply to apps with this category. These changes apply on the next revision of the app. To work around this issue for rename or delete:
        >
        > - First clear the checkbox for the category on any app that references it. Then apply that change, which revises the app.
        >     - Instead of the rename action, next create a new category with the new name, and add the new category to the relevant apps.
        >     - You can delete the category after you revise the apps.

    - **User documentation**: Specify the location of a file from which Software Center users can get more information about this application. This location is a website address, or a network path and file name. Make sure that users have access to this location.  

    - **Link text**: Specify the text that appears in place of "Additional information" when user documentation is specified.  

    - **Privacy URL**: Specify a website address to the privacy statement for the application.  

    - **Localized description**: Enter a description for this application in the selected language.  

    - **Keywords**: Enter a list of keywords in the selected language. These keywords help Software Center users search for the application.  

    - **Icon**: Select **Browse** to select an icon for this application. If you don't specify an icon, Configuration Manager uses a default icon. Icons can have pixel dimensions of up to 512x512.  

4. On the **Deployment Types** page of the Create Application wizard, choose **Add** to create a new deployment type. For more information, see [Create deployment types for the application](#bkmk_create-dt).  

5. Choose **Next**, review the application information on the **Summary** page, and then finish the Create Application wizard.  

The new application now appears in the **Applications** node of the Configuration Manager console.  

## <a name="bkmk_create-dt"></a> Create deployment types for the application  

If you [automatically detect application information](#bkmk_auto-app), you may not need to finish some of the steps in this section.  

> [!Note]  
> When you view the properties of an existing deployment type, the following sections correspond to tabs of the deployment type properties window:  
>
> - [Content](#bkmk_dt-content)
> - [Task Sequence](#bkmk_dt-ts)
> - [Detection Method](#bkmk_dt-detect)
> - [User Experience](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Return Codes](#bkmk_dt-return)
> - [Dependencies](#bkmk_dt-depend)
>  
> For information on the **Install Behavior** tab on the properties of a deployment type, see [Check for running executable files](check-for-running-executable-files.md).

### Start the Create Deployment Type wizard  

There are three ways to start the Create Deployment Type wizard:

- **In the Applications node**: In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Select an application, and then select **Create Deployment Type** in the ribbon.  

- **When creating an application**: When you [Manually specify application information](#bkmk_manual-app) in the Create Application wizard, select **Add** on the Deployment Types page.  

- **From application properties**: Select an existing application in the **Applications** node and select **Properties**. Switch to the **Deployment Types** tab, and select **Add**.

Then use one of the following procedures to [automatically identify](#bkmk_auto-dt) or [manually specify](#bkmk_manual-dt) deployment type information.  

### <a name="bkmk_auto-dt"></a> Automatically identify deployment type information  

1. On the **General** page of the Create Deployment Type wizard:  

    1. Select the application installation file **Type** to detect the deployment type information.  

    2. Select **Automatically identify information about this deployment type from installation files**.  

    3. In the **Location** box, specify the application installation file that you want to use to detect the deployment type information. This location is either a network path (`\\server\share\filename`) or a store link. You must have access to the network path and any subfolders that include application content.  

2. On the **Import Information** page of the Create Deployment Type wizard, review the information, and then select **Next**. If necessary, select **Previous** to go back and fix any errors.  

3. On the **General Information** page of the Create Deployment Type wizard, specify the following information:  

    > [!NOTE]  
    > Some of the deployment type information might already be present if it was read from the application installation files. Additionally, the displayed options might differ, depending on the deployment type that you're creating.  

    - **General Information** about the deployment type:  
        - The **Name** is required  

        - **Administrator comments** to further describe it  

        - **Languages** that are available for it  

    - **Installation program**: Specify the installation program and any properties that you require to install the deployment type.  

    - **Install behavior**: Select one of the three options for how Configuration Manager installs this deployment type. For more information on these options, see [User Experience](#bkmk_dt-ux).  

    - **Use an automatic VPN connection (if configured)**: If you've deployed a VPN profile to the device on which the user launches the app, connect the VPN when the app starts. This option is only for Windows 8.1 and Windows Phone 8.1. On Windows Phone 8.1 devices, if you deploy more than one VPN profile to the device, automatic VPN connections aren't supported. For more information, see [VPN profiles](../../protect/deploy-use/vpn-profiles.md).  

4. Choose **Next**, and then continue to [Deployment type Content options](#bkmk_dt-content).  

### <a name="bkmk_manual-dt"></a> Manually specify the deployment type information  

1. On the **General** page of the Create Deployment Type wizard, in the **Type** drop-down list, choose the application installation file type for this deployment type.

2. Select **Manually specify the deployment type information**, and then select **Next**.

3. On the **General Information** page of the Create Deployment Type wizard, specify a **Name** for the deployment type. Optionally specify **Administrator comments**, select the **Languages** for this deployment type, and then select **Next**.  

4. Continue to [Deployment type Content options](#bkmk_dt-content).  

### <a name="bkmk_dt-content"></a> Deployment type **Content** options  

On the **Content** page, specify the following information:  

> [!Note]  
> When you view the properties of an existing deployment type, some of these options appear on the **Content** tab and some on the **Programs** tab.  

- **Content location**: Specify the location of the content for this deployment type, or select **Browse** to choose the deployment type content folder.  

    > [!IMPORTANT]  
    > The System account of the site server computer must have permissions to the specified content location.  

  - **Persist content in the client cache**: The Configuration Manager client indefinitely keeps in its cache the deployment type content. The client persists the content even if the app is already installed. This option is useful with some deployments, like Windows Installer–based software. Windows Installer needs a local copy of the source content for applying updates. This option reduces the available cache space. If you select this option, it might cause a large deployment to fail at a later point if the cache doesn't have sufficient available space.

    > [!TIP]
    > This option persists the specific version of content that the client installs. If you update the content for this app, the client doesn't automatically cache this content again. Once an action happens that requires the new content, the client downloads the new content version.<!-- MEMDocs#684 -->

- **Installation program**: Specify the name of the installation program and any required installation parameters.  

  - **Installation start in**: Optionally specify the folder that has the installation program for the deployment type. This folder can be an absolute path on the client or a path to the distribution point folder that has the installation files.  

- **Uninstall program**: Optionally specify the name of the uninstall program and any required parameters.  

  - **Uninstall start in**: Optionally specify the folder that has the uninstall program for the deployment type. This folder can be an absolute path on the client. It can also be a relative path on a distribution point of the folder with the package.  

- **Repair program**: For Windows Installer and Script Installer deployment types, optionally specify the name of the repair program and any required parameters.<!--1357866-->  

  - **Repair start in**: Optionally specify the folder that has the repair program for the deployment type. This folder can be an absolute path on the client. It can also be a relative path on a distribution point of the folder with the package.  

- **Run installation and uninstall program as 32-bit process on 64-bit clients**: Use the 32-bit file and registry locations on Windows-based computers to run the installation program for the deployment type.  

#### Deployment type properties **Content** options

When you view the properties of a deployment type, the following options appear only on the **Content** tab:

- **Uninstall content settings**:  

  - **Same as install content**: If the install and uninstall content are the same, select this option. This option is the default.  

  - **No uninstall content**: If your application doesn't need content for uninstall, select this option.  

  - **Different from install content**: If the uninstall content is different from the install content, select this option.  

    - **Uninstall content location**: Specify the network path to the content that's used to uninstall the application.  

- **Allow clients to use distribution points from the default site boundary group**: Specify if clients should download and install the software from a distribution point in the site default boundary group when the content isn't available from a distribution point in the current or neighbor boundary groups.  

- **Deployment options**: Specify if clients should download the application when they use a distribution point from a neighbor or the default site boundary groups.  

> [!NOTE]
> Windows BranchCache is always enabled on clients. If the distribution point supports BranchCache, clients use it. For more information, see [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

### <a name="bkmk_dt-ts"></a> Deployment type **Task Sequence** options

<!--3555953-->

For more information on the task sequence deployment type, see [Task sequence deployment type](../get-started/creating-windows-applications.md#bkmk_tsdt).

On the **Task Sequence** page, specify the following information:

- **Install task sequence**: Select a task sequence that runs the installation process for this app.

- **Uninstall task sequence** (optional): Select a task sequence that removes this app.

> [!TIP]  
> If your task sequence doesn't appear in the list, double-check that it doesn't include any OS deployment or OS upgrade steps. Also confirm that it isn't marked as a high-impact task sequence. For more information, review the prerequisites for the [Task sequence deployment type](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="bkmk_dt-detect"></a> Deployment type **Detection Method** options

This procedure sets up a detection method that indicates the presence of the deployment type. In other words, whether the Windows device already has the application installed. Use one of the two following methods to create a detection method:

- [Configure rules to detect the presence of this deployment type](#bkmk_detect-rule)
- [Use a custom script to detect the presence of this deployment type](#bkmk_detect-script)

#### <a name="bkmk_detect-rule"></a> Configure rules to detect the presence of this deployment type

1. On the **Detection Method** page, the option to **Configure rules to detect the presence of this deployment type** is selected by default. Select **Add Clause**.  

2. In the **Detection Rule** dialog box, select a **Setting type** to detect the presence of the deployment type:  

    - **File System**: Detect whether a specified file or folder exists on a device. This detection indicates that the application is installed. Specify the following additional details:  

        - **Type**: Select whether it's a file or folder.  

        - **Path** (Required): Enter or browse to the local path on the device that includes the file or folder. For example, `C:\Program Files`. You can't specify a shared network path. If you select **Browse**, browse the local file system or connect to a representative client to browse.  

        - **File or folder name** (Required): Specify the specific file or folder name to detect in the above path. If the client detects this file or folder on the device, it considers the application as installed on the device.  

        - **This file or folder is associated with a 32-bit application on 64-bit systems**: The client first checks 32-bit file locations for the specified file or folder. If the file or folder isn't found, the client then searches 64-bit locations.  

    - **Registry**: Detect whether a specified registry key or registry value exists on a client device. This detection indicates that the application is installed. Specify the following additional details:  

        - **Hive** (Required): Choose a registry hive from the drop-down list. For example, `HKEY_LOCAL_MACHINE`.  

        - **Key** (Required): Specify the registry key to search in the above hive. For example, `SOFTWARE\Microsoft\Office`.  

        - **Value** (Optional): Enter a specific value to detect in the above key. If you want the client to detect the (Default) value, enable the option to **Use (Default) registry key value for detection**. When you enter a value or enable this option, you're required to select a **Data Type**.  

        - **This registry key is associated with a 32-bit application on 64-bit systems**: Select this option to first check 32-bit registry locations for the specified registry key. If the registry key isn't found, the client searches 64-bit locations.  

    - **Windows Installer**: Detect whether a specified Windows Installer file exists on a client device. This detection indicates that the application is installed. Specify the MSI **Product code** to detect on the client. If you select **Browse**, choose the MSI file from which to read the product code.

3. At the bottom of the Detection Rule window, specify whether the item must exist or satisfy a rule. For example, if you detect with a file, the following option is selected by default: **The file system setting must exist on the target system to indicate presence of this application**. Select the other option to create a rule for detection based on file or folder properties. These properties include Date Modified, Date Created, Version, or Size. These rule criteria are different for each setting type.  

4. Select **OK** to close the **Detection Rule** dialog box.  

When you create more than one detection method for a deployment type, you can group clauses together to create more complex logic.  

#### Group detection clauses *(optional)*

1. Create three or more detection method clauses on a deployment type.  

2. Select two or more consecutive clauses, and then select **Group**. You'll see the parentheses added to the associated columns, which show where the group starts and ends.  

    Example:

    | Connector  |  ( | Clause           |  )  |
    |------------|----|------------------|-----|
    |            |    | MSI Product Code |     |
    | Or         | (  | file1.text exists|     |
    | And        |    | file2.txt exists | )   |

3. To remove the group, select the grouped clauses, and then select **Ungroup**.  

*Continue* to the next section on using a custom script as a detection method. Or *skip* to the [User Experience](#bkmk_dt-ux) options for the deployment type.

#### <a name="bkmk_detect-script"></a> Use a custom script to check for the presence of a deployment type  

1. On the **Detection Method** page, select the **Use a custom script to detect the presence of this deployment type** box. Then select **Edit**.  

2. In the **Script Editor** dialog box, select a **Script type** to detect the deployment type: PowerShell, VBScript, or JScript.  

    > [!Note]  
    > When a Windows PowerShell script runs as a app detection method, the Configuration Manager client calls PowerShell with the `-NoProfile` parameter. This option starts PowerShell without profiles. A PowerShell profile is a script that runs when PowerShell starts. <!--3607762-->  

3. In the **Script contents** box, enter the script that you want to use, or paste in the contents of an existing script. Choose **Open** to browse to an existing saved script. Select **Clear** to remove the text in the Script contents field. If necessary, enable the option to **Run script as 32-bit process on 64-bit clients**.  

    > [!NOTE]  
    > The maximum size for a script is 32 KB.  

4. Select **OK** to save the script and close the **Script Editor** dialog box. Back on the Create Deployment Type wizard, the **Script Type** and **Script Length** fields update with details about your script.

#### About custom script detection methods  

Configuration Manager checks the results from the script. It reads the values written by the script to the standard output (STDOUT) stream, the standard error (STDERR) stream, and the exit code. If the script exits with a non-zero value, the script fails, and the application detection status is *Unknown*. If the exit code is zero, and STDOUT has data, the application detection status is *Installed*.

> [!TIP]
> When writing a detection script, if you return a zero exit code but don't return output (data in STDOUT), the application will not be detected as installed. For more information, see the following examples.

Use the following tables to check whether an application is installed from the output from a script:  

##### Zero exit code

|STDOUT|STDERR|Script result|Application detection state|
|---------|---------|---------|---------|
|Empty|Empty|Success|Not installed|
|Empty|Not empty|Failure|Unknown|
|Not empty|Empty|Success|Installed|
|Not empty|Not empty|Success|Installed|

##### Non-zero exit code

|STDOUT|STDERR|Script result|Application detection state|
|---------|---------|---------|---------|
|Empty|Empty|Failure|Unknown|
|Empty|Not empty|Failure|Unknown|
|Not empty|Empty|Failure|Unknown|
|Not empty|Not empty|Failure|Unknown|

##### Examples

Use the following PowerShell/VBScript examples to write your own application detection scripts:  

**Example 1**: The script returns an exit code that's not zero. This code indicates the script failed to run successfully. In this case, the application detection state is unknown.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Example 2**: The script returns an exit code of zero, but the value of STDERR isn't empty. This result indicates the script failed to run successfully. In this case, the application detection state is unknown.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Example 3**: The script returns an exit code of zero, which indicates it ran successfully. However, the value for STDOUT is empty, which indicates the application isn't installed.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Example 4**: The script returns an exit code of zero, which indicates it ran successfully. The value for STDOUT isn't empty, which indicates the application is installed.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Example 5**: The script returns an exit code of zero, which indicates it ran successfully. The values for STDOUT and STDERR aren't empty, which indicates the application is installed.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="bkmk_dt-ux"></a> Deployment type **User Experience** options

These settings specify how the client installs the application on devices, and what the user sees.  

On the **User Experience** page, specify the following information:  

- **Installation behavior**: In the drop-down list, select one of the following options:  

  - **Install for user**: The client only installs the application for the user to whom you deploy the application.  

  - **Install for system**: The client installs the application only once. It's available to all users.  

  - **Install for system if resource is device; otherwise, install for user**: If you deploy the application to a device, the client installs it for all users. If you deploy the application to a user, the client only installs it for that user.  

- **Logon requirement**: Select one of the following options:  

  - **Only when a user is logged on**  

  - **Whether or not a user is logged on**  

  - **Only when no user is logged on**  

    > [!NOTE]  
    > This option defaults to **Only when a user is logged on**. If you select **Install for user** in the **Installation behavior** drop-down list, you can't change this option.  

- **Installation program visibility**: Specify the mode in which the deployment type runs on client devices. Select one of the following options:  

  - **Maximized**: The deployment type runs maximized on client devices. Users see all installation activity.  

  - **Normal**: The deployment type runs in the normal mode based on system and program defaults. This mode is the default.  

  - **Minimized**: The deployment type runs minimized on client devices. Users might see the installation activity in the notification area or taskbar.  

  - **Hidden**: The deployment type runs hidden on client devices. Users see no installation activity.  

- **Allow users to view and interact with the program installation**: Specify whether a user can interact with the deployment type installation to set up the installation options.  

    If you selected the **Install for user** option in the **Installation behavior** drop-down list, this option is enabled by default.  

    > [!IMPORTANT]  
    > When you select the **Install for system** behavior, this setting is optional. This change is primarily to allow an end user to interact with the installation during a task sequence. For example, to run a setup process that prompts the end user for various options. Some application installers can't have user prompts silenced, or the installation process may require specific configuration values only known to the user. <!--1356976-->  
    >  
    > Installing in system context and allowing users to interact with the installation isn't a secure configuration. For more information, see [security and privacy for application management](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **Maximum allowed run time (minutes)**: Specify the maximum time in minutes that you expect the deployment type to run on the client computer. Specify this setting as a whole number greater than zero. The default value is 120 minutes (two hours).  

    Use this value for the following actions:  

  - To monitor the results from the deployment type.  

  - To check whether a deployment type is installed when you define maintenance windows on client devices. When a maintenance window is in place, a deployment type only starts if enough time is available in the maintenance window to accommodate the **Maximum Allowed Run Time** setting.  

    > [!IMPORTANT]  
    > A conflict might occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If the user sets the maximum run time to a period greater than the length of any available maintenance window, that deployment type doesn't run.  

- **Estimated installation time (minutes)**: Specify the estimated installation time of the deployment type. Users see this time in Software Center.  

#### Deployment type properties **User Experience** options

When you view the properties of a deployment type, the following options appear only on the **User Experience** tab:

Enforce specific post-installation behavior. Select one of the following options:  

- **Determine behavior based on return codes**: Handle reboots based on the codes configured on the [Return Codes](#bkmk_dt-return) tab. Software Center displays **Might Require a Reboot**. If a user is signed in during the install, they're prompted depending on the *deployment's* User Experience configuration.  

- **No specific action**: No reboot required after installation. Software Center reports that no reboot is required.  

- **The software install program might force a device restart**: Configuration Manager doesn't control or initiate a reboot, but the actual installation might do so without warning. Use this setting to prevent Configuration Manager from reporting installation failure when the installer initiates a reboot. Software Center displays **Might Require a Reboot**.  

- **Configuration Manager client will force a mandatory device restart**: Configuration Manager forces a device reboot after successful installation. Software Center reports that a reboot is required. If a user is signed in during the install, they're prompted depending on the *deployment's* User Experience configuration.  

### <a name="bkmk_dt-require"></a> Deployment type **Requirements**

Configuration Manager verifies these requirements on devices before installing the deployment type. Use requirements to further refine and control the devices or users that receive this application. For example, if you deploy the application to a user collection, specify the app's hardware requirements here.

1. On the **Requirements** page, select **Add** to open the **Create Requirement** dialog box.  

2. In the **Category** drop-down list, select whether this requirement is for a **Device** or a **User**.  

    Select **Custom** to use a previously created global condition. When you select **Custom**, you can also choose **Create** to create a new global condition. For more about global conditions, see [How to create global conditions](create-global-conditions.md).  

    > [!IMPORTANT]  
    > If you deploy the application to a device collection, the client ignores any requirement of the category **User** and the condition **Primary Device**.  

3. In the **Condition** drop-down list, select the condition to assess whether the user or device meets the installation requirements. The contents of this list vary depending on the selected category.  

4. In the **Operator** drop-down list, select the operator to use. This operator compares the selected condition to the specified value. It assesses whether the user or device meets the installation requirement. The available operators vary depending on the selected condition. When using the `One Of` operator, the Values field has validation that you have to enter one entry per row.

    > [!Note]  
    > The available requirements differ depending on the device type that the deployment type uses.  

5. In the **Value** box, specify the values to use for comparison. These values, along with the selected condition and operator, evaluate whether the user or device meets the installation requirements. The available values vary depending on the selected condition and the selected operator.  

6. Choose **OK** to save the requirement and close the **Create Requirement** dialog box.  

### <a name="bkmk_dt-depend"></a> Deployment type **Dependencies**  

Dependencies define one or more deployment types from another application that the client must install before it installs this deployment type.

> [!IMPORTANT]  
> In some cases, a deployment type is dependent on a deployment type that also has dependencies. The maximum number of supported dependencies in the chain is five.  

1. On the **Dependencies** page, select **Add**.  

2. In the Add Dependency window, enter the **Dependency group name**. This name refers to this group of application dependencies.  

3. In the Add Dependency window, select **Add**.  

4. In the **Specify Required Application** window, select an available application and at least one of its deployment types to use as a dependency.  

    > [!TIP]  
    > Select **View** to display the properties of the selected application or deployment type.  

5. Select **OK** to close the **Specify Required Application** window.  

6. If you want the client to automatically install the dependent application, select **Auto Install** next to the dependency.  

    > [!NOTE]  
    > You don't need to deploy a dependent application for the client to automatically install it.  

7. If you add more than one dependency, use the **Increase Priority** and **Decrease Priority** buttons. These actions change the order in which the client evaluates each dependency.  

8. Select **OK** to close the **Add Dependency** window.  

### <a name="bkmk_dt-return"></a> Deployment type **Return Codes**

> [!Note]  
> This page isn't in the Create Deployment Type wizard. It's only a tab on the properties of an existing deployment type.  

Specify return codes to control behaviors after the deployment type completes. For example, signal that a restart is required, the installation is complete.

1. On the **Return Codes** tab of the deployment type properties window, select **Add**.  

2. In the Add Return Code window, specify the **Return Code Value** that you expect from this deployment type. This value is any positive or negative integer between `-2147483648` and `2147483647`.  

3. Select a **Code Type** from the drop-down list. This setting defines how Configuration Manager interprets the specified return code from this deployment type. The available types vary based on the deployment type technology.  

    - **Success (no reboot)**: The deployment type successfully installed, and no reboot is necessary.  

    - **Failure (no reboot)**: The deployment type failed to install.  

    - **Hard Reboot**: The deployment type successfully installed, but requires the device to restart. Nothing else can be installed until the device restarts.  

    - **Soft Reboot**: The deployment type successfully installed, but requests the device to restart. Other installations can occur before the device restarts.  

    - **Fast Retry**: Another installation is already in progress on the device. The client retries every two hours, for a total of 10 times.  

4. Optionally, enter a **Name** and **Description** for this return code.

5. Select **OK** to close the Add Return Code window.  

#### Example: non-zero success

You're deploying an application that returns an exit code of `1` when it successfully installs. By default, Configuration Manager detects this non-zero return code as a failure. Specify the Return Code Value of `1`, and select the Code Type of **Success (no reboot)**. Now Configuration Manager interprets that return code as a success for this deployment type.

#### Default return codes

When you create some deployment types, Configuration Manager automatically adds the following return codes that are common to that technology:  

##### Windows Installer (\*.msi file)

|Value    |Code Type|
|---------|---------|
|0        |Success (no reboot)|
|1707     |Success (no reboot)|
|3010     |Soft Reboot|
|1641     |Hard Reboot|
|1618     |Fast Retry|

##### Script Installer

|Value    |Code Type|
|---------|---------|
|0        |Success (no reboot)|
|1641     |Hard Reboot|
|3010     |Soft Reboot|
|1618     |Fast Retry|

##### Windows app package (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)

|Value    |Code Type|
|---------|---------|
|15605    |Fast Retry|
|15618    |Fast Retry|

## <a name="bkmk_appv"></a> Additional options for App-V deployment types  

Configure additional options that are unique to deployment types for virtual applications (App-V).  

### <a name="bkmk_appv-content"></a> App-V deployment type **Content** options  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.  

2. Select an application with an App-V deployment type, and select **Properties**.  

3. In the application properties, switch to the **Deployment Types** tab. Select the App-V deployment type, and select **Edit**.  

4. In the deployment type properties, switch to the **Content** tab. Configure the following options as necessary:  

    - **Persist content in the client cache**: The Configuration Manager client won't delete from its cache the content for this deployment type.  

    - **Load content into App-V cache before launch**: Before the application starts, the Configuration Manager client loads into the App-V cache all content for this deployment type. The client doesn't pin the content in the cache. It deletes the content as necessary.  

5. Select **OK** to close the deployment type properties. Then select **OK** to close the application properties.  

### <a name="bkmk_appv-pub"></a> App-V deployment type **Publishing** options

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.  

2. Select an application with an App-V deployment type, and select **Properties**.  

3. In the application properties, switch to the **Deployment Types** tab. Select the App-V deployment type, and select **Edit**.  

4. In the deployment type properties, switch to the **Publishing** tab. Select the items in the virtual application that you want to publish.  

5. Select **OK** to close the deployment type properties. Then select **OK** to close the application properties.  

## <a name="bkmk_import"></a> Import an application  

Use the following procedure to import an application into Configuration Manager:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.  

2. In the ribbon, on the **Home** tab and the **Create** group, select **Import Application**.  

3. On the **General** page of the Import Application Wizard, specify the network path to the **File** to import. For example, `\\server\share\file.zip`. This file is a valid compressed archive (ZIP format) of an exported Configuration Manager application.  

4. On the **File Content** page, select the action to take if this application is a duplicate of an existing application. Create a new application, or ignore the duplicate and add a new revision to the existing application.  

5. On the **Summary** page, review the actions, and then finish the wizard.  

The new application appears in the **Applications** node.  

> [!TIP]  
> The Windows PowerShell cmdlet **Import-CMApplication** has the same function as this procedure. For more information, see [Import-CMApplication](/powershell/module/configurationmanager/import-cmapplication).  

For more information about how to export an application, see [Management tasks for applications](management-tasks-applications.md).

## <a name="bkmk_deploy-types"></a> Supported deployment types  

Configuration Manager supports the following deployment types for applications:

| Deployment type name | Description |
|--------------------------|----------------------|
| **Windows Installer (\*.msi file)** | A Windows Installer file (`.msi`). |
| **Windows app package (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** | Windows app package files (`.appx` or `.msix`) or Windows app bundle packages (`.appxbundle` or `.msixbundle`).<!--1357427--> |
| **Windows app package (in the Windows Store)** | Specify a link to the app in the Windows Store, or browse the store to select the app.<sup>[Note 1](#bkmk_note1)</sup> |
| **Script Installer** | Specify a script or program that runs on Windows clients to install content or to do an action. Use this deployment type for setup.exe installers or script wrappers. |
| **Microsoft Application Virtualization 4** | A Microsoft App-V v4 manifest. |
| **Microsoft Application Virtualization 5** | A Microsoft App-V v5 package file. |
| **Windows Phone app package (\*.xap file)** | A Windows Phone app package file. |
| **Windows Phone app package (in the Windows Phone Store)** | Specify a link to the app in the Windows Store. |
| **macOS X** | For macOS computers running the Configuration Manager client. Create a `.cmmac` file with the **CMAppUtil** tool. |
| **Web Application** | Specify a link to a web application. This deployment type installs a shortcut to the web application on the user's device. |
| **Windows Installer through MDM (\*.msi)** | Create and deploy Windows Installer-based apps to Windows devices using on-premises mobile device management (MDM). For more information, see [Deploy Windows Installer apps to MDM-enrolled Windows devices](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Task sequence** | Install or uninstall complex applications using task sequences. For more information, see [Task sequence deployment type](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> The Configuration Manager console may display other deployment types, but they are for platforms that are no longer supported. For more information, see [What happened to hybrid?](../../mdm/understand/what-happened-to-hybrid.md).

### <a name="bkmk_note1"></a> Note 1: Windows app package (in the Windows Store)

To deploy the app as a link to the Windows Store, configure the group policy **Turn off the Store application**. Set this policy to **Disabled** or **Not configured**. If you enable this setting, clients can't connect to the Windows Store to download and install applications.

Windows clients always evaluate deployment types that use a link to a store before other deployment types. Then the client evaluates deployment types by priority.

> [!TIP]
> Some store links may cause the following error in the Create Application Wizard: "Invalid Application link". For example, some store *Featured Apps* may cause this error. You can still select **Next** on the **General** page of the wizard. Configuration Manager successfully creates the app, and you can successfully deploy it.<!-- SCCMDocs-pr #4716 -->

## Next steps

After creating an application in Configuration Manager, the next step is to [deploy the application](deploy-applications.md).

Create a group of applications that you can send to a user or device collection as a single deployment. For more information, see [Create application groups](create-app-groups.md).

For more information about creating applications on different OS platforms, see the following articles:  

- [Create Windows applications](../get-started/creating-windows-applications.md)
- [Create Mac applications](../get-started/creating-mac-computer-applications.md)
- [Create Windows Embedded applications](../get-started/creating-windows-embedded-applications.md)
