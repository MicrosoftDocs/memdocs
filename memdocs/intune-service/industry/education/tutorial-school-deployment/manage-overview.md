---
title: Manage devices with Microsoft Intune
description: Overview of device management capabilities in Intune for Education, including remote actions, remote assistance, and inventory/reporting.
ms.date: 5/2/2024
ms.topic: tutorial
author: scottbreenmsft
ms.author: scbree
ms.manager: dougeby
ms.service: microsoft-intune
ms.subservice: education
---

# Manage devices with Microsoft Intune

Microsoft Intune offers a streamlined remote device management experience throughout the school year. IT administrators can optimize device settings, deploy new applications, updates, ensuring that security and privacy are maintained.

:::image type="content" source="./images/protect-manage.png" alt-text="The device lifecycle for Intune-managed devices - protect and manage devices" border="false":::

With Intune, there are several ways to manage students' devices. Groups can be created to organize devices and students, to facilitate remote management. You can determine which applications students have access to, and fine tune device settings and restrictions. You can also monitor which devices students sign in to, and troubleshoot devices remotely.

## Remote actions

✅ Remotely trigger actions on devices

Intune allows you to perform actions on devices without having to sign in to the devices. For example, you can send a command to a device to restart or to turn off, or you can locate a device.

### [Intune](#tab/intune)

:::image type="content" source="./images/intune-remote-actions-windows.png" alt-text="Remote actions available in Intune for Education when selecting a Windows device" lightbox="./images/intune-remote-actions-windows.png" border="true":::

Remote actions can be performed on one or multiple devices at once.

To learn more about remote actions in Intune, see [Remote actions](/mem/intune-service/remote-actions/device-management).

### [Intune For Education](#tab/intune-for-education)

:::image type="content" source="./images/remote-actions.png" alt-text="Remote actions available in Intune for Education when selecting a Windows device" lightbox="./images/remote-actions.png" border="true":::

With bulk actions, remote actions can be performed on multiple devices at once.

To learn more about remote actions in Intune for Education, see [Remote actions][EDU-1].

---

## Remote assistance

✅ View and control remote devices

With devices managed by Intune, you can remotely assist students and teachers that are having issues with their devices.

For more information, see [Remote assistance for managed devices][EDU-2].

## Device inventory and reporting

✅ View device information and reporting

With Intune, it's possible view and report on current devices, applications, settings, and overall health. You can also download reports to review or share offline.

### [Intune](#tab/intune)

Here are some examples of the reports available in Intune:

- Device compliance reports
- Device configuration reports
- Device enrollment reports
- Update reports
- Security reports
- Application reports

To learn more about reports in Intune, see [Reports in Intune](/mem/intune-service/fundamentals/reports).

### [Intune For Education](#tab/intune-for-education)

Here are the steps for generating reports in Intune for Education:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Reports**.
1. Select between one of the report types:
    - Device inventory
    - Device actions
    - Application inventory
    - Settings errors
    - Windows Defender
    - Autopilot deployment
1. If needed, use the search box to find specific devices, applications, and settings.
1. To download a report, select **Download**. The report downloads a comma-separated value (CSV) file, which you can view and modify in a spreadsheet app like Microsoft Excel.
    :::image type="content" source="./images/inventory-reporting.png" alt-text="Reporting options available in Intune for Education when selecting the reports blade" border="true":::

To learn more about reports in Intune for Education, see [Reports in Intune for Education][EDU-3].

---

________________________________________________________

> [!div class="nextstepaction"]
> [Next: Reset and Wipe >](reset-wipe.md)

<!-- Reference links in article -->

[EDU-1]: /intune-education/edu-device-remote-actions
[EDU-2]: /intune-education/remote-assist-mobile-devices
[EDU-3]: /intune-education/what-are-reports
