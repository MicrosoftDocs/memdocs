---
title: Troubleshooting Windows device enrollment problems in Microsoft Intune
titleSuffix: Microsoft Intune
description: Suggestions for troubleshooting some of the most common problems when you enroll Windows devices in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot Windows device enrollment problems in Microsoft Intune

This article helps Intune administrators understand and troubleshoot problems when enrolling Windows devices in Intune.

## Prerequisites
Before you start troubleshooting, it's important to collect some basic information. This information can help you better understand the problem and reduce the time to find a resolution.

Collect the following information about the problem:
- Is a valid Intune license assigned to the user? Before users can enroll their devices, they must have the necessary license assigned.
- Is the latest update installed on the Windows device? Some features in Intune only work with the latest version of Windows. There are many fixes for known issues available through Windows Update. Applying all the latest updates often fixes a Windows device enrollment problem. 
- What is the exact error message?
- Where do you see the error message?
- When did the problem start? Has enrollment ever worked? 
- What platform (Android, iOS/iPadOS, Windows) has the problem?
- How many users are affected? Are all users affected or just some?
- How many devices are affected? Are all devices affected or just some?
- What is the MDM authority?
- How is enrollment being performed? Is it "Bring your own device" (BYOD) or Apple Automated Device Enrollment (ADE) with enrollment profiles?

## Error messages

### This user is not authorized to enroll.

Error 0x801c003: "This user is not authorized to enroll. You can try to do this again or contact your system administrator with the error code (0x801c0003)."
Error 80180003: "Something went wrong. This user is not authorized to enroll. You can try to do this again or contact your system administrator with error code 80180003."

**Cause:** Any of the following conditions: 

- The user has already enrolled the maximum number of devices allowed in Intune.    
- The device is blocked by the device type restrictions.    
- The computer is running Windows 10 Home. However, enrolling in Intune or joining Azure AD is only supported on Windows 10 Pro and higher editions.

#### Resolution
There are several possible solutions to this issue:

##### Remove devices that were enrolled
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).    
2. Go to **Users** > **All Users**.    
3. Select the affected user account, and then click **Devices**.    
4. Select any unused or unwanted devices, and then click **Delete**. 

##### Increase the device enrollment limit

> [!NOTE]
> This method increases the device enrollment limit for all users, not just the affected user.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **Enrollment restrictions** > **Default** (under **Device limit restrictions**) > **Properties** > **Edit** (next to **Device limit**) > increase the **Device limit** (maximum 15)> **Review + Save**.    
 

##### Check device type restrictions
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with a global administrator account.
2. Go to **Devices** > **Enrollment restrictions**, and then select the **Default** restriction under **Device Type Restrictions**.    
3. Select **Platforms**, and then select **Allow** for **Windows (MDM)**.

    > [!IMPORTANT]
    > If the current setting is already **Allow**, change it to **Block**, save the setting, and then change it back to **Allow** and save the setting again. This resets the enrollment setting.

4. Wait for approximately 15 minutes, and then enroll the affected device again.    

##### Upgrade Windows 10 Home
[Upgrade Windows 10 Home to Windows 10 Pro](https://support.microsoft.com/help/12384/windows-10-upgrading-home-to-pro) or a higher edition. 



### This user is not allowed to enroll.

Error 0x801c0003: "This user is not allowed to enroll. You can try again or contact your system administrator with the error code 801c0003."

**Cause:** The **Users may join devices to Azure AD** setting is set to **None**. This prevents new users from joining their devices to Azure AD. Therefore Intune enrollment fails.

#### Resolution
1. Sign in to the [Azure portal](https://portal.azure.com/) as administrator.    
2. Go to **Azure Active Directory** > **Devices** > **Device Settings**.    
3. Set **Users may join devices to Azure AD** to **All**.    
4. Enroll the device again.   

### The device is already enrolled.

Error 8018000a: "Something went wrong. The device is already enrolled.  You can contact your system administrator with the error code 8018000a."

**Cause:** One of the following conditions is true:
- A different user has already enrolled the device in Intune or joined the device to Azure AD. To determine whether this is the case, go to **Settings** > **Accounts** > **Work Access**. Look for a message that's similar to the following: "Another user on the system is already connected to a work or school. Please remove that work or school connection and try again."    

#### Resolution

Use one of the following methods to resolve this issue:

##### Remove the other work or school account
1. Sign out of Windows, then sign in by using the other account that has enrolled or joined the device.    
2. Go to **Settings** > **Accounts** > **Work Access**, then remove the work or school account.
3. Sign out of Windows, then sign in by using your account.    
4. Enroll the device in Intune or join the device to Azure AD. 



### This account is not allowed on this phone.

Error: "This account is not allowed on this phone. Make sure the information you provided is correct, and then try again or request support from your company."

**Cause:** The user who tried to enroll the device doesn't have a valid Intune license.

#### Resolution
Assign a valid Intune license to the user, and then enroll the device.


### Looks like the MDM Terms of Use endpoint is not correctly configured.

**Cause:** One of the following conditions is true: 
 - You use both Mobile Device Management (MDM) for Office 365 and Intune on the tenant, and the user who tries to enroll the device doesn't have a valid Intune license or an Office 365 license.     
- The MDM terms and conditions in Azure AD is blank or doesn't contain the correct URL.    

#### Resolution

To fix this issue, use one of the following methods: 
 
##### Assign a valid license to the user
Go to the [Microsoft 365 Admin Center](https://admin.microsoft.com), and then assign either an Intune or an Office 365 license to the user.

##### Correct the MDM terms of use URL
  1. Sign in to the [Azure portal](https://portal.azure.com/), and then select **Azure Active Directory**.    
  2. Select **Mobility (MDM and MAM)**, and then click **Microsoft Intune**.    
  3. Select **Restore default MDM URLs**, verify that the **MDM terms of use URL** is set to **https://portal.manage.microsoft.com/TermsofUse.aspx**.    
  4. Choose **Save**.    


### Something went wrong.

Error 80180026: "Something went wrong. Confirm you are using the correct sign-in information and that your organization uses this feature. You can try to do this again or contact your system administrator with the error code 80180026."

**Cause:** This error can occur when you try to join a Windows 10 computer to Azure AD and both of the following conditions are true: 
- MDM automatic enrollment is enabled in Azure.    
- The Intune PC client (Intune PC agent) is installed on the Windows 10 computer.

#### Resolution
Use one of the following methods to address this issue:

##### Disable MDM automatic enrollment in Azure.
1. Sign in to the [Azure portal](https://portal.azure.com/).    
2. Go to **Azure Active Directory** > **Mobility (MDM and MAM)** > **Microsoft Intune**.    
3. Set **MDM User scope** to **None**, and then click **Save**.    
     
##### Uninstall
Uninstall the Intune PC client agent from the computer.    

### The software cannot be installed.

Error: "The software cannot be installed, 0x80cf4017."

**Cause:** The client software is out of date.

#### Resolution
1. Sign in to [https://admin.manage.microsoft.com](https://admin.manage.microsoft.com).    
2. Go to **Admin** > **Client Software Download**, and then click **Download Client Software**.    
3. Save the installation package, and then install the client software. 


### The account certificate is not valid and may be expired.

Error: "The account certificate is not valid and may be expired, 0x80cf4017."

**Cause:** The client software is out of date.

#### Resolution
1. Sign in to [https://admin.manage.microsoft.com](https://admin.manage.microsoft.com).    
2. Go to **Admin** > **Client Software Download**, and then click **Download Client Software**.    
3. Save the installation package, and then install the client software.    

### Your organization does not support this version of Windows. 

Error: "There was a problem. Your organization does not support this version of Windows.  (0x80180014)"

**Cause:** Windows MDM enrollment is disabled in your Intune tenant.

#### Resolution
To fix this issue in a stand-alone Intune environment, follow these steps: 
 
1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), chooses **Devices** > **Enrollment restrictions** > choose a device type restriction.    
2. Choose **Properties** > **Edit** (next to **Platform settings**) > **Allow** for **Windows (MDM)**.    
3. Click **Review + Save**.    

### A setup failure has occurred during bulk enrollment.

**Cause:** The Azure AD user accounts in the account package (Package_GUID) for the respective provisioning package aren't allowed to join devices to Azure AD. These Azure AD accounts are automatically created when you set up a provisioning package with Windows Configuration Designer (WCD) or the Set up School PCs app, and these accounts are then used to join the devices to Azure AD.

#### Resolution
1. Sign in to the [Azure portal](https://portal.azure.com/) as administrator.    
2. Go to **Azure Active Directory > Devices > Device Settings**.    
3. Set **Users may join devices to Azure AD** to **All** or **Selected**.

   If you choose **Selected**, click **Selected**, and then click **Add Members** to add all users who can join their devices to Azure AD. Make sure that all Azure AD accounts for the provisioning package are added.
 
For more information about how to create a provisioning package for Windows Configuration Designer, see [Create a provisioning package for Windows 10](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-create-package).

For more information about the Set up School PCs app, see [Use the Set up School PCs app](https://docs.microsoft.com/education/windows/use-set-up-school-pcs-app).


### Auto MDM Enroll: Failed 

When you try to enroll a Windows 10 device automatically by using Group Policy, you experience the following issues: 
- In Task Scheduler, under **Microsoft** > **Windows** > **EnterpriseMgmt**, the last run result of the **Schedule created by enrollment client for automatically enrolling in MDM from AAD** task is as follows: **Event 76 Auto MDM Enroll: Failed (Unknown Win32 Error code: 0x8018002b)**       
- In Event Viewer, the following event is logged under **Applications and Services Logs/Microsoft/Windows/DeviceManagement-Enterprise-Diagnostics-Provider/Admin**:   
    ```asciidoc
    Log Name: Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider/Admin
    Source: DeviceManagement-Enterprise-Diagnostics-Provider
    Event ID: 76
    Level: Error
    Description: Auto MDM Enroll: Failed (Unknown Win32 Error code: 0x80180002b)
    ```
**Cause:** One of the following conditions is true: 
- The UPN contains an unverified or non-routable domain, such as .local (like joe@contoso.local).    
- **MDM user scope** is set to **None**. 

#### Resolution
If the UPN contains an unverified or non-routable domain, follow these steps: 

1. On the server that Active Directory Domain Services (AD DS) runs on, open **Active Directory Users and Computers** by typing **dsa.msc** in the **Run** dialog, and then click **OK**.    
2. Click **Users** under your domain, and then do the following:  
    - If there's only one affected user, right-click the user, and then click **Properties**. On the **Account** tab, in the UPN suffix drop-down list under **User logon name**, select a valid UPN suffix such as contoso.com, and then click **OK**.    
    - If there are multiple affected users, select the users, in the **Action** menu, click **Properties**. On the **Account** tab, select the **UPN suffix** check box, select a valid UPN suffix such as contoso.com in the drop-down list, and then click **OK**.
3. Wait for the next synchronization, or force a Delta Sync from the Synchronization Server by running the following commands in an elevated PowerShell prompt:
    ```powershell
    Import-Module ADSync
    Start-ADSyncSyncCycle -PolicyType Delta
    ```

If **MDM user scope** is set to **None**, follow these steps: 
 
1. Sign in to the [Azure portal](https://portal.azure.com/), and then select **Azure Active Directory**.
2. Select **Mobility (MDM and MAM)**, and then select **Microsoft Intune**.    
3. Set **MDM user scope** to **All**. Or, set **MDM user scope** to **Some**, and select the Groups that can automatically enroll their Windows 10 devices.    
4. Set **MAM User scope** to **None**.


### An error occurred while creating Autopilot profile.

**Cause:** The device name template's specified naming format doesn't meet the requirements. For example, you use lowercase for the serial macro, such as %serial% instead of %SERIAL%.

#### Resolution

Make sure that the naming format meets the following requirements:

- Create a unique name for your devices. Names must be 15 characters or less, and can contain letters (a-z, A-Z), numbers (0-9), and hyphens (‐).
- Names can't be all numbers.
- Names can't contain blank space.
- Use the %SERIAL% macro to add a hardware-specific serial number. Or, use the %RAND:<# of digits>% macro to add a random string of numbers, the string contains <# of digits> digits. For example, MYPC-%RAND:6% generates a name such as MYPC-123456.

### Something went wrong. OOBEIDPS.

**Cause:** This issue occurs if there's a proxy, firewall, or other network device that's blocking access to the Identity Provider (IdP).

#### Resolution
Make sure that the required access to internet-based services for Autopilot isn't blocked. For more information, see [Windows Autopilot networking requirements](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements-network).

### Autopilot device enrollment failed with error HRESULT = 0x80180022

**Cause:** The device being provisioned is running Windows Home Edition

#### Resolution
Update the device to Pro edition or higher

### Registering your device for mobile management (Failed:3, 0x801C03EA).

**Cause:** The device has a TPM chip that supports version 2.0, but hasn't yet been upgraded to version 2.0.

#### Resolution
Upgrade the TPM chip to version 2.0.

If the issue persists, check whether the same device is in two assigned groups, with each group being assigned a different Autopilot profile. If it is in two groups, determine which Autopilot profile should be applied to the device, and then remove the other profile's assignment.

For more information about how to deploy a Windows device in kiosk mode with Autopilot, see [Deploying a kiosk using Windows Autopilot](https://blogs.technet.microsoft.com/mniehaus/2018/06/07/deploying-a-kiosk-using-windows-autopilot/).


### Securing your hardware (Failed: 0x800705b4).

Error 800705b4: 
```
Securing your hardware (Failed: 0x800705b4)
Joining your organization's network (Previous step failed)
Registering your device for mobile management (Previous step failed)
```

**Cause:** The targeted Windows device doesn't meet either of the following requirements:

- The device must have a physical TPM 2.0 chip. Devices with virtual TPMs (for example, Hyper-V VMs) or TPM 1.2 chips don't work with self-deploying mode.
- The device must be running one of the following versions of Windows:
    - Windows 10 build 1709 or a later version.
    - If Hybrid Azure AD Join is used, Windows 10 build 1809 or a later version.


#### Resolution
Make sure that the targeted device meets both requirements that are described in the **Cause** section.

For more information about how to deploy a Windows device in kiosk mode with Autopilot, see [Deploying a kiosk using Windows Autopilot](https://blogs.technet.microsoft.com/mniehaus/2018/06/07/deploying-a-kiosk-using-windows-autopilot/).


### Something went wrong. Error Code 80070774.

Error 0x80070774: Something went wrong. Confirm you are using the correct sign-in information and that your organization uses this feature. You can try to do this again or contact your system administrator with the error code 80070774.

This issue typically occurs before the device is restarted in a Hybrid Azure AD Autopilot scenario, when the device times out during the initial Sign in screen. It means that the domain controller can't be found or successfully reached because of connectivity issues. Or that the device has entered a state which can't join the domain.

**Cause:** The most common cause is that Hybrid Azure AD Join is being used and the Assign user feature is configured in the Autopilot profile. Using the Assign user feature performs an Azure AD join on the device during the initial sign-in screen which puts the device in a state where it can't join your on-premises domain. Therefore, the Assign user feature should only be used in standard Azure AD Join Autopilot scenarios.  The feature should be not used in Hybrid Azure AD Join scenarios.

Another possible cause for this error is that the Autopilot object's associated AzureAD device has been deleted. To resolve this, delete the Autopilot object and reimport the hash to generate a new one.

#### Resolution

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose >  **Devices** > **Windows** > **Windows devices**.
2. Select the device which is experiencing the issue > click the ellipsis (…) on the rightmost side.
3. Select **Unassign user** and wait for the process to finish.
4. Verify that the Hybrid Azure AD Autopilot profile is assigned before re-attempting OOBE.

#### Second resolution
If the issue persists, on the server that hosts the Offline Domain Join Intune Connector, check to see if Event ID 30312 is logged within the ODJ Connector Service log. Event 30312 resembles the following:

```
Log Name:      ODJ Connector Service
Source:        ODJ Connector Service Source
Event ID:      30132
Level:         Error
Description:
{
          "Metric":{
                   "Dimensions":{
                             "RequestId":"<RequestId>",
                             "DeviceId":"<DeviceId>",
                             "DomainName":"contoso.com",
                             "ErrorCode":"5",
                             "RetryCount":"1",
                              "ErrorDescription":"Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation",
                              "InstanceId":"<InstanceId>",
                              "DiagnosticCode":"0x00000800",
                              "DiagnosticText":"Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation [Exception Message: \"DiagnosticException: 0x00000800. Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation\"] [Exception Message: \"Failed to call NetProvisionComputerAccount machineName=<ComputerName>\"]"
                   },
                   "Name":"RequestOfflineDomainJoinBlob_Failure",
                   "Value":0
          }
}
```

This issue is usually caused by incorrectly delegating permissions to the organizational unit where the Windows Autopilot devices are created. For more information, see [Increase the computer account limit in the Organizational Unit](windows-autopilot-hybrid.md#increase-the-computer-account-limit-in-the-organizational-unit).

1. Open **Active Directory Users and Computers (DSA.msc)**.
2. Right-click the organizational unit that you will use to create hybrid Azure AD-joined computers > **Delegate Control**.
3. In the **Delegation of Control** wizard, select **Next** > **Add** > **Object Types**.
4. In the **Object Types** pane, select the **Computers** check box > **OK**.
5. In the **Select Users**, **Computers**, or **Groups** pane, in the **Enter the object names to select** box, enter the name of the computer where the Connector is installed.
6. Select **Check Names** to validate your entry > **OK** > **Next**.
7. Select **Create a custom task to delegate** > **Next**.
8. Select the **Only the following objects in the folder** check box, and then select the **Computer objects**, **Create selected objects in this folder**, and **Delete selected objects in this folder** check boxes.
9. Select **Next**.
10. Under **Permissions**, select the **Full Control** check box. This action selects all the other options.
11. Select **Next** > **Finish**.

### The Enrollment Status Page times out before the sign-in screen

**Cause:** This issue can arise if all the following conditions are true:
- You're using the Enrollment Status Page to track Microsoft Store for Business apps.
- You have an Azure AD Conditional Access policy that uses the require a device to marked as compliant control.
- The policy applies to All Cloud apps and Windows.

#### Resolution:
Try either of the following:
- Target your Intune compliance policies to devices. Make sure that compliance can be determined before the user logs on.
- Use offline licensing for store apps. This way, the Windows client doesn't have to check with the Microsoft Store before determining device compliance.

## Next steps

- [Troubleshoot device enrollment in Intune](troubleshoot-device-enrollment-in-intune.md)
- [Ask a question on the Intune forum](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Check the Microsoft Intune Support Team Blog](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Check the Microsoft Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)
- [Get support for Microsoft Intune](../fundamentals/get-support.md)
- [Find co-management enrollment errors](https://docs.microsoft.com/configmgr/comanage/how-to-monitor#enrollment-errors)
