---
# required metadata

title: Windows device enrollment guide for  Microsoft Intune
description: Enroll Windows devices using automatic enrollment, Windows Autopilot, group policy, and co-management enrollment options in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/14/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: mawierci, heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Deployment guide: Enroll Windows devices in Microsoft Intune

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create.

You have the following options when enrolling Windows devices:

- [Windows 10 Automatic enrollment](#windows-10-automatic-enrollment)
- [Windows Autopilot](#windows-autopilot)
- [Group policy](#group-policy)
- [Co-management](#co-management-enrollment)

This article provides recommendations on the Windows enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll Windows devices](../enrollment/windows-enrollment-methods.md).

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]
## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## Windows 10 Automatic enrollment

Use for personal/BYOD and organization-owned devices running Windows 10 and newer. Automatic enrollment:

- Uses the **Access school or work** feature on the devices.
- Uses the enrollment options you configure in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

Depending on the options you configure, Azure AD Premium might be required.

You can also use this enrollment method to automatically bulk enroll devices with the Windows Configuration Designer app.

---
| Feature | Use this enrollment option when |
| --- | --- |
| You have Azure AD Premium | ✔️ |
| You'll use Conditional Access (CA) on devices enrolled using [bulk enrollment](../enrollment/windows-bulk-enroll.md). | ✔️ On Windows 10 1803 and newer, CA is available for Windows devices enrolled using bulk enrollment. <br/><br/> ❌ On Windows 10 1709 and older, CA isn't available for Windows devices enrolled using bulk enrollment. |
| Devices are personal or BYOD. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> Bulk enrollment is available for organization-owned devices, not personal/BYOD.|
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated. or shared device. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization admin can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| You use the optional device enrollment manager (DEM) account. | ✔️ |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |

---

### Automatic enrollment administrator tasks

- Be sure your devices are running Windows 10 and newer. For a complete list, see [supported device platforms](supported-devices-browsers.md).
- Optional. Instead of users entering the Intune server name, you can create a CNAME record that's easier to enter, such as `EnterpriseEnrollment.contoso.com`. CNAME records associate a domain name with a specific server. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), test your CNAME record to make sure it's configured correctly. For more information, see [create a CNAME record](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Windows Enrollment** > **Automatic Enrollment**. In the configuration, you set the **MDM user scope** and **MAM user scope**:

  - **MDM user scope**: When set to **Some** or **All**, devices are joined to Azure AD, and devices are managed by Intune. It doesn't matter who's signed in to the device, or if devices are personal or BYOD. When set to **None**, devices aren't joined to Azure AD, and aren't managed by Intune.

    For example:

    - If you want to manage the device, then choose **Some** or **All**.
    - If you don't want to manage the device, then choose **None**.
    - If you want to only manage the organization account on the device, then choose **None**, and configure the **MAM user scope**.
    - If you want to manage the device *and* manage the organization account on the device, then choose **Some** or **All**, and configure the **MAM user scope**.

  - **MAM user scope**: When set to **Some** or **All**, the organization account on the device is managed by Intune. Devices are "registered" in Azure AD. Devices aren't "joined" to Azure AD, and aren't managed by Intune. This option is designed for BYOD or personal devices.

    For example:

    - If you want to manage the organization account on the device, then choose **Some** or **All**.
    - If you don't want to manage the organization account on the device, then choose **None**.
    - If you want to only manage the device, then choose **None**, and configure the **MDM user scope**.
    - If you want to manage the device *and* manage the organization account on the device, then choose **Some** or **All**, and configure the **MDM user scope**.

  For more information on joined devices vs. registered devices, see:

  - [Azure AD device identity](/azure/active-directory/devices/overview)
  - [Azure AD registered devices](/azure/active-directory/devices/concept-azure-ad-register)
  - [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join)

- For bulk enrollment, go to the Microsoft Store, and download the Windows Configuration Designer (WCD) app. Configure the Windows Configuration Designer app, and choose to enroll devices in Azure AD. A package file is created. Put the package file on a USB drive, or on a network share.

  In the account settings on the device, users sign in with their organization account, and select this package file. Then, users are automatically enrolled.

  If your end users are familiar with running a file from these locations, they can complete the enrollment. For more information, see [automatic bulk enrollment](../enrollment/windows-bulk-enroll.md).

### Automatic enrollment end user tasks

When users turn on the device, the next steps determine how they're enrolled. Be sure to clearly communicate the options users should choose on personal and organization-owned devices.

- **Organization-owned devices**: Users turn on the device, step through the out-of-box (OOB) experience, and sign in with their organization account. This step joins the device in Azure AD, and the device is considered organization-owned. The device is fully managed, regardless of who's signed in. Users can open the **Settings** app > **Accounts** > **Access work or school**. It shows they're connected.

  If users sign in with a personal account during the OOB experience, they can still join the devices to Azure AD using the following steps:

  1. Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**.
  2. In **Alternate actions**, select **Join this device to Azure Active Directory**, and enter the information they're asked.

  When joined, the devices show as organization owned, and show as Azure AD joined in the Endpoint Manager admin center. Devices are managed by Intune, regardless of who's signed in.

- **BYOD or personal devices**: Users turn on the device, step through the out-of-box (OOB) experience, and sign in with their personal account. To register the device in Azure AD:

  1. Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**.
  2. In **Connect**, users choose to enter an **Email address**, or choose to **Join this device to Azure Active Directory**:

      - **Email address**: Users enter their organization email address. They're asked for more information, including the Intune server name or [CNAME record](../enrollment/windows-enroll.md#registration-and-enrollment-cnames). Be sure to give them all the information they need to enter.

        This option registers the device in Azure AD. They show as personal, and show as Azure AD registered in the Endpoint Manager admin center. The organization user is managed by Intune, not the device.

        If you don't want to manage BYOD or personal devices, be sure users select **Email address**, and enter their organization email address.

      - **Join this device to Azure Active Directory**: Users enter the information they're asked, including their organization email address.

        This option joins the device in Azure AD. They show as organization owned, and show as Azure AD joined in the Endpoint Manager admin center. Devices are managed by Intune, regardless of who's signed in.

        If you want to manage BYOD or personal devices, be sure users select **Join this device to Azure Active Directory**. Users should also know that their personal devices will be managed by their IT.

  For more information on the end user experience, see [enroll Windows 10 devices](../user-help/enroll-windows-10-device.md).

- If using bulk enrollment, and your end users are familiar with running files from a network share or USB drive, they can complete the enrollment. If they're not comfortable with this step, then it's recommended that the admin enroll.

- On personal or BYOD non-Windows 10 devices, users must install the Company Portal app from the Microsoft Store. Once installed, they open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). They'll be asked for more information, including the Intune server name. Be sure to give them all the information they need to enter.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Windows Autopilot

Use on organization-owned devices running Windows 10 and newer. Windows Autopilot uses the Windows 10 OEM version preinstalled on the device. You don't have to wipe the devices or use custom OS images. It also requires Automatic Enrollment, and uses the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to create an enrollment profile. When users sign in with their organization account, they're automatically enrolled.

For more information on Windows Autopilot, see [Windows Autopilot overview](../../autopilot/windows-autopilot.md) or [Tutorial: Use Autopilot to enroll Windows devices](../enrollment/tutorial-use-autopilot-enroll-devices.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You purchase devices from an [OEM that supports the Windows Autopilot deployment service](https://aka.ms/windowsautopilot), or from resellers or distributors that are in the [Cloud Solution Partners (CSP)](https://partner.microsoft.com/membership/cloud-solution-provider) program. | ✔️ |
| Devices are hybrid Azure AD joined. | ✔️ <br/><br/> Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune. |
| You have remote workers, and want to send devices directly to these users. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ <br/><br/> You can update existing desktops running older Windows versions, such as Windows 7, to Windows 10. This option also uses Microsoft Endpoint Configuration Manager. |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| You have Azure AD Premium. | ✔️ <br/><br/> Windows Autopilot uses Automatic enrollment. Automatic enrollment requires Azure AD Premium. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization admin can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are personal or BYOD. | ❌ <br/><br/> Windows Autopilot is only for organization-owned devices. For BYOD or personal devices, use Automatic enrollment or User enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Windows Autopilot. If the admin will enroll and prepare devices before giving them to users, then you can use a DEM account. |

---

### Windows Autopilot administrator tasks

- Be sure your devices are running Windows 10 and newer. For a complete list, see [software requirements](../../autopilot/software-requirements.md).

- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), register the devices in to Windows Autopilot. This step joins the devices to Azure AD. For more specific information, see [Windows Autopilot registration overview](../../autopilot/registration-overview.md) and [Manual registration overview](../../autopilot/manual-registration.md).

- Create an Autopilot deployment profile. For more specific information, see [Create an Autopilot deployment profile](../../autopilot/profiles.md#create-an-autopilot-deployment-profile).

  When you create the profile, you also:

  - Configure the out-of-box deployment user experience, including [user driven](../../autopilot/user-driven.md), [pre-provision](../../autopilot/pre-provision.md), and more. For more specific information, see [Configure Autopilot profiles](../../autopilot/profiles.md).

  - Configure startup behaviors, such as disabling the local administrator, and skipping the EULA. 

  - Assign the Autopilot deployment profile to your Azure AD security groups. You can also exclude security groups.

  - For hybrid Azure AD joined devices, you register the devices, create the deployment profile, and assign the profile. You'll also install the Intune Connector for Active Directory. This connector communicates between on-premises Active Directory and Azure AD.

  For more specific information, see [Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

After the profile is assigned, the devices start showing in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Devices** > **Windows**).

### Windows Autopilot end user tasks

The end user experience depends on the Windows Autopilot deployment option you chose, such as [user driven](../../autopilot/user-driven.md) or [pre-provision](../../autopilot/pre-provision.md).

- **Self-Deploying mode**: No actions. This option doesn't associate a user with the device. Users just turn on the device, and the enrollment automatically starts. 

  For more specific information, see [self deployment](../../autopilot/self-deploying.md).

- **Pre-provisioning**: Users turn on the device, and sign in with their organization or school account. The enrollment automatically starts. Since the device is pre-provisioned by admins, the enrollment is faster compared to **User-driven**.

  For more specific information, see [pre-provisioned deployment](../../autopilot/pre-provision.md).

- **Existing devices**: Your users must do the following steps:

  1. Open the Software Center app, and select **Operating systems**.
  2. Select **Autopilot for existing devices** > **Install**. Content downloads, the drives are formatted, and Windows 10 installs.

      This step can take some time, and users must wait.

  3. Autopilot runs, and users sign in with their organization or school account. The enrollment can automatically start. For more specific information, see [existing devices deployment](../../autopilot/existing-devices.md).

- **User driven**: Users turn on the device, and sign in with their organization or school account. The enrollment automatically starts. For more specific information, see [user-driven deployment](../../autopilot/user-driven.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Group policy

This enrollment option is available for domain-joined devices that you want to manage using Intune. Before enrolling, the devices must be hybrid Azure AD joined. Meaning, the devices are registered in on-premises Active Directory (AD), and registered in Azure AD. Once registered in Azure AD, they're available to enroll in Intune, and receive the settings and device features you configure.

You create a group policy on your local AD. When a group policy refresh occurs on the device, users are notified to complete the configuration. The configuration uses the user's Azure AD account to automatically enroll the device in Intune.

For more specific information, see [Enroll a Windows 10 device automatically using Group Policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

---
| Feature | Use this enrollment option when |
| --- | --- |
| Devices are hybrid Azure AD joined. | ✔️ <br/><br/> Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune. |
| You have Azure AD Premium. | ✔️ <br/><br/> Group policy enrollment requires Azure AD Premium. |
| You have remote workers. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization administrator can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are personal or BYOD. | ❌ <br/><br/> For BYOD or personal devices, use Automatic enrollment or User enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. They shouldn't be enrolled using the Intune classic agents. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Group policy. |

---

### Group policy administrator tasks

For more specific information on this enrollment method, see [Enroll a Windows 10 device automatically using Group Policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy#configure-the-auto-enrollment-group-policy-for-a-single-pc).

- Be sure your Windows 10 devices are [supported in Intune](supported-devices-browsers.md), and [supported for group policy enrollment](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).
- Register your AD into Azure AD. For more specific information, see [Azure AD integration with MDM](/windows/client-management/mdm/azure-active-directory-integration-with-mdm).
- Be sure your devices are hybrid Azure AD joined devices. The devices must be registered in local AD and in Azure AD.
- In local on-premises AD, create an **Enable automatic MDM enrollment using default Azure AD credentials** group policy. When group policy is refreshed, this policy is pushed to the devices, and users complete the configuration using their domain account (`user@contoso.com`).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Group policy end user tasks

- Users are notified that there are configuration changes. The policy refresh may require users to sign in with their organization or school account (`user@contoso.com`). The enrollment automatically starts.

## Co-management enrollment

If you use Configuration Manager, and want to continue to use Configuration Manager, then co-management enrollment is for you. Co-management manages Windows 10 devices using Configuration Manager and Microsoft Intune together. You cloud-attach your existing Configuration Manager environment to Endpoint Manager. This enrollment option runs some workloads in Configuration Manager, and other workloads in Endpoint Manager.

For more specific information on co-management, see [What is co-management?](../../configmgr/comanage/overview.md).

> [!NOTE]
> Tenant attach is also an option when using Configuration Manager. You don't enroll devices, but you can upload your Configuration Manager devices to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Use the admin center to run some remote actions, see your on-premises servers, and get OS information. For more information, see [enable tenant attach](../../configmgr/tenant-attach/device-sync-actions.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You use Configuration Manager. | ✔️ |
| Devices are hybrid Azure AD joined. | ✔️ <br/><br/> Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune. |
| Devices are enrolled in Intune. | ✔️ <br/><br/> You have devices you want to bring to co-management. Devices may have been enrolled using Windows Autopilot, or are direct from your hardware OEM. |
| You have Azure AD Premium. | ✔️ <br/><br/>  Azure AD Premium may be required depending on your co-management configuration. For more specific information, see [Paths to co-management](../../configmgr/comanage/quickstart-paths.md). |
| You have remote workers. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| Devices are personal or BYOD. | ✔️ |
| You have new or existing devices. | ✔️ <br/><br/> For devices that aren't running Windows 10 and newer, such as Windows 7, you'll need to upgrade. For more specific information, see [Upgrade Windows 10 for co-management](../../configmgr/comanage/quickstart-upgrade-win10.md). |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization admin can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be co-managed, users need to unenroll from the current MDM provider. They shouldn't be enrolled using the Intune classic agents. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to co-management. |

---

### Co-management administrator tasks

The administrator tasks and requirements depend on the co-management option you choose. For more specific information, see [Paths to co-management](../../configmgr/comanage/quickstart-paths.md).

When setting up co-management, you choose to:

- Automatically enroll existing Configuration Manager-managed devices to Intune. This option requires hybrid Azure AD joined devices. For more specific information, see [Tutorial: Enable co-management for existing Configuration Manager clients](../../configmgr/comanage/tutorial-co-manage-clients.md).

- Bring existing Intune enrolled Windows 10 devices to also be managed by Configuration Manager. In this situation, these devices aren't hybrid Azure AD joined devices. Meaning, the devices are registered in Azure AD. They're not registered in on-premises local Active Directory.

  For more specific information, see [Tutorial: Enable co-management for new internet-based devices](../../configmgr/comanage/tutorial-co-manage-new-devices.md).

### Co-management end user tasks

Both options use Automatic enrollment. With Automatic enrollment, users sign in with their organization account (`user@contoso.com`), and then are automatically enrolled. They can also open the **Settings** app > **Accounts** > **Access work or school** > **Connect**, and sign in with organization email address and password.

Configuration Manager may randomize the enrollment, so it may not occur immediately. When enrollment completes, it's ready to receive the policies and profiles you create.

## Next steps

- [MAM-WE](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
