## Enable Windows automatic enrollment  
1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
1. Go to **Devices** > **Enrollment**.     
1. Go to the **Windows** tab. Then select **Automatic Enrollment**.  

   > [!NOTE]
   >  Automatic MDM enrollment is a premium Microsoft Entra feature available for Microsoft Entra ID Premium subscribers. If you can't see the automatic enrollment settings, select **Automatic MDM enrollment is available only for Microsoft Entra ID Premium subscribers** to activate a free trial.   
1. Select **Microsoft Intune**.   
1. Select the **MDM user scope**. This setting enables automatic MDM enrollment for Microsoft Entra users so that you can manage their devices in Microsoft Intune.

   Your options are:  
   
   - **None** - Automatic MDM enrollment is disabled for all users. You can still manage devices in Microsoft Intune but users must initiate MDM enrollment.  
   - **Some** - Automatic MDM enrollment is enabled for the users you select.    
   - **All** - Automatic MDM enrollment is enabled for all users. Their devices automatically enroll in Intune when they join or register with Microsoft Entra ID.  
      
      > [!TIP]
      > If your intent is to enable automatic MDM enrollment for Windows BYOD devices, configure the MDM user scope to **All** or **Some**. Then configure the WIP user scope to **None** or **Some**,  ensuring that users are not members of a group targeted by both user scopes). 
   
   ![Screenshot shows the Microsoft Entra MDM user scope.](../enrollment/media/windows-enroll/auto-enroll-scope.png)  
1. Use the Microsoft Intune default values for these URLs:   
   - **MDM Terms of use URL**
   - **MDM Discovery URL**
   - **MDM Compliance URL**  
 
1. For **WIP user scope**, select **None**. If the WIP user scope is set to any other value, make sure the selected users aren't a part of the MDM user scope. 
   
   > [!IMPORTANT]
    > If a user is included in both the MDM user scope and WIP user scope: 
    > - The MDM user scope takes precedence if they're on a corporate-owned device. The device automatically enrolls in Microsoft Intune when they set it up for work.  
    > - The WIP user scope takes precedence if they bring their own device. The device doesn't enroll in Microsoft Intune for device management. Microsoft Purview Information Protection policies are applied if you configured them.  

1. Select **Save**.    

## Multifactor authentication  

Two-factor authentication is not enabled for automatic enrollment by default. We recommend requiring multifactor authentication during device registration. For more information, see [Getting started with the Azure Multi-Factor Authentication Server](/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).  
