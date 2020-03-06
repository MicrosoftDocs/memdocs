---
title: Troubleshooting Jamf Pro integration with Microsoft Intune
titleSuffix: Microsoft Intune
description: Suggestions for troubleshooting some of the most common problems when you integrate Jamf Pro for Mac devices, with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot integration of Jamf Pro with Microsoft Intune

This article helps Intune administrators understand and troubleshoot problems with integration of Jamf Pro for macOS with Intune.

> [!TIP]  
> Much of the information in this article originally appeared in [Troubleshoot problems when you integrate Jamf with Microsoft Intune](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) on support.microsoft.com.

## Prerequisites

Before you start troubleshooting, collect some basic information to clarify the problem and reduce the time to find a resolution. For example, when you encounter a Jamf-Intune integration-related issue, always verify that the prerequisites have all been met. Review the following considerations before you start troubleshooting:

- Review the prerequisites from [Integrate Jamf Pro with Intune](conditional-access-integrate-jamf.md#prerequisites).
- All users must have Microsoft Intune and Microsoft AAD Premium P1 licenses 
- You must have a user account that has Microsoft Intune Integration permissions in the Jamf Pro console.
- You must have a user account that has Global Admin permissions in Azure.


Consider the following information when investigating Jamf Pro integration with Intune: 
- What is the exact error message?
- Where is the error message?
- When did the problem start?  Has Jamf Pro integration with Intune ever worked?
- How many users are affected? Are all users affected or just some?
- How many devices are affected? Are all devices affected or just some?
 

## Common problems 

The following information can help you identify and resolve common problems for devices after you set up Intune and Jamf Pro integration.  

| Problem   | More information                  |
|-----------------|--------------------------|
| **Devices are marked as unresponsive in Jamf Pro**  | [Devices fail to check in with Jamf Pro or with Azure AD](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Mac devices prompt for keychain sign-in when you open an app Devices fail to register**  | [Users are prompted for for their password to allow apps to register with Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **Devices fail to register**  | The following causes might apply: <br> **-** [***Cause 1*** - The Jamf Pro app in Azure has incorrect permissions](#cause-1) <br> **-** [***Cause 2*** - There is an issue for the *Jamf Native macOS Connector* in Azure AD](#cause-2) <br> **-** [***Cause 3*** - The user doesn't have a valid Intune or Jamf license](#cause-3) <br> **-** [***Cause 4*** - The user didn't use Jamf Self Service to start the Company Portal app](#cause-4) <br> **-** [***Cause 5*** - Intune integration is turned off](#cause-5) <br> **-** [***Cause 6*** - The device was previously enrolled in Intune, or the user has tried to register the device multiple times](#cause-6) <br> **-** [***Cause 7*** - JamfAAD requests access to a "Microsoft Workplace Join Key" from the users' keychain](#cause-7) |
|  **Mac device shows compliant in Intune but noncompliant in Azure** | [Device registration issues](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Duplicate entries appear in the Intune console for Mac devices enrolled by using Jamf** | [Multiple registrations fro the same device](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **Compliance policy fails to evaluate the device** | [Policy targets device groups](#compliance-policy-fails-to-evaluate-the-device) |
| **Could not retrieve the access token for Microsoft Graph API** | The following causes might apply: <br> -[Permissions for the Jamf Pro app in Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Expired license for Jamf or Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Ports are not open](#the-required-ports-arent-open-on-your-network)|
 

### Devices are marked as unresponsive in Jamf Pro  

**Cause**: The following are common causes of devices being marked as *Unresponsive* by Jamf Pro:

- Device fails to check in with Jamf Pro.  
  Jamf Pro expects devices to check in every 15 minutes. Devices are marked as unresponsive by Jamf when they fail to check in over a 24-hour period.  

- Device fails to check in with Azure AD.  
  With successful registration to Azure AD, macOS devices receive an Azure token:
  - This token refreshes every 12 hours.   
  - When the token refresh fails for 24 hours or more, Jamf Pro marks the device as unresponsive.  
  - If the Azure token expires, users are prompted to sign in to Azure to obtain a new token. A refresh token for Azure access is generated every seven days.

**Resolution**  
After a device is marked as *Unresponsive* by Jamf Pro, the enrolled user of the device must sign in to correct the non-responsive state. It must be the user who has work-placed joined the account as they have the identity from Intune in their login keychain.



### Mac devices prompt for keychain sign-in when you open an app  

After you configure Intune and Jamf Pro integration and deploy conditional access policies, users of devices managed with Jamf Pro receive prompts for a password when opening Microsoft Office 365 applications, like Teams, Outlook, and other apps that require Azure AD authentication. 

For example, a prompt with text similar to the following example appears when opening Microsoft Teams:

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**Cause**: These prompts are generated by Jamf Pro for each applicable app that requires Azure AD registration. 

**Resolution**   
At the prompt, the user must provide their device password to sign in to Azure AD. Options include:
- **Deny** - Do not sign in and not use the app.
- **Allow** -  A one time sign-in. The next time the app opens, it prompts for sign-in again.
- **Always Allow** - The sign-in credentials are cached for the application. The next time the app opens, it doesn't prompt for sign-in.  

Selecting *Always Allow* for one app only approves that app for future sign-in. Additional apps prompt for authentication until they also are set as *Always Allow*. Cached credentials for one app can't be used by another app.  

### Devices fail to register  

There are several common causes for Mac devices that fail to register.  

#### Cause 1  

**The Jamf Pro enterprise application in Azure has the wrong permission or has more than one permission**  

  When you create the app in Azure, you must remove all default API permissions and then assign Intune a single permission of *update_device_attributes*. 

  **Resolution**  
  Review and if necessary correct the permissions for the Jamf app you created in Azure AD. See the procedure to [create an application for Jamf in Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### Cause 2  

**The **Jamf Native macOS Connector** app wasn't created in your Azure AD tenant or consent for the connector was signed by an account that doesn’t have global admin rights**  

  **Resolution**  
  See the *Configuring macOS Intune Integration* section in [Integrating with Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) on docs.jamf.com. 

#### Cause 3

**The user doesn't have a valid Intune or Jamf license**  

  Lack of a valid license can result in the following error, which indicates that the Jamf license is expired:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Resolution**
  - Jamf license: Contact Jamf for assistance to obtain a new license for Jamf.  
  - Intune license: Assign the user a valid license or contact Microsoft or your Partner for information about how to obtain a current license.

#### Cause 4  

**The user didn't use *Jamf Self Service* to start the Company Portal app**

For a device to successfully enroll and register with Intune through Jamf, the user must use Jamf Self Service to open the Intune Company Portal. If the user opens the company portal manually, the device enrolls and registers without its connection to Jamf.  

To determine which service the device used to enroll and register, look in the Company Portal app on the device. When registered through Jamf, you should receive a notification to open the Self-Service app to make changes.

In the Company Portal app, the user might see **`Not registered`**, and an entry similar to the following example might appear in the Company Portal logs:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Resolution**  
To change the registration source from Intune to Jamf:
1. [Unenroll the macOS device from Intune](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos). To avoid further complications for devices that aren't fully removed from Intune, see [*Cause 6*](#cause-6) in this list of causes.  

2. On the device, use Jamf Self Service to open the Company Portal app, and then enroll the device with Intune. This task requires you to have [used Jamf to deploy the Company Portal app for macOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro), and to have [created a policy in Jamf Pro that registers the users device with Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. When the portal opens, the first screen you see prompts you to Sign In. Use your work or school account  

4. The Company Portal confirms your account information and shows your Device Enrollment and Device Compliance statuses. Yellow triangles highlight the actions you need to take to secure your macOS device for school or work. Click Begin to start enrollment.  

5. If prompted, type in your computer's sign-in information.  
     
It might take a few minutes to enroll your device in management. During this time, you can do other things on your device. You'll receive a message after you've completed Company Access Setup to let you know you're done.

#### Cause 5  

**Intune integration is turned off**

If Intune integration is turned off, users receive a pop-up window in the Company Portal with the following message when they try to register a device:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

The Jamf Pro server sends a pulse to the Intune servers when integration is turned off that tells Intune that integration is disabled. 

**Resolution**  
Re-enable Intune integration within Jamf Pro. See [Configure Microsoft Intune Integration in Jamf Pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a>Cause 6  

**The device was previously enrolled in Intune, or the user has tried to register the device multiple times**

If a device is unenrolled from Jamf but not correctly removed from Intune, or several registration attempts are made, you might see multiple instances of the same device in the portal. This causes Jamf enrollment to fail.

**Resolution**  
1. On the Mac, start **Terminal**.
2. Run **sudo JAMF removemdmprofile**.
3. Run **sudo JAMF removeFramework**.
4. On the JAMF Pro server, delete the computer’s inventory record.
5. Delete the device from AzureAD.
6. Delete the following files on the device if they exist:
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Microsoft Session Transport Key (public AND private keys)
   - Microsoft Workplace Join Key (public AND private keys)
7. Remove anything from the keychain on the device that references *Microsoft*, *Intune*,  or *Company Portal*, including DeviceLogin.microsoft.com certificates. Remove *JAMF* references except for JAMF public and private key. 
   > [!IMPORTANT]  
   > Removing the public and private key will break device enrollment.

8. Delete any of the following entries that you find:  
   - Kind: Application password ; Account: com.microsoft.workplacejoin.thumbprint
   - Kind: Application password ; Account: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Kind: Certificate ; Issued by: MS-Organization-Access
   - Kind: Identity preference ; Name (ADFS STS URL if present): https://adfs\<DNSName>.com/adfs/ls
   - Kind: Identity preference ; Name: https://enterpriseregistration.windows.net
   - Kind: Identity preference ; Name: https://enterpriseregistration.windows.net/  
9. Restart the Mac device.
10. Uninstall Company Portal from the device.
11. Go to portal.manage.microsoft.com and delete out all the instances of the Mac device. Wait at least 30 minutes before you go to the next step.
12. Re-enroll the device in JAMF Pro.
13. Reopen Self Service and start Registration policy.


#### Cause 7  

**JamfAAD requests access to a "Microsoft Workplace Join Key" from the users' keychain**

During registration, the user of a macOS device receives the following prompt to allow JamfAAD access to a key from their keychain: 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
	
   To allow this, enter the “login” keychain password
```

**Resolution**  
To successfully register the device with Azure AD, Jamf requires the user to provide their account password, and select **Allow**.

This request is similar to the request for [Mac devices prompt for keychain sign-in when you open an app](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app), earlier in this article.  

 
### Mac device shows compliant in Intune but noncompliant in Azure  

**Cause**: The following conditions can cause a device to show as compliant in Intune but not as compliant in Azure:  
- The device isn’t registered correctly.  
- The device was registered multiple times without the necessary cleanup.

**Resolution**  
To resolve this issue, follow the resolution for [*Cause 6*](#cause-6) for  *Devices fail to register*, earlier in this article. 


### Duplicate entries appear in the Intune console for Mac devices enrolled by using Jamf  
 
**Cause**: A device is registered with Intune multiple times, typically being re-registered after being removed from Intune.  

When a device is removed from Intune and Jamf Pro integration, some data can be left behind which can cause successive registrations to create duplicate entries.  

**Resolution**  
To resolve this issue, follow the resolution for [*Cause 6*](#cause-6) for  *Devices fail to register*, earlier in this article. 

### Compliance policy fails to evaluate the device  

**Cause**: Jamf integration with Intune doesn’t support compliance policy that targets device groups. 

**Resolution**  
Modify compliance policy for macOS devices to be assigned to user groups. 


### Could not retrieve the access token for Microsoft Graph API

You receive the following error:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

The source of this error can be one of the following causes: 

#### There's a permission issue with the Jamf Pro application in Azure

While registering the Jamf Pro app in Azure, one of the following conditions occurred:  
- The app received more than one permission.
- The **Grant admin consent for *\<your company>*** option wasn't selected.  

**Resolution**  
See the resolution for Cause 1 for [Devices fail to register](#devices-fail-to-register), earlier in this article.

#### A license required for Jamf-Intune integration has expired

**Resolution**: See the resolution for Cause 3 for [Devices fail to register](#devices-fail-to-register). 

#### The required ports aren't open on your network

**Resolution**: Review the information for network ports in [Prerequisites](conditional-access-integrate-jamf.md#prerequisites) for integrating Jamf Pro with Intune.


## Next steps
Learn more about [integrating Jamf Pro with Intune](conditional-access-integrate-jamf.md)