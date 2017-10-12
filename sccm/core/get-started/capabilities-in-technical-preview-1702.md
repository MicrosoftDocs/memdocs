---
title: "Capabilities in Technical Preview 1702"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1702."
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1702 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1702. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

##  Send feedback from the Configuration Manager console

This preview introduces new feedback options in the Configuration Manager console. The Feedback options lets you send feedback directly to the development team, by way of the Configuration Manager UserVoice feedback website.  

>You can find the **Feedback** option:
-  In the ribbon, at the far left of the Home tab of each node.  
   ![Ribbon](./media/feedback-home.png)

-  When you right-click on any object in the console.   
    ![Righ-click option](./media/feedback-option.png)   

Choosing **Feedback** opens your browser to the Configuration Manager UserVoice feedback website, at https://configurationmanager.uservoice.com/forums/300492-ideas.
##  Changes for Updates and Servicing
The following are introduced with this preview.

**Simpler update choices**  
The next time your infrastructure qualifies for two or more updates, only the latest update is downloaded. For example, if your current site version is two or more older than the most recent version that is available, only that most recent update version is downloaded automatically.  

You have the option to download and install the other available updates, even when they are not the most current version. However, you will receive a warning that the update has been replaced by a newer one. To download an update that is *Available to Download*, select the update in the console and then click **Download**.

**Improved cleanup of older updates**   
We added an automatic clean-up function that deletes the unneeded downloads from the ‘EasySetupPayload’ folder on your site server.  


## Peer Cache improvements
Starting with this release, a peer cache source computer will reject a request for content when the peer cache source computer meets any of the following conditions:  
 - 	Is in low battery mode.
 -  CPU load exceeds 80% at the time the content is requested.
 -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10.
 -  There are no more available connections to the computer.   

You can configure these settings using the client agent config class for the peer source feature (*SMS_WinPEPeerCacheConfig*) when you use the System Center Configuration Manager SDK.

When the computer rejects a request for the content, the requesting computer will continue to seek content form alternate sources in its pool of available content source locations.   

## <a name="azurediscovery"></a> Use Azure Active Directory Domain Services to manage devices, users, and groups

With this technical preview version you can manage devices that are joined to an Azure Active Directory (AD) Domain Services managed domain. You can also discover devices, users, and groups in that domain with various Configuration Manager Discovery methods.

The technical preview site infrastructure, clients, and the Azure AD Domain Services domain must all run in Azure.


### Set up Configuration Manager to use Azure AD
To use Azure AD with Configuration Manager, you’ll need the following:
-	Azure subscription.
-	Azure AD with Domain Services (DS).
-	A Configuration Manager site that runs on an Azure VM that is joined to your Azure AD.
-	Configuration Manager clients that run in the same Azure AD environment.

To configure Azure AD Domain Service, see [Get started with Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### Discover resources
After you set up Configuration Manager to run in Azure AD, you can use the following Active Directory discovery methods to search
Azure AD for resources:  
- Active Directory System Discovery
- Active Directory User Discovery
- Active Directory Group Discovery  

For each method you use, edit the LDAP query to search the Azure AD OU structures instead of the containers that are typical to on-premises Active Directory. This requires you to direct the query to search your Active Directory in your Azure subscription.  

The following examples use an Azure AD of *contoso.onmicrosoft.com*:
 - **System Discovery**   
Azure AD stores devices under the **AADDC Computers** OU.  Configure the following:  
  -	*LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **User Discovery**
AAD stores users under the **AADDC Users** OU.  Configure the following:
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Group Discovery**  
Azure AD does not have an OU that stores groups. Instead, use the same general structure as the System or User queries and configure the LDAP query to point to the OU that contains the groups you want to discover.

See the following for more information about Azure AD:  
 - [Azure Active Directory Domain Services](https://azure.microsoft.com/en-us/services/active-directory-ds) on azure.microsoft.com.
 - [Active Directory Domain Services Documentation](https://docs.microsoft.com/azure/active-directory-domain-services) on docs.microsoft.com.

## Conditional access device compliance policy improvements

A new device compliance policy rule is available to help you block access to corporate resources that support conditional access, when users are using apps that are part of a non-compliant list of apps. The non-compliant list of apps can be defined by the admin when adding the new compliant rule **Apps that cannot be installed**. This rule requires the admin to enter the **App Name**, the **App ID**, and the **App Publisher** (optional) when adding an app to the non-compliant list. This setting only applies to iOS and Android devices.

Additionally, this helps organizations to mitigate data leakage through unsecured apps, and prevent excessive data consumption through certain apps.

- Learn more [how device compliance policies work](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Learn more [how to create device compliance policies](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### Try it out

**Scenario:** Identify apps that might be causing data leakage by sending corporate data outside your company, or that are causing excessive data consumption, then [create a conditional access device compliance policy](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) that adds these apps into the non-compliant list of apps. This will block access to corporate resources that support conditional access until the user can remove the blocked app.

## Antimalware client version alert
Beginning with this preview version, Configuration Manager Endpoint Protection provides an alert if more than 20% (default) of managed clients are using an expired version of the antimalware client (i.e. Windows Defender or Endpoint Protection client).

### Try it out
Ensure Endpoint Protection is enabled on all desktop and server clients using client settings policy. You can now view **Antimalware Client Version** and **Endpoint Protection Deployment Status** by going **Assets and Compliance** > **Overview** > **Devices** > **All Desktops and Serve Clients**. To check for an alert, view **Alerts** in the **Monitoring** workspace. If more than 20% of managed clients are running an expired version of antimalware software, the Antimalware client version is outdated alert is displayed. This alert doesn’t appear on the **Monitoring** > **Overview** tab. To update expired antimalware clients, enable software updates for antimalware clients.

To configure the percentage at which the alert is generated, expand **Monitoring** > **Alerts** > **All Alerts**, double-click **Antimalware clients out of date** and modify the **Raise alert if percentage of managed clients with an outdated version of the antimalware client is more than** option.

## Compliance assessment for Windows Update for Business updates
You can now configure a compliance policy update rule to include a Windows Update for Business assessment result as part of the conditional access evaluation.
> [!IMPORTANT]
> You must have Windows 10 Insider Preview Build 15019 or later to use compliance assessment for Windows Update for Business updates.

### Allow Windows Update for Business to manage Windows 10 updates
To gather compliance assessment information for Windows Update for Business updates, use the following procedure to configure the client agent setting to explicitly allow Windows Update for Business to manage Windows 10 updates.
1. In the Configuration Manager console, go to **Administration** > **Client Settings**.
2. In the properties for the client settings, go to **Software Updates**, and select **Yes** for the **Manage Windows 10 updates with Windows Update for Business** setting.

### Create a compliance policy for Windows Update for Business assessment
1. In the Configuration Manager console, go to **Assets and Compliance** > **Compliance Settings** > **Compliance policies**.
2. Click **Create Compliance Policy** or select an existing compliance policy to modify.
3. On the General page, provide a name and description, select **Compliance rules for devices managed with the Configuration Manager client**, set the non-compliance severity for reporting, and click **Next**.
4. On the Supported Platforms page, select **Windows 10**, and then click **Next**.
5. On the Rules page, click **New....**, and then for **Condition** choose **Require Windows Update for Business compliance**. The **Value** setting is automatically set to **True**.

The new policy displays in the **Compliance Policies** node of the **Assets and Compliance** workspace.

### Deploy a compliance policy
1. In the Configuration Manager console, go to **Assets and Compliance** > **Compliance Settings**, and then click **Compliance Policies**.
2. On the **Home** tab, in the **Deployment** group, click **Deploy**.
3. In the **Deploy Compliance Policy** dialog box, click **Browse** to select the user collection to which to deploy the policy.
   Additionally, you can select options to generate alerts when the policy is not compliant, and also to configure the schedule by which this policy will be evaluated for compliance.
4. When you are done, click **OK**.

### Monitor the compliance policy
After you create the compliance policy, you can monitor the compliance results in the Configuration Manager console. For details, see [Monitor the compliance policy](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## Improvements to Software Center settings and notification messages for high-impact task sequences
This release includes the following improvements to Software Center settings and notification messages for high-impact deployment task sequences:

- In the properties for the task sequence, you can now configure any task sequence, including non-operating system task sequences, as a high-risk deployment. Any task sequence that meets certain conditions is automatically defined as high-impact. For details, see [Manage high-risk deployments](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- In the properties for the task sequence, you can choose to use the default notification message or create your own custom notification message for high-impact deployments.
- In the properties for the task sequence, you can configure Software Center properties, which include make a restart required, the download size of the task sequence, and the estimated run time.
- The default high-impact deployment message for in-place upgrades now states that
your apps, data, and settings are automatically migrated. Previously, the default message for any operating system installation indicated that all apps, data, and settings would be lost, which was not true for an in-place upgrade.

### Set a task sequence as a high-impact task sequence
Use the following procedure to set a task sequence as high-impact.
> [!NOTE]
> Any task sequence that meets certain conditions is automatically defined as high-impact. For details, see [Manage high-risk deployments](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **User Notification** tab, select **This is a high-impact task sequence**.

### Create a custom notification for high-risk deployments
1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **User Notification** tab, select **Use custom text**.
>  [!NOTE]
>  You can only set user notification text when the **This is a high-impact task sequence** is selected.

4. Configure the following settings (max of 255 characters for each text box):

   **User notification headline text**: Specifies the blue text that displays on the Software Center user notification. For example, in the default user notification, this section contains something like "Confirm you want to upgrade the operating system on this computer".

   **User notification message text**: There are three text boxes that provide the body of the custom notification.
   - 1st text box: Specifies the main body of text, typically containing instructions for the user. For example, in the default user notification, this section contains something like "Upgrading the operating system will take time and your computer might restart several times."
   - 2nd text box: Specifies the bold text under the main body of text. For example, in the default user notification, this section contains something like "This in-place upgrade installs the new operating system and automatically migrates your apps, data, and settings."
   - 3rd text box: Specifies the last line of text under the bold text. For example, in the default user notification, this section contains something like "Click Install to begin. Otherwise, click Cancel."   

   Let's say you configure the following custom notification in properties.

   ![Custom notification for a task sequence](.\media\user-notification.png)

   The following notification message will be displayed when the end-user opens the installation from Software Center.

   ![Custom notification for a task sequence](.\media\user-notification-enduser.png)

### Configure Software Center properties
Use the following procedure to configure the details for the task sequence displayed in Software Center. These details are for information only.  
1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **General** tab, the following settings for Software Center are available:
  - **Restart required**: Lets the user know whether a restart is required during the installation.
  - **Download size (MB)**: Specifies how many megabytes is displayed in Software Center for the task sequence.  
  - **Estimated run time (minutes)**: Specifies the estimated run time in minutes that's displayed in Software Center for the task sequence.


## Check for running executable files before installing an application

In the *<deployment type name>* **Properties** dialog box of a deployment type, on the Install Behavior tab, you can now specify one of more executable files that, if running, will block the installation of the deployment type. The user must close the running executable file (or it can be closed automatically for deployments with a purpose of required) before the deployment type can be installed.

### Try it out.

1.	In the properties of a Configuration Manager deployment type, choose the **Install Behavior** tab.
2.	Choose **Add** to add one or more executable file names you want to check for. You can also add a display name to make it easier for users to identify applications in the list.
3.	If the deployment will have a purpose of required, in the deploy software wizard, you can optionally choose to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**.

If the application was deployed as **Available**, and an end user tries to install an application, they will be prompted to close any running executables you specified before they can proceed with the installation.

If the application was deployed as **Required**, and the option **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** is selected, they will see a dialog box which informs them that executables you specified will be automatically closed when the application installation deadline is reached. You can schedule these dialogs in **Client Settings** > **Computer Agent**. If you don’t want the end user to see these messages, select **Hide in Software Center and all notifications** on the **User Experience** tab of the deployment’s properties.

If the application was deployed as **Required** and the option **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** is not selected, then the installation of the app will fail if one or more of the specified applications are running.

## Create PFX certificates with S MIME support

You can now create a PFX certificate profile that supports S/MIME and deploy it to users.  This certificate can then be used for S/MIME encryption and decryption across devices that the user has enrolled.

Additionally, you can now specify multiple certification authorities (CAs) on multiple Certificate Registration Point site system roles and then assign which CAs process requests as part of the certificate profile.

For iOS devices, you can associate a PFX certificate profile to an email profile and enable S/MIME encryption.  This then enables S/MIME in the native email client on iOS and associates the correct S/MIME encryption certificate to it.

For more information about certificates in Configuration Manager, see [Introduction to certificate profiles in System Center Configuration Manager]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## New compliance settings for iOS devices

We've added new settings you can use in your configuration items for iOS devices. These are settings that previously existed in Microsoft Intune in a standalone configuration, and are now available when you use Intune with Configuration Manager. If you need help with any of these settings, see [iOS policy settings in Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune).

- **Sync data from managed apps to iCloud**
- **Handoff to continue activities on other device**
- **iCloud Photo Sharing**
- **iCloud Photo Library**
- **Trust new enterprise app authors**
- **Allow the user to download content from the iBook store flagged as 'Erotica'** (supervised mode only)
- **Force paired Apple Watches to use wrist detection**
- **Password for AirPlay outgoing requests**
- **Modify account settings** (supervised mode only)
- **Changes to app cellular data usage settings** (supervised mode only)
- **Erase all content and settings** (supervised mode only)
- **Configure restrictions on device** (supervised mode only)
- **Use host pairing to control the devices an iOS device can pair with** (supervised mode only)
- **Install configuration profiles and certificates** (supervised mode only)
- **Device name modification** (supervised mode only)
- **Passcode modification** (supervised mode only)
- **Apple Watch pairing** (supervised mode only)
- **Notification settings modification** (supervised mode only)
- **Wallpaper modification** (supervised mode only)
- **Diagnostics submission settings modification** (supervised mode only)
- **Bluetooth Modification** (supervised mode only)
- **AirDrop** (supervised mode only)
- **Use Siri to query user-generated content from the Internet** (supervised mode only)
- **Siri profanity filter** (supervised mode only)
- **Return results from the Internet in Spotlight search** (supervised mode only)
- **Word definition lookup** (supervised mode only)
- **Predictive keyboards** (supervised mode only)
- **Auto-correction** (supervised mode only)
- **Keyboard spell-check** (supervised mode only)
- **Keyboard shortcuts** (supervised mode only)
<!--- - **Enterprise app trust settings modification** --->
- **Installing apps using Apple Configurator and iTunes only** (supervised mode only)
- **Automatic app downloads** (supervised mode only)
- **Make changes to the Find My Friends app settings** (supervised mode only)
- **Access to the iBooks store** (supervised mode only)
- **Messages app** (supervised mode only)
- **Podcasts** (supervised mode only)
- **Apple Music** (supervised mode only)
- **iTunes Radio** (supervised mode only)
- **Apple News** (supervised mode only)
- **Game Center** (supervised mode only)
- **Treat AirDrop as an unmanaged destination**

## Android for Work support

Starting with Technical Preview version 1702, you can bind a Google account to your hybrid MDM tenant. This allows you to do the following:

- Enroll [supported Android devices](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) as Android for Work, creating work profiles on those enrolled devices
- Approve apps in the Play for Work store, sync them with the Configuration Manager console, and then deploy them to devices' work profiles
- Create and deploy configuration items to configure work profile and password settings for those devices
- Create and deploy compliance policy items and resource access profiles for Android for Work devices as you already do for Android devices
- Perform selective wipe on Android for Work devices

When you enroll a device as Android for Work creates a work profile on the device which Intune can manage. This work profile exists side-by-side with the personal profile on the Android device. Users can easily switch between work profile apps and personal profile apps. You cannot manage items in the personal profile. Personal apps and data remain unmanaged. Configuration Manager has full control over the work profile and its contents and can remove it from the device.

Android for Work is a separate platform from Android, and you will need to decide which form of management to use for Android devices that support work profiles.

### Try it out!
The following sections describe Android for Work management.

#### Enable Android for Work management
1. Create a Google account at https://accounts.google.com/SignUp to use as your Android for Work admin account that will be associated with all Android for Work management tasks for this Intune tenant. This could be a Google account shared among the administrators who manage Android devices. This is the Google account that your organization uses to manage and publish apps in the Play for Work console. You will use this account to approve apps in the Play for Work store, so keep track of the account name and password.
2. Enable Android enrollment by binding the Google account to the Intune tenant managed in Configuration Manager:
  1. Go to **Administration** > **Overview** > **Cloud Services** > **Microsoft Intune Subscriptions** and select your Intune subscription.
  2. In the ribbon, click **Configure Platforms** > **Android** and make sure **Enable Android enrollment** is checked.
  3. In the ribbon, click **Configure Platforms** > **Android for Work**.
  4. In the dialog box, click **Configure Android for Work in the Intune console**. The Intune console opens in your web browser.
  5. Use your Intune administrator credentials to log in to the Intune portal.
  6. Click **Configure** to open Google Play's Android for Work website.
  7. On Google's sign-in page, enter the Google account credentials from step 1, and then provide your company information.
3. When you return to the Intune portal, Android for Work is enabled and you have three enrollment options for Android for Work devices:
  - **Manage all devices as Android** - (Disabled) All Android devices, including devices that support Android for Work, will be enrolled as conventional Android devices
  - **Manage supported devices as Android for Work** - (Enabled) All devices that support Android for Work are enrolled as Android for Work devices. Any Android device that does not support Android for Work is enrolled as a conventional Android device.
  - **Manage supported devices for users only in these groups as Android for Work** - (Testing) Lets you target Android for Work management to a limited set of users. Only members of the selected groups who enroll a device that supports Android for Work are enrolled as Android for Work devices. All others are enrolled as Android devices.
  
> [!NOTE]
> A known issue prevents the **Manage supported devices for users only in these groups as Android for Work** option from working as expected. Users' devices in the specified Azure AD groups will enroll as Android instead of Android for Work. To test Android for Work, you must use the **Manage all supported devices as Android for Work**.


  In order to enable Android for Work enrollment, you must choose one of the bottom two options. The **Manage supported devices for users only in these groups as Android for Work** option requires you have Azure Active Directory security groups set up first.

You'll see the account name and organization name in the Intune portal when the binding is complete; at that point, you can close both browsers.

#### Approve and deploy Android for Work apps
Follow these steps to approve apps in the Play for Work store, sync them to the Configuration Manager console, and deploy them to managed Android for Work devices. To deploy apps to users' work profiles, you'll need to approve the apps in Play for Work, and then sync the apps with the Configuration Manager console.

1. Open a browser and go to: https://play.google.com/work.
2. Sign in using the Google admin account you bound to your Intune tenant.
3. Browse for apps you'd like to deploy in your environment and click **Approve** for each of them.
4. In the Configuration Manager console, go to **Administrator** > **Overview** > **Cloud Services** > **Android for Work** and click **Sync**.
5. Wait for up to 10 minutes for apps to sync, and then go **Software Library** > **Overview** > **Application Management** > **License Information for Store Apps**.
6. Click on an app synced from Play for Work and then click **Create Application**.
7. Complete the wizard and click **Close**.
8. Go to **Software Library** > **Overview** > **Application Management** > **Applications**, select an Android for Work apps, and deploy as usual.

To sync Play for Work apps with Configuration Manager, you must approve at least one app on the Play for Work website.

#### Enroll an Android for Work device
How you enroll Android for Work devices is similar to enrollment for Android. Download and run the Company Portal app for Android on your mobile device. You will be prompted to create a work profile as part of the enrollment process.  Once the work profile is created, you must switch to the managed version of the Company Portal. The managed Company Portal is tagged with a small orange briefcase in the bottom-right corner.

#### Create and deploy a configuration item
Android for Work has two setting groups for configuration items:
- Password
- Work Profile

You can configure content sharing between work profiles, as well as the following configuration items on devices running Android 6 or higher:
- The behavior for apps asking for specific permissions
- Whether notifications for applications within the work profile are visible on the lock screen

To try this, create a configuration item through the standard workflow, choose **Android for Work** on the **General** page and configure settings for each of the setting groups, adding the configuration item to a baseline, and deploying as usual. These settings will only apply to devices enrolled as Android for Work, and not those enrolled as Android.

#### Perform selective wipe
Devices enrolled as Android for Work can only be selectively wiped because you only manage the work profile. This protects the personal profile from being wiped. Performing a selective wipe on an Android for Work device removes the work profile, including all apps and data, and unenrolls the device.

To selectively wipe an Android for Work device, use the normal [selective wipe process](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) in the Configuration Manager console.

#### Known issues for Android for Work
**Configuring sync schedule in Android for Work email profiles causes them to fail to deploy**
One of the options in the ConfigMgr UI for Android for Work email profiles is "Schedule". On other platforms, this allows the admin to configure a schedule for syncing email and other email account data down to the mobile devices it's deployed to. However, it does not work for Android for Work email profiles, and choosing any option other than "Not Configured" will cause the profile to not be deployed to any devices.
