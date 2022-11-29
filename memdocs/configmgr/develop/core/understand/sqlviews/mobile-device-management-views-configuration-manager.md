---
title: Mobile device management views
titleSuffix: Configuration Manager
description: Information about the mobile device configuration items and configuration packages.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 3c8dc27b-0839-488d-9931-c897f136bfad
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Mobile device management views in Configuration Manager

Mobile device management views in Configuration Manager contain information about the mobile device configuration items and configuration packages. The mobile device management status views provide client deployment and client health state information, and the mobile device management hardware inventory views contain information about the inventory collected from mobile device.

The following sections provide detailed information about mobile device management views, mobile device management status views, and mobile device management hardware inventory views.

## Mobile device management status views

The mobile device management status views contain information about the mobile device deployment and client health states. For more information about status views, see [Status and alert views in Configuration Manager](status-alert-views-configuration-manager.md). The status views that contain mobile devices information are described in this section.

### v_DeviceClientDeploymentState

Lists all Configuration Manager mobile device clients, by device client ID, NetBIOS name, and device ID, and the last device deployment state reported, as well as the assigned site code, device client version, and so on. The view is also listed and described in the [Client deployment views in Configuration Manager](client-deployment-views-configuration-manager.md) topic.
The view can be joined to other views by using the **DeviceClientID**, **DeviceNetBiosName**, and **DeviceDeploymentState** columns. The **DeviceDeploymentState** column contains the state ID for topic type 800. The **DeviceClientID** column contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view. The Configuration Manager states are listed in the **v_StateNames** view.

### v_DeviceClientHealthState

Lists all Configuration Manager mobile device clients, by device client ID, NetBIOS name, and device ID, and the health state of the device, as well as the assigned site code, owner name, and so on. The view is also listed and described in the [Client status views in Configuration Manager](client-status-views-configuration-manager.md) topic.
The view can be joined to other views by using the **DeviceClientID**, **DeviceNetBiosName**, **HealthType**, and **HealthState** columns. The **DeviceClientID** column in this view contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view. The **HealthType** column in this view contains the same information as the **TopicType** column in the **v_StateNames** view and the **HealthState** column in this view contains the same information as the **StateID** column in the **v_StateNames** status view. Client health state messages have a state type from 1000 to 1004. The Configuration Manager states are listed in the **v_StateNames** view.

### v_DeviceClientUpdateState

Lists information about client updates applied to the mobile device client.
The view can be joined to other views by using the **DeviceClientID**, **DeviceNetBiosName**, and **DeviceDeploymentState** columns. The **DeviceDeploymentState** column contains the state ID for topic type 800. The **DeviceClientID** column contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view. The Configuration Manager states are listed in the **v_StateNames** view.

### v_RBAC_WinRTSideLoadingKeys

Lists information about the configured sideloading keys for Windows RT including a description, the maximum number of activations allowed, the type of key and more.
It is unlikely that this view will be joined to other views.

## Mobile device management views

The mobile device management views contain information about the status of mobile devices in your hierarchy and contain the information described in this section.

### v_DM_RetireRecords

Lists information about devices that have been retired from management.
The view can be joined with other views by using the **DeviceName** column.

### v_DM_WipeRecords

Lists information about devices that have been wiped by Configuration Manager.
The view can be joined with other views by using the **DeviceName** column.

## Mobile device management hardware inventory views

The mobile device management hardware inventory views contain information about mobile devices that is retrieved as part of hardware inventory. For more information about hardware inventory views, see [Hardware inventory views in Configuration Manager](hardware-inventory-views-configuration-manager.md). The hardware inventory views that contain mobile device information are described in this section.

### v_GS_DEVICE_CERTIFICATES

Lists information about the certificates on devices, including the revision ID, issuer, where it is located in the certificate store, the subject, the dates the certificate is valid, and so on.
The view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_COMPUTERSYSTEM

Lists information about the Configuration Manager devices, including the manufacturer, model, phone number, processor, and more.
The view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_DISPLAY

Lists information about the displays found on Configuration Manager devices including the display resolution, number of colors and more.
The view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_MEMORY

Lists information about the memory found on Configuration Manager devices.
The view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_OS_INFORMATION

Lists information about the operating system found on Configuration Manager devices.
The view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_POWER

Lists information about power settings and the battery on Configuration Manager devices.
The view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_CLIENT

Lists information about the device client on Configuration Manager managed devices.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_CLIENTAGENTVERSION

Lists information about the client version installed on Configuration Manager managed client devices.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_EMAIL

Lists information about the email settings on a device. This includes the email address, domain, synchronization server and more.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_ENCRYPTION

Lists information about the encryption settings on devices including for email, phone memory and external storage devices.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_BLUETOOTH

Lists information about whether Bluetooth is enabled on device clients.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_CAMERA

Lists information about the camera on mobile devices including whether it is enabled.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_EXCHANGE

Lists Microsoft Exchange settings for mobile devices, such as the maximum size of file attachment, when email is sent, synchronization settings and more.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_INFO

Lists general information about mobile devices including the manufacturer and model, the operating system and more.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_INSTALLEDAPPLICATIONS

Lists the name and version of all applications installed on the device.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_IRDA

Lists information about the IRDA (infra-red) port on devices and whether it is enabled.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_MEMORY_ADDRESS

Lists the memory address ranges found on the device.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_PASSWORD

Lists information about the password settings on mobile devices, such as the maximum incorrect passwords that can be entered before the device is wiped, when the password expires, and more.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_POLICY

Lists information about policies assigned to devices.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_WINDOWSSECURITYPOLICY

Lists information about the Windows Security policy assigned to Windows Mobile devices.
This view can be joined with other views by using the **ResourceID** column.

### v_GS_DEVICE_WLAN

Lists information about network settings on mobile devices, including whether the network is enabled.
This view can be joined with other views by using the **ResourceID** column.

## Exchange ActiveSync views

### v_EAS_Organization

Lists information about the Exchange Server and the organization that manage mobile devices.
It is unlikely that this view will be joined to other views.

### v_EAS_Property

Lists information about all devices that are managed by Exchange ActiveSync. This includes the device ID, name, domain, the operating system of the device and more.
This view can be joined to other views by using the **DeviceID** column.

### v_DeviceJailBrokenStatus

Lists, by **ItemKey**, devices and whether they have been jailbroken.
It is unlikely that this view will be joined to other views.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
