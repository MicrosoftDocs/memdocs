---
title: Create applications
titleSuffix: Configuration Manager
description: Create applications with deployment types, detection methods and requirements to install software.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Create applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A Configuration Manager application has one or more deployment types. These deployment types include the installation files and information that are required to install software on devices. A deployment type also has rules, such as detection methods and requirements, that specify when and how the client installs the software.  

 Create applications by using the following methods:  

-   Automatically create the application and deployment types by reading the application installation files.  

-   Manually create the application and then add deployment types later.  

-   Import an application from a file.  

> [!NOTE]  
>  For detailed information about creating iOS, Windows Phone, and Android applications, see [Create applications for mobile devices](../../mdm/deploy-use/create-applications.md).  



## Start the create application wizard  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Application**.  



## Specify whether you want to automatically detect application information or manually define the information  

-   Automatically detect application information to create a basic application with a single deployment type. For example, a Windows Installer file that has no dependencies or requirements. After you create an application by using this procedure, you can edit it as needed to add or change deployment types and add detection methods, dependencies, or requirements.  

-   Manually specify application information to create more complex applications that have multiple deployment types, dependencies, detection methods, or requirements.  

### Automatically detect application information  

1.  On the **General** page of the Create Application wizard, select **Automatically detect information about this application from installation files**.  

2.  In the **Type** drop-down list, select the application installation file type that you want to use to detect application information. For information about the available installation types, see [Deployment types supported by Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) in this topic.  

3.  In the **Location** box, specify the UNC path (in the form *\\\\server\\share\\\filename*) or the store link for the application installation file that you want to use to detect application information. Alternatively, click **Browse** to browse to the installation file.  

	> [!IMPORTANT]  
	>  When you select **Windows Installer (\*.msi file)** as an application type, all of the files in the specified folder are imported, and are sent to distribution points. Ensure that the folder that you specify contains only the files that are necessary to install the application. Configuration Manager is tested to support up to 20,000 application files in the application package. If your application has more files, consider creating multiple applications that have a smaller number of files.  

	>  You must have access to the UNC path that has the application and any subfolders that include application content.  

4.  On the **Import Information** page of the Create Application wizard, review the information that was imported, and then choose **Next**. If necessary, you can choose **Previous** to go back and fix any errors.  

5.  On the **General Information** page of the Create Application wizard, specify the following information:  

    > [!NOTE]  
    >  If Configuration Manager automatically detects this information from the application installation files, it's already populated here. Additionally, the displayed options might be different depending on the application type that you create.  

    -   General information about the application, like the application name, comments, and version. To help you find the application in the Configuration Manager console, specify an optional reference.  

    -   **Installation program**: Specify the installation program and any required properties that are needed to install the application deployment type.  

        > [!TIP]  
        >  If the installation program doesn't appear, choose **Browse** and browse to the installation program location.  

    -   **Install behavior**: Specify whether the application deployment type is installed for only the currently logged-on user or for all users. A third option is to install for all users if it is deployed to a device, or only to a specific user if it is deployed to a user.  

    -   **Use an automatic VPN connection (if configured)**: If a VPN profile has been deployed to the device on which the app is launched, launch the VPN connection when the app starts (Windows 8.1 and Windows Phone 8.1 only).  

         On Windows Phone 8.1 devices, automatic VPN connections aren't supported if more than one VPN profile has been deployed to the device.  

         For more information, see [VPN profiles](../../protect/deploy-use/vpn-profiles.md).  

    - **Provision this application for all users on the device**<!--1358310-->: Starting in version 1806, provision an application with a Windows app package for all users on the device. For more information, see [Create Windows applications](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  

       > [!Tip]  
       > If you're modifying an existing application, this setting is on the **User Experience** tab of the Windows app package deployment type properties.  


6.  Choose **Next**, review the application information on the **Summary** page, and then finish the Create Application wizard.  

The new application appears in the **Applications** node of the Configuration Manager console, and you have finished creating an application. If you want to add more deployment types to the application, see [Create deployment types for the application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in this topic.  

### Manually specify application information  

1.  On the **General** page of the Create Application wizard, select **Manually specify the application information**, and then choose **Next**.  

2.  Specify general information about the application, like the application name, comments, and version. To help you find the application in the Configuration Manager console, specify an optional reference.  

3.  On the **Application Catalog** page of the Create Application wizard, specify the following information:  

    -   **Selected language**: In the drop-down list, select the language version of the application that you want to set up. Choose **Add/Remove** to set up more languages for this application.  

    -   **Localized application name**: Specify the application name in the language that you selected in the **Selected language** drop-down list.  

        > [!IMPORTANT]  
        >  You must specify a localized application name for each language version that you set up.  

    -   **User categories**: Choose **Edit** to specify application categories in the language that you selected in the **Selected Language** drop-down list. Users of Software Center can use these selected categories to help filter and sort the available applications.  

    -   **User documentation**: Choose **Browse** to specify the location of a file that Software Center users can read to get more information about this application. This location is a URL, or a network path and file name.

    -   **Link text**: Specify the text that appears in place of the URL to the application.  

    -   **Application Privacy URL**: Specify a URL that links to the privacy statement for the application.  

    -   **Localized description**: Enter a description for this application in the language that you selected in the **Selected Language** drop-down list.  

    -   **Keywords**: Enter a list of keywords in the language that you selected in the **Selected Language** drop-down list. These keywords help Software Center users search for the application.  

    -   **Icon**: Choose **Browse** to select an icon for this application from the available icons. If you do not specify an icon, a default icon is used for this application. You can now set an icon with a pixel dimensions of up to 512x512.

    -   **Display this as a featured app and highlight it in the company portal**: This option prominently displays the app in the company portal.  

4.  On the **Deployment Types** page of the Create Application wizard, choose **Add** to create a new deployment type.  

 For more information, see [Create deployment types for the application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Choose **Next**, review the application information on the **Summary** page, and then finish the Create Application wizard.  

The new application appears in the **Applications** node of the Configuration Manager console.  



##  Create deployment types for the application  
 If you automatically detect application information, you might not need to finish some of the steps in these procedures.  

### Start the create deployment type wizard  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  Select an application, and then on the **Home** tab, in the **Application** group, choose **Create Deployment Type**.  

> [!TIP]  
>  You can also start the Create Deployment Type wizard from the Create Application wizard and from the **Deployment Types** tab of the *<application name\>* **Properties** dialog box.  

### Specify whether you want to automatically detect deployment type information or manually set up the information  
 Use one of the following procedures to automatically detect or manually set up deployment type information.  

#### Automatically detect deployment type information  

1.  On the **General** page of the Create Deployment Type wizard, select **Automatically identify information about this deployment type from installation files**.  

2.  In the **Type** box, select the application installation file type that you want to use to detect the deployment type information.  

3.  In the **Location** box, specify the network path or specify the store link to the application installation files. Configuration Manager uses these files to detect the deployment type information. You can also choose **Browse** to locate the installation file.  

    > [!NOTE]  
    >  You must have access to the network path that has the application and any subfolders that include the application content.  

4.  On the **Import Information** page of the Create Deployment Type wizard, review the information that was imported, and then choose **Next**. You can also choose **Previous** to go back and fix any errors.  

5.  On the **General Information** page of the Create Deployment Type wizard, specify the following information:  

    > [!NOTE]  
    >  Some of the deployment type information might already be present if it was read from the application installation files. Additionally, the displayed options might differ, depending on the deployment type that you're creating.  

    -   General information about the deployment type, like the name, admin comments, and available languages.  

    -   **Installation program**: Specify the installation program and any properties that you require to install the deployment type.  

    -   **Install behavior**: Specify whether to install the deployment type for the current user or for all users. A third option is to install for all users if it is deployed to a device, or only to a specific user if it is deployed to a user.  

    -   **Use an automatic VPN connection (if configured)**: If a VPN profile has been deployed to the device on which the app is launched, launch the VPN connection when the app starts (Windows 8.1 and Windows Phone 8.1 only). If multiple VPN profiles have been deployed to a Windows 8.1 device, the first deployed VPN profile is used by default.  

         On Windows Phone 8.1 devices, automatic VPN connections aren't supported if more than one VPN profile has been deployed to the device.  

         For more information, see [VPN profiles](../../protect/deploy-use/vpn-profiles.md).  

6.  Choose **Next**, and then continue to [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

#### Manually set up the deployment type information  

1.  On the **General** page of the Create Deployment Type wizard, in the **Type** drop-down list, choose the application installation file type for this deployment type. 

2.  Select **Manually specify the deployment type information**, and then click **Next**.

3.  On the **General Information** page of the Create Deployment Type wizard, specify a name for the deployment type. Optionally specify a description and the languages for this deployment type, and then click **Next**.  

4.  Continue to [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

###  Specify content options for the deployment type  

1.  On the **Content** page of the Create Deployment Type wizard, specify the following information:  

    -   **Content location**: Specify the location of the content for this deployment type, or select **Browse** to choose the deployment type content folder.  

        > [!IMPORTANT]  
        >  The System account of the site server computer must have permissions to the content location that you specify.  

    -   **Uninstall content settings**: Specify one of the following options:
        - **Same as install content**: If the install and uninstall content are the same, select this option. This option is the default.
        - **No uninstall content**: If your application does not need content for uninstall, select this option.
        - **Different from install content**: If the uninstall content is different from the install content, select this option. Then specify the location of the application content that is used to uninstall the application.
5. Click **OK** to close the deployment type properties dialog box.

    -   **Persist content in the client cache**: Select this option to specify whether the client indefinitely retains the content in the cache. The client retains the content even if the app is already installed. This option is useful with some deployments, like Windows Installer–based software. Windows Installer needs a local copy of the source content for applying updates. Although this option does reduce the available cache space. If you select this option, it might cause a large deployment to fail at a later point if the cache does not have sufficient available space.  

    -   **Allow clients to share content with other clients on the same subnet**: To reduce load on the network, select this option. Clients download content from other local clients on the network that have already downloaded and cached the content. This option utilizes Windows BranchCache technology.  

    -   **Installation program**: Specify the name of the installation program and any required installation parameters, or choose **Browse** to locate the installation file.  

    -   **Installation start in**: Optionally, specify the folder that has the installation program for the deployment type. This folder can be an absolute path on the client or a path to the distribution point folder that has the installation files.  

    -   **Uninstall program**: Optionally, specify the name of the uninstall program and any required parameters, or choose **Browse** to locate it.  

    -   **Uninstall start in**: Optionally, specify the folder that has the uninstall program for the deployment type. This folder can be an absolute path on the client. It can also be a relative path on a distribution point of the folder with the package.  

    -   **Run installation and uninstall program as 32-bit process on 64-bit clients**: Use the 32-bit file and registry locations on Windows-based computers to run the installation program for the deployment type.  

2.  Choose **Next**.  

### Set up detection methods to indicate the presence of the deployment type (Windows PCs only)  
 This procedure sets up  a detection method that indicates whether the deployment type is already installed.  

1.  On the **Detection Method** page of the Create Deployment Type wizard, select **Configure rules to detect the presence of this deployment type**, and then choose **Add Clause**.  

    > [!NOTE]  
    >  You can also select **Use a custom script to detect the presence of this deployment type**. For more information, see [Use a custom script to check for the presence of a deployment type](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  In the **Detection Rule** dialog box, in the **Setting type** drop-down list, select the method that you want to use to detect the presence of the deployment type. You can choose from the following available methods:  

    -   **File System**: Detect whether a specified file or folder exists on a client device. This detection indicates that the application is installed.  

        > [!NOTE]  
        >  The **File system** setting type doesn't support specifying a UNC path to a network share in the Path field. You can only specify a local path on the client device.  
        >   
        >  To check 32-bit file locations for the specified file or folder, first select **This file or folder is associated with a 32-bit application on 64-bit systems**. If the file or folder isn't found, 64-bit locations are searched.  

    -   **Registry**: Detect whether a specified registry key or registry value exists on a client device. This detection indicates that the application is installed.  

        > [!NOTE]  
        >  To check 32-bit registry locations for the specified registry key, first select **This registry key is associated with a 32-bit application on 64-bit systems**. If the registry key is not found, 64-bit locations are searched.  

    -   **Windows Installer**: Detect whether a specified Windows Installer file exists on a client device. This detection indicates that the application is installed.  

3.  Specify details about the item to detect whether this deployment type is installed. For example, you can use a file, folder, registry key, registry value, or a Windows Installer product code.  

4.  Specify whether the item must exist or satisfy a rule. For example, if you detect with a file, select **The file system setting must exist on the target system to indicate presence of this application**.  

5.  Choose **Next** to close the **Detection Rule** dialog box.  

####  Use a custom script to check for the presence of a deployment type  

1.  On the **Detection Method** page of the Create Deployment Type wizard, select the **Use a custom script to detect the presence of this deployment type** box, and then choose **Edit**.  

2.  In the **Script Editor** dialog box, in the **Script type** drop-down list, select the script language that you want to use to detect the deployment type.  

3.  In the **Script contents** box, enter the script that you want to use. You can also paste the contents of an existing script in this field, or choose **Open** to browse to an existing saved script. Configuration Manager checks the results from the script. It reads the values written by the script to the standard output (STDOUT) stream, the standard error (STDERR) stream, and the exit code. If the script exits with a nonzero value, the script fails and the application detection status is unknown. If the exit code is zero and STDOUT has data, the application detection status is Installed.  

 Use the following table to check whether an application is installed from the output from a script:  

|Script exit code|Details|
|--------------------------------|-----------------|
|0|**Data read from STDOUT**: Empty<br /><br /> **Data read from STDERR**: Empty<br /><br /> **Script result**: Success<br /><br /> **Application detection state**: Not installed|  
|0|**Data read from STDOUT**: Empty<br /><br /> **Data read from STDERR**: Not empty<br /><br /> **Script result**: Failure<br /><br /> **Application detection state**: Unknown|  
|0|**Data read from STDOUT**: Not empty<br /><br /> **Data read from STDERR**: Empty<br /><br /> **Script result**: Success<br /><br /> **Application detection state**: Installed|  
|0|**Data read from STDOUT**: Not empty<br /><br /> **Data read from STDERR**: Not empty<br /><br /> **Script result**: Success<br /><br /> **Application detection state**: Installed|  
|Non-zero value|**Data read from STDOUT**: Empty<br /><br /> **Data read from STDERR**: Empty<br /><br /> **Script result**: Failure<br /><br /> **Application detection state**: Unknown|  
|Non-zero value|**Data read from STDOUT**: Empty<br /><br /> **Data read from STDERR**: Not empty<br /><br /> **Script result**: Failure<br /><br /> **Application detection state**: Unknown|  
|Non-zero value|**Data read from STDOUT**: Not empty<br /><br /> **Data read from STDERR**: Empty<br /><br /> **Script result**: Failure<br /><br /> **Application detection state**: Unknown|  
|Non-zero value|**Data read from STDOUT**: Not empty<br /><br /> **Data read from STDERR**: Not empty<br /><br /> **Script result**: Failure<br /><br /> **Application detection state**: Unknown|  

The following table has Microsoft Visual Basic (VB) sample scripts that you can use to write your own application detection scripts.  

|Visual Basic sample script|Description|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|The script returns an exit code that is not zero, which indicates that it failed to run successfully. In this case, the application detection state is unknown.|  
|**WScript.StdErr.Write "Script failed"**<br /><br /> **WScript.Quit(0)**|The script returns an exit code of zero, but the value of STDERR is not empty. This result indicates that the script failed to run successfully. In this case, the application detection state is unknown.|  
|**WScript.Quit(0)**|The script returns an exit code of zero, which indicates that it ran successfully. However, the value for STDOUT is empty, which indicates that the application is not installed.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.Quit(0)**|The script returns an exit code of zero, which indicates that it ran successfully. The value for STDOUT is not empty, which indicates that the application is installed.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.StdErr.Write "Completed"**<br /><br /> **WScript.Quit(0)**|The script returns an exit code of zero, which indicates that it ran successfully. The values for STDOUT and STDERR are not empty, which indicates that the application is installed.|  

 > [!NOTE]  
 >  The maximum size that you can use for a script is 32 kilobytes (KB).  

4.  Choose **OK** to close the **Script Editor** dialog box.  

### Specify user experience options for the deployment type  
 These settings specify how the client installs the application on devices, and what the user sees.  

1.  On the **User Experience** page of the Create Deployment Type wizard, specify the following information:  

    -   **Installation behavior**: In the drop-down list, select one of the following options:  

        -   **Install for User**: The application is installed only for the user to whom the application is deployed.  

        -   **Install for System**: The application is installed only once, and it is available to all users.  

        -   **Install for System if resource is device; otherwise install as user**: If the application is deployed to a device, the client installs it for all users. If the application is deployed to a user, the client only installs it for that user.  

    -   **Logon requirement**: Specify the logon requirements for this deployment type from the following options:  

        -   **Only when a user is logged on**  

        -   **Whether or not a user is logged on**  

        -   **Only when no user is logged on**  

        > [!NOTE]  
        >  This option defaults to **Only when a user is logged on**. If you select **Install for user** in the **Installation behavior** drop-down list, you can't change this option.  

    -   **Installation program visibility**: Specify the mode in which the deployment type runs on client devices. The following options are available:  

        -   **Maximized**: The deployment type runs maximized on client devices. Users see all installation activity.  

        -   **Normal**: The deployment type runs in the normal mode based on system and program defaults. This mode is the default.  

        -   **Minimized**: The deployment type runs minimized on client devices. Users might see the installation activity in the notification area or taskbar.  

        -   **Hidden**: The deployment type runs hidden on client devices. Users see no installation activity.  

    -   **Allow users to view and interact with the program installation**: Specify whether a user can interact with the deployment type installation to set up the installation options.  

        > [!NOTE]  
        >  If you select the **Install for user** option in the **Installation behavior** drop-down list, this option is enabled by default.  

        > [!IMPORTANT]
        > Starting in version 1802, this setting is optional when you select the **Install for system** behavior. This change is primarily to allow an end user to interact with the installation during a task sequence. For example, to run a setup process that prompts the end user for various options. Some application installers can't have user prompts silenced, or the installation process may require specific configuration values only known to the user. <!--1356976-->
        > 
        > Installing in system context and allowing users to interact with the installation is not a secure configuration. For more information, see [security and privacy for application management](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).

    -   **Maximum allowed run time (minutes)**: Specify the maximum time that the program is expected to run on the client computer. You can specify this setting as a whole number greater than zero. The default setting is 120 minutes.  

         This value is used to:  

        -   Monitor the results from the deployment type.  

        -   Check whether a deployment type is installed when maintenance windows are defined on client devices. When a maintenance window is in place, a program only starts if enough time is available in the maintenance window to accommodate the **Maximum Allowed Run Time** setting.  

        > [!IMPORTANT]  
        >  A conflict might occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If the user sets the maximum run time to a period greater than the length of any available maintenance window, that deployment type doesn't run.  

    -   **Estimated installation time (minutes)**: Specify the estimated installation time of the deployment type. Users see this time in Software Center.  

    -   **Specify specific reboot behavior**: Specify the post-installation action. The following options are available:  

        -   **Determine behavior based on return codes**: Handle reboots based on the codes configured on the Return Codes tab. Software Center displays **Might Require a Reboot**. If a user is logged in during the install, they are prompted depending on the deployment's User Experience configuration.  

        -   **No specific action**: No reboot required after installation. Software Center reports that no reboot is required.  
        -   **The software installation program might force a device restart**: Configuration Manager doesn't control or initiate a reboot, but the actual installation might do so without warning. Use this setting to prevent Configuration Manager from reporting installation failure when the installer initiates a reboot. Software Center displays **Might Require a Reboot**.  

        -   **Configuration Manager client will force a mandatory device restart**: Configuration Manager forces a device reboot after successful installation. Software Center reports that a reboot is required. If a user is logged in during the install, they are prompted depending on the deployment's User Experience configuration.

### Specify requirements for the deployment type  

1.  On the **Requirements** page of the Create Deployment Type wizard, choose **Add** to open the **Create Requirement** dialog box, and add a new requirement.  

    > [!NOTE]  
    >  You can also add new requirements on the **Requirements** tab of the *<deployment type name\>* **Properties** dialog box.  

2.  In the **Category** drop-down list, select whether this requirement is for a device or a user. Select **Custom** to use a previously created global condition. When you select **Custom**, you can also choose **Create** to create a new global condition. For more about global conditions, see [How to create global conditions](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  If you deploy the application to a device collection, the client ignores any requirement of the category **User** and the condition **Primary Device**.  
    >   
    >  If you used System Center 2012 R2 Configuration Manager SP1 to create a Windows package and program or task sequence that has Windows 10 as a requirement, and then upgrade to System Center Configuration Manager, the requirements for Windows 10 might be removed. To fix this problem, specify the requirements again. Although the requirement was removed from the requirements display, it's still processed correctly on devices.  

3.  In the **Condition** drop-down list, select the condition that you want to use to assess whether the user or device meets the installation requirements. The contents of this list vary depending on the selected category.  

4.  In the **Operator** drop-down list, select the operator to use. This operator compares the selected condition to the specified value. It assesses whether the user or device meets the installation requirements. The available operators vary depending on the selected condition.  

    > [!IMPORTANT]  
    >  The available requirements differ depending on the device type that the deployment type uses.  

5.  In the **Value** box, specify the values to use. These values, along with the selected condition and operator, evaluate whether the user or device meets the installation requirements. The available values vary depending on the selected condition and the selected operator.  

6.  Choose **OK** to save the requirement and close the **Create Requirement** dialog box.  

### Specify dependencies for the deployment type  
 Dependencies define one or more deployment types from another application that must be installed before a deployment type is installed. You can set up the dependent deployment types to be installed automatically before a deployment type is installed.  

> [!IMPORTANT]  
>  In some cases, a deployment type is dependent on a deployment type that also has dependencies. The maximum number of supported dependencies in the chain is five.  

1.  On the **Dependencies** page of the Create Deployment Type wizard, choose **Add**.  

    > [!IMPORTANT]  
    >  You can also add new dependencies on the **Dependencies** tab of the *<deployment type name\>* **Properties** dialog box.  

2.  In the **Add Dependency** dialog box, choose **Add**.  

3.  In the **Specify Required Application** dialog box, select an existing application and one of the application deployment types to use as a dependency.  

    > [!TIP]  
    >  You can choose **View** to display the properties of the selected application or deployment type.  

4.  Choose **OK** to close the **Specify Required Application** dialog box.  

5.  If you want a dependent application to be automatically installed, select **Auto Install** next to the dependent application.  

    > [!NOTE]  
    >  You don't need to deploy a dependent application for it to be automatically installed.  

6.  In the **Add Dependency** dialog box under **Dependency group name**, enter a name to refer to this group of application dependencies.  

7.  Optionally, use the **Increase Priority** and **Decrease Priority** buttons. These actions change the order in which the client evaluates each dependency.  

8.  Choose **OK** to close the **Add Dependency** dialog box.  

### Confirm the deployment type settings and finish the wizard  

1.  Review the **Summary**. Choose **Next** to create the deployment type. Choose **Previous** to go back and change the settings for the deployment type.  

2.  After the **Progress** page finishes, review the actions that the wizard took, and then choose **Close** to finish the wizard.  

3.  If you started the Create Deployment Type wizard from the Create Application wizard, you return to the **Deployment Types** page of the Create Application wizard.  



## Set up additional options for deployment types that contain virtual applications  
 Use the following procedures to set up additional options for deployment types that include virtual applications.  

### Set up content options for Application Virtualization (App-V) deployment types  

1.  In the Configuration Manager console, choose **Software Library** > **Applications**.  

2.  In the **Applications** list, select an application that has an App-V deployment type. Then, on the **Home** tab, in the **Properties** group, choose **Properties**.  

3.  In the *<Application Name\>* **Properties** dialog box, on the **Deployment Types** tab, select an App-V deployment type, and then choose **Edit**.  

4.  In the *<Deployment Type Name\>* **Properties** dialog box, on the **Content** tab, set up the following options if necessary:  

    -   **Persist content in the client cache**: Select this option to ensure that the content for this deployment type is not deleted from the Configuration Manager client cache.  

    -   **Load content into App-V cache before launch**: Select this option to ensure that all content for the virtual application is loaded into the App-V cache before the application starts. This option also ensures that the application content is not pinned in the cache. The client deletes the content as necessary.  

5.  Choose **OK** to close the *<Deployment Type Name\>* **Properties** dialog box.  

6.  Choose **OK** to close the *<Application Name\>* **Properties** dialog box.  

### Set up publishing options for App-V deployment types  

1.  In the Configuration Manager console, choose **Software Library** > **Applications**.  

3.  In the **Applications** list, select an application that has an App-V deployment type. Then, on the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  In the *<Application Name\>* **Properties** dialog box, on the **Deployment Types** tab, select an App-V deployment type, and then choose **Edit**.  

5.  In the *<Deployment Type Name\>* **Properties** dialog box, on the **Publishing** tab, select the items in the virtual application that you want to publish.  

6.  Choose **OK** to close the *<Deployment Type Name\>* **Properties** dialog box.  

7.  Choose **OK** to close the *<Application Name\>* **Properties** dialog box.  



## Import an application  
 Use the following procedure to import an application into Configuration Manager. For information about how to export an application, see [Management tasks for System Center Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md).  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.   

3.  On the **Home** tab, in the **Create** group, choose **Import Application**.  

4.  On the **General** page of the **Import Application wizard**, choose **Browse**. Then specify a network path to the .zip file with the application to import.  

5.  On the **File Content** page, select the action to take if the application that you are trying to import is a duplicate of an existing application. You can create a new application or ignore the duplicate and add a new revision to the existing application.  

6.  On the **Summary** page, review the actions to be taken, and then finish the wizard.  

 The new application appears in the **Applications** node.  

> [!TIP]  
>  The Windows PowerShell cmdlet **Import-CMApplication** has the same function as this procedure. For more information, see [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  



##  Deployment types supported by Configuration Manager  

|Deployment type name|More information|  
|--------------------------|----------------------|  
|**Windows Installer (\*.msi file)**|Creates a deployment type from a Windows Installer file.|  
|**Windows app package (\*.appx, \*.appxbundle)**|Creates a deployment type for Windows 8 or later. Select a Windows app package file or a Windows app bundle package.|  
|**Windows app package (in the Windows Store)**|Creates a deployment type for Windows 8 or later. Specify a link to the app in the Windows Store, or browse the store to select the app.<br /><br /> To deploy the app as a link to the Windows Store, configure the group policy setting **Turn off the Store application** to **Disabled** or **Not configured**. If this setting is enabled, clients can't connect to the Windows Store to download and install applications.<br /><br /> Windows 8 deployment types that use a link to a store are always evaluated before other deployment types, irrespective of their priority.|  
|**Script Installer**|Creates a deployment type that specifies a script that runs on client devices to install content or to do an action.|  
|**Microsoft Application Virtualization 4**|Creates a deployment type from a Microsoft Application Virtualization 4 manifest|  
|**Microsoft Application Virtualization 5**|Creates a deployment type from a Microsoft Application Virtualization 5 package file.|  
|**Windows Phone app package (\*.xap file)**|Creates a deployment type from a Windows Phone app package file.|  
|**Windows Phone app package (in the Windows Phone Store)**|Creates a deployment type by specifying a link to the app in the Windows Phone store.|  
|**App Package for iOS (\*.ipa file)**|Creates a deployment type from an iOS app package file.|  
|**App Package for iOS from App Store**|Creates a deployment type by specifying a link to the iOS app in the App Store.|  
|**App Package for Android (\*.apk file)**|Creates a deployment type from an Android app package file.|  
|**App Package for Android on Google Play**|Creates a deployment type by specifying a link to the app on Google Play.|  
|**Mac OS X**|Creates a deployment type for Mac computers from a .cmmac file that you have created by using the CMAppUtil tool.<br /><br /> Applies only to Mac computers running the Configuration Manager client.|  
|**Web Application**|Creates a deployment type that specifies a link to a web application. The deployment type installs a shortcut to the web application on the user’s device.<br /><br /> If you installed the Microsoft Intune managed browser on iOS or Android devices, ensure that users can only use the managed browser to open the app. Use one of the following formats when you specify a link to the app: replace **http:** with **http-intunemam:** or **https:** with **https-intunemam:**<br /><br /> - **http-intunemam://<path to web app\>**<br /><br /> - **https-intunemam://<path to web app\>**<br /><br /> You can use Configuration Manager application requirements to ensure that apps you want to associate with the managed browser are only installed to iOS and Android devices.<br /><br /> For more about the Intune managed browser, see [Manage Internet access using managed browser policies](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer through MDM (\*.msi)**|This installer type lets you create and deploy Windows Installer-based apps to PCs that run Windows 10.<br /><br /> The following considerations apply when you use this installer type:<br><br>- You can only upload a single file with the extension .msi.<br /><br /> - The file's product code and product version are used for app detection.<br /><br /> - The default restart behavior of the app is used. Configuration Manager does not control this restart.<br /><br /> - Per-user MSI packages are installed for a single user.<br /><br /> - Per-machine MSI packages are installed for all users on the device.<br /><br /> - Dual-mode MSI packages currently only install for all users on the device.<br /><br /> - App updates are supported when the MSI product code of each version is the same.|  



## Next steps

After creating an application in Configuration Manager, the next step is to [deploy the application](/sccm/apps/deploy-use/deploy-applications).