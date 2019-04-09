---
title: OneDrive for Business Profiles
titleSuffix: Configuration Manager
description: Redirect Windows known folders to OneDrive for Business
ms.date: 04/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# OneDrive for Business Profiles

Starting in Configuration Manager version 1902, you can create OneDrive for Business Profiles for moving Windows known folders to OneDrive for Business. These folders include Desktop, Documents, and Pictures. In each profile you can specify settings for moving the Windows known folders. For more information on OneDrive for Business, see [Redirect and move Windows known folders to OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## Prerequisites

- [Find your Office 365 tenant ID](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Deploy the OneDrive sync client version 18.111.0603.0004 or later. For more information, see [Deploy OneDrive apps by using System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="bkmk_odfb"></a> Redirect Windows known folders to OneDrive
<!--3556021-->
Use Configuration Manager to move Windows known folders to OneDrive for Business. These folders include Desktop, Documents, and Pictures. To simplify your Windows 10 upgrades, deploy these settings to Windows 7 clients before deploying a task sequence. 

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select the **OneDrive for Business Profiles** node.  

   ![OneDrive for Business Profiles node](media/onedrive-for-business-profiles-node.png)
2. In the ribbon, select **Create OneDrive for Business Profile**.  

3. Specify a name to identify this policy, and select **Next**.  

4. Select the platforms that will be provisioned with the OneDrive for Business profile. When you're finished selecting the platforms, click **Next**.

    ![Select platforms for the OneDrive for Business profile](media/onedrive-for-business-profile-select-platforms.png) 

5. On the **Settings** page:

    1. Specify your Office 365 tenant ID.  

    2. Select one of the following options to move the known folders to OneDrive:  

        - **Prompt users to move Windows known folders to OneDrive**: With this option, the user sees a wizard to move their files. If they choose to postpone or decline moving their folders, OneDrive periodically reminds them.  

        - **Silently move Windows known folders to OneDrive**: When this policy applies to the device, the OneDrive client automatically redirects the known folders to OneDrive for Business.  

            - **Show notification to users after folders have been redirected**: If you enable this option, the OneDrive client notifies the user after it moves their folders.  

    3. **Prevent users from redirecting their Windows known folders back to their PC**: Disables the option in OneDrive for Business on the client for users to move these folders back to the device.  

       ![OneDrive for Business Known Folder Move Settings](media/onedrive-for-business-profile-move-folder-settings.png)

6. Complete the wizard, then deploy the policy.  


## Deploy the OneDrive for Business Profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select the **OneDrive for Business Profiles** node.  


2. Select the profile, then select **Deploy** in the ribbon.

3. Specify the following settings for your deployment:

   1. **Collection** - Click **Browse...** then select the collection for which you want to deploy the profile.  
   1. --placeholder--
   1. ---placeholder--
 
    ![Deploy OneDrive for Business profile](media/onedrive-for-business-deploy-profile.png)


## Known issues

After you create a OneDrive for Business profile, the Configuration Manager console unexpectedly closes. The wizard successfully created the profile. The same behavior occurs when viewing a policy in the OneDrive for Business Profiles node. 

## Workaround
To manage these profiles, use the following PowerShell cmdlets:


```PowerShell
# View all OneDrive for Business profiles
Get-CMConfigurationPolicy -Fast | Where-Object { $_.CategoryInstance_UniqueIDs -eq "SettingsAndPolicy:SMS_OneDriveKnownFolderMigrationSettings" }

# Deploy a profile
# Use the LocalizedDisplayName property value of the policy as the CommonProfileName parameter.
New-CMConfigurationPolicyDeployment -CommonProfileName "my ODfB profile" -CollectionName "my collection"

# Delete a profile
Remove-CMConfigurationPolicy -Name "my ODfB profile"
```

For more information, see the following articles:
- [Get-CMConfigurationPolicy](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmconfigurationpolicy?view=sccm-ps)
- [New-CMConfigurationPolicyDeployment](https://docs.microsoft.com/powershell/module/ConfigurationManager/New-CMConfigurationPolicyDeployment?view=sccm-ps)
- [Remove-CMConfigurationPolicy](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmconfigurationpolicy?view=sccm-ps)

## Next steps
