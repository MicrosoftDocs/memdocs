---
title: Deploy Remote Help with Microsoft Intune
description: Follow the steps to deploy Remote Help with Microsoft Intune on Windows, macOS, and Android Enterprise.
author: lenewsad
ms.author: lanewsad
ms.date: 10/01/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: karawang
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- graph-interactive
---

 # Deploying Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [remote-help-overview](includes/remote-help-overview.md)]

This article describes the steps to deploy Remote Help with Microsoft Intune.

- [⚙️Set up your tenant](#configure-remote-help-for-your-tenant)
- [⬇️Download Remote Help](#download-remote-help-apps)
- [🛠️Install Remote Help](#install-remote-help-apps)
- [🔒Configure Conditional Access](#setup-conditional-access-for-remote-help)

When planning your deployment of Remote Help, consider the following best practices:

- **User Communication and Training**: To drive adoption and effective use, provide documentation or brief training for both your helpdesk and end-users:
- **Helpdesk Training**: Make sure your support team knows how to initiate sessions (via Intune or via the Remote Help app), how to generate/enter session codes, and the limitations (for example, they should know they can't help users outside the tenant). Emphasize security practices, like always confirming end-user consent on the call before taking control. Microsoft's documentation and support videos can be good training material.
- **End-User Guidance**: Let your users know that a new remote support tool is available. Instruct them on how a support session is initiated – e.g., "When you contact the IT helpdesk, they may ask you to open the Remote Help app and share a code, or you might receive a popup notification to allow screen sharing." Reassure them that the tool is secure and only authorized IT will be able to connect, and that they will always have to explicitly allow any screen sharing or control.
- **Security Monitoring**: Keep an eye on the usage to detect any anomalous behavior. For instance, Intune's audit logs and Entra ID sign-in logs will show who is signing into Remote Help. Unusual times or unknown helpers should be investigated. Also ensure that when staff leave the support team, you remove them from the Remote Help roles to revoke their ability to use the tool.
- **Updates and New Features**: Remote Help is evolving. Microsoft may roll out new features (for example, the ability to support more platforms or an improved web helper dashboard). Stay updated via the Intune release notes or tech community blogs. Knowing these updates can help you refine your support process.

## Configure Remote Help for your tenant

To configure your tenant to support Remote Help, review and complete the following tasks. These tasks are important to configure for all Remote Help platforms that are supported.

### Task 1: Enable Remote Help

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Remote Help**.

2. On the **Settings** tab:
   1. Set **Enable Remote Help** to **Enabled** to allow the use of remote help. By default, this setting is *Disabled*.
   2. Set **Allow Remote Help to unenrolled devices** to **Enabled** if you want to allow this option. By default, this setting is *Disabled*.
   3. Set **Disable chat** to **Yes** to remove the chat functionality in the Remote Help app. By default, chat is enabled and this setting is set to **No**.

3. Select **Save**.

> [!NOTE]
> When you purchase licenses or start a trial, it could take a while to become active (anywhere between 30 minutes to 8 hours).
> When you try to create a Remote Help session you may continue to see messages indicating that Remote Help isn't enabled for the tenant even if you enabled Remote Help in the tenant after activation.

### Task 2: Configure permissions for Remote Help

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

To protect the privacy of users who may be using the sharer device, helpers should use the minimum level of privilege required to remotely assist the device. Only request an Unattended session if you know that there's no user at the sharer device to accept the remote help session.

The following Intune RBAC permissions manage the use of the Remote Help app. Set each to *Yes* to grant the permission:

- Category: **Remote Help app**
- Permissions:
  - **Elevation** : Yes/No
  - **View screen** : Yes/No
  - **Take full control** : Yes/No
  - **Unattended control** : Yes/No

> [!NOTE]
> If the **Take full control** permission is set to *Yes*, then by default, the user will have additional permission to **View screen**, even if the user's **View screen** permission is set to *No.*
> If the **Elevation** permission is set to *Yes*, then by default, the user will have additional permission to **View screen** and **Take full control**, even if the user's **View screen** and **Take full control** permission is set to *No.*
> If the **Unattended control** permission is set to *Yes*, then, by default, the user will have additional permission to **View screen**, **Take full control**, and **Elevation**, even if the user's **View screen**, **Take full control**, and **Elevation** permissions is set to *No.*

- Category: **Remote tasks**
- Permissions:
  - **Offer remote assistance** : Yes/No

By default, the built-in **Help Desk Operator** role sets all of these permissions to **Yes**. You can use the built-in role or create custom roles to grant only the remote tasks and Remote Help app permissions that you want different groups of users to have. For more information on using Intune RBAC, see [Role-based access control](../fundamentals/role-based-access-control.md).

### Task 3: Assign user to roles

After creating the custom roles that you can use to provide different users with Remote Help permissions, proceed to assign users to those roles.

1. Sign into [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration**  > **Roles** >  and select a role that grants Remote Help app permissions.

2. Select **Assignments**  > **Assign** to open **Add Role Assignment**.

3. On the *Basics* page, enter an **Assignment name** and optional **Assignment description**, and then choose **Next**.

4. On the **Admin Groups** page, select the group that contains the user you want to give the permissions to. Choose **Next**.

5. On the **Scope (Groups)** page, choose a group containing the users/devices that a member is allowed to manage. You also can choose all users or all devices. Choose **Next** to continue.

   >[!IMPORTANT]
   >If a sharer or a sharer's device isn't in the scope of a helper, that helper cannot provide assistance. When assisting an unenrolled device, the "All Devices" scope group will not include these devices. Instead, you should use the user scope group during the assignment process.
   >
   > If you specify an exclude group for an assignment such as a policy or app assignment, it needs to either be nested in one of the RBAC assignment [scope groups](role-based-access-control.md#about-intune-role-assignments), or it needs to be separately listed as a scope group in the RBAC role assignment.

6. On the **Review + Create** page, when you're done, choose **Create**. The new assignment is displayed in the list of assignments.

## Download Remote Help apps

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

Download the latest version of Remote Help direct from Microsoft at [aka.ms/downloadremotehelp](https://aka.ms/downloadremotehelp).

The most recent version of Remote Help is **5.1.1998.0**

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

Download the latest version of Remote Help directly from Microsoft at [aka.ms/downloadremotehelpmacos](https://aka.ms/downloadremotehelpmacos).

The most recent version of Remote Help is **1.0.2509231**.

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

The Remote Help app for Android is available from the Google Play store at [Remote Help - Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune.remotehelp).

---

## Install Remote Help apps

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

Remote Help is available as download from Microsoft and must be installed on each device before that device can be used to participate in a Remote Help session. By default, Remote Help opts users into automatic updates and updates itself when an update is available.

Some users may choose to opt out of automatic updates. However, when a new version of Remote Help is necessary, the app prompts users to install that version upon opening. You can use the same process to download and install Remote Help to install an updated version. There's no need to uninstall the previous version before installing the updated version.

- Intune admins can download and deploy the app to enrolled devices. For more information about app deployments, see [Install apps on Windows devices](../apps/apps-windows-10-app-deploy.md#install-apps-on-windows-devices).
- Individual users who have permissions to install apps on their devices can also download and install Remote Help.

> [!NOTE]
>
> - On May 2022, existing users of Remote Help will see a recommended upgrade screen when they open the Remote Help app. Users will be able to continue using Remote Help without upgrading.
> - On May 23, 2022, existing users of Remote Help will see a mandatory upgrade screen when they open the Remote Help app. They will not be able to proceed until they upgrade to the latest version of Remote Help.
> - Remote Help will now require Microsoft Edge WebView2 Runtime. During the Remote Help installation process, if Microsoft Edge WebView2 Runtime is not installed on the device, then Remote Help installation will install it. When uninstalling Remote Help, Microsoft Edge WebView2 Runtime will not be uninstalled.

#### Deploy Remote Help as an Enterprise App Catalog app

The Enterprise App Catalog is a collection of prepackaged Win32 apps that have been designed and prepared by Microsoft to support Intune. An Enterprise App Catalog app is a Windows app that you can add via the Enterprise App Catalog in Intune. This app type leverages the Win32 platform and has support for customizable capabilities. Remote Help is available in the Enterprise App Catalog. To learn more, see [Add an Enterprise App Catalog app to Microsoft Intune](/mem/intune-service/apps/apps-add-enterprise-app#add-a-windows-catalog-app-win32-to-intune).

#### Deploy Remote Help as a Win32 app

To deploy Remote Help with Intune, you can add the app as a Windows Win32 app, and define a detection rule to identify devices that don't have the most current version of Remote Help installed. Before you can add Remote Help as a Win32 app, you must repackage *remotehelpinstaller.exe* as a *.intunewin* file, which is a Win32 app file you can deploy with Intune. For information on how to repackage a file as a Win32 app, see [Prepare the Win32 app content for upload](../apps/apps-win32-prepare.md).

After you repackage Remote Help as a *.intunewin* file, use the procedures in [Add a Win32 app](../apps/apps-win32-add.md) with the following details to upload and deploy Remote Help. In the following, the repackaged remotehelpinstaller.exe file is named *remotehelp.intunewin*.

   > [!IMPORTANT]
   > Make sure the file you dowloaded is renamed to **remotehelpinstaller.exe**.

1. On the App information page, select **Select app package file**, and locate the *remotehelp.intunewin* file you've previously prepared, and then select **OK**.

   Add a *Publisher* and then select **Next**. The other details on the App Information page are optional.

1. On the Program page, configure the following options:

   - For *Install command line*, specify **remotehelpinstaller.exe /quiet acceptTerms=1**
   - For *Uninstall command line*, specify **remotehelpinstaller.exe /uninstall /quiet acceptTerms=1**

    To opt out of automatic updates, specify enableAutoUpdates=0 as part of the install command **remotehelpinstaller.exe /quiet acceptTerms=1 enableAutoUpdates=0**

   > [!IMPORTANT]
   > The command line options *acceptTerms* and *enableAutoUpdates* are always case sensitive.

   You can leave the rest of the options at their default values and select **Next** to continue.

1. On the Requirements page, configure the following options to meet your environment, and then select **Next**:

   - *Operating system architecture*
   - *Minimum operating system*

1. On the Detection rules page, for *Rules format*, select **Manually configure detection rules**, and then select **Add** to open the *Detection rule* pane. Configure the following options:

   - For *Rule type*, select **File**
   - For *Path*, specify **C:\Program Files\Remote Help**
   - For *File or folder*, specify **RemoteHelp.exe**
   - For *Detection method*, select **String (version)**
   - For *Operator*, select **Greater than or equal to**
   - For *Value*, specify the Remote Help version that you're deploying. For example, **10.0.22467.1000**. See the following note for details on how to get the Remote Help version.
   - Leave *Associated with a 32-bit app on 64-bit clients* set to **No**

> [!NOTE]
> To get the version of the **RemoteHelp.exe**, install RemoteHelp manually to a machine and run the following Powershell command **(Get-Item "$env:ProgramFiles\Remote Help\RemoteHelp.exe").VersionInfo**. From the output make a note of the FileVersion and use it to specify the *Value* in the detection rule.

1. Proceed to the Assignments page, and then select an applicable device group or device groups that should install the Remote Help app. Remote Help is applicable when targeting group(s) of devices and not for User groups.

1. Complete creation of the Windows app to have Intune deploy and install Remote Help on applicable devices.

#### Windows Firewall details

Automatic firewall rule creation from the Remote Help installer has been removed. However, if needed, System administrators can create firewall rules.

Depending on the environment that Remote Help is utilized in, it may be necessary to create firewall rules to allow Remote Help through the Windows Firewall. In some situations when it's necessary, the following Remote Help executables should be allowed through the firewall:

- C:\Program Files\Remote help\RemoteHelp.exe
- C:\Program Files\Remote help\RHService.exe
- C:\Program Files\Remote help\RemoteHelpRDP.exe

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macOS)

#### Install and update Remote Help native app

The Remote Help native app is available to download from Microsoft and must be installed on the device you're trying to help before that device can be used to participate in a Remote Help session.

> [!TIP]
> The native app is only required if full control of the helpers device is required, otherwise you can use [Remote Help web app](remote-help-webapp.md).

#### Deploy macOS Remote Help

For enrolled devices, you can streamline the user experience by installing Remote Help on behalf of your users.

For more information on installing Remote Help through Intune as a required install, see [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md).

For more information on making Remote Help available in Company Portal for the user to install, see [How to add macOS line-of-business apps to Microsoft Intune](../apps/lob-apps-macos.md).

#### Update Remote Help

Remote Help receives the latest versions through the [Microsoft AutoUpdate (MAU) application](/DeployOffice/mac/update-office-for-mac-using-msupdate#application-identifiers). Users can opt in for automatic updates to ensure Remote Help is up to date.

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

To set up Remote Help for Android, you need to complete the following steps:

1. Deploy the Remote Help app.

2. Grant permissions.

   - Configure camera permissions.

   - Configure permission setup for Zebra devices.

   - Configure permission setup for Samsung devices.

#### Deploy Remote Help app

1. Using Managed Google Play, add the [Remote Help app from Microsoft](https://play.google.com/store/apps/details?id=com.microsoft.intune.remotehelp).

2. On devices that you want to use Remote Help, assign the app as **Required**. This setting allows automatic installation of the app on those devices.

#### Grant permissions

To protect user privacy on the device, both the Android OS and device OEMs require certain permissions to be granted to the Remote Help app.

> [!NOTE]
> We do not recommend installing or allow-list apps capable of screen recording or mirroring if you intend to use unattended mode in your organization for risky operations.

##### Camera

The Remote Help app requires Camera permissions.

> [!NOTE]
> Remote Help doesn't store camera input. These permissions are only used to initiate a remote help session between the device and the Intune service.

You can autogrant them through app configuration policy:

1. Go to **Apps** > **Configuration** > **Create** a new policy for **Managed devices**.

2. Create the policy for **Android Enterprise** with type **Fully managed, Dedicated, and Corporate-Owned Work Profile Only**. Target the policy to the **Remote Help** app that you approved earlier.

3. Under **Permissions**, add **CAMERA** permissions. Then, set the permission state to **Auto grant**.

4. Assign the profile to the devices on which you want to use Remote Help.

##### Permission setup for Zebra devices

On Zebra devices, permissions are granted through Zebra OEMConfig profiles.

For instructions on how to set up OEMConfig, go to [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

If you're planning to use Remote Help on a device running on Android 11, you need to enable another Zebra package as a system app. For more information on how to enable system apps, see [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md)

|Build|System app to be enabled|
|--------|------------------------------|
|Any build of Android 11 that is earlier than 11-20-18.00-RG-U00 |com.symbol.tool.stagenow|
|11-20-18.00-RG-U00 or 11-20-18.00-RG-U02|com.zebra.devicemanager|
|Any build of Android 11 that is later than 11-20-18.00-RG-U02 |(None required)|

##### Instructions for Zebra OEMConfig powered by MX

*Zebra OEMConfig Powered by MX* is a new version of the OEMConfig app released in May 2023.

> [!NOTE]
> On Android 11, the new OEM Config schema (Zebra OEMConfig powered by MX) doesn't work if the BSP version is HE_FULL_UPDATE_11-20-18.00-RG-U00-STD-HEL-04. You must upgrade to a later BSP to use the new OEMConfig app. For instructions on updating supported Zebra devices with Intune, see [Zebra LifeGuard Over-the-Air Integration with Microsoft Intune](../protect/zebra-lifeguard-ota-integration.md)

Use OEMConfig to deploy the following settings on devices that you want to use Remote Help with:

1. Under **Permission Access Configuration**, configure the following details:

  | Key                      | Value                                           |
  |-----------------------------------|-----------------------------------------------|
  | Package Name | com.microsoft.intune.remotehelp  |
  | Package Signing Certificate | ```MIIGDjCCA/agAwIBAgIEUiDePDANBgkqhkiG9w0BAQsFADCByDELMAkGA1UEBhMCVVMxEzARBgNVBAgTCldhc2hpbmd0b24xEDAOBgNVBAcTB1JlZG1vbmQxHjAcBgNVBAoTFU1pY3Jvc29mdCBDb3Jwb3JhdGlvbjErMCkGA1UECxMiV2luZG93cyBJbnR1bmUgU2lnbmluZyBmb3IgQW5kcm9pZDFFMEMGA1UEAxM8TWljcm9zb2Z0IENvcnBvcmF0aW9uIFRoaXJkIFBhcnR5IE1hcmtldHBsYWNlIChEbyBOb3QgVHJ1c3QpMB4XDTEzMDgzMDE4MDIzNloXDTM2MTAyMTE4MDIzNlowgcgxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpXYXNoaW5ndG9uMRAwDgYDVQQHEwdSZWRtb25kMR4wHAYDVQQKExVNaWNyb3NvZnQgQ29ycG9yYXRpb24xKzApBgNVBAsTIldpbmRvd3MgSW50dW5lIFNpZ25pbmcgZm9yIEFuZHJvaWQxRTBDBgNVBAMTPE1pY3Jvc29mdCBDb3Jwb3JhdGlvbiBUaGlyZCBQYXJ0eSBNYXJrZXRwbGFjZSAoRG8gTm90IFRydXN0KTCCAiIwDQYJKoZIhvcNAQEBBQADggIPADCCAgoCggIBAKl5psvH2mb9nmMz1QdQRX3UFJrl4ARRp9Amq4HC1zXFL6oCzhq6ZkuOGFoPPwTSVseBJsw4FSaX21sDWISpx/cjpg7RmJvNwf0IC6BUxDaQMpeo4hBKErKzqgyXa2T9GmVpkSb2TLpL8IpLtkxih8+GB6/09DkXR10Ir+cE+Pdkd/4iV44oKLxTbLprX1Rspcu07p/4JS6jO5vgDVV9OqRLLcAwrlewqua9oTDbAp/mDldztp//Z+8XiY6j/AJCKFvn+cA4s6s5kYj/jsK4/wt9nfo5aD9vRzE2j2IIH1T0Qj6NLTNxB7+Ij6dykE8QHJ7Vd/Y5af9QZwXyyPdSvwqhvKafS0baSqy1gLaNLA/gc/1Sh/ASXaDEhKHHAsLChkVFCE7cPwKPnBHudNBmS6HQ6Zo3UMwYVQVe7u+6jjvfo4gqmZglMhhzhauekNrHV91E+GkY3NGH2cHDEbpbl0JAAdWsI4jtJSN8c9Y8lSX00D7KdQ2NJhYl7mJsS10/3Ex1HYr8nDRq/IlAhGdSVC/qc9RktfYiYcmfZ/Iel5n+KkQt1svrF1TDCHYg/bcC7BhCwlaoa4Nu0hvLHvSbrsnB+gKtovCCilswPwCnDdAYmSMnwsAtBwJXqxD6HXbBCNX4A+qUrR+sYhmFa8jIVzAXa4I3iTvVQkTvrf9YriP7AgMBAAEwDQYJKoZIhvcNAQELBQADggIBAEdMG13+y2OvUHP1lHP22CNXk5e2lVgKZaEEWdxqGFZPuNsXsrHjAMOM4ocmyPUYAlscZsSRcMffMlBqbTyXIDfjkICwuJ+QdD7ySEKuLA1iWFMpwa30PSeZP4H0AlF9RkFhl/J9a9Le+5LdQihicHaTD2DEqCAQvR2RhonBr4vOV2bDnVParhaAEIMzwg2btj4nz8R/S0Nnx1O0YEHoXzbDRYHfL9ZfERp+9I8rtvWhRQRdhh9JNUbSPS6ygFZO67VECfxCOZ1MzPY9YEEdCcpPt5rgMEKVh7VPH14zsBuky2Opf6rGGS1m1Q26edG9dPtnAYax5AIkUG6cI3tW957qmUVSnIvlMzt6+OMYSKf5R5fdPdRlH1l8hak9vMxO2l344HyD0vAmbk01dw44PhIfuoq2qNAIt3lweEhZna8m5s9r1NEaRTf1BrVHXloAM+sipd5vQNs6oezSCicU7vwvUH1hIz0FOiCsLPTyxlfHk3ESS5QsivJS82TLSIb9HLX07OyENRRm8cVZdDbz6rRR+UWn1ZNEM9q56IZ+nCIOCbTjYlw1oZFowJDCL1IH8i7nhKVGBWf7TfukucDzh8ThOgMyyv6rIPutnssxQqQ7ed6iivc1y4Graihrr9n2HODRo3iUCXi+G4kfdmMwp2iwJz+Kjhyuqf7lhdOld6cs``` |

2.For the package you created, under **Package > Permissions**, add a new permission as follows:

  | Key                      | Value                                           |
  |-----------------------------------|-----------------------------------------------|
  | Name| System Alert Window  |
  | State | Grant  |

3.For the package created in step 1, under **Package** > **Allowed Services**, add two allowed services:

- One allowed service with a Service Identifier of `com.zebra.eventinjectionservice` 

- Another allowed service with a Service Identifier of `com.zebra.remotedisplayservice` 

##### Instructions for Legacy Zebra OEMConfig

When you use Legacy Zebra OEMConfig the OEMConfig profiles are applied as one-off actions, not persistent policy states. Make sure to deploy the OEMConfig profile after the Remote Help app is installed on the device. Also, if you uninstall and reinstall the Remote Help app on the device, you'll need to re-apply these OEMConfig settings after the app is reinstalled. You can create a new OEMConfig profile and assign it to the device, or edit the previously created OEMConfig profile.

Use OEMConfig to deploy the following settings on devices that you want to use Remote Help:

1. Under Permission Access Configuration, configure the following details:

  | Name                      | Description                                           |
  |-----------------------------------|-----------------------------------------------|
  | Permission Access Action | Grant |
  | Grant Permission Access Action | System Alert Window |
  | Grant Application Package | com.microsoft.intune.remotehelp |
  | Grant Application Signature |```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```|

> [!NOTE]
> The OEMConfig setting requires version MX 10.4 and higher on the device. For devices running a lower MX version, the display overlay permission must be manually granted to the Remote Help app. Contact Zebra for specific steps on your device or refer to the setup instructions for this permission on Samsung devices.

2.In a separate transaction step, under Service Access Configuration, create the following details:

  | Name                      | Description                                           |
  |-----------------------------------|-----------------------------------------------|
  | Service Binding Action | Allow |
  | Allow Service Identifier | com.zebra.eventinjectionservice  |
  | Service Caller Action | Allow |
  | Allow Service Identifier | com.zebra.eventinjectionservice |
  | Allow Caller Package | com.microsoft.intune.remotehelp |
  | Allow Caller Signature | ```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```|

3.In another transaction step, under Service Access Configuration, configure the following details:

  | Name                      | Description                                           |
  |-----------------------------------|-----------------------------------------------|
  | Service Binding Action | Allow |
  | Allow Service Identifier | com.zebra.remotedisplayservice |
  | Service Caller Action | Allow |
  | Allow Service Identifier | com.zebra.remotedisplayservice |
  | Allow Caller Package | com.microsoft.intune.remotehelp |
  | Allow Caller Signature | ```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```|

> [!NOTE]
> This setting enables unattended access and is only available on Zebra devices running MX 9.3 or later.

#### Permission setup for Samsung devices

In this section:

- Display overlay permission
- Knox KLMS Agent consent

##### Display overlay permission

> [!IMPORTANT]
> If the device is in kiosk mode, designate the Settings app as a system app so it can launch. See [Granting overlay permissions to Managed Home Screen for Android Enterprise dedicated devices](https://techcommunity.microsoft.com/t5/intune-customer-success/granting-overlay-permissions-to-managed-home-screen-for-android/ba-p/3247041) for detailed instructions.

The Remote Help app needs the **Display over other apps** or **Appear on top** permission to display the Remote Help session UI. To grant this permission, create an OEMConfig profile that configures the permissions in the OEMConfig app.

##### Knox KLMS Agent consent

On some devices, the user also needs to agree to Samsung's KLMS Agent terms and conditions before the app can work.

1. After installing the Remote Help app, launch it. The prompt is automatically displayed when the app is launched.

2. Agree to the terms and conditions and tap **Confirm**.

> [!NOTE]
>
> - On Knox 2.8-3.7 (inclusive) this consent is revoked if the Remote Help app is uninstalled.
> - If the user agreed to KLMS license terms through another app, the prompt might not appear.

---

## Setup Conditional Access for Remote Help

This section outlines the steps for provisioning the Remote Help service on the tenant for Conditional Access.

1. Open PowerShell in admin mode.
    - It may be necessary to install [Microsoft Graph PowerShell](/powershell/microsoftgraph/installation) 
2. Within PowerShell enter the following commands:

### Installation

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

### Sign in

Use the `Connect-MgGraph` command to sign in with the required scopes. You'll need to sign in with an admin account to consent to the required scopes.
```powershell

Connect-MgGraph -Scopes "Application.ReadWrite.All"
```

### Create the service principal

Create a Service Principal using the `Remote Assistance Service` AppId "1dee7b72-b80d-4e56-933d-8b6b04f9a3e2".

```powershell
New-MgServicePrincipal -AppId "1dee7b72-b80d-4e56-933d-8b6b04f9a3e2"
```

```Output
DisplayName                                     Id AppId                                   ServicePrincipalType
----                                         ------- -----------                                   ---------------
RemoteAssistanceService                      3d5ff82b-a5f2-483a-xxxx-9514ed66f7c5        1dee7b72-b80d-4e56-933d-8b6b04f9a3e2
```

This output has been shortened for readability.

The ID corresponds to the app ID for the Remote Assistance Service.

The display name is **Remote Assistance Service**, which is the backend service for Remote Help. 

### Sign out

Use the `Disconnect-MgGraph` command to sign out.

```powershell
Disconnect-MgGraph
```

### Building a Conditional Access policy

After the Remote Help service principal is created, learn more on how to set up a [conditional access policy.](/entra/identity/conditional-access/concept-conditional-access-policies)

To apply conditional access policies to Remote Help, follow these steps:

1. Navigate to the conditional access policy that you created.
2. Select **Target resources**
     1. Select **Resources (formerly cloud apps)** to specify what this policy applies to.
     2. Select **Exclude**.
     3. Select **Select resources**.
     4. Under **Select**, check the **RemoteAssistanceService** with the app ID of 1dee7b72-b80d-4e56-933d-8b6b04f9a3e2

### Try an interactive demo

The [Remote Help]( https://regale.cloud/Microsoft/viewer/1746/remote-help/index.html#/0/0) interactive demo walks you through scenarios step-by-step with interactive annotations and navigation controls.

## Streamline macOS Native app operating system permissions

On macOS, applications that access and control the screen require permission. By default, users must accept these permissions. macOS allows some control capabilities for each type of privacy setting using *Privacy Preferences Policy Control*.

|Permission|MDM control capabilities|
|---|---|
|Accessibility|✅ Allow</br>✅ Allow Standard User To Set System Service</br></br>macOS allows this property to be set on behalf of the user to *Allow*, reducing the number of steps required to use the Remote Help native client|
|Screen sharing|✅ Allow Standard User To Set System Service</br></br>This permission by default requires administrator privileges to allow it. macOS doesn't allow this property to be set to *Allow* by MDM but you can enable the ability for standard users to accept this permission.|

With settings catalog, we can streamline the end users experience for allowing these permissions.

### [:::image type="icon" source="../media/icons/intune.svg"::: **Intune Admin Console**](#tab/intuneadminconsole)

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices > Manage devices > Configuration > Create > macOS > Settings catalog**
1. Enter a name and description for the profile. For example, "macOS Remote Help privacy permissions" and select **Next**
1. Select **Add settings** and in the settings picker, navigate to **Privacy > Privacy Preferences Policy Control > Services**
    1. Under **Accessibility** select:
      - **Authorization**
      - **Code Requirement**
      - **Identifer**
      - **Identifer type**
      - **Static code**
    1. Under **Screen Capture** select:
      - **Authorization**
      - **Code Requirement**
      - **Identifer**
      - **Identifer type**
      - **Static code**
1. Close the **Add settings** pane and select **+ Edit instance** under **Accessibility** and configure the following settings:

    | Name | Configuration |
    |---|---|
    | Authorization | Allow |
    | Code Requirement | `identifier "com.microsoft.remotehelp" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = UBF8T346G9` |
    | Identifier | com.microsoft.remotehelp |
    | Identifier type | bundle ID |
    | Static Code | False |

1. Select **Save** and select **+ Edit instance** under **Screen Capture** and configure the following settings:

    | Name | Configuration |
    |---|---|
    | Authorization | Allow Standard User To Set System Service |
    | Code Requirement | `identifier "com.microsoft.remotehelp" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = UBF8T346G9` |
    | Identifier | com.microsoft.remotehelp |
    | Identifier type | bundle ID |
    | Static Code | False |
1. Select **Next**, configure scope tags as required, assign the profile to groups as required, review settings and **Create** the policy.

### [:::image type="icon" source="../media/icons/graph.svg"::: **Microsoft Graph**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../includes/graph-explorer-intro.md)]

This will create a policy in your tenant with the name **_MSLearn_Example_macOS Remote Help - Privacy Preferences Policy Control**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_macOS Remote Help - Privacy Preferences Policy Control","description":"","platforms":"macOS","technologies":"mdm,appleRemoteManagement","roleScopeTagIds":["0"],"settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_com.apple.tcc.configuration-profile-policy","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_accessibility","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_authorization","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_authorization_0","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_coderequirement","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationStringSettingValue","value":"identifier \"com.microsoft.remotehelp\" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = UBF8T346G9"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_identifier","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationStringSettingValue","value":"com.microsoft.remotehelp"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_identifiertype","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_identifiertype_0","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_staticcode","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.tcc.configuration-profile-policy_services_accessibility_item_staticcode_false","children":[]}}]}]},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_screencapture","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_authorization","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_authorization_2","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_coderequirement","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationStringSettingValue","value":"identifier \"com.microsoft.remotehelp\" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = UBF8T346G9"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_identifier","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationStringSettingValue","value":"com.microsoft.remotehelp"}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_identifiertype","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_identifiertype_0","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_staticcode","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.tcc.configuration-profile-policy_services_screencapture_item_staticcode_false","children":[]}}]}]}]}]}]}]}}]}
```
[!INCLUDE [graph-explorer-steps](../includes/graph-explorer-steps.md)]

---

## Next steps

[Get support in Microsoft Intune admin center](../../get-support.md).
