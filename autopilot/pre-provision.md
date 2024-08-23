---
title: Windows Autopilot for pre-provisioned deployment
description: Windows Autopilot for pre-provisioned deployment.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
ms.reviewer: jubaptis
manager: aaroncz
author: frankroj
ms.author: frankroj
ms.date: 07/23/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier1
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot for pre-provisioned deployment

Windows Autopilot helps organizations easily provision new devices by using the preinstalled OEM image and drivers. This functionality lets end users get their devices business-ready by using a simple process.

:::image type="content" source="images/wg01.png" alt-text="Diagram of the OEM process.":::

Windows Autopilot can also provide a _pre-provisioning_ service that helps partners or IT staff pre-provision a fully configured and business-ready Windows PC. From the end user's perspective, the Windows Autopilot user-driven experience is unchanged, but getting their device to a fully provisioned state is faster.

With **Windows Autopilot for pre-provisioned deployment**, the provisioning process is split. The time-consuming portions are done by IT, partners, or OEMs. The end user simply completes a few necessary settings and policies and then they can begin using their device.

:::image type="content" source="images/wg02.png" alt-text="Diagram of the OEM process with partner.":::

Pre-provisioned deployments use Microsoft Intune in currently supported versions of Windows. Such deployments build on existing Windows Autopilot [user-driven scenarios](user-driven.md) and support user-driven mode scenarios for both Microsoft Entra joined and Microsoft Entra hybrid joined devices.

## Prerequisites

In addition to [Windows Autopilot requirements](requirements.md), Windows Autopilot for pre-provisioned deployment also requires:

- A currently supported version of Windows.
- Windows Pro, Enterprise, or Education editions.
- An Intune subscription.
- Physical devices that support Trusted Platform Module (TPM) 2.0 and device attestation. Virtual machines aren't supported. The pre-provisioning process uses Windows Autopilot self-deploying capabilities, so TPM 2.0 is required. The TPM attestation process also requires access to a set of HTTPS URLs that are unique for each TPM provider. For more information, see the entry for Autopilot self-Deploying mode and Autopilot pre-provisioning in [Networking requirements](requirements.md?tabs=networking#autopilot-self-deploying-mode-and-autopilot-pre-provisioning).
- Network connectivity. Using wireless connectivity requires selecting region, language and keyboard before being able to connect and start provisioning.
- An enrollment status page (ESP) profile must be targeted to the device.

> [!IMPORTANT]
>
> - Because the OEM or vendor performs the pre-provisioning process, this process **doesn't require access to an end-user's on-prem domain infrastructure**. The pre-provisioning process is unlike a typical Microsoft Entra hybrid joined scenario because rebooting the device is postponed. The device is resealed before the time when connectivity to a domain controller is expected. Instead the domain network is contacted when the device is unboxed on-premises by the end-user.
>
> - See [Windows Autopilot known issues](known-issues.md) and [Troubleshooting Windows Autopilot device import and enrollment](troubleshooting-faq.yml#troubleshooting-windows-autopilot-device-import-and-enrollment) to review known issues and their solutions.

## Preparation

Devices slated for pre-provisioning are registered for Autopilot via the normal registration process.

To be ready to try out Windows Autopilot for pre-provisioned deployment, make sure that existing Windows Autopilot user-driven scenarios can be successfully used:

- User-driven Microsoft Entra join. Make sure that devices can be deployed using Windows Autopilot and join them to a Microsoft Entra ID tenant.

- User-driven with Microsoft Entra hybrid join. To enable the features of Microsoft Entra hybrid join, make sure that the following actions can be performed:

  - Deploy devices using Windows Autopilot.
  - Join the devices to an on-premises Active Directory domain.
  - Register the devices with Microsoft Entra ID.

  > [!IMPORTANT]
  >
  > Microsoft recommends deploying new devices as cloud-native using Microsoft Entra join. Deploying new devices as Microsoft Entra hybrid join devices isn't recommended, including through Autopilot. For more information, see [Microsoft Entra joined vs. Microsoft Entra hybrid joined in cloud-native endpoints: Which option is right for your organization](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined#which-option-is-right-for-your-organization).

If these scenarios can't be completed, Windows Autopilot for pre-provisioned deployment also doesn't succeed since it builds on top of these scenarios.

Before the pre-provisioning process can be started in the provisioning service facility, another Autopilot profile setting must be configured. A detailed tutorial on how to configure an Autopilot profile for pre-provisioning is available in the following articles:

- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](tutorial/pre-provisioning/azure-ad-join-workflow.md)
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join in Intune](tutorial/pre-provisioning/hybrid-azure-ad-join-workflow.md)

The pre-provisioning process applies all device-targeted policies from Intune. Those policies include certificates, security templates, settings, apps, and more - anything targeting the device. Additionally, any Win32 or line-of-business (LOB) apps are installed if they meet the following conditions:

- Configured to install in the device context.
- Assigned to either the device or to the user preassigned to the Autopilot device.

> [!IMPORTANT]
>
> Make sure not to target both Win32 and LOB apps to the same device. If both Win32 and LOB apps need to be targeted to the device, consider using [Windows Autopilot device preparation](device-preparation/overview.md). For more information, see [Add a Windows line-of-business app to Microsoft Intune](/mem/intune/apps/lob-apps-windows).

> [!NOTE]
>
> To ensure easy access into pre-provisioning mode, select the language mode as user specified in Autopilot profiles. The pre-provisioning technician phase installs all device-targeted apps and any user-targeted, device-context apps that are targeted to the assigned user. If there's no assigned user, then it only installs the device-targeted apps. Other user-targeted policies aren't applied until the user signs into the device. To verify these behaviors, be sure to create appropriate apps and policies targeted to devices and users.

## Scenarios

Windows Autopilot for pre-provisioned deployment supports two distinct scenarios:

- User-driven deployments with Microsoft Entra join. The device is joined to a Microsoft Entra tenant.

- User-driven deployments with Microsoft Entra hybrid join. The device is joined to an on-premises Active Directory domain, and separately registered with Microsoft Entra ID.

  > [!IMPORTANT]
  >
  > Microsoft recommends deploying new devices as cloud-native using Microsoft Entra join. Deploying new devices as Microsoft Entra hybrid join devices isn't recommended, including through Autopilot. For more information, see [Microsoft Entra joined vs. Microsoft Entra hybrid joined in cloud-native endpoints: Which option is right for your organization](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined#which-option-is-right-for-your-organization).

Each of these scenarios consists of two parts, a technician flow and a user flow. At a high level, these parts are the same for Microsoft Entra join and Microsoft Entra hybrid join. The differences are primarily seen by the end user in the authentication steps.

### Technician flow

After the customer or IT Admin targets all the apps and settings they want for their devices through Intune, the pre-provisioning technician can begin the pre-provisioning process. The technician could be a member of the IT staff, a services partner, or an OEM - each organization can decide who should perform these activities. Regardless of the scenario, the process done by the technician is the same:

- Boot the device.
- From the first out-of-box experience (OOBE) screen (which could be a language selection, locale selection screen, or the Microsoft Entra sign-in page), don't select **Next**. Instead, press the Windows key five times to view another options dialog. From that screen, select the **Windows Autopilot provisioning** option and then select **Continue**.

- On the **Windows Autopilot Configuration** screen, it displays the following information about the device:
  - The Autopilot profile assigned to the device.
  - The organization name for the device.
  - The user assigned to the device (if there's one).
  - A QR code containing a unique identifier for the device. This code can be used to look up the device in Intune, which might be needed to make configuration changes. For example, assign a user or add the device to groups needed for app or policy targeting.

    > [!NOTE]
    >
    > The QR codes can be scanned using a companion app. The app also configures the device to specify who it belongs to. The Autopilot team created an open-source sample of a companion app that integrates with Intune by using the Graph API. It's available on [GitHub](https://github.com/Microsoft/WindowsAutopilotCompanion).

- Validate the information displayed. If any changes are needed, make the changes, and then select **Refresh** to redownload the updated Autopilot profile details.

- Select **Provision** to begin the provisioning process.

If the pre-provisioning process completes successfully:

- A success status screen appears with information about the device, including the same details presented previously. For example, Autopilot profile, organization name, assigned user, and QR code. The elapsed time for the pre-provisioning steps is also provided.

- Select **Reseal** to shut down the device. At that point, the device can be shipped to the end user.

> [!NOTE]
>
> Technician flow inherits behavior from [self-deploying mode](self-deploying.md). Self-Deploying Mode uses the Enrollment Status Page to hold the device in a provisioning state. The device being in a provisioning state prevents the user from proceeding to the desktop after enrollment but before software and configuration are done applying. As such, if Enrollment Status Page is disabled, the reseal button can appear before software and configuration is done applying. This behavior can allow proceeding to the user flow before the technician flow provisioning is complete. The success screen validates that enrollment was successful, not that the technician flow is necessarily complete.

If the pre-provisioning process fails:

- An error status screen appears with information about the device, including the same details presented previously. For example, Autopilot profile, organization name, assigned user, and QR code. The elapsed time for the pre-provisioning steps is also provided.
- Diagnostic logs can be gathered from the device, and then it can be reset to start the process over again.

### User flow

<!-- MAXADO 8850476 & 8911061 -->

> [!IMPORTANT]
>
> - In order to make sure tokens are refreshed properly between the Technician flow and the User flow, wait at least 90 minutes after running the Technician flow before running the User flow. This scenario mainly affects lab and testing scenarios when the User flow is run within 90 minutes after the Technician flow completes.
>
> - The User flow should be run within six months after the Technician flow finishes. Waiting more than six months can cause the certificates used by the Intune Management Engine (IME) to no longer be valid leading to errors such as:
>
>   `Error code: [Win32App][DetectionActionHandler] Detection for policy with id: <policy_id> resulted in action status: Failed and detection state: NotComputed.`
>
> - Compliance in Microsoft Entra ID is reset during the User flow. Devices might show as compliant in Microsoft Entra ID after the Technician flow completes, but then show as noncompliant once the User flow starts. Allow enough time after the User flow completes for compliance to reevaluate and update.

If the pre-provisioning process completed successfully and the device was resealed, deliver the device to the end user. The end user completes the normal Windows Autopilot user-driven process following these steps:

- Power on the device.

- Select the appropriate language, locale, and keyboard layout.

- Connect to a network (if using Wi-Fi). Internet access is always required. If using Microsoft Entra hybrid join, there must also be connectivity to a domain controller.

- If using Microsoft Entra join, on the branded sign-on screen, enter the user's Microsoft Entra credentials.

- If using Microsoft Entra hybrid join, the device will reboot; after the reboot, enter the user's Active Directory credentials.

  > [!NOTE]
  >
  > In certain circumstances, Microsoft Entra credentials might also be prompted for during a Microsoft Entra hybrid join scenario. For example, if ADFS isn't being used.

- More policies and apps are delivered to the device, as tracked by the Enrollment Status Page (ESP). Once complete, the user can access the desktop.

The device ESP reruns during the user flow so that both device and user ESP run when the user logs in. This behavior allows the ESP to install other policies that are assigned to the device after the device completes the technician phase.

> [!NOTE]
>
> If the Microsoft Account Sign-In Assistant (wlidsvc) is disabled during the Technician Flow, the Microsoft Entra sign-in option might not show. Instead, users are asked to accept the EULA, and create a local account, which might not be the desired behavior.

## Deploying a device

For more information on starting a deployment on a device when using Windows Autopilot for pre-provisioned, see the Technician flow and User flow steps of the Windows Autopilot for pre-provisioned deployment tutorials:

- [Microsoft Entra join](tutorial/pre-provisioning/azure-ad-join-workflow.md):
  - [Technician flow](tutorial/pre-provisioning/azure-ad-join-technician-flow.md).
  - [User flow](tutorial/pre-provisioning/azure-ad-join-user-flow.md).
- [Microsoft Entra hybrid](tutorial/pre-provisioning/hybrid-azure-ad-join-workflow.md):
  - [Technician flow](tutorial/pre-provisioning/hybrid-azure-ad-join-technician-flow.md).
  - [User flow](tutorial/pre-provisioning/hybrid-azure-ad-join-user-flow.md).

## Related content

<!-- Intune 12378279 -->

- [Pre-provisioning video](https://youtu.be/nE5XSOBV0rI).
- [What is a device identity?](/azure/active-directory/devices/overview).
- [Learn more about cloud-native endpoints](/mem/solutions/cloud-native-endpoints/cloud-native-endpoints-overview).
- [Tutorial: Set up and configure a cloud-native Windows endpoint with Microsoft Intune](/mem/solutions/cloud-native-endpoints/cloud-native-windows-endpoints).
- [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/device-join-plan).
- [A framework for Windows endpoint management transformation](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/a-framework-for-windows-endpoint-management-transformation/ba-p/2460684).
- [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201).
- [Success with remote Windows Autopilot and hybrid Azure Active Directory join](https://techcommunity.microsoft.com/t5/intune-customer-success/success-with-remote-windows-autopilot-and-hybrid-azure-active/ba-p/2749353).
