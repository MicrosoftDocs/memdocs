---
# required metadata
title: Prerequisites for organizational messages | Microsoft Intune  
description: Find out what's required to use organizational messages in Microsoft Intune.        
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/31/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure 
ms.collection:
- tier2
- M365-identity-device-management
---

# Organizational messages prerequisites   

*Applies to Windows 11*   

This article describes the tenant, message, and configuration requirements for organizational messages. Employees will not receive messages until you complete all prerequisites.  
## Version requirements  
Organizational messages are supported on devices running [Windows 11, version 22H2 or later](https://blogs.windows.com/windowsexperience/2022/09/20/how-to-get-the-windows-11-2022-update/).   

## Licensing requirements  
The organizational message feature is included with the following licenses:  

* Microsoft 365 E3  
* Microsoft 365 E5  
* Windows 10/11 Enterprise E3 with Microsoft Intune Plan 1    
* Windows 10/11 Enterprise E5 with Microsoft Intune Plan 1 

For more information about license options, see [Microsoft Intune licensing](../fundamentals/licenses.md).  

## Role-based access control requirements  
To create organizational messages in Microsoft Intune, you must be assigned one of these roles: 

* Azure AD Global administrator  
* Intune administrator  
* Organizational messages manager (Microsoft Intune role)  
* Organizational messages writer (Azure AD role)  

You can also create a custom role for people managing organization messages by using role-based access control (RBAC). For more information about how to use built-in roles and custom roles, see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).    

## Logo requirements  
Logos must meet these requirements:  

* PNG file 
* Transparent background 
* Size requirements:    
    * Taskbar messages: 64 x 64 pixels  
    * Notification area messages: 48 x 48 pixels
    * Get Started app messages: 50 pixels long x 50 - 100 pixels wide  

## Policy requirements  
There are certain experience and Windows Spotlight policies in Microsoft Intune that block the delivery of organizational messages. This section describes how to adjust all settings so that delivery is always allowed and works as intended. 

### Organizational messages delivery policy  
> [!IMPORTANT]
> This policy is required for devices running [Windows 11, version 22H2, build 10.0.22621.900](https://support.microsoft.com/help/5020044) and later. If you don't enable this policy, these devices can't receive organizational messages. The policy isn't required on devices running earlier builds.  

Enable the delivery of organizational messages in all new and existing policies that are targeted at users and devices receiving organizational messages.  

 1. Go to **Settings catalog** > **Experience** > **Enable delivery of organizational messages (User)**.  
 2. For **Enable delivery of organizational messages**, switch the toggle to **Enabled**.  

### Windows Spotlight policy       
 Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and configure the Windows Spotlight policies using a Microsoft Intune [device restrictions profile template](../configuration/device-restrictions-configure.md) or the [settings catalog](../configuration/settings-catalog.md). Make sure to adjust these policies in all new and existing policies that are targeted at users and devices receiving organizational messages.  

> [!NOTE]
> If you use the Windows 10/11 MDM security baseline, you will need to change the **Windows Spotlight** policy to **Not configured**. The Windows Spotlight policy controls organizational messages and messages coming from Microsoft. To continue blocking messages from Microsoft as defined in the Windows 10/11 MDM security baseline, [configure the Microsoft messaging policy](organizational-messages-prerequisites.md#microsoft-messaging-policy).

#### Template profiles    
Go to **Devices** > **Windows** > **Configuration profiles**, and in a new or existing template profile select **Device restrictions** > **Windows Spotlight**.    

* To allow taskbar messages:   
  * **Windows Spotlight**: Select **Not configured**.    
  * **Windows Tips**: Select **Not configured**.    
* To allow notification area messages:  
  * **Windows Spotlight**: Select **Not configured**.  
  * **Windows Spotlight in action center**: Select **Not configured**.  
* To allow Get Started app messages: 
  * **Windows Spotlight**: Select **Not configured**.      

#### Settings catalog profiles        
In a new or existing Windows configuration profile, select **Settings catalog** > **Add settings**. Use the **Settings picker** to add the settings to your profile. Then adjust the setting toggles as needed under **Configuration settings**.      

All of these settings are in the settings catalog, in the **Experience** category.  

* To allow taskbar messages:  
  * Add **Allow Windows Spotlight (User)**: Switch the toggle to **Allow**.    
  * Add **Allow Windows Tips**: Switch the toggle to **Allow**.  
* To allow notification area messages:    
  * Add **Allow Windows Spotlight (User)**: Switch the toggle to **Allow**.  
  * Add **Allow Windows Spotlight on Action Center (User)**: Switch the toggle to **Allow**.  
* To allow Get Started app messages:  
  * Add **Allow Windows Spotlight (User)**: Switch the toggle to **Allow**.   
  * Add **Disable Cloud Optimized Content**: Switch the toggle to **Disabled**.   

#### Policy CSP   
The configuration service provider (CSP) policies available for Windows 11 include:  
* [Experience/AllowWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight) 
* [Experience/AllowWindowsTips](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)   
* [Experience/AllowWindowsSpotlightOnActionCenter](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)  
* [Experience/DisableCloudOptimizedContent](/windows/client-management/mdm/policy-csp-experience#experience-disablecloudoptimizedcontent)  

### Microsoft messaging policy        
If you currently block messages that come from Microsoft, you can continue to do so while also allowing organizational messages to come through.  

1.  Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Tenant administration** > **Organizational messages**.    
2. In the **Overview** tab, go to step 2 under **Before you create a message**.      
3. **Decide whether to block messages directly from Microsoft, while allowing admin messages to display**: Switch the toggle to **Allow** to allow both Microsoft messages and organizational messages. Switch the toggle to **Block** to block Microsoft messages and allow organizational messages.   

## Attention: New Azure AD tenants        
If you recently created your Azure AD tenant, the organizational messages feature won't be available to use right away. It will become available 36 to 64 hours after you create the tenant.   

## Next steps 
Now that prerequisites are complete, you can [create organizational messages](organizational-messages-create.md) in Microsoft Intune.    
