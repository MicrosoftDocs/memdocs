---
title: Set up device management
description: Learn how to configure the Intune service and set up the environment for education.
ms.date: 5/2/2024
ms.topic: tutorial
ms.author: scbree
author: scottbreenmsft
zone_pivot_groups: platforms-windows-ios
ms.manager: dougeby
ms.service: microsoft-intune
ms.subservice: education
---

# Set up Microsoft Intune

Without the proper tools and resources, managing hundreds or thousands of devices in a school environment can be a complex and time-consuming task. Microsoft Intune is a collection of services that simplifies the management of devices at scale.

The Microsoft Intune service can be managed in different ways.

- **Intune admin center** is the primary Intune interface that supports the entire device lifecycle, from the enrollment phase through retirement. IT administrators can manage all settings across all Intune supported platforms.
- **Intune for Education** is a curated view of Intune that supports the entire device lifecycle, from the enrollment phase through retirement. IT administrators can start managing classroom devices with bulk enrollment options and a streamlined deployment. At the end of the school year, IT admins can reset devices, ensuring they're ready for the next year.

    :::image type="content" source="./images/intune-education-portal.png" alt-text="Intune for Education dashboard" lightbox="./images/intune-education-portal.png" border="true":::

    For more information, see [Intune for Education documentation][INT-1].

> [!TIP]
> **Intune** and **Intune for Education** both configure the **Intune** service. Changes made in one console will be reflected in the other. However, **Intune for Education** only supports a subset of policies and apps curated to suit simple K-12 scenarios on Windows and iPadOS.

---

> [!div class="checklist"]
>In this section you will:
>
> - Review Intune's licensing prerequisites
> - Configure the Intune service for education devices

## Prerequisites

✅ Check out the requirements for device management

Before configuring settings with Intune, consider the following prerequisites:

- **Intune subscription.** Microsoft Intune is licensed in three ways:
  - As a standalone service
  - As part of [Enterprise Mobility + Security][MSFT-1]
  - As part of a [Microsoft 365 Education subscription][MSFT-2]
- **Intune for Education device platforms.** Intune for Education can manage devices running a supported version of Windows 10, Windows 11, Windows 11 SE, and iPadOS
- **Intune device platforms.** Intune can manage devices running a supported version of Windows 10, Windows 11, Windows 11 SE, iOS, iPadOS, macOS, Android, and Linux
- **Network requirements.** Confirm all the required network endpoints can access without SSL inspection or any type of filtering. See [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints) for a list of endpoints.

For more information, see [Intune licensing][MEM-1] and [this comparison sheet][MSFT-3], which includes a table detailing the *Microsoft Modern Work Plan for Education*.

## Configure the Intune service for Education devices

The Intune service can be configured in different ways, depending on the needs of your school. In this section, you configure the Intune service using settings commonly implemented by K-12 school districts.

### Configure enrollment restrictions

✅ Restrict which devices can be managed

With enrollment restrictions, you control which devices can enroll and be managed by Intune. For example, you can prevent the enrollment of personal devices.

To block personally owned devices from enrolling:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **Enroll devices** > **Device platform restrictions**.
1. Select the tab for the platform you want to restrict.
1. Select **Create restriction**.
1. On the **Basics** page, provide a name for the restriction and, optionally, a description > **Next**.
1. On the **Platform settings** page, in the **Personally owned devices** field, select **Block** > **Next**.
    :::image type="content" source="./images/enrollment-restrictions.png" alt-text="This screenshot is of the device enrollment restriction page in Microsoft Intune admin center." lightbox="./images/enrollment-restrictions.png":::
1. Optionally, on the **Scope tags** page, add scope tags > **Next**.
1. On the **Assignments** page, select **Add groups**, and then use the search box to find and choose groups to which you want to apply the restriction > **Next**.
1. On the **Review + create** page, select **Create** to save the restriction.

For more information, see [Create a device platform restriction][MEM-2].

### Optional configuration

✅ Configure optional tenant configuration

- Customize branding according to organization policies. For more information, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](/mem/intune/apps/company-portal-app).
- Create Terms and conditions according to organization policies. For more information, see [Terms and conditions for user access](/mem/intune/enrollment/terms-and-conditions-create).

::: zone pivot="windows"

### Configure Windows enrollment

✅ Configure which users can enroll Windows devices

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **Enroll devices** > **Automatic Enrollment**.
1. Set the **MDM user scope** to **All** or **Some** and select a group if you want to restrict enrollment to certain users.
    > [!IMPORTANT]
    > The MDM user scope must be set to *All* if provisioning pacakges are used to enroll devices.
1. Set **MAM user scope** to **None**.
    :::image type="content" source="./images/intune-windows-enrollment.png" alt-text="A screenshot showing the MDM user scope and MAM user scope." lightbox="./images/intune-windows-enrollment.png":::
1. Select **Save**.

For more information, see [Enable Windows automatic enrollment](/mem/intune/enrollment/windows-enroll#enable-windows-automatic-enrollment).

### Disable Windows Hello for Business

✅ Disable functionality typically inaccessible to students

Windows Hello for Business is a biometric authentication feature that allows users to sign in to their devices using a PIN, password, or fingerprint. Windows Hello for Business is enabled by default on Windows devices, and to set it up, users must perform for multifactor authentication (MFA). As a result, this feature may not be ideal for students, who may not have MFA enabled.

> [!NOTE]
> **Passwordless for Students**
> If you're interested in using Windows Hello for Business with students, you may be interested in checking out our guidance on how you can use Temporary Access Pass. For more information, see [Passwordless for Students](/microsoft-365/education/deploy/protect-passwordless-students)

It's common for Windows Hello for Business to be disabled at the tenant level. Then, a policy can be targted at users or devices that need it. For example, staff and teachers.

To disable Windows Hello for Business at the tenant level:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **By platform** > **Windows** > **Device onboarding** > **Enrollment**.
1. Select **Windows Hello for Business**.
1. Ensure that **Configure Windows Hello for Business** is set to **disabled**.
1. Select **Save**.

:::image type="content" source="./images/whfb-disable.png" alt-text="Disablement of Windows Hello for Business from Microsoft Intune admin center." lightbox="./images/whfb-disable.png":::

For more information how to enable Windows Hello for Business on specific devices, see [Create a Windows Hello for Business policy][MEM-4].

### Configure Intune data collection policy

✅ Configure Endpoint analytics

Intune needs permission to collect data for Endpoint analytics on Windows devices.

To enable data collection:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Reports** > **Endpoint analytics** > **Settings**.
1. Under **Intune data collection policy**, select **Intune data collection policy**.
    :::image type="content" source="./images/intune-data-collection-policy.png" alt-text="Selecting the Intune data collection policy." lightbox="./images/intune-data-collection-policy.png":::
1. Select **Properties**.
1. Under **Configuration settings** select **Edit**.
1. Set **Health Monitoring** to **Enable**.
1. Select **Scope** and tick **Endpoint analytics**.
    :::image type="content" source="./images/intune-data-collection-policy-settings.png" alt-text="A screenshot showing the configuration of the Intune data collection policy." lightbox="./images/intune-data-collection-policy-settings.png":::
1. Select **Review + Save**.
1. Select **Save**.

For more information on data collection, see [Endpoint analytics data collection](/mem/analytics/data-collection).

### Configure Windows data

✅ Configure tenant Windows data settings

Intune needs permission to collect certain data for Windows update reports on Windows devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Tenant administration** > **Connectors and tokens** > **Windows data**
1. Under **Windows data** select **On**.
1. Review the **Windows license verification** section and configure as per your licensing.
    :::image type="content" source="./images/intune-windows-data.png" alt-text="A screenshot showing the configuration of the Intune Windows data settings." lightbox="./images/intune-windows-data.png":::
1. Click **Save**.

For more information, see [Enable use of Windows diagnostic data by Intune](/mem/intune/protect/data-enable-windows-data).

### Configure Windows device diagnostics

✅ Allow remote retrieval of diagnostic information

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Tenant administration** > **Device diagnostics**.
1. Configure settings as per your requirements.

This table provides the settings most commonly set by customers, but can be customized to suit your schools needs.

| Setting | Common configuration |
| --- | --- |
| Device diagnostics are available for corporate-managed devices running Windows 10, version 1909 and later, or Windows 11. Diagnostics may include user identifiable information such as user or device name. | Enabled |
| Automatically capture diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and Windows 11. Diagnostics may include user identifiable information such as user or device name. | Enabled |

For more information, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

### (Optional) Configure the Enrollment Status Page

Consider enabling the Enrollment Status Page if planning to use Windows Autopilot to enroll Windows devices in Intune.

The enrollment status page (ESP) displays the provisioning status to people enrolling Windows devices and signing in for the first time. You can configure the ESP to block device use until all required policies and applications are installed. Device users can look at the ESP to track how far along their device is in the setup process.

Additional information:

- [Windows Autopilot Enrollment Status Page](/autopilot/enrollment-status)
- [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status)

This table provides the settings most commonly set by customers, but can be customized to suit your schools needs.

| **Blade** | **Configuration group** | **Setting** | **Value** |
| --- | --- | --- | --- |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General\\Enrollment Status Page | Default\\Show app and profile configuration progress | Yes |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General\\Enrollment Status Page | Default\\Show an error when installation takes longer than specified number of minutes | 120 |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General\\Enrollment Status Page | Default\\Show custom message when time limit or error occurs | Yes |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General\\Enrollment Status Page | Default\\Turn on log collection and diagnostics page for end users | Yes |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General\\Enrollment Status Page | Default\\Only show page to devices provisioned by out-of-box experience (OOBE) | Yes |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General\\Enrollment Status Page | Enrollment Status Page\\Default\\Block device use until required apps are installed if they are assigned to the user/device | *All* or *Selected* with the minimum apps required. <br><br>For example, Microsoft 365 apps or web content filtering softtware |

::: zone-end

::: zone pivot="ios"

### Set up Apple MDM Certificate

#### [Intune](#tab/intune)

To set up an Apple MDM certificate, see [Get an Apple MDM push certificate](/mem/intune/enrollment/apple-mdm-push-certificate-get#steps-to-get-your-certificate).

#### [Intune for Education](#tab/intune-for-education)

To set up an Apple MDM certificate in Intune for Education, see [Add an MDM push certificate](/intune-education/setup-ios-device-management)

---

> [!IMPORTANT]
> The Apple MDM certificate needs to be renewed yearly. Make a note in your calendar to renew the certificate in just under a year from when you add the certificate. You can can view the expiry date in the console at any time.

### Configure Volume Purchase Program (VPP)

#### [Intune](#tab/intune)

To set up an Apple VPP, see [How to manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune](/mem/intune/apps/vpp-apps-ios).

#### [Intune for Education](#tab/intune-for-education)

To set up an Apple VPP in Intune for Education, see [Configure VPP tokens](/intune-education/setup-ios-device-management#configure-vpp-tokens).

---

> [!IMPORTANT]
> The Apple VPP token needs to be renewed yearly. Make a note in your calendar to renew the token in just under a year from when you add the token. You can can view the expiry date in the console at any time.

### Configure Automated Device Enrollment (ADE)

If you plan to integrate Apple School Manager and use Automated Device Enrollment follow these steps.

#### [Intune](#tab/intune)

To set up an Apple MDM certificate, see [Set up automated device enrollment in Intune](/mem/intune/enrollment/device-enrollment-program-enroll-ios).

#### [Intune for Education](#tab/intune-for-education)

To set up an Apple ADE in Intune for Education, see [Configure enrollment program token](/intune-education/setup-ios-device-management#configure-enrollment-program-token).

---

> [!IMPORTANT]
> The Apple ADE token needs to be renewed yearly. Make a note in your calendar to renew the token in just under a year from when you add the token. You can can view the expiry date in the console at any time.

::: zone-end

---

## Next steps

With the Intune service configured, you can configure policies and applications in preparation for the deployment of students' and teachers' devices.

> [!div class="nextstepaction"]
> [Next: Configure devices >](configure-devices-overview.md)

<!-- Reference links in article -->

[MEM-1]: /mem/intune/fundamentals/licenses
[MEM-2]: /mem/intune/enrollment/enrollment-restrictions-set
[MEM-4]: /mem/intune/protect/windows-hello#create-a-windows-hello-for-business-policy

[INT-1]: /intune-education/what-is-intune-for-education

[MSFT-1]: https://www.microsoft.com/microsoft-365/enterprise-mobility-security
[MSFT-2]: https://www.microsoft.com/licensing/product-licensing/microsoft-365-education
[MSFT-3]: https://edudownloads.azureedge.net/msdownloads/Microsoft-Modern-Work-Plan-Comparison-Education_11-2021.pdf
