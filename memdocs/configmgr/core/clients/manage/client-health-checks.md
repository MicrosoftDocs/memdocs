---
title: Client health checks
titleSuffix: Configuration Manager
description: The checks that the Configuration Manager client runs regularly to keep healthy.
ms.date: 04/01/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: reference
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Client health checks

*Applies to: Configuration Manager (current branch)*

The Configuration Manager client regularly runs the checks and remediations to keep healthy. For more information, see [How to monitor clients](monitor-clients.md).

## Client checks

### Verify that the client was installed correctly

<!--AD9CAF50-6602-4857-A9F4-64864EA30BDF-->

If the client isn't correctly installed, start by troubleshooting client install. Review the ccmsetup.log. Often, remediation requires that you reinstall the client.

### Verify that client prerequisites are installed

<!--2F373187-6295-4CBB-BE9E-8E43C459883A-->

Verify that the [client prerequisites](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md) are installed. It reads the file ccmsetup.xml in the client installation folder to discover the prerequisites. By default: `C:\Windows\ccmsetup\ccmsetup.xml`

Most client prerequisites are available by default in Windows, or installed automatically by the Configuration Manager client. To remediate problems with prerequisites, you can try to install them manually, or reinstall the client.

### Verify that there is sufficient disk space

Verify that there is greater that 1% disk space remaining on C drive.

### Verify the client service

There are three checks for the **SMS Agent Host** client service (`CcmExec`):

- First, it verifies that the service exists.<!--8883C683-04C8-4228-BB76-2EDD666BA781--> If it doesn't exist, you need to reinstall the client.

- Next, it verifies that the service startup type is automatic.<!--13F46523-5B82-417d-A363-A644E80CAD76--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

- Then it verifies that the client service is running.<!--70BECB51-44A1-4b46-8A23-6EA3D345B677--> The remediation for this check is to start the client service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service. Review client logs to make sure it's not failing to start.

### Verify that client check has recently run

<!--33F46523-5B82-417d-A363-A644E80CAD76-->

Verify that the client check scheduled task (`CcmEval`) has run at least one time in the past three days. You can manually run the scheduled task. Make sure that Windows can run scheduled tasks.

### Verify that the client database is healthy

<!--7B9F8FF6-EDF7-42CA-A67F-073A2E161C19-->

The client uses a built-in version of SQL Server Compact Edition (CE) to locally store information. If this check fails, reinstall the Configuration Manager client to remediate.

### Verify WMI

There are several checks specific to WMI. The first three checks are for the **Windows Management Instrumentation** (WMI) service (`Winmgmt`).

- Verify that the service exists.<!--4AB7D77D-3BB0-4EAB-BEFD-7C0F7DA10296--> WMI is a fundamental component of Windows. If this service doesn't exist, you may need to reinstall Windows.

- Verify that the service startup type is automatic.<!--518C0699-03F8-4F38-85C4-4D319EAEFC05--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

- Verify that the service is running.<!--7F4B6E15-2221-455B-9615-93C379E470D5--> The remediation for this check is to start the WMI service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service.

There are two other checks to test the overall health of WMI on the device:

- The WMI repository integrity test checks that Configuration Manager client entries exist in WMI.<!--A81778B5-9A1E-4A52-9C6E-6939CEFAA118--> If this check fails, reinstall the Configuration Manager client.

- The WMI event sink test checks whether the Configuration Manager-related WMI event sink is lost.<!--C35E790D-4C05-40A8-BB46-A68578966D19--> If this check fails, restart the client service.

### Verify the antimalware service

There are two checks for whatever antimalware service is registered with Windows:

- Verify that the antimalware service startup type is automatic.<!--09886543-BE8B-431F-BC00-7D917632E22C--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

- Verify that the antimalware service is running.<!--5B50566C-363E-4F1C-8A7D-6F2D2A51B142--> The remediation for this check is to start the antimalware service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service.

If you're using Windows Defender, the Configuration Manager client also verifies the **Windows Defender Antivirus Network Inspection Service** (`WdNisSvc`).<!--6BC824B4-BD8C-4779-BB10-ABDBCD5AFAEB--> It checks to make sure the service startup type is manual.

### Verify Windows Update service

This check verifies that the **Windows Update** service (`wuauserv`) startup type is automatic or manual.<!--E8030BE0-B773-4742-B6A1-0870CF139117,D6CB32EA-423D-44CB-9C58-97CE55D2148E--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

### Verify the policy platform

There are three checks for the **Microsoft Policy Platform** service (`lppsvc`):

- Verify that the service exists.<!--7EF00FDD-3DF0-496A-A999-AADD1B3016C1--> The policy platform is one of the [prerequisite components that the Configuration Manager client automatically installs](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#components-automatically-downloaded-during-installation). If this service doesn't exist, reinstall the Configuration Manager client.

- Verify that the service startup type is manual.<!--D9D0245D-0617-4C2F-8837-84A397AC5B22--> To remediate a failure with this check, reset the service startup type to manual. Check group policies to make sure something isn't automatically configuring the service startup type.

- Policy platform WMI integrity test.<!--0614757F-7AA6-4933-965B-06D6A8243D0B--> Repair the policy platform.<!-- need to validate with engineering whether this older process is valid and supported: http://sccmbrokeit.blogspot.com/2013/10/sccm-2012-client-troubleshooting.html -->

### Verify BITS service

There are two checks for the **Background Intelligent Transfer Service** (`BITS`):

- Verify that the service exists.<!--5CC6C949-5001-4765-84B4-DD4FDC1E6940--> BITS is a fundamental component of Windows. If this service doesn't exist, you may need to reinstall Windows.

- Verify that the service startup type is automatic or manual.<!--C6E29CF5-F9B2-450B-AE61-C4B256A75023--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

### Verify remote control

If you enable the [remote control agent in client settings](../deploy/about-client-settings.md#remote-tools), there are two checks for the **Configuration Manager Remote Control** service (`CmRcService`):

- Verify that the service type is automatic or manual.<!--9040BA8C-580D-4FCA-8846-BBD5F5BB1597--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

- Verify that the service is running.<!--9DCD49EF-E021-46FF-A777-49210B558527--> The remediation for this check is to start the remote control service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service.

### Verify wake-up proxy

If you enable the [wake-up proxy in client settings](../deploy/about-client-settings.md#power-management), there are two checks for the **Configuration Manager Wake-up Proxy** service:

- Verify that the service startup type is automatic.<!--934F12E3-295E-4BA0-AE0F-09859685720F--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something isn't automatically configuring the service startup type.

- Verify that the service is running.<!--43029EED-EB9D-4E35-A5F7-7FDD93EC8C57--> The remediation for this check is to start the wake-up proxy service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service.

<!-- need to confirm if these checks are still applicable

|WMI repository read and write test<!--14E6774A-1795-4E09-B17D-B6F36A124205--|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  

|Verify that the client WMI provider is healthy<!--690A959D-6210-4930-865F-E3BB82F02133--|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|

717C0799-02F8-2F38-25C4-2D319EAEFC07	Verify/Remediate Mobile Devices state.

 -->

## Most common check failures

The following checks have the most commonly reported failures. The numbers are included to provide scale between the checks.

- Verify CcmEval task has run in recent cycles (4,950)
- Verify client prerequisites (554)
- Verify Windows Update service startup type (399)
- Verify Configuration Manager Remote Control service status (345)
- Verify Configuration Manager Remote Control service startup type (294)
- Verify SMS Agent Host service status (249)
- Verify SQL Server CE database is healthy (157)
- Verify client WMI Provider (131)
- Verify client installation (120)
- WMI event sink test (93)

## Next steps

[Client health dashboard](client-health-dashboard.md)

[How to configure client status](../deploy/configure-client-status.md#automatic-remediation-exclusion)

[How to deploy clients to Windows computers](../deploy/deploy-clients-to-windows-computers.md)

[Configuration Manager troubleshooting](/troubleshoot/mem/configmgr/welcome-configuration-manager)
