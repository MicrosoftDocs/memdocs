---
title: "Create applications | Microsoft Docs"
description: "Create and deploy applications and deployment types with System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---
# Create applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A System Center Configuration Manager application has the files and information that are required to deploy software to a device. An application has one or more deployment types that comprise the installation files and information that are required to install software. A deployment type also has rules that specify when and how the software is deployed.  

 You can create applications by using the following methods:  

-   Automatically create the application and deployment types by reading the application installation files.  

-   Manually create the application and then add deployment types later.  

-   Import an application from a file.  

> [!NOTE]  
>  [Create applications for mobile devices](../../mdm/deploy-use/create-applications.md) provides detailed information about creating iOS, Windows Phone, and Android applications.  

Use the following steps to create Configuration Manager applications and deployment types.  

## Start the create application wizard  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Application**.  

## Specify whether you want to automatically detect application information or manually define the information  

-   Automatically detect application information when you want to create a simple application that has a single deployment type, like a Windows Installer file that has no dependencies or requirements. After you create an application by using this procedure, you can edit it as needed to add or change deployment types and add detection methods, dependencies, or requirements.  

-   Manually specify application information to create more complex applications that have multiple deployment types, dependencies, detection methods, or requirements.  

### Automatically detect application information  

1.  On the **General** page of the Create Application wizard, select **Automatically detect information about this application from installation files**.  

2.  In the **Type** drop-down list, select the application installation file type that you want to use to detect application information. For information about the available installation types, see [Deployment types supported by Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) in this topic.  

3.  In the **Location** box, specify the UNC path (in the form *\\\\server\\share\\\filename*) or the store link for the application installation file that you want to use to detect application information. Alternatively, click **Browse** to browse to the installation file.  

	> [!IMPORTANT]  
	>  When you select **Windows Installer (\*.msi file)** as an application type, all of the files in the folder that you specify will be imported with the application and will be sent to distribution points. Ensure that the folder that you specify contains only the files that are necessary to install the application. Configuration Manager is tested to support up to 20,000 application files in the application package. If your application has more files, consider creating multiple applications that have a smaller number of files.  

	>  You must have access to the UNC path that has the application and any subfolders that contain application content.  

4.  On the **Import Information** page of the Create Application wizard, review the information that was imported, and then choose **Next**. If necessary, you can choose **Previous** to go back and fix any errors.  

5.  On the **General Information** page of the Create Application wizard, specify the following information:  

    > [!NOTE]  
    >  Some of this information might already be populated if it was automatically obtained from the application installation files. Additionally, the displayed options might be different depending on the application type that you create.  

    -   General information about the application, like the application name, comments, version, and an optional reference to help you find the application in the Configuration Manager console.  

    -   **Installation program**--Specify the installation program and any required properties that are needed to install the application deployment type.  

        > [!TIP]  
        >  If the installation program does not appear, choose **Browse** and browse to the installation program location.  

    -   **Install behavior**--Specify whether the application deployment type will be installed for only the currently logged-on user or for all users. You can also specify that the deployment type will be installed for all users if it is deployed to a device, or only to a specific user if it is deployed to a user.  

    -   **Use an automatic VPN connection (if configured)**--If a VPN profile has been deployed to the device on which the app is launched, launch the VPN connection when the app starts (Windows 8.1 and Windows Phone 8.1 only).  

         On Windows Phone 8.1 devices, automatic VPN connections are not supported if more than one VPN profile has been deployed to the device.  

         For more about VPN profiles, see [VPN profiles](../../protect/deploy-use/vpn-profiles.md).  

6.  Choose **Next**, review the application information on the **Summary** page, and then finish the Create Application wizard.  

The new application appears in the **Applications** node of the Configuration Manager console, and you have finished creating an application. If you want to add more deployment types to the application, see [Create deployment types for the application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in this topic.  

### Manually specify application information  

1.  On the **General** page of the Create Application wizard, select **Manually specify the application information**, and then choose **Next**.  

2.  Specify general information about the application, like the application name, comments, version, and an optional reference to help you find the application in the Configuration Manager console.  

3.  On the **Application Catalog** page of the Create Application wizard, specify the following information:  

    -   **Selected language**--In the drop-down list, select the language version of the application that you want to set up. Choose **Add/Remove** to set up more languages for this application.  

    -   **Localized application name**--Specify the application name in the language that you selected in the **Selected language** drop-down list.  

        > [!IMPORTANT]  
        >  You must specify a localized application name for each language version that you set up.  

    -   **User categories**--Choose **Edit** to specify application categories in the language that you selected in the **Selected Language** drop-down list. Users of Software Center can use these selected categories to help filter and sort the available applications.  

    -   **User documentation**--Choose **Browse** to specify the URL to, or the UNC path and file name of, a file that users of Software Center can read to get more information about this application.  

    -   **Link text**--Specify the text that will appear in place of the URL to the application.  

    -   **Application Privacy URL**--Specify a URL that links to the privacy statement for the application.  

    -   **Localized description**--Enter a description for this application in the language that you selected in the **Selected Language** drop-down list.  

    -   **Keywords**--Enter a list of keywords in the language that you selected in the **Selected Language** drop-down list. These keywords will help users of Software Center search for the application.  

    -   **Icon**--Choose **Browse** to select an icon for this application from the available icons. If you do not specify an icon, a default icon will be used for this application.  

    -   **Display this as a featured app and highlight it in the company portal**--Select this option to display the app prominently in the company portal.  

4.  On the **Deployment Types** page of the Create Application wizard, choose **Add** to create a new deployment type.  

 For more information, see [Create deployment types for the application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Choose **Next**, review the application information on the **Summary** page, and then finish the Create Application wizard.  

The new application appears in the **Applications** node of the Configuration Manager console.  

##  Create deployment types for the application  
 If you select **Automatically identify information about this deployment type from installation files** on the **General** page of the Create Deployment Type wizard, you might not need to finish some of the steps in the following procedures.  

## Start the create deployment type wizard  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  Select an application, and then on the **Home** tab, in the **Application** group, choose **Create Deployment Type**.  

> [!TIP]  
>  You can also start the Create Deployment Type wizard from the Create Application wizard and from the **Deployment Types** tab of the *<application name\>* **Properties** dialog box.  

## Specify whether you want to automatically detect deployment type information or manually set up the information  
 Use one of the following procedures to automatically detect or manually set up deployment type information.  

### Automatically detect deployment type information  

1.  On the **General** page of the Create Deployment Type wizard, select **Automatically identify information about this deployment type from installation files**.  

2.  In the **Type** box, select the application installation file type that you want to use to detect the deployment type information.  

3.  In the **Location** box, specify the UNC path (in the form *\\\\server\\share\\filename*) or specify the store link to the application installation files and the content that you want to use to detect the deployment type information. You can also choose **Browse** to locate the installation file.  

    > [!NOTE]  
    >  You must have access to the UNC path that has the application and any subfolders that contain the application content.  

4.  On the **Import Information** page of the Create Deployment Type wizard, review the information that was imported, and then choose **Next**. You can also choose **Previous** to go back and fix any errors.  

5.  On the **General Information** page of the Create Deployment Type wizard, specify the following information:  

    > [!NOTE]  
    >  Some of the deployment type information might already be present if it was read from the application installation files. Additionally, the displayed options might differ, depending on the deployment type that you are creating.  

    -   General information about the deployment type, like the name, admin comments, and available languages.  

    -   **Installation program**--Specify the installation program and any properties that you require to install the deployment type.  

    -   **Install behavior**-- Specify whether to install the deployment type for the current user or for all users. You can also specify whether to install the deployment type for all users if it is deployed to a device, or whether to install the deployment type to a user only if it is deployed to a user.  

    -   **Use an automatic VPN connection (if configured)**--If a VPN profile has been deployed to the device on which the app is launched, launch the VPN connection when the app starts (Windows 8.1 and Windows Phone 8.1 only). If multiple VPN profiles have been deployed to a Windows 8.1 device, the first deployed VPN profile is used by default.  

         On Windows Phone 8.1 devices, automatic VPN connections are not supported if more than one VPN profile has been deployed to the device.  

         For more about VPN profiles, see [VPN profiles in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

6.  Choose **Next**, and then continue to [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

### Manually set up the deployment type information  

1.  On the **General** page of the Create Deployment Type wizard, select **Manually specify the deployment type information**.  

2.  In the **Type** box, choose the application installation file type that you want to use to detect the deployment type information. You can choose the same installation types that you would use when you automatically detect the deployment type information, and you can also specify a script to install the deployment type.  

3.  On the **General Information** page of the Create Deployment Type wizard, specify a name for the deployment type, an optional description, and the languages in which you want to make this deployment type available, and then choose **Next**.  

4.  Continue to [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

##  Specify content options for the deployment type  

1.  On the **Content** page of the Create Deployment Type wizard, specify the following information:  

    -   **Content location**--Specify the location of the content for this deployment type, or select **Browse** to choose the deployment type content folder.  

        > [!IMPORTANT]  
        >  The System account of the site server computer must have permissions to the content location that you specify.  

    -   **Uninstall content settings**--Specify one of the following options:
        - **Same as install content**--Select this option if the install and uninstall content are the same. This is the default behavior.
        - **No uninstall content**--Select this option if your application does not need content for uninstall.
        - **Different from install content**--Select this option if the uninstall content is different from the install content.

4. If you selected **Different from install content**, browse to, or enter the location of the application content that is used to uninstall the application.
5. Click **OK** to close the deployment type properties dialog box.

    -   **Persist content in the client cache**--Select this option to specify whether the content should be retained in the cache on the client computer indefinitely, even if it has already been run. Although this option can be useful with some deployments, like Windows Installer–based software that requires a local source copy to be available for applying updates, it will reduce the available cache space. If you select this option, it might cause a large deployment to fail at a later point if the cache does not have sufficient available space.  

    -   **Allow clients to share content with other clients on the same subnet**--Select this option to reduce load on the network by allowing clients to download content from other local clients on the network that have already downloaded and cached the content. This option utilizes Windows BranchCache technology.  

    -   **Installation program**--Specify the name of the installation program and any required installation parameters, or choose **Browse** to locate the installation file.  

    -   **Installation start in**--Optionally, specify the folder that has the installation program for the deployment type. This folder can be an absolute path on the client or a path to the distribution point folder that has the installation files.  

    -   **Uninstall program**--Optionally, specify the name of the uninstall program and any required parameters, or choose **Browse** to locate it.  

    -   **Uninstall start in**--Optionally, specify the folder that has the uninstall program for the deployment type. This folder can be an absolute path on the client or a path that is relative to the distribution point folder that has the package.  

    -   **Run installation and uninstall program as 32-bit process on 64-bit clients**--Use the 32-bit file and registry locations on Windows-based computers to run the installation program for the deployment type.  

2.  Choose **Next**.  

## Set up detection methods to indicate the presence of the deployment type (Windows PCs only)  
 This procedure sets up  a detection method that indicates whether the deployment type is already installed.  

1.  On the **Detection Method** page of the Create Deployment Type wizard, select **Configure rules to detect the presence of this deployment type**, and then choose **Add Clause**.  

    > [!NOTE]  
    >  You can also select **Use a custom script to detect the presence of this deployment type**. For more information, see [Use a custom script to check for the presence of a deployment type](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  In the **Detection Rule** dialog box, in the **Setting type** drop-down list, select the method that you want to use to detect the presence of the deployment type. You can choose from the following available methods:  

    -   **File System**--Use this method to detect whether a specified file or folder exists on a client device, thus indicating that the application is installed.  

        > [!NOTE]  
        >  The **File system** setting type does not support specifying a UNC path to a network share in the Path field. You can only specify a local path on the client device.  
        >   
        >  To check 32-bit file locations for the specified file or folder, select the option **This file or folder is associated with a 32-bit application on 64-bit systems** first. If the file or folder is not found, 64-bit locations will be searched.  

    -   **Registry**--Use this method to detect whether a specified registry key or registry value exists on a client device, thus indicating that the application is installed.  

        > [!NOTE]  
        >  To check 32-bit registry locations for the specified registry key, select the option **This registry key is associated with a 32-bit application on 64-bit systems** first. If the registry key is not found, 64-bit locations will be searched.  

    -   **Windows Installer**--Use this method to detect whether a specified Windows Installer file exists on a client device, thus indicating that the application is installed.  

3.  Specify details about the item that you want to use to detect whether this deployment type is installed. For example, you can use a file, folder, registry key, registry value, or a Windows Installer product code.  

4.  Specify details about the value that you want to assess against the item that you use to detect whether the deployment type is installed. For example, if you use a file to check whether the deployment type is installed, you can select **The file system setting must exist on the target system to indicate presence of this application**.  

5.  Choose **Next** to close the **Detection Rule** dialog box.  

###  Use a custom script to check for the presence of a deployment type  

1.  On the **Detection Method** page of the Create Deployment Type wizard, select the **Use a custom script to detect the presence of this deployment type** box, and then choose **Edit**.  

2.  In the **Script Editor** dialog box, in the **Script type** drop-down list, select the script language that you want to use to detect the deployment type.  

3.  In the **Script contents** box, enter the script that you want to use. You can also paste the contents of an existing script in this field, or choose **Open** to browse to an existing saved script. Configuration Manager checks the results from the script by reading the values that are written to the Standard Out (STDOUT) output stream, the Standard Error (STDERR) output stream, and the exit code from the script. If the exit code is a nonzero value, the script has failed and the application detection status is unknown. If the exit code is zero and STDOUT has data, the application detection status is Installed.  

 Use the following table to see how to use the output from a script to check whether an application is installed.  

|Script exit code|Details|
|--------------------------------|-----------------|
|0|**Data read from STDOUT**--Empty<br /><br /> **Data read from STDERR**--Empty<br /><br /> **Script result**--Success<br /><br /> **Application detection state**--Not installed|  
|0|**Data read from STDOUT**--Empty<br /><br /> **Data read from STDERR**--Not empty<br /><br /> **Script result**--Failure<br /><br /> **Application detection state**--Unknown|  
|0|**Data read from STDOUT**--Not empty<br /><br /> **Data read from STDERR**--Empty<br /><br /> **Script result**--Success<br /><br /> **Application detection state**--Installed|  
|0|**Data read from STDOUT**--Not empty<br /><br /> **Data read from STDERR**--Not empty<br /><br /> **Script result**--Success<br /><br /> **Application detection state**--Installed|  
|Non-zero value|**Data read from STDOUT**--Empty<br /><br /> **Data read from STDERR**--Empty<br /><br /> **Script result**--Failure<br /><br /> **Application detection state**--Unknown|  
|Non-zero value|**Data read from STDOUT**--Empty<br /><br /> **Data read from STDERR**--Not empty<br /><br /> **Script result**--Failure<br /><br /> **Application detection state**--Unknown|  
|Non-zero value|**Data read from STDOUT**--Not empty<br /><br /> **Data read from STDERR**--Empty<br /><br /> **Script result**--Failure<br /><br /> **Application detection state**--Unknown|  
|Non-zero value|**Data read from STDOUT**--Not empty<br /><br /> **Data read from STDERR**--Not empty<br /><br /> **Script result**--Failure<br /><br /> **Application detection state**--Unknown|  

The following table has Microsoft Visual Basic (VB) sample scripts that you can use to write your own application detection scripts.  

|Visual Basic sample script|Description|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|The script returns an exit code that is not zero, which indicates that it failed to run successfully. In this case, the application detection state is unknown.|  
|**WScript.StdErr.Write "Script failed"**<br /><br /> **WScript.Quit(0)**|The script returns an exit code of zero, but the value of STDERR is not empty, which indicates that the script failed to run successfully. In this case, the application detection state is unknown.|  
|**WScript.Quit(0)**|The script returns an exit code of zero, which indicates that it ran successfully. However, the value for STDOUT is empty, which indicates that the application is not installed.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.Quit(0)**|The script returns an exit code of zero, which indicates that it ran successfully. The value for STDOUT is not empty, which indicates that the application is installed.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.StdErr.Write "Completed"**<br /><br /> **WScript.Quit(0)**|The script returns an exit code of zero, which indicates that it ran successfully. The values for STDOUT and STDERR are not empty, which indicates that the application is installed.|  

 > [!NOTE]  
 >  The maximum size that you can use for a script is 32 kilobytes (KB).  

4.  Choose **OK** to close the **Script Editor** dialog box.  

## Specify user experience options for the deployment type  
 These settings specify how the application will be installed on devices and what the user will see.  

1.  On the **User Experience** page of the Create Deployment Type wizard, specify the following information:  

    -   **Installation behavior**--In the drop-down list, select one of the following options:  

        -   **Install for User**--The application is installed only for the user to whom the application is deployed.  

        -   **Install for System**--The application is installed only once, and it is available to all users.  

        -   **Install for System if resource is device; otherwise install as user**--If the application is deployed to a device, it will be installed for all users. If the application is deployed to a user, it will be installed for only that user.  

    -   **Logon requirement**--Specify the logon requirements for this deployment type from the following options:  

        -   **Only when a user is logged on**  

        -   **Whether or not a user is logged on**  

        -   **Only when no user is logged on**  

        > [!NOTE]  
        >  This option defaults to **Only when a user is logged on**, and it cannot be changed if you selected **Install for user** in the **Installation behavior** drop-down list.  

    -   **Installation program visibility**--Specify the mode in which the deployment type will run on client devices. The following options are available:  

        -   **Maximized**--The deployment type runs maximized on client devices. Users will see all installation activity.  

        -   **Normal**--The deployment type runs in the normal mode based on system and program defaults. This is the default mode.  

        -   **Minimized**--The deployment type runs minimized on client devices. Users might see the installation activity in the notification area or taskbar.  

        -   **Hidden**--The deployment type runs hidden on client devices, and users will see no installation activity.  

    -   **Allow users to view and interact with the program installation**--Specify whether a user can interact with the deployment type installation to set up the installation options.  

        > [!NOTE]  
        >  This option is enabled by default if you selected the **Install for user** option in the **Installation behavior** drop-down list.  

    -   **Maximum allowed run time (minutes)**--Specify the maximum time that the program is expected to run on the client computer. You can specify this setting as a whole number greater than zero. The default setting is 120 minutes.  

         This value is used to:  

        -   Monitor the results from the deployment type.  

        -   Check whether a deployment type will be installed when maintenance windows are defined on client devices. When a maintenance window is in place, a program will start only if enough time is available in the maintenance window to accommodate the **Maximum Allowed Run Time** setting.  

        > [!IMPORTANT]  
        >  A conflict might occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If the user sets the maximum run time to a period that exceeds the length of any available maintenance window, that deployment type will not be run.  

2.  **Estimated installation time (minutes)**--Specify the estimated time that installation of the deployment type will take. This is displayed to users of Software Center.  

## Specify requirements for the deployment type  

1.  On the **Requirements** page of the Create Deployment Type wizard, choose **Add** to open the **Create Requirement** dialog box, and add a new requirement.  

    > [!NOTE]  
    >  You can also add new requirements on the **Requirements** tab of the *<deployment type name\>* **Properties** dialog box.  

2.  In the **Category** drop-down list, select whether this requirement is for a device or a user, or select **Custom** to use a previously created global condition. When you select **Custom**, you can also choose **Create** to create a new global condition. For more about global conditions, see [How to create global conditions](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Any requirement of the category **User** and the condition **Primary Device** will be ignored if you deploy the application to a device collection.  
    >   
    >  If you created a Windows package and program or task sequence that has Windows 10 as a requirement using System Center 2012 R2 Configuration Manager SP1 and then upgrade to System Center Configuration Manager, the requirements for Windows 10 might be removed. To fix this problem, specify the requirements again. Note that although the requirement has been removed from the requirements display, it is still processed correctly on devices.  

3.  In the **Condition** drop-down list, select the condition that you want to use to assess whether the user or device meets the installation requirements. The contents of this list will vary depending on the selected category.  

4.  In the **Operator** drop-down list, select the operator that will be used to compare the selected condition to the specified value to assess whether the user or device meets the installation requirements. The available operators will vary depending on the selected condition.  

    > [!IMPORTANT]  
    >  The available requirements will differ depending on the device type that the deployment type uses.  

5.  In the **Value** box, specify the values that will be used with the selected condition and operator to evaluate whether the user or device meets the installation requirements. The available values will vary depending on the selected condition and the selected operator.  

6.  Choose **OK** to save the requirement and close the **Create Requirement** dialog box.  

## Specify dependencies for the deployment type  
 Dependencies define one or more deployment types from another application that must be installed before a deployment type is installed. You can set up the dependent deployment types to be installed automatically before a deployment type is installed.  

> [!IMPORTANT]  
>  In some cases, a deployment type is dependent on a deployment type that also has dependencies. The maximum number of supported dependencies in the chain is five.  

1.  On the **Dependencies** page of the Create Deployment Type wizard, choose **Add** if you want to specify the deployment types that must be installed before this deployment type can be installed.  

    > [!IMPORTANT]  
    >  You can also add new dependencies on the **Dependencies** tab of the *<deployment type name\>* **Properties** dialog box.  

2.  In the **Add Dependency** dialog box, choose **Add**.  

3.  In the **Specify Required Application** dialog box, select an existing application and one of the application deployment types to use as a dependency.  

    > [!TIP]  
    >  You can choose **View** to display the properties of the selected application or deployment type.  

4.  Choose **OK** to close the **Specify Required Application** dialog box.  

5.  If you want a dependent application to be automatically installed, select **Auto Install** next to the dependent application.  

    > [!NOTE]  
    >  A dependent application does not need to be deployed to be automatically installed.  

6.  In the **Add Dependency** dialog box under **Dependency group name**, enter a name to refer to this group of application dependencies.  

7.  Optionally, use the **Increase Priority** and **Decrease Priority** buttons to change the order in which each dependency is evaluated.  

8.  Choose **OK** to close the **Add Dependency** dialog box.  

## Confirm the deployment type settings and finish the wizard  

1.  On the **Summary** page of the Create Deployment Type wizard, review the actions that the wizard will take. Choose **Next** to create the deployment type, or choose **Previous** to go back and change the settings for the deployment type.  

2.  After the **Progress** page finishes, review the actions that the wizard took, and then choose **Close** to finish the wizard.  

3.  If you started the Create Deployment Type wizard from the Create Application wizard, you will return to the **Deployment Types** page of the Create Application wizard.  

## Set up additional options for deployment types that contain virtual applications  
 Use the following procedures to set up additional options for deployment types that contain virtual applications.  

### Set up content options for Application Virtualization (App-V) deployment types  

1.  In the Configuration Manager console, choose **Software Library** > **Applications**.  

2.  In the **Applications** list, select an application that has an App-V deployment type. Then, on the **Home** tab, in the **Properties** group, choose **Properties**.  

3.  In the *<Application Name\>* **Properties** dialog box, on the **Deployment Types** tab, select an App-V deployment type, and then choose **Edit**.  

4.  In the *<Deployment Type Name\>* **Properties** dialog box, on the **Content** tab, set up the following options if required:  

    -   **Persist content in the client cache**--Select this option to ensure that the content for this deployment type is not deleted from the Configuration Manager client cache.  

    -   **Load content into App-V cache before launch**--Select this option to ensure that all content for the virtual application is loaded into the App-V cache before the application starts. Selection of this option also ensures that the application content is not pinned in the cache and can be deleted as required.  

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

4.  On the **General** page of the **Import Application wizard**, choose **Browse**, and then specify a UNC path to the .zip file that has the application you want to import.  

5.  On the **File Content** page, select the action that will be taken if the application that you are trying to import is a duplicate of an existing application. You can create a new application or ignore the duplicate and add a new revision to the existing application.  

6.  On the **Summary** page, review the actions to be taken, and then finish the wizard.  

 The new application appears in the **Applications** node.  

> [!TIP]  
>  The Windows PowerShell cmdlet **Import-CMApplication** has the same function as this procedure. For more information, see [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) in Microsoft System Center 2012 Configuration Manager SP1 Cmdlet Reference.  

##  Deployment types supported by Configuration Manager  

|Deployment type name|More information|  
|--------------------------|----------------------|  
|**Windows Installer (\*.msi file)**|Creates a deployment type from a Windows Installer file.|  
|**Windows app package (\*.appx, \*.appxbundle)**|Creates a deployment type for the Windows 8, Windows RT, or later from a Windows app package file or Windows app bundle package.|  
|**Windows app package (in the Windows Store)**|Creates a deployment type for Windows 8, Windows RT, or later by specifying a link to the app in the Windows Store or by browsing the store to select the app you require.<br /><br /> If you want to deploy the app as a link to the Windows Store, make sure that the Group Policy setting **Turn off the Store application** is set to **Disabled** or **Not configured**. If this setting is enabled, clients will not be able to connect to the Windows Store to download and install applications.<br /><br /> Windows 8 deployment types that use a link to a store are always evaluated before other deployment types, irrespective of their priority.|  
|**Script Installer**|Creates a deployment type that specifies a script that runs on client devices to install content or to do an action.|  
|**Microsoft Application Virtualization 4**|Creates a deployment type from a Microsoft Application Virtualization 4 manifest|  
|**Microsoft Application Virtualization 5**|Creates a deployment type from a Microsoft Application Virtualization 5 package file.|  
|**Windows Phone app package (\*.xap file)**|Creates a deployment type from a Windows Phone app package file.|  
|**Windows Phone app package (in the Windows Phone Store)**|Creates a deployment type by specifying a link to the app in the Windows Phone store.|  
|**Windows Mobile Cabinet**|Creates a deployment type for Windows Mobile devices from a Windows Mobile Cabinet (CAB) file.|  
|**App Package for iOS (\*.ipa file)**|Creates a deployment type from an iOS app package file.|  
|**App Package for iOS from App Store**|Creates a deployment type by specifying a link to the iOS app in the App Store.|  
|**App Package for Android (\*.apk file)**|Creates a deployment type from an Android app package file.|  
|**App Package for Android on Google Play**|Creates a deployment type by specifying a link to the app on Google Play.|  
|**Mac OS X**|Creates a deployment type for Mac computers from a .cmmac file that you have created by using the CMAppUtil tool.<br /><br /> Applies  only to Mac computers running the Configuration Manager client.|  
|**Web Application**|Creates a deployment type that specifies a link to a web application. The deployment type installs a shortcut to the web application on the user’s device.<br /><br /> If you have installed the Intune managed browser on iOS or Android devices that you manage, you can ensure that users can only use the managed browser to open the app. To do this, use one of the following formats when you specify a link to the app by replacing **http:** with **http-intunemam:** or **https:** with **https-intunemam:**<br /><br /> - **http-intunemam://<path to web app\>**<br /><br /> - **https-intunemam://<path to web app\>**<br /><br /> You can use Configuration Manager application requirements to ensure that apps you want to associate with the managed browser are only installed to iOS and Android devices.<br /><br /> For more about the Intune managed browser, see [Manage Internet access using managed browser policies](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer through MDM (\*.msi)**|This installer type lets you create and deploy Windows Installer-based apps to PCs that run Windows 10.<br /><br /> The following considerations apply when you use this installer type:<br><br>- You can only upload a single file with the extension .msi.<br /><br /> - The file's product code and product version are used for app detection.<br /><br /> - The default restart behavior of the app will be used. Configuration Manager does not control this.<br /><br /> - Per-user MSI packages will be installed for a single user.<br /><br /> - Per-machine MSI packages will be installed for all users on the device.<br /><br /> - Dual-mode MSI packages currently only install for all users on the device.<br /><br /> - App updates are supported when the MSI product code of each version is the same.|  
