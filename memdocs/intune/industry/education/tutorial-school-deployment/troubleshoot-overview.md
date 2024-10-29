---
title: Troubleshoot Windows devices
description: Learn how to troubleshoot Windows devices from Intune and contact Microsoft Support for issues related to Intune and other services.
ms.date: 05/02/2024
zone_pivot_groups: platforms-windows-ios
ms.topic: tutorial
ms.author: scbree
author: scottbreenmsft
ms.manager: dougeby
---

# Troubleshoot devices

Microsoft Intune provides many tools that can help you troubleshoot devices.

- [Troubleshooting device enrollment in Intune][MEM-2]
- [Troubleshooting policies and profiles in Microsoft Intune][MEM-5]
- [Troubleshooting device actions in Intune][MEM-3]

::: zone pivot="windows"
Here's a collection of resources to help you troubleshoot Windows devices managed by Intune:

- [Troubleshooting Windows Autopilot overview][MEM-9]
- [Troubleshoot Windows Wi-Fi profiles][MEM-6]
- [Troubleshooting BitLocker with the Intune encryption report][MEM-4]
- [Troubleshooting custom settings][MEM-8]
- [Troubleshooting Win32 app installations with Intune][MEM-7]
- [**Collect diagnostics**][MEM-10] is a remote action that lets you collect and download Windows device logs without interrupting the user
  :::image type="content" source="./images/intune-diagnostics.png" alt-text="Intune for Education dashboard" lightbox="./images/intune-diagnostics.png" border="true":::

::: zone-end

::: zone pivot="ios"
Here's a collection of resources to help you troubleshoot iOS devices managed by Intune:

- [iOS or iPadOS devices aren't checking in with the Intune service](/troubleshoot/mem/intune/device-enrollment/ios-devices-inactive)
- [Troubleshooting iOS/iPadOS device enrollment errors in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors)
- [iOS or iPadOS device is stuck on an enrollment screen](/troubleshoot/mem/intune/device-enrollment/device-stuck-in-enrollment)
- [Troubleshooting profile installation failed error on iOS or iPadOS devices](/troubleshoot/mem/intune/device-enrollment/profile-installation-failed)
- [Intune enrollment process doesn't start on Apple Automated Device Enrollment devices](/troubleshoot/mem/intune/device-enrollment/apple-dep-device-fails-auto-enrollment)
- [ADE enrollment error 'XPC_TYPE_ERROR Connection invalid'](/troubleshoot/mem/intune/device-enrollment/dep-enrollment-xpc-type-error)
- [You can't access company resources on an Intune-enrolled ADE device](/troubleshoot/mem/intune/device-protection/cannot-access-company-resources-on-dep)
::: zone-end

## How to contact Microsoft Support

Microsoft provides global technical, pre sales, billing, and subscription support for cloud-based device management services. This support includes Microsoft Intune, Configuration Manager, Windows 365, and Microsoft Managed Desktop.

Follow these steps to obtain support in Microsoft Intune provides many tools that can help you troubleshoot Windows devices:

- Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
- Select **Troubleshooting + support** > **Help and support**.
    :::image type="content" source="images/advanced-support.png" alt-text="Screenshot that shows how to obtain support from Microsoft Intune." lightbox="images/advanced-support.png":::
- Select the required support scenario: Configuration Manager, Intune, Co-management, or Windows 365.
- Above **How can we help?**, select one of three icons to open different panes: *Find solutions*, *Contact support*, or *Service requests*.
- In the **Find solutions** pane, use the text box to specify a few details about your issue. Depending on the presence of specific keywords, the console provides help like:
  - Run diagnostics: start automated tests and investigations of your tenant from the console to reveal known issues. When you run a diagnostic, you may receive mitigation steps to help with resolution.
  - View insights: find links to documentation that provides context and background specific to the product area or actions relating to your issue.
  - Recommended articles: browse suggested troubleshooting topics and other content related to your issue.
- If needed, use the *Contact support* pane to file an online support ticket.
  > [!IMPORTANT]
  > When opening a case, be sure to include as many details as possible in the *Description* field. Such information includes: timestamp and date, device ID, device model, serial number, OS version, and any other details relevant to the issue.
- To review your case history, select the **Service requests** pane. Active cases are at the top of the list, with closed issues also available for review.

For more information, see [Microsoft Intune support page][MEM-1].

________________________________________________________

> [!div class="nextstepaction"]
> [Next: Common Education configuration overview >](common-config-overview.md)

<!-- Reference links in article -->
[MEM-1]: /mem/get-support
[MEM-2]: /troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune
[MEM-3]: /troubleshoot/mem/intune/troubleshoot-device-actions
[MEM-4]: /troubleshoot/mem/intune/troubleshoot-bitlocker-admin-center
[MEM-5]: /troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune
[MEM-6]: /troubleshoot/mem/intune/troubleshoot-wi-fi-profiles#troubleshoot-windows-wi-fi-profiles
[MEM-7]: /troubleshoot/mem/intune/troubleshoot-win32-app-install
[MEM-8]: /troubleshoot/mem/intune/troubleshoot-csp-custom-settings
[MEM-9]: /autopilot/troubleshooting-faq#troubleshooting-windows-autopilot-overview
[MEM-10]: /mem/intune/remote-actions/collect-diagnostics
