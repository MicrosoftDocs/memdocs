---
title: "Capabilities in Technical Preview 1605"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1605."
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Capabilities in Technical Preview 1605 for System Center Configuration Manager*Applies to: System Center Configuration Manager (Technical Preview)*
This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1605. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.  

 **Known Issues in this Technical Preview:**  

-   With Technical Preview 1605, if you update the properties of a management point after it is installed, you might see a console error which forces the console to close.  If this happens, you can uninstall the management point and then reinstall the management point using the desired settings. Alternately, you  can modify the management point prior to installing  Technical Preview 1605.  

-   When you use the Windows Store for Business feature with the Technical Preview 1604 and then upgrade to Technical Preview 1605, you can no longer view  the onboarding data. All other functionally continues to work. If you onboarded with the Technical Preview 1604, you remain onboarded after you install Technical Preview 1605 and need take no further action.  

 **The following are new features you can try out with this version.**  

##  <a name="BKMK_PerAppVPN"></a> Per-app VPN for Windows 10 devices  
 For Windows 10 devices managed using Configuration Manager with Intune, you can add a list of apps that automatically open a VPN connection that you have configured through the Configuration Manager admin console. You have the option of restricting VPN traffic to those apps, or you can continue to allow all traffic through the VPN connection.  

 **Requirements**:  

-   Configuration Manager with Intune  

-   A Windows 10 VPN profile that has been deployed to at least one device  

##  <a name="BKMK_InstallSU"></a> Improvements to the Install software updates task sequence  
 The following improvements have been made to the Install Software Updates task sequence:  

-   A new task sequence variable, SMSTSSoftwareUpdateScanTimeout, is available to give you the ability to control the timeout on the software updates scan during the Install software updates task sequence step. The default value is 30 minutes.  

-   There have been improvements to logging. The smsts.log log file will contain new log entries that reference other log files that will help you to troubleshoot issues during the software updates installation process.  

##  <a name="BKMK_PrepareConfigMgrClient"></a> Improvements to the Prepare ConfigMgr Client for Capture task sequence step  
 The Prepare ConfigMgr Client step will now completely remove the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured operating system image it will install a new Configuration Manager client each time.  

##  <a name="BKMK_Grace"></a> Grace period for required application deployments  
 In some cases, you might want give users more time to install required application deployments beyond any deadlines you configured. For example, if an end user has just returned from vacation, they might have to wait for a long while as overdue application deployments are installed. However, they can still immediately install the application at any time they want.  

 To help solve this problem, you can now define a **grace period** by deploying Configuration Manager client settings to a collection.  

 To configure the grace period, take the following actions:  

1.  On the **Computer Agent** page of client settings, configure the new property **Grace period for enforcement after deployment deadline (hours)** with a value between **1** and **120** hours.  

2.  In a new application deployment, or in the properties of an existing deployment, on the **Scheduling** page, select the checkbox **Delay enforcement of this deployment according to user preferences**, up to the grace period defined in client settings.  

     All deployments that have this check-box selected and are which are targeted to devices to which you also deployed the client setting will use the grace period.  

 In this release, the grace period you configure is not used by client devices. If you configure a grace period and select the checkbox, the application will be installed in the first non-business window that the user configured after the deadline.  

 Similar options have been added to the software updates deployment wizard,  automatic deployment rules wizard, and properties pages. However, these are not currently implemented in this technical preview.  

##  <a name="BKMK_Remote"></a> New experience for remote device actions  
 The experience for performing remote device actions from the Configuration Manager console has been improved.  
Common actions such as **Retire/Wipe**, **Reset Passcode**, **Remote Lock**, and **Bypass Activation Lock** can now be found in the **Remote Device Actions** menu accessed from the **Assets and Compliance** workspace.  

 ![New Remote Device Actions screenshot](media/New-Remote-Device-Actions.png)  

 You can find the status for each of these operations in the following places:  

-   In the details pane when you select a device from the **Devices** node.  

-   On the **Properties** page for a device.  

-   On the main page of the **Devices** node (not all columns might be visible by default).  

 For more information about iOS Activation Lock bypass, see [Help protect iOS devices with Activation Lock bypass for Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock), in particular, the **Current known issues with Activation Lock bypass in the Configuration Manager Technical Preview** section.  

##  <a name="BKMK_WSFB"></a> Windows Store for Business apps  
 The [Windows Store for Business](https://www.microsoft.com/business-store) is where you can find and purchase apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can manage volume-purchased apps from the Configuration Manager console, for example:  

-   You can synchronize the list of purchased apps with Configuration Manager  

-   Apps that are synchronized appear in the Configuration Manager console and you can deploy these like any other apps  

-   Every 24 hours, Configuration Manager downloads app licensing information from the store, and you can review this in the Configuration Manager console  

 In the 1604 technical preview release, you could synchronize and view apps from the Windows Store for Business in the Configuration Manager console. In this release, we have added the ability to create and deploy Configuration Manager applications from synchronized store apps.  

### Set up Windows Store for Business synchronization  

1.  In Azure Active Directory, register Configuration Manager as a “Web Application and/or Web API” management tool. This will give you a client ID that you will need later.  

    1.  In the Active Directory node of [https://manage.windowsazure.com](https://manage.windowsazure.com), select your Azure Active Directory, then click **Applications** > **Add**.  

    2.  Click **Add an application my organization is developing**.  

    3.  Enter a name for the application, select **Web application** and/or **Web API**, then click the **Next** arrow.  

    4.  Enter the same URL for both the **Sign-on URL** and **App ID URI**. The URL can be anything and does not need to resolve to a real address. For example, you can enter **https://&lt;yourdomain>/sccm**.  

    5.  Complete the wizard.  

2.  In Azure Active Directory, create a client key for the registered management tool.  

    1.  Highlight the application you just created and click **Configure**.  

    2.  Under **Keys**, select a duration from the list, and click **Save**. This will create a new client key. Do not navigate away from this page until you have successfully onboarded Windows Store for Business to Configuration Manager.  

3.  In the Windows Store for Business, configure Configuration Manager as the store management tool.  

    1.  Open [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) and sign-in if prompted.  

    2.  Accept the terms of use if required.  

    3.  Under **Management Tools**, click **Add a management tool**.  

    4.  In **Search for the tool by name**, type the name of the application you created in AAD previously, then click **Add**.  

    5.  Click **Activate** next to the application you just imported.  

    6.  In the **Show Offline-Licensed Apps** wizard, click **Yes** if you want to allow offline-licensed applications to be purchased.  

4.  Purchase at least one app from the Windows Store for Business.  

5.  In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, then click **Windows Store for Business.**  

6.  On the **Home** tab, in the **Create** group, click **Add Windows Store for Business Account**.  

7.  Add your tenant ID, client id, and client key from Azure Active Directory, then complete the wizard.  

8.  Once you are done, you will see the account you configured in the **Windows Store for Business Accounts** list in the Configuration Manager console.  

### Try it out!  
 Try to complete the following task and then let us know how it worked by using our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) page on the Microsoft Connect site:  

 Create and deploy a Configuration Manager application from a Windows Store for Business offline licensed app.  

1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then click **License Information for Store Apps**.  

2.  Choose the app you want to deploy, then, in the **Home** tab, in the **Create** group, click **Create Application**.  

 A Configuration Manager application is created containing the Windows Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.  

> [!IMPORTANT]  
>  When you create a Configuration Manager application with a single deployment type from an offline licensed app, this can be deployed to devices that are MDM managed and also managed with the Configuration Manager client. If you try to deploy an app with multiple deployment types, the installation will fail.  
>   
>  You cannot currently deploy online licensed apps with Configuration Manager.  

##  <a name="BKMK_VPP2"></a> General improvements for volume-purchased apps  

-   In this release, volume-purchased apps from the Windows Store for Business, and the iOS app store have been consolidated into the same view, **License Information for Store Apps**.  

-   For iOS volume-purchased apps, the Apple Volume Purchase Program tab has been removed from the **App Package for iOS Browser** dialog box in the Create Application wizard. To create a volume-purchased app for iOS, use these steps:  

    1.  1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then click **License Information for Store Apps**.  

    2.  2.  Choose the app you want to deploy, then, in the **Home** tab, in the **Create** group, click **Create Application**.  

-   The location you use to get and upload an Apple VPP token for volume-purchased apps in the Configuration Manager console has changed. You can now do this in the **Admin** workspace under the **Cloud Services** > **Apple Volume Purchase Program Tokens** node.  

##  <a name="BKMK_VPP"></a> Enterprise Data Protection (EDP)  
 You can create configuration items that let you deploy your enterprise data protection (EDP) policies, including letting you choose your protected apps, your EDP-protection level, and how to find enterprise data on the network. For more information about EDP, see the following topics:  

-   [Protect your enterprise data using enterprise data protection (EDP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp)  

-   [Create and deploy an enterprise data protection (EDP) policy using System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm)  

##  <a name="BKMK_End"></a> End users can install apps from the Company Portal  
 On-premises MDM was introduced in the System Center Configuration Manager version 1511. In previous versions, you could deploy applications to MDM-managed Windows 10 devices with a deployment purpose of **Required** install for on-premises MDM managed devices.  

 In this release, you can now deploy apps with a deployment purpose of **Available** to users of on-premises MDM managed Windows 10 computers, and users can now install these apps themselves from the Company Portal.
In this technical preview, if the Company Portal is open for more than 15 minutes, the end user will see an error message. To work around the issue, restart the Company Portal.  

### Before you start  

#### Server prerequisites  

-   .NET 4.5 or higher (requires restart)  

-   PowerShell 3.0 for configuration script (requires restart)  

#### Client prerequisites  

-   Windows 10 Desktop 1511 (OS build 10586.218) or later  

#### General prerequisites  

-   Ensure you have completed the [Preparation steps for On-premises Mobile Device Management](https://technet.microsoft.com/library/mt613153.aspx) and [enrolled your devices](https://technet.microsoft.com/library/mt627870.aspx).  

-   For the best application install experience when using the Company Portal, make sure Configuration Manager has an active connection to Microsoft Intune.  

-   If you choose the bulk-enrollment option, configure user device affinity for the enrolled device before you try this scenario.  

### Configuration steps  

#### Install the Application Catalog roles and enable Mobile Device Management support  

1.  Add the Application Catalog Web Service and Web Site roles  

    1.  Select **HTTPS mode** and the **Allow mobile devices to use this Application Catalog Web Service point** option.  

    2.  Limitations in this Technical Preview:  

        -   You must uninstall any existing Application Catalog roles before selecting the option to allow mobile devices to connect.  

        -   Make sure there is only one set of Application Catalog roles and the roles are co-located on the same site system with the Enrollment point and Enrollment Proxy point roles.  

2.  Verify that the following components are operational from the Component Status node in the Configuration Manager console:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### Configure boundaries  
 Configure required boundaries for intranet-only Distribution Points.  

> [!NOTE]  
>  Only IPv4 range boundaries are supported at this time for mobile device management.  

### Deploy the Company Portal application and configuration  

1.  Use the configuration script included with the technical preview to prepare the Company Portal deployment and configuration:  

    1.  Open an elevated PowerShell command window.  

    2.  Run **set-executionPolicy RemoteSigned**  

    3.  From the folder **&lt;SCCM installation directory\>\cd.latest\SMSSETUP\TOOLS\MDM** run **.\ConfigurationScript.ps1**  

     The configuration script does the following:  

    1.  Creates a Configuration Manager application with a Windows app package deployment type using **CompanyPortalOnPremisesMDM.appx** in the same folder.  

    2.  Creates a configuration item and configuration baseline that configures the Company Portal.  

    3.  Deploys both the configuration baseline and the application, and adds the application to all distribution points.  

    > [!NOTE]  
    >  If the Application Catalog roles are not co-located with the primary site, take the following actions:  
    >   
    >  -   In the **Assets and Compliance** workspace, locate the **OnPremMDM Portal Configuration CI - server urls** configuration item  
    > -   Change the **Compliance Rules** value to the fully-qualified domain name of the site system where the Application Catalog roles are located.  

2.  Once the Company Portal application and its configuration are both deployed, verify the application and configuration baseline are compliant for the given device using **Deployments** section of the Configuration Manager console. The Company Portal will appear as **Company Portal (Technical Preview)** in the Start menu on the device.  

### Try it out!  
 Try to complete the following tasks and then let us know how it worked by using our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) page on the Microsoft Connect site:  

1.  Deploy several applications with supported deployment types to a user collection with a deployment purpose of **Available**. For this technical preview, applications that require admin approval are not supported and will not be displayed in the Company Portal.  

2.  Users can then browse for, and install apps from the Company Portal.  

     After you open Company Portal, you will see an authentication dialog box named **System Center Configuration Manager** Specify the user’s Active Directory credentials (either in the form of user@domain or domain\user) to log in.  

##  <a name="BKMK_SW1"></a> New tabs for Updates and Operating Systems in Software Center  
 In this release, the following changes have been made to improve the layout of the Software Center application:  

-   The **Applications** tab has been split into three separate tabs for **Updates**, **Operating systems** (which were both previously found in the **Filters** list), and **Applications**.  

##  <a name="BKMK_ServerGroups"></a> Service a  server group  
 Technical Preview for System Center Configuration Manager, version 1511, included the ability to create a collection where all devices in the collection make up a server group. Then, you could configure the server group settings to use when you deploy software updates to the server group, control the percentage of computers that are updated at any given time, and configure pre-deployment and post-deployment PowerShell scripts to run custom actions.  

 Technical Preview for System Center Configuration Manager, version 1605, adds the ability to update the computers in the server group in a specified order that you define, adds enhanced monitoring to view the status for the computers in the server group, and provides the ability to clear the deployment locks that is useful when clients have failed to install the software updates and are preventing other clients from installing their software updates.  

### Try it out!  
 Try to complete the following tasks and then let us know how it worked by using our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) page on the Microsoft Connect site:  

-   I can create a collection that represents a server group. For this test, you can configure your collect membership rules to have 2 machines in this collection.   

-   I can specify that computers in the server group install software updates in a specific order based on the server group  settings for the collection. Use the sample scripts in the procedure to specify the pre-deployment and post-deployment scripts.  

-   I can deploy a software update to this collection. Review the start.txt and end.txt files (created from the sample scripts)  in C:\temp and verify start and end times for the deployment on the computers in the server group. Review the UpdatesDeployment.log file for more information.  

#### To create a collection for a server group  

1.  [Create a device collection](https://technet.microsoft.com/library/gg712295.aspx) that contains the computers in the server group.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**, right-click the collection that contains the computers in the server group, and then click **Properties**.  

3.  On the **General** tab, select **All devices are part of the same server group**, and then click **Settings**.  

4.  On the **Server Group Settings** page, specify one of the following settings:  

    -   **Allow a percentage of machines to be updated at the same time**: Specifies that only a certain percentage of clients are updated at any one time. If, for example, the collection has 10 clients, and the collection is configured to update 30% of clients at the same time, then only 3 clients will install software updates at any given time.  

    -   **Allow a number of machines to be updated at the same time**: Specifies that only a certain number of clients are updated at any one time.  

    -   **Specify the maintenance sequence**: Specifies that the clients in the collection will be updated one at a time in the sequence that you configure. A client will only install software updates after the client that is ahead of it in the list has finished installing its software updates.  

5.  Specify whether to use a pre-deployment (node drain) script or post-deployment (node resume) script.  

    > [!TIP]  
    >  The following are examples that you can use in testing for pre-deployment and post-deployment scripts that write the current time to a text file:  
    >   
    >  **Pre-deployment**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Post-deployment**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### To deploy software updates to the server group and monitor status  

1.  [Deploy software updates](https://technet.microsoft.com/library/gg712304.aspx) to the server group collection.  

2.  [Monitor the software update deployment](https://technet.microsoft.com/library/gg712304.aspx). In addition to the standard monitoring views for software updates deployment, a new state description is displayed when a client is waiting for its turn to install the software updates. **Waiting for lock** is displayed for this new state.  

#### To clear the deployment locks for computers in a server group  

1.  In the **Assets and Compliance** workspace, click **Device Collections**, and click the collection to clear deployment locks.  

2.  On the **Home** tab, in the **Deployment** group, click **Clear Server Group Deployment Locks**. When clients have failed to install the software updates and are preventing other clients from installing their software updates, the deployment locks can be manually cleared.  

##  <a name="BKMK_ATP"></a> Support for Windows Defender Advanced Threat Protection service  
 Windows Defender Advanced Threat Protection (ATP) is a new service that will help enterprises to detect, investigate, and respond to advanced attacks on their networks. Learn more about [Windows Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager can help you onboard and monitor managed Windows 10 Anniversary Edition client devices.  

### Try it now!  
 Try to complete the following tasks and then let us know how it worked by using our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) page on the Microsoft Connect site:  

-   Onboard devices to the Windows Defender Advanced Threat Protection (ATP) online service  

-   Monitor Windows Defender ATP deployment to managed devices  

 **Prerequisites**  

-   Subscription to the Windows Defender Advanced Threat Protection online service  

-   Clients running Windows 10, Anniversary Edition (build 14328 and greater)  

-   Create a client onboarding configuration file  

    ##### How to create an onboarding configuration file  

    1.  Logon to the Windows Defender ATP online service  

    2.  Click on the **Client On-boarding** menu item  

    3.  Select **System Center Configuration Manager** and click **Download package**.  

    4.  Download the compressed archive (.zip) file and extract the contents.  


##### Onboard devices for Windows Defender ATP  

1.  In the Configuration Manager console, navigate **Assets and Compliance** > **Overview** > **Endpoint Protection** > **Windows Defender ATP Policies** and click **Create Windows Defender ATP Policy**. The Windows Defender ATP Policy Wizard opens.  

2.  Type the **Name** and **Description** for the Windows Defender ATP policy and select **Onboarding**. Click Next.  

3.  **Browse** to the Configuration file provided by your organization’s Windows Defender ATP cloud service tenant. Click **Next**.  

4.  Specify the file samples that are collected and shared from managed devices for analysis.  

    -   **None** – No sample files are collected for analysis  

    -   **Portable executable files** – Files such as program files (.exe), dynamic-library link (.dll) files, font files, and similar files that can be exploited in cyberattacks are collected and shared for analysis  

     Click **Next**.  

5.  Review the summary and complete the wizard.  

6.  You can now deploy the Windows Defender ATP policy to managed client computers by clicking **Deploy**.  

##### Monitor Windows Defender ATP  

1.  In the Configuration Manager console, navigate **Monitoring** > **Overview** > **Security** and then click **Windows Defender ATP**.  

2.  Review the Windows Defender Advanced Threat Protection dashboard.  

    -   **Windows Defender Agent Deployment Status** – The number and percentage of eligible managed client computers with active Windows Defender ATP policy onboarded  

    -   **Windows Defender ATP Agent Health** – Percentage of computer clients reporting status for their Windows Defender ATP agent  

        -   **Healthy** - Working properly  

        -   **Inactive** - No data sent to service during time period  

        -   **Agent state** - The system service for the agent in Windows isn't running  

        -   **No onboarded** - Policy was applied but the agent has not reported policy onboard  

##  <a name="BKMK_DHA"></a> On-premises Device Health Attestation  
 Health attestation for Windows 10 devices can now be configured to communicate using the on-premises infrastructure. Administrators can specify whether reporting is done via the cloud or on-premises resources. If on-premises is selected for health attestation reporting, then a URL can be specified for the service. This enables client PCs without internet access to  enable and manage devices using health attestation.  

### Enable health attestation for on-premises devices  
 In 1605, we’ve fixed a few bugs discovered in 1604 Technical Preview.  To try it out, configure on-premises Health Attestation Service using client agent settings.  

1.  In the Configuration Manager console, navigate **Administration** > **Overview** > **Client settings**, and then set **Use on-premises Health Attestation Service** to **Yes**.  

2.  Specify the **On-premise Health Attestation Service URL**, and then click **OK**.  

##  <a name="BKMK_RestartOptions"></a> New restart options for Windows 10 clients after software update installation  
 When a software update that requires a restart is deployed using Configuration Manager and installed on a computer, a pending restart is scheduled and a restart dialog box is displayed. Currently, for Windows 8 and above, if you shut down or restart the computer using the Windows Power options (instead of from the restart dialog), the restart dialog remains after the computer restarts and the computer will need to restart at the configured deadline. In this technical preview, the option to **Update and Restart** and **Update and Shutdown** will be available on Windows 10 computers in the Windows Power options whenever there is a pending restart for a Configuration Manager software update. After using one of these options, the restart dialog will not display after the computer restarts.  

##  <a name="BKMK_IMEI"></a> Pre-declare corporate-owned devices with IMEI or iOS serial number  
 You can now identify corporate-owned devices by importing their international station mobile equipment identity (IMEI) numbers. You can upload a comma-separated values (.csv) file containing device IMEI numbers or you can manually enter device information.  You can also import serial numbers for iOS devices.  Imported information will set ownership of the devices that enroll as “Corporate”.  An Intune license is still required for each user that accesses the service.  

### Try it out!  
 Try to complete the following tasks and then let us know how it worked by using our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) page on the Microsoft Connect site:  

-   Import a set of IMEI numbers in a .csv file. Each row can contain the IMEI number followed by a details field.  

-   Manually import IMEI numbers from the Configuration Manager console.  

-   Import a set of iOS serial numbers in a .csv file. Again, each row contains a number followed by any details for the device.  

##### Pre-declare corporate-owned devices with IMEI or iOS serial number  

1.  In the Configuration Manager console, go **Assets and Compliance** > **Overview** > **All Corporate-owned Devices** > **Pre-declared Devices**, and then click **Create Pre-declared Devices**. The Pre-declared Devices wizard opens.  

2.  Specify how you want to add device information:  

    -   **Upload a .csv file containing IMEI numbers and details** - To upload a list of numbers, see Step #3.  

    -   **Manually add IMEI numbers and details** - To manually enter information, type the IMEI number or iOS serial number and details for the devices, and then proceed to Step #4.  

3.  For uploaded files, Browse to the .csv file containing information to pre-declare corporate-owned devices. The file must have the following format, excluding the top row (provided for guidance only):  

    |**IMEI #**|**iOS Serial**|**OS**|**Details**|
    |---|---|---|---|
    |123456789012345||WINDOWS|Company-owned Windows device|
    |123456789012|A0BCD0EFGH0J|IOS|Company-owned iOS devices|
    |123456789012346||ANDROID|Company-owned Android device|

     **Columns:**  

    -   Column 1: IMEI number – Either an IMEI number or iOS serial number is required for each row  

    -   Column 2: iOS serial number – Only iOS serial numbers can be pre-declared. Use IMEI number for other device platforms  

    -   Column 3: Operating system of the device (capitalization required):  

        -   IOS – All iOS devices  

        -   WINDOWS – Includes Windows Phone, Window 10 Mobile, and Windows PCs  

        -   ANDROID – All Android devices  

    -   Column 4: Details – Additional device information that appears in the Configuration Manager console  

     Click **Next**.  

4.  Review the results of the file import. Previously imported IMEI or serial numbers will have their details updated with new details.  Click **Next** to continue or **Back** to preserve updated details, and then complete the wizard.  
