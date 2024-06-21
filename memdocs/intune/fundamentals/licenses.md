---
# required metadata

title: Licenses available for Microsoft Intune
description: Intune is available with these licenses
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Microsoft Intune licensing

Microsoft Intune is available for different customer needs and organization sizes, from a simple-to-use management experience for schools and small businesses, to more advanced functionality required by enterprise customers. Most licenses that include Microsoft Intune also grant the rights to use Microsoft Configuration Manager, as long as the subscription remains active. An admin must have a license assigned to them to administer Intune (unless you [allow unlicensed admins](unlicensed-admins.md)).

## Microsoft Intune

The following plans are available for Microsoft Intune. For more information about the plans and pricing, see [Discover Microsoft Intune Plans and Pricing](https://www.microsoft.com/security/business/microsoft-intune-pricing).

### Microsoft Intune Plan 1

A cloud-based unified endpoint management solution that is included in the following licenses:

- Microsoft 365 E5
- Microsoft 365 E3
- Enterprise Mobility + Security E5
- Enterprise Mobility + Security E3
- Microsoft 365 Business Premium
- Microsoft 365 F1
- Microsoft 365 F3
- Microsoft 365 Government G5
- Microsoft 365 Government G3
- Microsoft Intune for Education

> [!NOTE]
> For additional licensing information about Intune for Education, see [Microsoft 365 Education](/office365/servicedescriptions/office-365-platform-service-description/microsoft-365-education).

### Microsoft Intune Plan 2

An add-on to Microsoft Intune Plan 1 that offers advanced endpoint management capabilities. Intune Plan 2 is included in Microsoft Intune Suite.

For information about trial and purchasing, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

### Microsoft Intune Suite

An add-on to Microsoft Intune Plan 1 that unifies mission-critical advanced endpoint management and security solutions.

For information about trial and purchasing, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

## Microsoft Intune for Education

Intune Plan 1 for Education is included in the following licenses:

- Microsoft 365 Education A5
- Microsoft 365 Education A3

## Licensing for Configuration Manager-managed devices in Intune

For existing Configuration Manager-managed devices to enroll into Intune for co-management at scale without user interaction, co-management uses a Microsoft Entra feature called Windows 10 auto-enrollment. Auto-enrollment with co-management requires licenses for both Microsoft Entra ID P1 or P2 (AADP1) and Microsoft Intune Plan 1. Starting on December 1, 2019, you no longer need to assign individual Intune licenses for this scenario. Microsoft Intune now includes the Intune licenses for co-management. The separate AADP1 licensing requirement remains the same for this scenario to work. You still need to assign Intune licenses for other enrollment scenarios.

## Additional information

- A Microsoft Intune user and device subscription is available as a standalone, in addition to the bundles listed above.
- A Microsoft Intune device-only subscription is available to manage kiosks, dedicated devices, phone-room devices, IoT, and other single-use devices that don't require user-based security and management features. For more information, see [Device-only licenses](../fundamentals/licenses.md#device-only-licenses).
- The appropriate Microsoft Intune license is required if a user or device benefits directly or indirectly from the Microsoft Intune service, including access to the Microsoft Intune service through a [Microsoft API](/legal/microsoft-apis/terms-of-use).
- Intune isn't included in licenses not in the previous tables.

## Unlicensed admins

For more information about giving administrators access to the Microsoft Intune admin center without them having an Intune license, see [Unlicensed admins](unlicensed-admins.md).

## Device-only licenses

Microsoft Intune offers a device-only subscription service that helps organizations manage devices that aren't affiliated with specific users.

You can purchase device licenses based on your estimated usage. Microsoft Intune device licenses are applicable when a device is enrolled through any of the following methods:

- [Windows Autopilot Self-Deploying mode](/autopilot/self-deploying)
- [Apple Device Enrollment Program without user affinity](../enrollment/device-enrollment-program-enroll-ios.md)
- [Apple School Manager without user affinity](../enrollment/apple-school-manager-set-up-ios.md)
- [Apple Configurator without user affinity](../enrollment/apple-configurator-enroll-ios.md)
- [Android Enterprise dedicated](../enrollment/android-kiosk-enroll.md)
- [Using a device enrollment manager account](../enrollment/device-enrollment-manager-enroll.md)

> [!NOTE]
> Visit the [Microsoft Licensing](https://www.microsoft.com/licensing/default) page, or contact your account representative if you have any questions or you would like to receive the latest information about product editions, product licensing updates, volume licensing plans, and other information related to your specific use cases.

### Device-only license limitations

When a device is enrolled by using a device license, the following Intune functions aren't supported:

- [Intune app protection policies](../apps/app-protection-policy.md)
- [Conditional access](../protect/conditional-access.md)
- User-based management features, such as email and calendaring

## Confirm your licenses

A Microsoft Intune license is created for you when you sign up for the Intune free trial. As part of this trial, you'll also have a trial Enterprise Mobility + Security (EMS) subscription. An Enterprise Mobility + Security (EMS) subscription includes both Microsoft Entra ID P1 or P2 and Microsoft Intune.

> [!NOTE]
> If you are unable to access this portal using the step below, or if you don't have an Intune license, you can sign up now for the [Intune free trial](./free-trial-sign-up.md). When setting up Intune, you can give an administrators access to the Microsoft Intune admin center [without them requiring an Intune license](./unlicensed-admins.md).

To confirm your Microsoft Intune license or trial, use the following steps:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Tenant status**.<br>
   Under the **Tenant details** tab, you will see the **MDM authority**, the **Total licenses users**, and the **Total Intune licenses**.
3. Select **Tenant administration** > **Roles** > **My permissions**.
4. Confirm you are an **administrator** with **full** permissions to **all** Intune resources.

> [!NOTE]
> For more in-depth information about Microsoft Intune, see the learning module: [Set up Microsoft Intune](/training/modules/set-up-microsoft-intune?azure-portal=true).

To check on your Microsoft Entra ID P1 or P2 license, use the following steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **Microsoft Entra ID**.
3. Select **Overview**. On the **Overview** pane, select the **Overview** tab if it isn't already selected.
4. Under **Basic information**, view your license.

If you don't have a license for Microsoft Entra ID P1 or P2, see [Sign up for Microsoft Entra ID P1 or P2 editions](/azure/active-directory/fundamentals/active-directory-get-started-premium).

## Next steps

For the latest information about product editions, product licensing updates, volume licensing plans, and other information related to your specific use cases, see the [Microsoft Licensing](https://www.microsoft.com/licensing/default) page.

For information about how user and device licenses affect access to services, as well as how to assign a license to a user, see the [Assign Intune licenses to your user accounts article](licenses-assign.md).
