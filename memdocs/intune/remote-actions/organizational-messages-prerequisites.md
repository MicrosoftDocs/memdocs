---
# required metadata
title: Prerequisites for organizational messages | Microsoft Intune  
description: Learn about the prerequisites for organizational messages.      
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/16/2022
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
ms.collection: M365-identity-device-management
---

# Organizational messages prerequisites   

*Applies to Windows 11*  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

This article describes the tenant, message, and configuration requirements for organizational messages. Employees will not receive messages until you complete all prerequisites.  

## Version requirements  
Organizational messages are supported on devices running [Windows 11, version 22H2 or later](https://blogs.windows.com/windowsexperience/2022/09/20/how-to-get-the-windows-11-2022-update/).   

## Licensing requirements  
The organizational message feature is included with the following licenses:  

* Microsoft 365 E3  
* Microsoft 365 E5  
* Endpoint Management + Security E3 and Windows Enterprise E3    
* Endpoint Management + Security E5 and Windows Enterprise E5  

For more information about license options, see [Microsoft Intune licensing](../fundamentals/licenses.md).  

## Role-based access control requirements  
To create organizational messages in Microsoft Intune, you must be assigned one of these roles: 

* Azure AD Global administrator  
* Intune administrator  
* Organizational messages manager (Microsoft Intune role)  
* Organizational messages writer (Azure AD role)  

For more information about role-based access control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).  

## Logo requirements  
Logos must meet these requirements:  

* PNG file 
* Transparent background 
* Size requirements:    
    * Taskbar messages: 64 x 64 pixels  
    * Notification area messages: 48 x 48 pixels
    * Get Started app messages: 50 pixels long x 50 - 100 pixels wide  

## URL requirements  
The domain for your custom destination URLs must be added to your list of verified Azure AD custom domain names. For more information, see [Add your custom domain - Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain#add-your-custom-domain-name-to-azure-ad).  

## Policy requirements  
There are certain experience and Windows Spotlight policies in Microsoft Intune that block the delivery of organizational messages. This section describes how to adjust all settings so that delivery is always allowed and works as intended. 

### Organizational messages delivery policy 
Enable the delivery of organizational messages in all new and existing policies that are targeted at users and devices receiving organizational messages. 

 1. Go to **Settings catalog** > **Experience** > **Enable delivery of organizational messages (User)**. 
 2. For **Enable delivery of organizational messages**, switch the toggle to **Enabled**.  

> [!NOTE]
> This policy is required for devices with http://support.microsoft.com/help/5020044 and later. If not enabled, devices will not receive organizational messages. The policy isn't required on devices running earlier builds.

### Windows Spotlight policy     
Configure these policies using a Microsoft Intune [device restrictions profile template](../configuration/device-restrictions-configure.md) or the [settings catalog](../configuration/settings-catalog.md). Make sure to adjust these policies in all new and existing policies that are targeted at users and devices receiving organizational messages. 

> [!NOTE]
> If you use the Windows 10/11 MDM security baseline, you will need to change the **Windows Spotlight** policy to **Not configured**. The Windows Spotlight policy controls organizational messages and messages coming from Microsoft. To continue blocking messages from Microsoft as defined in the Windows 10/11 MDM security baseline, [configure the Microsoft messaging policy](organizational-messages-prerequisites.md#microsoft-messaging-policy).

#### Template profiles    
Go to **Configuration profiles** > **Templates** > **Device restrictions** > **Windows Spotlight** to edit these settings.    

* To allow taskbar messages:   
  * **Windows Spotlight**: Select **Not configured**.    
  * **Windows Spotlight Tips**: Select **Not configured**.    
* To allow notification area messages:  
  * **Windows Spotlight**: Select **Not configured**.  
  * **Windows Spotlight on Action Center**: Select **Not configured**.  
* To allow Get Started app messages: 
  * **Windows Spotlight**: Select **Not configured**.      

#### Settings catalog profiles        
Go to the **Settings catalog** > **Experience** > **Allow Windows Spotlight (User)** to edit these settings.  

* To allow taskbar messages:  
  * **Allow Windows Spotlight (User)**: Select **Allow**.    
  * **Windows Spotlight Tips**: Select **Allow**. 
* To allow notification area messages:    
  * **Windows Spotlight (User)**: Select **Allow**.  
  * **Windows Spotlight on Action Center**: Select **Allow**.  
* To allow Get Started app messages:  
  * **Allow Windows Spotlight (User)**: Select **Allow**.   
   * **Disable Cloud Optimized Content**: Select **Disabled**.   

#### Policy CSP   
The configuration service provider (CSP) policies available for Windows 11 include:  
* [Experience/AllowWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight) 
* [Experience/AllowWindowsTips](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)   
* [Experience/AllowWindowsSpotlightOnActionCenter](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)  
* [Experience/DisableCloudOptimizedContent](/windows/client-management/mdm/policy-csp-experience#experience-disablecloudoptimizedcontent)  

### Microsoft messaging policy        
If you currently block messages that come from Microsoft, you can continue to do so while also allowing organizational messages to come through.  

1. Go to **Organizational messages (preview)**.    
2. In the **Overview** tab, go to step 2 under **Before you create a message**.      
3. **Decide whether to block messages directly from Microsoft, while allowing admin messages to display**: Switch the toggle to **Allow** to allow both Microsoft messages and organizational messages. Switch the toggle to **Block** to block Microsoft messages and allow organizational messages.   


## Next steps 
Now that prerequisites are complete, you can [create organizational messages](organizational-messages-create.md) in Microsoft Intune.    
