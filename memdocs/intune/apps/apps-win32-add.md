---
title: Add and assign Win32 apps to Microsoft Intune
titleSuffix:
description: Learn how to add, assign, and manage Win32 apps with Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add, assign, and monitor a Win32 app in Microsoft Intune

After you have [prepared a Win32 app to be upload to Intune](apps-win32-prepare.md) using the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730), you can add the app to Intune. To learn more about preparing a Win32 app to be uploaded, see [Prepare Win32 app content for upload](apps-win32-prepare.md).

## Prerequisites

To use Win32 app management, be sure you meet the following criteria:

- Windows 10 version 1607 or later (Enterprise, Pro, and Education versions)
- Windows 10 client needs to be: 
  - Devices must be joined to Azure AD and auto-enrolled. The Intune management extension supports Azure AD joined, hybrid domain joined, group policy enrolled devices are supported. 
  > [!NOTE]
  > For the group policy enrolled scenario - The end user uses the local user account to AAD join their Windows 10 device. The user must log onto the device using their AAD user account and enroll into Intune. Intune will install the Intune Management extension on the device if a PowerShell script or a Win32 app is targeted to the user or device.
- Windows application size is capped at 8 GB per app.

Much like a standard line-of-business (LOB) app, you can add a Win32 app to Microsoft Intune. This type of app is typically written in-house or by a 3rd party. 

## Process flow to add a Win32 app to Intune

<img alt="Process flow to add a Win32 app to Intune" src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## Add a Win32 app to Intune

The following steps provide guidance to help you add a Windows app to Intune.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **Windows app (Win32)**.

    > [!IMPORTANT]
    > Be sure to use the latest version of the Microsoft Win32 Content Prep Tool. If you don't use the latest version, you will see a warning indicating that the app was packaged using an older version of the Microsoft Win32 Content Prep Tool. 

4. Click **Select**. The **Add app** steps are displayed.

## Step 1: App information

### Select the app package file

1. In the **Add app** pane, click **Select app package file**. 
2. In the **App package file** pane, select the browse button. Then, select a Windows installation file with the extension *.intunewin*.
   The app details will be displayed.
3. When you're finished, select **OK** on the **App package file** pane.

### Set app information

1. In the **App information** page, add the details for your app. Depending on the app that you chose, some of the values in this pane might be automatically filled in.
    - **Name**: Enter the name of the app as it appears in the company portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.
    - **Description**: Enter the description of the app. The description appears in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Category**: Select one or more of the built-in app categories, or select a category that you created. Categories make it easier for users to find the app when they browse through the company portal.
    - **Show this as a featured app in the Company Portal**: Display the app prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL appears in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL appears in the company portal.
    - **Developer**: Optionally, enter the name of the app developer.
    - **Owner**: Optionally, enter a name for the owner of this app. An example is **HR department**.
    - **Notes**: Enter any notes that you want to associate with this app.
    - **Logo**: Upload an icon that is associated with the app. This icon is displayed with the app when users browse through the company portal.
2. Click **Next** to display the **Program** page.

## Step 2: Program

1. In the **Program** page, configure the app installation and removal commands for the app:
    - **Install command**: Add the complete installation command line to install the app. 

        For example, if your app filename is **MyApp123**, add the following:<br>
        `msiexec /p "MyApp123.msp"`<p>
        And, if the application is `ApplicationName.exe`, the command would be the application name followed by the command arguments (switches) supported by the package. <br>
        For example:<br>
        `ApplicationName.exe /quiet`<br>
        In the above command, the `ApplicationName.exe` package supports the `/quiet` command argument.<p> 
        For the specific arguments supported by the application package, contact your application vendor.

        > [!IMPORTANT]
        > Admins must be careful when they utilize the command tools. Unexpected or harmful commands may be passed using the the install and uninstall command field.

    - **Uninstall command**: Add the complete uninstall command line to uninstall the app based on the app's GUID. 

        For example:<br>
        `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

    - **Install behavior**: Set the install behavior to either **System** or **User**.

        > [!NOTE]
        > You can configure a Win32 app to be installed in **User** or **System** context. **User** context refers to only a given user. **System** context refers to all users of a Windows 10 device.
        >
        > End users are not required to be logged in on the device to install Win32 apps.
        > 
        > The Win32 app install and uninstall will be executed under admin privilege (by default) when the app is set to install in user context and the end user on the device has admin privileges.
    
    - **Device restart behavior**: Select one of the following options:
        - **Determine behavior based on return codes**: Choose this option to restart the device based on the return codes.
        - **No specific action**: Choose this option to suppress device restarts during the app installation of MSI-based apps.
        - **App install may force a device restart**: Choose this option to allow the app installation to complete without suppressing restarts.
        - **Intune will force a mandatory device restart**: Choose this option to always restart the device after a successful app installation.

    - **Specify return codes to indicate post-installation behavior**: Add the return codes used to specify either app installation retry behavior or post-installation behavior. Return code entries are added by default during app creation. However, you can add additional return codes or change existing return codes.
        1. In the **Code type** column, set the **Code type** to one of the following:
            - **Failed** – The return value that indicates an app installation failure.
            - **Hard reboot** – The hard reboot return code does not allow next  Win32 apps to be installed on the client without reboot. 
            - **Soft reboot** – The soft reboot return code allows the next Win32 app to be installed without requiring a client reboot. Reboot is necessary to complete installation of the current application.
            - **Retry** – The retry return code agent will attempt to install the app three times. It will wait for 5 minutes between each attempt. 
            - **Success** – The return value that indicates the app was successfully installed.
        2. If needed, click **Add** to add additional return codes, or modify existing return codes.
2. Click **Next** to display the **Requirements** page.        

## Step 3: Requirements

1. In the **Requirements** page, specify the requirements that devices must meet before the app is installed:
    - **Operating system architecture**: Choose the architectures need to install the app.
    - **Minimum operating system**: Select the minimum operating system needed to install the app.
    - **Disk space required (MB)**: Optionally, add the free disk space needed on the system drive to install the app.
    - **Physical memory required (MB)**: Optionally, add the physical memory (RAM) required to install the app.
    - **Minimum number of logical processors required**: Optionally, add the minimum number of logical processors required to install the app.
    - **Minimum CPU speed required (MHz)**: Optionally, add the minimum CPU speed required to install the app.
    - **Configure additional requirement rules**: 
        1. Click **Add** to display the **Add a Requirement rule** pane and configure additional requirement rules. Select the **Requirement type** to choose the type of rule that you will use to determine how a requirement is validated. Requirement rules can be based on file system information, registry values, or PowerShell scripts. 
            - **File**: When you choose **File** as the **Requirement type**, the requirement rule must detect a file or folder, date, version, or size. 
                - **Path** – The full path of the folder containing the file or folder to detect.
                - **File or folder** - The file or folder to detect.
                - **Property** – Select the type of rule used to validate the presence of the app.
                - **Associated with a 32-bit app on 64-bit clients** - Select **Yes** to expand any path environment variables in the 32-bit context on 64-bit clients. Select **No** (default) to expand any path variables in the 64-bit context on 64-bit clients. 32-bit clients will always use the 32-bit context.
            - **Registry**: When you choose **Registry** as the **Requirement type**, the requirement rule must detect a registry setting based on value, string, integer, or version.
                - **Key path** – The full path of the registry entry containing the value to detect.
                - **Value name** - The name of the registry value to detect. If this value is empty, the detection will happen on the key. The (default) value of a key will be used as detection value if the detection method is other than file or folder existence.
                - **Registry key requirement** – Select the type of registry key comparison used to determine how the requirement rule is validated.
                - **Associated with a 32-bit app on 64-bit clients** - Select **Yes** to search the 32-bit registry on 64-bit clients. Select **No** (default) search the 64-bit registry on 64-bit clients. 32-bit clients will always search the 32-bit registry.
            - **Script**: Choose **Script** as the **Requirement type**, when you cannot create a requirement rule based on file, registry, or any other method available to you in the Intune console.
                - **Script file** – For PowerShell script based requirement rule, if exist code is 0, we will detect the STDOUT in more detail. For example, we can detect STDOUT as an integer that has a value of 1.
                - **Run script as 32-bit process on 64-bit clients** - Select **Yes** to run the script in a 32-bit process on 64-bit clients. Select **No** (default) to run the script in a 64-bit process on 64-bit clients. 32-bit clients run the script in a 32-bit process.
                - **Run this script using the logged on credentials**: Select **Yes** to run the script using the signed in device credentials**.
                - **Enforce script signature check** - Select **Yes** to verify that the script is signed by a trusted publisher, which will allow the script to run with no warnings or prompts displayed. The script will run unblocked. Select **No** (default) to run the script with end-user confirmation without signature verification.
                - **Select output data type**: Select the data type used when determining a requirement rule match.
        2. When you're finished setting the requirement rules, select **OK**.
2. Click **Next** to display the **Detection rules** page.   

## Step 4: Detection rules

1. In the **Detection rules** page, configure the rules to detect the presence of the app:
    
    **Rules format**: Select how the presence of the app will be detected. You can choose to either manually configure the detection rules or use a custom script to detect the presence of the app. You must choose at least one detection rule. 

    > [!NOTE]
    > In the **Detection rules** pane, you can choose to add multiple rules. The conditions for **all** rules must be met to detect the app.
    >
    > If Intune detects that the app is not present on the device, Intune will offer the app again after 24 hours. This will only occur for apps targeted with required intent.

    - **Manually configure detection rules** - You can select one of the following rule types:
        1. **MSI** – Verify based on MSI version check. This option can only be added once. When you choose this rule type, you have two settings:
            - **MSI product code** – Add a valid MSI product code for the app.
            - **MSI product version check** – Select **Yes** to verify the MSI product version in addition to the MSI product code.
        2. **File** – Verify based on file or folder detection, date, version, or size.
            - **Path** – The full path of the folder containing the file or folder to detect.
            - **File or folder** - The file or folder to detect.
            - **Detection method** – Select the type of detection method used to validate the presence of the app.
            - **Associated with a 32-bit app on 64-bit clients** - Select **Yes** to expand any path environment variables in the 32-bit context on 64-bit clients. Select **No** (default) to expand any path variables in the 64-bit context on 64-bit clients. 32-bit clients will always use the 32-bit context.
            
            **Examples of file-based detection**
            1. Check for file existence.
         
                ![Screenshot of detection rule pane - file existence](./media/apps-win32-app-management/apps-win32-app-03.png)
        
            2. Check for folder existence.
         
                ![Screenshot of detection rule pane - folder existence](./media/apps-win32-app-management/apps-win32-app-04.png)
        
        3. **Registry** – Verify based on value, string, integer, or version.
            - **Key path** – The full path of the registry entry containing the value to detect. A valid syntax is HKEY_LOCAL_MACHINE\Software\WinRAR or HKLM\Software\WinRAR.
            - **Value name** - The name of the registry value to detect. If this value is empty, the detection will happen on the key. The (default) value of a key will be used as detection value if the detection method is other than file or folder existence.
            - **Detection method** – Select the type of detection method used to validate the presence of the app.
            - **Associated with a 32-bit app on 64-bit clients** - Select **Yes** to search the 32-bit registry on 64-bit clients. Select **No** (default) search the 64-bit registry on 64-bit clients. 32-bit clients will always search the 32-bit registry.
            
            **Examples for registry-based detection**
            1. Check for registry key exists.
            
                ![Screenshot of detection rule pane - registry key exists](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
            2. Check if registry value exists.
        
                ![Screenshot of detection rule pane - registry value exists](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
            3. Check for registry value string equals.
        
                ![Screenshot of detection rule pane - registry value string equals](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
    - **Use a custom detection script** – Specify the PowerShell script that will be used to detect this app. 
    
       1. **Script file** – Select a PowerShell script that will detect the presence of the app on the client. The app will be detected when the script both returns a 0 value exit code and writes a string value to STDOUT.

       2. **Run script as 32-bit process on 64-bit clients** - Select **Yes** to run the script in a 32-bit process on 64-bit clients. Select **No** (default) to run the script in a 64-bit process on 64-bit clients. 32-bit clients run the script in a 32-bit process.

       3. **Enforce script signature check** - Select **Yes** to verify that the script is signed by a trusted publisher, which will allow the script to run with no warnings or prompts displayed. The script will run unblocked. Select **No** (default) to run the script with end-user confirmation without signature verification.
    
            Intune agent checks the results from the script. It reads the values written by the script to the standard output (STDOUT) stream, the standard error (STDERR) stream, and the exit code. If the script exits with a nonzero value, the script fails and the application detection status is not installed. If the exit code is zero and STDOUT has data, the application detection status is Installed. 

            > [!NOTE]
            > Microsoft recommends encoding your script as UTF-8. When the script exits with the value of 0, the script execution was success. Second output channel indicates app was detected - STDOUT data indicates that the app was found on the client. We do not look for a particular string from STDOUT.

2. Once you have added your rule(s), select **Next** to display the **Dependencies** page.

## Step 5: Dependencies

App dependencies are applications that must be installed before your Win32 app can be installed. You can require that other apps are installed as dependencies. Specifically, the device must install the dependent app(s) before it installs the Win32 app. ​There is a maximum of 100 dependencies, which includes the dependencies of any included dependencies, as well as the app itself. You can add Win32 app dependencies only after your Win32 app has been added and uploaded to Intune. Once your Win32 app has been added, you'll see the **Dependencies** option on the pane for your Win32 app. 

Any Win32 app dependency needs to be also be a Win32 app. It does not support depending on other app types, such as single MSI LOB apps or Store apps.

When adding an app dependency, you can search based on the app name and publisher. Additionally, you can sort your added dependencies based on app name and publisher. Previously added app dependencies cannot be selected in the added app dependency list. 

You can choose whether or not to install each dependent app automatically. By default, the **Automatically install** option is set to **Yes** for each dependency. By automatically installing a dependent app, even if the dependent app is not targeted to the user or device, Intune will install the app on the device to satisfy the dependency before installing your Win32 app.​ It's important to note that a dependency can have recursive sub-dependencies, and each sub-dependency will be installed before installing the main dependency. Additionally, installation of dependencies does not follow an install order at a given dependency level.

### Select the dependencies

In the **Dependencies** page, select applications that must be installed before your Win32 app can be installed:
1. Click **Add** to display the **Add dependency** pane.
3. Once you have added the dependent app(s), click **Select**.
4. Choose whether to automatically install the dependent app by selecting **Yes** or **No** under the **Automatically Install** column.
5. Click **Next** to display the **Scope tags** page.

### Understand additional dependency details

The end user will see Windows Toast Notifications indicating that dependent apps are being downloaded and installed as part of the Win32 app installation process. Additionally, when a dependent app is not installed, the end user will commonly see one of the following notifications:
- 1 or more dependent apps failed to install​
- 1 or more dependent app requirements not met​
- 1 or more dependent apps are pending a device reboot

If you choose not to **Automatically install** a dependency, the Win32 app installation will not be attempted. Additionally, app reporting will show that the dependency was flagged as `failed` and also provide a failure reason. You can view the dependency installation failure by clicking on a failure (or warning) provided in the Win 32 app [installation details](troubleshoot-app-install.md#win32-app-installation-troubleshooting).​

Each dependency will adhere to Intune Win32 app retry logic (try to install 3 times after waiting for 5 minutes) and the global re-evaluation schedule.​ Also, dependencies are only applicable at the time of installing the Win32 app on the device. Dependencies are not applicable for uninstalling a Win32 app.​ To delete a dependency, you must click on the ellipses (three dots) to the left of the dependent app located at the end of the row of the dependency list.​ 

## Step 6: Select scope tags (optional)
You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

1. Click **Select scope tags** to optionally add scope tags for the app. 
2. Click **Next** to display the **Assignments** page.

## Step 7: Assignments

You can select the **Required**, **Available for enrolled devices**, or **Uninstall** group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md) and [Assign apps to groups with Microsoft Intune](apps-deploy.md).

1. For the specific app, select an assignment type:
    - **Required**: The app is installed on devices in the selected groups.
    - **Available for enrolled devices**: Users install the app from the Company Portal app or Company Portal website.
    - **Uninstall**: The app is uninstalled from devices in the selected groups.
2. Click **Add group** and assign the groups that will use this app.
3. In the **Select groups** pane, select to assign based on users or devices.
4. After you have selected your groups, you can also set **End user notifications**, **Availability**, and **Installation deadline**. For more information, see [Set Win32 app availability and notifications](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. If you want to exclude any groups of users from being affected by this app assignment, select **Included** under the **MODE** column. The **Edit assignment** pane will be displayed. You can set the **mode** from being **Included** to being **Excluded**. Click **OK** to close the **Edit assignment** pane.
6. In the **App settings** section, select the **Delivery optimization priority** for the app. This setting will determine how the app content will be downloaded. You can choose to download the app content in background mode or foreground mode based on assignment. 
7. Once you have completed setting the assignments for the apps, click **Next** to display the **Review + create** page.

## Step 8: Review and create

1. Review the values and settings you entered for the app. Verify that you configured the app information correctly.
2. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade for the line-of-business app is displayed.

At this point, you have completed steps to add a Win32 app to Intune. For information about app assignment and monitoring, see [Assign apps to groups with Microsoft Intune](apps-deploy.md) and [Monitor app information and assignments with Microsoft Intune](apps-monitor.md).

## Next steps

- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
