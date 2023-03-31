---
# required metadata

title: Sideload Windows apps
titleSuffix: Microsoft Intune 
description: Learn how to sign line-of-business apps so you can use Intune to deploy them.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: e44f1756-52e1-4ed5-bf7d-0e80363a8674

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier1
- M365-identity-device-management
- Windows
---
# Sign line-of-business apps so they can be deployed to Windows devices with Intune

As an Intune administrator, you can deploy line-of-business (LOB) Universal apps to Windows 8.1 Desktop or Windows 10/11 Desktop & Mobile devices, including the Company Portal app. To deploy *.appx* apps to Windows 8.1 Desktop or Windows 10/11 Desktop & Mobile devices you can use code-signing certificate from a public certification authority already trusted by your Windows devices, or you can use your own certificate authority. This process is called sideloading. Sideloading is installing, and then running or testing an app that isn't certified by the Microsoft Store. For example, an app that is internal to your company only.

 > [!NOTE]
 > Microsoft Intune will be ending support on October 21, 2022 for devices running Windows 8.1. Intune will no longer support Windows 8.1 sideloading.
 > 
 > Windows 8.1 Desktop requires either an enterprise policy to enable sideloading or the use of Sideloading Keys (automatically enabled for domain-joined devices). For more information, see [Windows 8 sideloading](/archive/blogs/scd-odtsp/windows-8-sideloading-requirements-from-technet).

## Windows 10/11 sideloading

In Windows 10/11, sideloading is different than in earlier versions of Windows:

- You can unlock a device for sideloading using an enterprise policy. Intune provides a device config policy called "Trusted app installation". Setting this to **allow** is all that is needed for devices that already trust the certificate used to sign the appx app.

- Symantec Phone certificates and Sideloading License keys are not required. However if an on-premises certificate authority is not available then you may need to obtain a code signing certificate from a public certification authority. For more information, see [Introduction to Code Signing](/windows/desktop/SecCrypto/cryptography-tools#introduction-to-code-signing).

### Code sign your app

The first step is to code sign your appx package. For details, see [Sign app package using SignTool](/windows/uwp/packaging/sign-app-package-using-signtool).

### Upload your app

Next, you must upload the signed appx file. For details, see [Add a Windows line-of-business app to Microsoft Intune](lob-apps-windows.md).

If you deploy the app as required to users or devices then you do not need the Intune Company Portal app. However if you deploy the app as available to users, then they can either use the Company Portal app from the Public Microsoft Store, use the Company Portal app from the Private Microsoft Store for Business, or you will need to sign and manually deploy the Intune Company Portal app.

### Upload the code-signing certificate

If your Windows 10/11 device does not already trust the certificate authority, then after you have signed your appx package and uploaded it to the Intune service, you need to upload the code signing certificate to Intune using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Click **Tenant administration** > **Connectors and tokens** > **Windows enterprise certificates**.
3. Select a file under **Code-signing certificate file**.
4. Select your *.cer* file and click **Open**.
5. Click **Upload** to add your certificate file to Intune.

Now any Windows 10/11 Desktop & Mobile device with an appx deployment by the Intune service will automatically download the corresponding enterprise certificate and the application will be allowed to launch after installation.

Intune only deploys the latest .cer file that was uploaded. If you have multiple appx files created by different developers that are not associated with your organization, then you will need to either have them provide unsigned appx files for signing with your certificate, or provide them the code signing certificate used by your organization.

## How to renew the Symantec enterprise code-signing certificate

The certificate used to deploy Windows Phone 8.1 mobile apps was discontinued on February 28 2019 and is no longer available for renewal from Symantec. Also, Intune has ended support for Windows 10 mobile as of August 10, 2020.

## How to install the updated certificate for line-of-business (LOB) apps

Windows Phone 8.1

The Intune service can no longer deploy LOB apps for this platform once the existing Symantec Mobile Enterprise code-signing certificate expires.

Windows 8.1 Desktop/Windows 10 Desktop & Mobile

If the cert period has expired then the appx files may stop launching. You should obtain a new .cer file and follow the instructions to code-sign each deployed appx file and re-upload all appx files and the updated .cer file to the Windows Enterprise Certificates section of the Intune in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Manually deploy Windows 10 Company Portal app

If you do not want to provide access to the Microsoft Store, you can manually deploy the Windows 10 Company Portal app directly from Intune even if you haven't integrated Intune with the Microsoft Store for Business (MSFB). Alternatively, if you have integrated, then you could deploy the Company Portal app using [deploy apps using MSFB](store-apps-windows.md).

 > [!NOTE]
 > This option will require deploying manual updates each time an app update is released.

1. Sign in to your account in the [Microsoft Store for Business](https://www.microsoft.com/business-store) and acquire the **offline license** version of the Company Portal app.  
2. Once the app has been acquired, select the app in the **Inventory** page.  
3. Select **Windows 10 all devices** as the **Platform**, then the appropriate **Architecture** and download. An app license file is not needed for this app.
   ![Image of Windows 10 X86 Package details for Download](./media/app-sideload-windows/Win10CP-all-devices.png)
4. Download all the packages under "Required Frameworks". This must be done for x86, x64, ARM, and ARM64 architectures – resulting in a total of 9 packages as shown below.

   ![Image of dependency files to Download ](./media/app-sideload-windows/Win10CP-dependent-files.png)
5. Before uploading the Company Portal app to Intune, create a folder (e.g., C:&#92;Company Portal) with the packages structured in the following way:
   1. Place the Company Portal package into C:\Company Portal. Create a Dependencies subfolder in this location as well.  
      ![Image of Dependencies folder saved with APPXBUN file](./media/app-sideload-windows/Win10CP-Dependencies-save.png)
   2. Place the nine dependencies packages in the Dependencies folder.  
      If the dependencies are not placed in this format, Intune will not be able to recognize and upload them during the package upload, causing the upload to fail with the following error.  
      <img alt="Error message - The Windows app dependency must be provided." src="./media/app-sideload-windows/Win10CP-error-message.png" width="200">
6. Return to Intune, then upload the Company Portal app as a new app. Deploy it as a required app to the desired set of target users.  

See [Deploying an appxbundle with dependencies via Microsoft Intune MDM](/archive/blogs/configmgrdogs/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm) for more information about how Intune handles dependencies for Universal apps.  

### How do I update the Company Portal on my users' devices if they have already installed the older apps from the store?

If your users have already installed the Windows 8.1 Company Portal apps from the Store, then they should be automatically updated to the new version with no action required from you or your user. If the update does not happen, ask your users to check that they have enabled autoupdates for Store apps on their devices.

### How do I upgrade my sideloaded Windows 8.1 Company Portal app to the Windows 10 Company Portal app?

Our recommended migration path is to delete the deployment for the Windows 8.1 Company Portal app by setting the deployment action to "Uninstall". Once this is done, the Windows 10 Company Portal app can be deployed using any of the above options.  

If you need to sideload the app and deployed the Windows 8.1 Company Portal without signing it with the Symantec Certificate, follow the steps in the Deploy directly via Intune section above to complete the upgrade.

If you need to sideload the app and you signed and deployed the Windows 8.1 Company Portal with the Symantec code-signing certificate, follow the steps in the section below.  

### How do I upgrade my signed and sideloaded Windows 8.1 Company Portal app to the Windows 10 Company Portal app?

Our recommended migration path is to delete the existing deployment for the Windows 8.1 Company Portal app by setting the deployment action to "Uninstall". Once this is done, the Windows 10 Company Portal app can be deployed normally.  

Otherwise, the Windows 10 Company Portal app needs to be appropriately updated and signed to ensure that the upgrade path is respected.  

If the Windows 10 Company Portal app is signed and deployed in this way, you will need to repeat this process for each new app update when it is available in the store. The app will not automatically update when the store is updated.  

Here's how you sign and deploy the app in this way:

1. Download the [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/intunecpscript). This script requires the Windows SDK for Windows 10 to be installed on the host computer. To download the Windows SDK, see [Windows 10 SDK for Windows 10](https://go.microsoft.com/fwlink/?linkid=162443).
2. Download the Windows 10 Company Portal app from the Microsoft Store for Business, as detailed above.  
3. Run the script with the input parameters detailed in the script header to sign the Windows 10 Company Portal app (extracted below). Dependencies do not need to be passed into the script. These are only required when the app is being uploaded to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

|       Parameter       |                                                                    Description                                                                    |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| InputWin10AppxBundle  |                                             The path to where the source appxbundle file is located.                                              |
| OutputWin10AppxBundle |                                                  The output path for the signed appxbundle file.                                                  |
|       Win81Appx       |                          The path to where the Windows 8.1 Company Portal (.APPX) file is located.                           |
|      PfxFilePath      |                                   The path to Symantec Enterprise Mobile Code Signing Certificate (.PFX) file.                                    |
|      PfxPassword      |                                     The password of the Symantec Enterprise Mobile Code Signing Certificate.                                      |
|      PublisherId      |      The Publisher ID of the enterprise. If absent, the 'Subject' field of the Symantec Enterprise Mobile Code Signing Certificate is used.       |
|        SdkPath        | The path to the root folder of the Windows SDK for Windows 10. This argument is optional and defaults to ${env:ProgramFiles(x86)}\Windows Kits\10 |

The script will output the signed version of the Windows 10 Company Portal app when it has finished running. You can then deploy the signed version of the app as an LOB app via Intune, which will upgrade the currently deployed versions to this new app.
