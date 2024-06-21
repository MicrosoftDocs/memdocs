---
# required metadata

title: Windows device enrollment guide for Microsoft Intune
description: Enroll Windows devices using Automatic enrollment, Windows Autopilot, group policy, and co-management enrollment options in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/28/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Enrollment guide: Enroll Windows client devices in Microsoft Intune

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create.

You have the following options when enrolling Windows devices:

- [Windows automatic enrollment](#windows-automatic-enrollment)
- [Windows Autopilot](#windows-autopilot)
- [BYOD: User enrollment](#byod-user-enrollment)
- [Co-management with Configuration Manager](#co-management-enrollment)

This article provides enrollment recommendations and includes an overview of the administrator and user tasks for each option.

There's also a visual guide of the different enrollment options for each platform:

[![A visual representation of Intune enrollment options by platform](./media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Before you begin

For all Intune-specific prerequisites and configurations needed to prepare your tenant for enrollment, go to [Enrollment guide: Microsoft Intune enrollment](deployment-guide-enrollment.md).

## Windows automatic enrollment

Use for personal and corporate-owned devices running Windows 10 and Windows 11. Microsoft Entra ID P1 or P2 is required with some automatic enrollment options.

Automatic enrollment:

- Uses the **Access school or work** feature on the devices (**Settings** app > **Accounts**).
- Uses the enrollment options you configure in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

You can use this enrollment option to:

- Enable automatic enrollment for personal devices that register and join in Microsoft Entra ID.
- Automatically [bulk enroll devices with the Windows Configuration Designer app](../enrollment/windows-bulk-enroll.md).
- Automatically [enroll Microsoft Entra hybrid joined devices using group policy](/windows/client-management/enroll-a-windows-10-device-automatically-using-group-policy).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You use Windows client. | ✅ <br/><br/> Configuration Manager supports Windows Server. |
| You have Microsoft Entra ID P1 or P2 | ✅ |
| You'll use Conditional Access (CA) on devices enrolled using [bulk enrollment](../enrollment/windows-bulk-enroll.md) with a provisioning package. | ✅ On Windows 11 and Windows 10 1803+, CA is available for Windows devices enrolled using bulk enrollment. <br/><br/> ❌ On Windows 10 1709 and older, CA isn't available for Windows devices enrolled using bulk enrollment. |
| You have remote workers. | ✅ |
| Devices are personal or BYOD. | ✅ <br/><br/> ❌ If you use Group Policy, then bulk enrollment and automatic enrollment are for corporate-owned devices, not personal or BYOD. |
| Devices are owned by the organization or school. | ✅  |
| You have new or existing devices. | ✅ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✅ <br/><br/> Bulk enrollment is for organization-owned devices, not personal or BYOD.|
| Devices are associated with a single user. | ✅ |
| Devices are user-less, like kiosk, dedicated, or shared device. | ✅ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization admin can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| You use the optional device enrollment manager (DEM) account. | ✅ <br/><br/> ❌ DEM accounts don't work with Group Policy. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |

---

### Automatic enrollment administrator tasks

- Be sure your devices are running Windows 10/11. For a complete list, go to [supported device platforms](supported-devices-browsers.md).

- Optional. Instead of users entering the Intune server name, you can create a CNAME record that's easier to enter, like `EnterpriseEnrollment.contoso.com`. CNAME records associate a domain name with a specific server. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), test your CNAME record to make sure it's configured correctly. For more information, go to [create a CNAME record](../enrollment/windows-enrollment-create-cname.md).
- In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Windows Enrollment** > **Automatic Enrollment**. In the configuration, you set the **MDM user scope** and **MAM user scope**:

  - **MDM user scope**: When set to **Some** or **All**, devices are joined to Microsoft Entra ID, and devices are managed by Intune. It doesn't matter who's signed in to the device, or if devices are personal or BYOD. When set to **None**, devices aren't joined to Microsoft Entra ID, and aren't managed by Intune.

    For example:

    - If you want to manage the device, then choose **Some** or **All**.
    - If you don't want to manage the device, then choose **None**.
    - If you want to only manage the organization account on the device, then choose **None**, and configure the **MAM user scope**.
    - If you want to manage the device *and* manage the organization account on the device, then choose **Some** or **All**, and configure the **MAM user scope**.

  - **MAM user scope**: When set to **Some** or **All**, the organization account on the device is managed by Intune. Devices are "registered" in Microsoft Entra ID. Devices aren't "joined" to Microsoft Entra ID, and aren't managed by Intune. This option is designed for BYOD or personal devices.

    For example:

    - If you want to manage the organization account on the device, then choose **Some** or **All**.
    - If you don't want to manage the organization account on the device, then choose **None**.
    - If you want to only manage the device, then choose **None**, and configure the **MDM user scope**.
    - If you want to manage the device *and* manage the organization account on the device, then choose **Some** or **All**, and configure the **MDM user scope**.

    For more information on joined devices vs. registered devices, go to:

    - [Microsoft Entra device identity](/entra/identity/devices/overview)
    - [Microsoft Entra registered devices](/entra/identity/devices/concept-device-registration)
    - [Microsoft Entra joined devices](/entra/identity/devices/concept-directory-join)

- For bulk enrollment, go to the Microsoft Store, and download the Windows Configuration Designer (WCD) app. Configure the Windows Configuration Designer app, and choose to enroll devices in Microsoft Entra ID. A package file is created. Put the package file on a USB drive, or on a network share.

  In the account settings on the device, users sign in with their organization account, and select this package file. Then, users are automatically enrolled.

  If your end users are familiar with running a file from these locations, they can complete the enrollment. For more information, go to [automatic bulk enrollment](../enrollment/windows-bulk-enroll.md).

- For automatic enrollments using group policy:

  - Be sure your Windows client devices are supported in Intune, and [supported for group policy enrollment](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).
  - Register your Active Directory in Microsoft Entra ID. For more specific information, go to [Microsoft Entra integration with MDM](/windows/client-management/mdm/azure-active-directory-integration-with-mdm).
  - Be sure your devices are Microsoft Entra hybrid joined devices. The devices must be registered in local AD and in Microsoft Entra ID.
  - In local on-premises AD, create an **Enable automatic MDM enrollment using default Microsoft Entra credentials** group policy. When group policy is refreshed, this policy is pushed to the devices, and users complete the configuration using their domain account (example: `user@contoso.com`).

  In the Intune admin center, you can use [Group Policy analytics](../configuration/group-policy-analytics.md) to see your on-premises group policies settings that are supported by cloud MDM providers, including Microsoft Intune.

  > [!TIP]
  > If you want a cloud native solution to manage devices, then Windows Autopilot (in this article) might be the best enrollment option for your organization.

### Automatic enrollment end user tasks

When users turn on the device, the next steps determine how they're enrolled. Clearly communicate the options users should choose on personal and organization-owned devices.

- **Organization-owned devices**: Users turn on the device, step through the out-of-box experience (OOBE), and sign in with their work or school account (example: `user@contoso.com`). This step joins the device in Microsoft Entra ID, and the device is considered organization-owned. The device is fully managed, regardless of who's signed in. Users can open the **Settings** app and go to **Accounts** > **Access work or school** to confirm that their work account is connected.

  If users sign in with a personal account during the OOBE, they can still join the devices to Microsoft Entra ID using the following steps:

  1. Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**.
  2. In **Alternate actions**, select **Join this device to Azure Active Directory**, and enter the information they're asked. This step joins the device to Microsoft Entra ID.

  When joined, the devices show as organization owned. In the Intune admin center, devices show as Microsoft Entra joined. Devices are managed by Intune, regardless of who's signed in.

  Users on devices enrolled using Group Policy are notified that there were configuration changes. The policy refresh can require users to sign in with their work or school account. Device enrollment automatically starts.

- **BYOD or personal devices**: Users turn on the device, step through the out-of-box experience (OOBE), and sign in with their personal account. To register the device in Microsoft Entra ID:

  1. Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**.
  2. In **Connect**, users choose to enter an **Email address**, or choose to **Join this device to Azure Active Directory**:

      - **Email address**: Users enter their organization email address. They're asked for more information, including the Intune server name or [CNAME record](../enrollment/windows-enrollment-create-cname.md). Be sure to give them all the information they need to enter.

        This option registers the device in Microsoft Entra ID. The devices show as personal, and show as Microsoft Entra registered in the Intune admin center. The organization user is managed by Intune; the device isn't managed by Intune.

        If you don't want to manage BYOD or personal devices, users must select **Email address**, and enter their organization email address.

      - **Join this device to Azure Active Directory**: Users enter the information they're asked, including their organization email address.

        This option joins the device in Microsoft Entra ID. The devices show as organization owned, and show as Microsoft Entra joined in the Intune admin center. Devices are managed by Intune, regardless of who's signed in.

        If you want to manage BYOD or personal devices, users must select **Join this device to Azure Active Directory**. Users should also know that their personal devices will be managed by their IT.

  For more information on the end user experience, go to [enroll Windows client devices](../user-help/enroll-windows-10-device.md).

- If using bulk enrollment, and your end users are familiar with running files from a network share or USB drive, they can complete the enrollment. If they're not comfortable with this step, then it's recommended that the admin enrolls.

- On personal or BYOD non-Windows client devices, users must install the Company Portal app from the Microsoft Store. Once installed, they open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). They're asked for more information, including the Intune server name. Be sure to give them all the information they need to enter.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Windows Autopilot

Use on organization-owned devices running Windows 10/11.

Windows Autopilot uses the Windows client OEM version preinstalled on the device. You don't have to wipe the devices or use custom OS images. Windows Autopilot also requires Automatic enrollment, and uses the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to create an enrollment profile. When users sign in with their organization account, they're automatically enrolled.

For more information about Windows Autopilot, go to [Windows Autopilot overview](/autopilot/overview) or [Windows Autopilot scenarios](/autopilot/tutorial/autopilot-scenarios).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You use Windows client. | ✅ <br/><br/> Configuration Manager supports Windows Server. |
| You purchase devices from an [OEM that supports the Windows Autopilot deployment service](https://aka.ms/windowsautopilot), or from resellers or distributors that are in the [Cloud Solution Partners (CSP)](https://partner.microsoft.com/membership/cloud-solution-provider) program. | ✅ |
| Devices are Microsoft Entra hybrid joined. | ✅ <br/><br/> Microsoft Entra hybrid joined devices are joined to your on-premises Active Directory, and registered with your Microsoft Entra ID. Devices in Microsoft Entra ID are available to Intune. Devices that aren't registered in Microsoft Entra ID aren't available to Intune. <br/><br/>A full Microsoft Entra joined solution might be better for your organization. For more information, go to the [Success with remote Windows Autopilot and Microsoft Entra hybrid join](https://techcommunity.microsoft.com/t5/intune-customer-success/success-with-remote-windows-autopilot-and-hybrid-azure-active/ba-p/2749353) blog.|
| You have remote workers. | ✅ <br/><br/> The OEM or partner can send devices directly to your users.|
| Devices are owned by the organization or school. | ✅ |
| You have new or existing devices. | ✅ <br/><br/> You can update existing desktops running older Windows versions, like Windows 7, to Windows 10. This option also uses Microsoft Configuration Manager. |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✅ |
| You have Microsoft Entra ID P1 or P2. | ✅ <br/><br/> Windows Autopilot uses Automatic enrollment. Automatic enrollment requires Microsoft Entra ID P1 or P2. |
| Devices are associated with a single user. | ✅ |
| Devices are user-less, like kiosk, dedicated, or shared. | ✅ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization admin can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are personal or BYOD. | ❌ <br/><br/> Windows Autopilot is only for organization-owned devices. For BYOD or personal devices, use [Windows automatic enrollment](#windows-automatic-enrollment) (in this article) or a [User enrollment option](#byod-user-enrollment) (in this article). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Windows Autopilot. |

---

### Windows Autopilot administrator tasks

- Be sure your devices are running a currently supported version of Windows. For a complete list, go to [software requirements](/autopilot/requirements?tabs=software#software-requirements).

- In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), register the devices in to Windows Autopilot. This step joins the devices to Microsoft Entra ID. For more specific information, go to [Windows Autopilot registration overview](/autopilot/registration-overview) and [Manual registration overview](/autopilot/manual-registration).

- Create an Autopilot deployment profile. For more specific information, go to [Create an Autopilot deployment profile](/autopilot/profiles#create-an-autopilot-deployment-profile).

  When you create the profile, you also:

  - Configure the out-of-box deployment user experience, including [user driven](/autopilot/user-driven), [pre-provision](/autopilot/pre-provision), and more. For more specific information, go to [Configure Autopilot profiles](/autopilot/profiles).

  - Configure startup behaviors, like disabling the local administrator, and skipping the EULA.

  - Assign the Autopilot deployment profile to your Microsoft Entra security groups. You can also exclude security groups.

  - For Microsoft Entra hybrid joined devices, you register the devices, create the deployment profile, and assign the profile. You'll also install the Intune Connector for Active Directory. This connector communicates between on-premises Active Directory and Microsoft Entra ID.

  For more specific information, go to [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](/autopilot/windows-autopilot-hybrid).

After the profile is assigned, the devices start showing in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Devices** > **By platform** > **Windows**).

### Windows Autopilot end user tasks

The end user experience depends on the Windows Autopilot deployment option you chose, like [user driven](/autopilot/user-driven) or [pre-provision](/autopilot/pre-provision).

- **Self-Deploying mode**: No actions. This option doesn't associate a user with the device. Users just turn on the device, and the enrollment automatically starts.

  For more specific information, go to [Windows Autopilot self-deploying mode](/autopilot/self-deploying).

- **Pre-provisioning**: Users turn on the device, and sign in with their organization or school account. The enrollment automatically starts. Since the device is pre-provisioned by admins, the enrollment is faster compared to **User-driven**.

  For more specific information, go to [pre-provisioned deployment](/autopilot/pre-provision).

- **Existing devices**: Your users must do the following steps:

  1. Open the **Software Center** app, and select **Operating systems**.
  2. Select **Autopilot for existing devices** > **Install**. Content downloads, the drives are formatted, and Windows client OS installs.

      This step can take some time, and users must wait.

  3. Windows Autopilot runs, and users sign in with their organization or school account. The enrollment can automatically start. For more specific information, go to [existing devices deployment](/autopilot/existing-devices).

- **User driven**: Users turn on the device, and sign in with their organization or school account. The enrollment automatically starts. For more specific information, go to [user-driven deployment](/autopilot/user-driven).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## BYOD: User enrollment

Use for personal or BYOD (bring your own device) and organization-owned devices running Windows 10/11.

User enrollment uses the **Settings** app > **Accounts** > **Access school or work** feature on the devices. There's some overlap with User enrollment and Automatic enrollment.

With User enrollment, you can "register" the devices with Microsoft Entra ID or "join" the devices in Microsoft Entra ID:

- **Register**: When you register devices in Microsoft Entra ID, the devices show as personal in the Intune admin center. Users get access to organization resources, like email. This option is common for BYOD or personal devices.
- **Join**: When you join devices in Microsoft Entra ID, the devices are fully managed by Intune, and will receive any policies you create. This option is common for organization-owned devices. If users want their personal devices fully managed by Intune (and their organization IT), then they can join their personal devices.

> [!WARNING]
> In the **Settings** app > **Accounts** > **Access school or work**, you might see an **Enroll only in device management** option. This option doesn't register the device in Microsoft Entra ID. From an Intune perspective, we don't recommend this MDM-only option for BYOD or personal devices. As a result, this guide doesn't include any additional information or guidance.

---
| Feature | Use this enrollment option when |
| --- | --- |
| You use Windows client. | ✅ <br/><br/> Configuration Manager supports Windows Server. |
| Devices are Microsoft Entra hybrid joined. | ✅ <br/><br/> Microsoft Entra hybrid joined devices are joined to your on-premises Active Directory, and registered with your Microsoft Entra ID. Devices in Microsoft Entra ID are available to Intune. Devices that aren't registered in Microsoft Entra ID aren't available to Intune. <br/><br/>A full Microsoft Entra joined solution might be better for your organization. For more information, go to the [Success with remote Windows Autopilot and Microsoft Entra hybrid join](https://techcommunity.microsoft.com/t5/intune-customer-success/success-with-remote-windows-autopilot-and-hybrid-azure-active/ba-p/2749353) blog. |
| You have Microsoft Entra ID P1 or P2. |❌ Microsoft Entra ID P1 or P2 isn't required.<br/><br/> ✅   If the devices join Microsoft Entra ID, then they can use Microsoft Entra ID P1 or P2 features, like Conditional Access. |
| You have remote workers. | ✅ <br/><br/> Users should know that their personal devices might be managed by the organization IT. |
| Devices are personal or BYOD. | ✅ |
| Devices are owned by the organization or school. | ✅ <br/><br/> You can use User enrollment, but it's recommended to use [Windows Autopilot](#windows-autopilot) (in this article) or [Windows Automatic enrollment](#windows-automatic-enrollment) (in this article). They require fewer steps for your users. |
| You have new or existing devices. | ✅ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✅ |
| Devices are associated with a single user. | ✅ |
| Devices are user-less, like kiosk, dedicated, or shared device. | ❌ <br/><br/> The user enrollment options require a user to sign in with an organization account, and use the Settings app, which isn't common on shared devices.  |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to User enrollment. |
| Devices are managed by another MDM provider. | ✅ A device managed by another MDM provider can register in Microsoft Entra ID.<br/><br/>❌ To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |

---

### User enrollment administrator tasks

Other than having Intune setup, there are minimal administrator tasks with this enrollment method.

- Be sure your devices are running Windows 10 and newer. For a complete list, go to [supported device platforms](supported-devices-browsers.md).

- Optional. Instead of users entering the Intune server name, you can create a CNAME record that's easier to enter, like `EnterpriseEnrollment.contoso.com`. CNAME records associate a domain name with a specific server. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), test your CNAME record to make sure it's configured correctly. For more information, go to [create a CNAME record](../enrollment/windows-enrollment-create-cname.md).

- Decide if users can do organization work on personal devices. On personal devices, users are typically administrators, and used a personal email account (`user@outlook.com`) to configure the device. To register these devices in Microsoft Entra ID, use the Settings app. As an admin, tell users the options they should choose. Be specific.

  If an Intune Automatic enrollment policy will also deploy, then let users know the impact ([MDM user scope vs. MAM user scope](#automatic-enrollment-administrator-tasks) (in this article)).

- If you have existing organization-owned devices and are enrolling them into Intune the first time, then we recommend using [Automatic enrollment](#windows-automatic-enrollment) (in this article).

  Users can use the **Settings** app > **Accounts** to **Join this device to Azure Active Directory**, which joins the device to Microsoft Entra ID. If they do, deploy an [Automatic enrollment](#windows-automatic-enrollment) (in this article) policy to enroll the device in Intune.

- If you have new organization-owned devices, then we recommend using [Windows Autopilot](#windows-autopilot) (in this article) or use [Automatic enrollment](#windows-automatic-enrollment) (in this article). In the out-of-box experience (OOBE), users enter their organization account (`user@contoso.com`). This step registers the devices in Microsoft Entra ID. Deploy an [Automatic enrollment](#windows-automatic-enrollment) (in this article) policy to enroll the device in Intune.

  If users use their personal email account in the OOBE, then the device isn't registered in Microsoft Entra ID, and the Automatic enrollment policy isn't deployed. In this scenario, users use the Settings app to **Join this device to Azure Active Directory**, which joins the device to Microsoft Entra ID. When the device is joined in Microsoft Entra ID, the Automatic enrollment policy deploys, and enrolls the device in Intune.

### User enrollment end user tasks

Clearly communicate the options users should choose on personal and organization-owned devices. For more information on the end user experience, go to [enroll Windows client devices](../user-help/enroll-windows-10-device.md).

- **BYOD or personal devices**: These devices are probably existing devices that are already configured with a personal email account (`user@outlook.com`). Users must register the device using the Settings app:

  1. Connect the device to the internet.

  2. Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**.

  3. In **Connect**, users choose to enter an **Email address**, or choose to **Join this device to Azure Active Directory**:

      - **Email address**: Users enter their organization email address and password. They're asked for more information, including the Intune server name or CNAME record. Be sure to give them all the information they need to enter.

        This option registers the device in Microsoft Entra ID. The devices show as personal, and show as Microsoft Entra registered in the Intune admin center. The organization user is managed by Intune; the device isn't managed by Intune.

        If you or your users don't want the organization IT to manage BYOD or personal devices, users must select **Email address**.

      - **Join this device to Azure Active Directory**: Users enter the information they're asked, including their organization email address and password.

        This option joins the device in Microsoft Entra ID. The devices show as organization owned, and show as Microsoft Entra joined in the Intune admin center. Devices are managed by Intune, regardless of who's signed in.

        If you want to manage BYOD or personal devices, users must select **Join this device to Azure Active Directory**. Users should also know that their personal devices will be managed by their IT.

- **Organization-owned devices**: These devices can be existing devices or new devices. If new devices, users turn on the device, step through the out-of-box experience (OOBE), and sign in with their organization account (`user@contoso.com`). This step joins the device in Microsoft Entra ID, and the device is considered organization-owned. The device is fully managed, regardless of who's signed in. Users can open the **Settings** app > **Accounts** > **Access work or school**. It shows they're connected.

  For existing devices, or if users sign in with a personal account during the OOBE, they can join the devices to Microsoft Entra ID using the following steps:

  1. Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**.
  2. In **Alternate actions**, select **Join this device to Azure Active Directory**, and enter the information they're asked.

   This step joins the device to Microsoft Entra ID. When joined, the devices show as organization owned, and show as Microsoft Entra joined in the Intune admin center. Devices are managed by Intune, regardless of who's signed in.

## Co-management enrollment

If you use Configuration Manager, and want to continue to use Configuration Manager, then co-management enrollment is for you.

Co-management manages Windows 10/11 devices using Configuration Manager and Microsoft Intune together. You cloud-attach your existing Configuration Manager environment to Intune. This enrollment option runs some workloads in Configuration Manager, and other workloads in Intune.

For more specific information on co-management, go to [What is co-management?](../../configmgr/comanage/overview.md).

> [!NOTE]
> Tenant attach is also an option when using Configuration Manager. You don't enroll devices, but you can upload your Configuration Manager devices to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Use the admin center to run some remote actions, go to your on-premises servers, and get OS information. For more information, go to [enable tenant attach](../../configmgr/tenant-attach/device-sync-actions.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You use Windows client. | ✅ <br/><br/> Configuration Manager supports Windows Server. |
| You use Configuration Manager. | ✅ <br/><br/> Configuration Manager can manage Windows Server. |
| Devices are Microsoft Entra hybrid joined. | ✅ <br/><br/> Microsoft Entra hybrid joined devices are joined to your on-premises Active Directory, and registered with your Microsoft Entra ID. Devices in Microsoft Entra ID are available to Intune. Devices that aren't registered in Microsoft Entra ID aren't available to Intune. |
| Devices are enrolled in Intune. | ✅ <br/><br/> You have devices you want to bring to co-management. Devices might have been enrolled using Windows Autopilot, or are direct from your hardware OEM. |
| You have Microsoft Entra ID P1 or P2. | ✅ <br/><br/>  Microsoft Entra ID P1 or P2 might be required depending on your co-management configuration. For more specific information, go to [Paths to co-management](../../configmgr/comanage/quickstart-paths.md). |
| You have remote workers. | ✅ |
| Devices are owned by the organization or school. | ✅ |
| Devices are personal or BYOD. | ✅ |
| You have new or existing devices. | ✅ <br/><br/> For devices that aren't running Windows 10/11, like Windows 7, you'll need to upgrade. For more specific information, go to [Upgrade Windows 10 for co-management](../../configmgr/comanage/quickstart-upgrade-win10.md). |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✅ |
| Devices are associated with a single user. | ✅ |
| Devices are user-less, like kiosk, dedicated, or shared. | ✅ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization admin can sign in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also create a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be co-managed, users need to unenroll from the current MDM provider. They shouldn't be enrolled using the Intune classic agents. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to co-management. |

---

### Co-management administrator tasks

The administrator tasks and requirements depend on the co-management option you choose. For more specific information, go to [Paths to co-management](../../configmgr/comanage/quickstart-paths.md).

When setting up co-management, you choose to:

- Automatically enroll existing Configuration Manager-managed devices to Intune. This option requires Microsoft Entra hybrid joined devices. For more specific information, go to [Tutorial: Enable co-management for existing Configuration Manager clients](../../configmgr/comanage/tutorial-co-manage-clients.md).

- Bring existing Intune enrolled Windows 10/11 devices to also be managed by Configuration Manager. In this situation, these devices aren't Microsoft Entra hybrid joined devices. Meaning, the devices are registered in Microsoft Entra ID. They're not registered in on-premises local Active Directory.

  For more specific information, go to [Tutorial: Enable co-management for new internet-based devices](../../configmgr/comanage/tutorial-co-manage-new-devices.md).

### Co-management end user tasks

Both options use Automatic enrollment. With Automatic enrollment, users sign in with their organization account (`user@contoso.com`), and then are automatically enrolled. They can also open the **Settings** app > **Accounts** > **Access work or school** > **Connect**, and sign in with organization email address and password.

Configuration Manager can randomize the enrollment, so enrollment might not occur immediately. When enrollment completes, it's ready to receive the policies and profiles you create.

## Related articles

- [MAM without enrollment](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
