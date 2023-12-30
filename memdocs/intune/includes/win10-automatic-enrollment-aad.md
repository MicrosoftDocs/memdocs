## Enable Windows automatic enrollment

If you enable MDM automatic enrollment, enrollment in Intune will occur when:  

* A Microsoft Entra user adds their work or school account to their personal device.
* A corporate-owned device joins to your Microsoft Entra ID. 

1. Sign in to [Microsoft Azure](https://portal.azure.com).  
2. Go to **Microsoft Entra ID** > **Mobility (MDM and MAM)**.  
3. Select **Microsoft Intune**.  

4. Configure **MDM User scope**. Specify which users' devices should be managed by Microsoft Intune. These Windows 10 devices can automatically enroll for management with Microsoft Intune.

   - **None** - MDM automatic enrollment disabled
   - **Some** - Select the **Groups** that can automatically enroll their Windows 10 devices
   - **All** - All users can automatically enroll their Windows 10 devices

      > [!IMPORTANT]
      > For Windows BYOD devices, the MAM user scope takes precedence if both the MAM user scope and the MDM user scope (automatic MDM enrollment) are enabled for all users (or the same groups of users). The device will not be MDM enrolled, and Windows Information Protection (WIP) Policies will be applied if you have configured them.
      >
      > If your intent is to enable automatic enrollment for Windows BYOD devices to an MDM: configure the MDM user scope to **All** (or **Some**, and specify a group) and configure the MAM user scope to **None** (or **Some**, and specify a group – ensuring that users are not members of a group targeted by both MDM and MAM user scopes).
      >
      >For [corporate devices](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices), the MDM user scope takes precedence if both MDM and MAM user scopes are enabled. The device will get automatically enrolled in the configured MDM.

   > [!NOTE]
   > MDM user scope must be set to a Microsoft Entra group that contains user objects.

   ![Screenshot shows the Azure portal, where you can configure M D M User scope.](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Use the default values for the following URLs:
    - **MDM Terms of use URL**
    - **MDM Discovery URL**
    - **MDM Compliance URL**

6. Select **Save**. 

## Multifactor authentication  

Two-factor authentication is not enabled for automatic enrollment by default. We recommend requiring multifactor authentication during device registration. For more information, see [Getting started with the Azure Multi-Factor Authentication Server](/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).  
