## Enable Windows automatic enrollment  
1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
1. Go to **Devices** > **Enrollment**.     
1. Go to the **Windows** tab. Then select **Automatic Enrollment**.  

> [!IMPORTANT]
>  Automatic MDM enrollment is a premium Microsoft Entra feature available for Microsoft Entra ID Premium subscribers. If you can't see the automatic enrollment settings, select **Automatic MDM enrollment is available only for Microsoft Entra ID Premium subscribers** to activate a free trial.   
 
1. Select **Microsoft Intune**.   
1. Select the **MDM user scope**. Your options:  
   
   - **None** - Automatic MDM enrollment is disabled for all users. You can still manage devices in Microsoft Intune but users must first initiate MDM enrollment.  
   - **Some** - Automatic MDM enrollment is enabled for the users you select.    
   - **All** - Automatic MDM enrollment is enabled for all users.

    *MDM user scope* enables automatic MDM enrollment for Microsoft Entra users so that you can manage devices in Microsoft Intune.
   
   ![Screenshot shows the Azure portal, where you can configure M D M User scope.](../enrollment/media/windows-enroll/auto-enroll-scope.png)
 
1. For **WIP user scope**, select **None**.  If the WIP user scope is already configured, make sure the users in the MDM users scope aren't members of a WIP-targeted group.  
1. Use the Microsoft Intune default values for these URLs:   
   - **MDM Terms of use URL**
   - **MDM Discovery URL**
   - **MDM Compliance URL**
1. Select **Save**.    

   [!IMPORTANT]
      > For Windows BYOD devices, the WIP user scope takes precedence if both the WIP user scope and the MDM user scope are enabled for the same users. The device won't enroll in Microsoft Intune. Windows Information Protection (WIP) policies will be applied if you have them.
      >
      > If your intent is to enable automatic enrollment for Windows BYOD devices to an MDM: configure the MDM user scope to **All** (or **Some**, and specify a group) and configure the WIP user scope to **None** (or **Some**, and specify a group – ensuring that users are not members of a group targeted by both MDM and WIP user scopes).
      >
      >For [corporate devices](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices), the MDM user scope takes precedence if both MDM and WIP user scopes are enabled. The device will automatically enroll in Microsoft Intune.  

## Multifactor authentication  

Two-factor authentication is not enabled for automatic enrollment by default. We recommend requiring multifactor authentication during device registration. For more information, see [Getting started with the Azure Multi-Factor Authentication Server](/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).  
