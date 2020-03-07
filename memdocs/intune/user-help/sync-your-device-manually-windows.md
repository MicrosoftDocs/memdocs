---
# required metadata

title: Manually sync your Windows device | Microsoft Docs
description:
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/24/2018
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: priyar
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Sync your Windows device manually

When app installation speed is less than ideal, initiate a manual device sync. Manual syncs force your device to connect with Intune for the latest updates and communications. Installation speed may increase after the device sync is complete.

Intune supports manual sync from the Company Portal app, desktop taskbar or Start menu, and from the device Settings app. Company Portal app functionality is supported on Windows 10 devices running the Creator's Update (1703) or later. 

All Windows devices can be synced from the device Settings app, including:

* [Windows 10 desktop](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   
* [Windows 10 Mobile](#windows-10-mobile)  
* [Windows Phone 8.1](#windows-phone-81)    

## Sync directly from Company Portal app for Windows
Complete these steps to manually sync any Windows 10 device running Creator's Update (version 1703) or later.

1. Open the Company Portal app on your device.

2. Select **Settings** > **Sync**.

    ![Screenshot home page of Company Portal app, Settings highlighted](./media/RS1_homePage_settings_04.png)  
    
    ![Screenshot settings page of Company Portal app, Sync button highlighted](./media/RS1_settingspage_sync05.png)  

## Sync from device taskbar or Start menu   

You can also access the sync control outside of the app, from your device's desktop. This way is useful if you have the app pinned directly to your taskbar or Start menu, and want to quickly sync.  

1. Find the Company Portal app icon in your taskbar or Start menu.  
2. Right-click the app's icon so its menu (also referred to as a jump list) appears.  

    ![Screenshot of the Windows taskbar on a device's desktop. Company Portal app icon has been clicked to show a menu with options "Pin to taskbar," "Close window," and "Sync this device" action.](./media/sync-device-from-start-menu-1807.png)  

3. Select **Sync this device**. The Company Portal app opens to the **Settings** page and initiates your sync.  

## Sync from Settings App 
Complete these steps to manually sync your Microsoft HoloLens, Windows 10 desktop, Windows 10 Mobile, or Windows Phone 8.1 devices from the Settings app.  

### Windows 10 desktop
1. On your device, select **Start** > **Settings**.

2. Select **Accounts**.

    ![Choosing Accounts on the Settings page](./media/win10pc-sync-2-settings-accounts.png)  

3. Multiple versions of Windows 10 exist for desktops. Compare your screen to the screenshots below to determine which set of steps to follow. 

    * If your screen reads **Access work or school**, skip to the steps in [Access work or school](#access-work-or-school-steps).

    ![Access work or school option in settings app](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * If your screen reads **Work access**, skip to the steps under [Work access](#work-access-steps).  

    ![Choosing work access as the account type](./media/win10pc-sync-3-work-access.png)

#### Access work or school steps

1. Click **Access work or school**.

    ![Screenshot showing Access work or school option](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Select the account that has a briefcase icon next to it. If you don't see this account at all, your company may have configured your settings a different way. Instead, click the account that has a Microsoft logo next to it.

     ![Choose your account name next to the briefcase or Microsoft logo](./media/win10pc-rs1-sync-info-button.png)

3. Click **Info**. 

4. Click **Sync**. 

#### Work access steps

1. Click **Work access**.

    ![Choosing work access as the account type](./media/win10pc-sync-3-work-access.png)

2. Under **Enroll in to device management**, select the name of your company.

    ![Choosing the company name for device management](./media/win10pc-sync-4-tap-com-name.png)

3. Click **Sync**. The button remains disabled until the sync is complete.

    ![Choosing the Sync button](./media/win10pc-sync-5-tap-sync.png)  


### Windows 10 Mobile

   1. On your device, go to **All apps** > **Settings** > **Accounts**.

       ![Choosing Accounts on the Settings screen](./media/win10m-sync-1-settings-accounts.png)

   2. Select **Work access**.

       ![Choosing work access as the account type](./media/win10m-sync-2-work-access.png)

   3. Under **Enroll in to device management**, select your company name.

       ![Choosing the company name for device management](./media/win10m-sync-3-tap-comp-name.png)

   4. Select the **Sync** icon. The button remains disabled until the sync is complete.

       ![Choosing the Sync icon](./media/win10m-sync-4-tap-sync.png)  
### Microsoft HoloLens  
These instructions apply to HoloLens devices running the Windows 10 Anniversary Update (also known as RS1). 
1. Open the Settings app on your device.  

2. Select **Accounts** > **Work Access**.  
    ![Screenshot HoloLens settings app, accounts link highlighted](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Select your connected account > **Sync**.
    ![Screenshot HoloLens settings app, sync button highlighted](./media/RS1_holoLens_SyncRS1_Sync_08.png)  

### Windows Phone 8.1

1. Go to **All apps** > **Settings** > **workplace**.

    ![List of settings](./media/wp81-1-sync-settings-workplace.png)

2. Select the name of your company.

    ![Choosing the company name for the workplace account](./media/wp81-2-sync-tap-compname.png)

3. Select the **Sync** icon.

    ![Choosing the Sync icon](./media/wp81-3-sync-tap-sync-button.png)

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
