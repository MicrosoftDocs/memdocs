---
title: Client health checks
titleSuffix: Configuration Manager
description: The checks that the Configuration Manager client runs regularly to keep healthy.
ms.date: 11/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Client health checks

*Applies to: Configuration Manager (current branch)*

The Configuration Manager client regularly runs the checks and remediations to keep healthy. For more information, see [How to monitor clients](monitor-clients.md).

## Client checks

### Verify that the client was installed correctly

<!--AD9CAF50-6602-4857-A9F4-64864EA30BDF-->

If the client isn't correctly installed, start by troubleshooting client install. Review the ccmsetup.log. Oftentimes, remediation requires that you reinstall the client.

### Verify the client service

There are three checks for the **SMS Agent Host** client service (`CcmExec`):

- First, it verifies that the service exists.<!--8883C683-04C8-4228-BB76-2EDD666BA781--> If it doesn't exist, you need to reinstall the client.

- Next, it verifies that the service startup type is automatic.<!--13F46523-5B82-417d-A363-A644E80CAD76--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something else isn't automatically configuring the service startup type.

- Then it verifies that the client service is running.<!--70BECB51-44A1-4b46-8A23-6EA3D345B677-->. The remediation for this check is to start the client service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service. Review client logs to make sure it's not failing to start.

### Verify that client check has recently run

<!--33F46523-5B82-417d-A363-A644E80CAD76-->

Verify that the client check scheduled task (`CcmEval`) has run at least one time in the past three days. You can manually run the scheduled task. Make sure that Windows is able to run scheduled tasks.

### Verify that the client database is healthy

<!--7B9F8FF6-EDF7-42CA-A67F-073A2E161C19-->

The client uses Microsoft SQL Server Compact Edition (CE) to locally store information. If this check fails, reinstall the Configuration Manager client to remediate.

### Verify WMI

There are several checks specific to WMI. The first three checks are for the **Windows Management Instrumentation** (WMI) service (`Winmgmt`).

- Verify that the service exists.<!--4AB7D77D-3BB0-4EAB-BEFD-7C0F7DA10296--> WMI is a fundamental component of Windows. If this service doesn't exist, you may need to reinstall Windows.
- Verify that the service startup type is automatic.<!--518C0699-03F8-4F38-85C4-4D319EAEFC05--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something else isn't automatically configuring the service startup type.
- Verify that the service is running.<!--7F4B6E15-2221-455B-9615-93C379E470D5--> The remediation for this check is to start the WMI service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service.

There are two other checks to test the overall health of WMI on the device:

- The WMI repository integrity test checks that Configuration Manager client entries exist in WMI.<!--A81778B5-9A1E-4A52-9C6E-6939CEFAA118--> If this check fails, reinstall the Configuration Manager client.
- The WMI event sink test checks whether the Configuration Manager-related WMI event sink is lost.<!--C35E790D-4C05-40A8-BB46-A68578966D19--> If this check fails, restart the client service.

### Verify the antimalware service

There are two checks for whatever antimalware service is registered with Windows:

- Verify that the antimalware service startup type is automatic.<!--09886543-BE8B-431F-BC00-7D917632E22C--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something else isn't automatically configuring the service startup type.
- Verify that the antimalware service is running.<!--5B50566C-363E-4F1C-8A7D-6F2D2A51B142--> The remediation for this check is to start the antimalware service. Then monitor it to make sure it keeps running. Review Windows event logs to see if there are any related activities that might be stopping the service.

### Verify Windows Update service

This check verifies that the **Windows Update** service (`wuauserv`) startup type is automatic or manual.<!--E8030BE0-B773-4742-B6A1-0870CF139117,D6CB32EA-423D-44CB-9C58-97CE55D2148E--> To remediate a failure with this check, reset the service startup type to automatic. Check group policies to make sure something else isn't automatically configuring the service startup type.


| Verify that the **Microsoft Policy Platform** service (`lppsvc`) exists<!--7EF00FDD-3DF0-496A-A999-AADD1B3016C1--> | Repair the policy platform |  |
| Verify that the policy platform service startup type is manual<!--D9D0245D-0617-4C2F-8837-84A397AC5B22--> | Reset the service startup type to manual |  |
| Policy platform WMI integrity test<!--0614757F-7AA6-4933-965B-06D6A8243D0B--> | Repair the policy platform |  |
| Verify that the **Background Intelligent Transfer Service** (BITS) exists<!--5CC6C949-5001-4765-84B4-DD4FDC1E6940--> | No remediation |  |
| Verify that the BITS startup type is automatic or manual<!--C6E29CF5-F9B2-450B-AE61-C4B256A75023--> | Reset the service startup type to automatic |  |
| Verify that the Network Inspection Service startup type is manual<!--6BC824B4-BD8C-4779-BB10-ABDBCD5AFAEB--> | Reset the service startup type to manual |  |
| Verify that the **Configuration Manager Remote Control** service (`CmRcService`) startup type is automatic or manual<!--9040BA8C-580D-4FCA-8846-BBD5F5BB1597--> | Reset the service startup type to automatic |  |
| Verify that the remote control service is running<!--9DCD49EF-E021-46FF-A777-49210B558527--> | Start the remote control service |  |
| Verify that the **Configuration Manager Wake-up Proxy** service (ConfigMgr Wake-up Proxy) is running<!--43029EED-EB9D-4E35-A5F7-7FDD93EC8C57--> | Start the wake-up proxy service | This check is made only if the **Power Management**: **Enable wake-up proxy** client setting is set to **Yes** on supported client operating systems. |
| Verify that the wake-up proxy service (ConfigMgr Wake-up Proxy) startup type is automatic<!--934F12E3-295E-4BA0-AE0F-09859685720F--> | Reset the wake-up proxy service startup type to automatic | This check is made only if the **Power Management**: **Enable wake-up proxy** client setting is set to **Yes** on supported client operating systems. |

<!-- need to confirm if these checks are still applicable
|WMI repository read and write test<!--14E6774A-1795-4E09-B17D-B6F36A124205--|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy<!--690A959D-6210-4930-865F-E3BB82F02133--|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->

## Most common check failures

The following checks are the most commonly reported failures. The numbers are included to provide scale between the checks.

- Verify CcmEval task has run in recent cycles (4,950)
- Verify/Remediate client prerequisites (554)
- Verify/Remediate Windows Update service startup type on Windows 8 (399)
- Verify/Remediate Configuration Manager Remote Control service status (345)
- Verify/Remediate Configuration Manager Remote Control service startup type (294)
- Verify/Remediate SMS Agent Host service status (249)
- Verify/Remediate SQL CE database is healthy (157)
- Verify/Remediate client WMI Provider (131)
- Verify/Remediate client installation (120)
- WMI Event Sink Test (93)

## Next steps

[Client health dashboard](client-health-dashboard.md)

[How to configure client status](../deploy/configure-client-status.md#automatic-remediation-exclusion)

[How to deploy clients to Windows computers](../deploy/deploy-clients-to-windows-computers.md)

[Configuration Manager troubleshooting](/troubleshoot/mem/configmgr/welcome-configuration-manager)
