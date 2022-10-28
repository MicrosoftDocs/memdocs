---
author: banreet
ms.author: banreetkaur
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.localizationpriority: medium
---

### Server connectivity endpoints

The service connection point needs to communicate with the following endpoints:

| Endpoint  | Function  |
|-----------|-----------|
| `https://aka.ms` | Used to locate the service |
| `https://graph.windows.net` | Used to automatically retrieve settings like CommercialId when attaching your hierarchy to Desktop Analytics (on Configuration Manager Server role). For more information, see [Configure the proxy for a site system server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection memberships, deployment plans, and device readiness status with Desktop Analytics (on Configuration Manager Server role only). For more information, see [Configure the proxy for a site system server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | For diagnostic data from on-premises service connector to gain insights about the health of cloud-connected services.<!--7541816--> |

### User experience and diagnostic component endpoints

Client devices need to communicate with the following endpoints:

| Endpoint  | Function  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 10, version 1809 or later, or version 1803 with the 2018-09 cumulative update or later installed. |
| `https://v10.events.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 10, version 1803 _without_ the 2018-09 cumulative update installed. |
| `https://v10.vortex-win.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 10, version 1709 or earlier. |
| `https://vortex-win.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 7 and Windows 8.1 |

### Client connectivity endpoints

Client devices need to communicate with the following endpoints:

| Index | Endpoint  | Function  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Enables the compatibility update to send data to Microsoft. |
| 2 | `http://adl.windows.com` | Allows the compatibility update to receive the latest compatibility data from Microsoft. |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1803 or earlier. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required for device health reports in Windows 10, version 1809 or later. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1809 or later. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1809 or later. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1809 or later. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1809 or later. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1809 or later. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows Error Reporting (WER)](/windows/win32/wer/windows-error-reporting). Required to monitor deployment health in Windows 10, version 1809 or later. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Online Crash Analysis (OCA)](/windows/win32/dxtecharts/crash-dump-analysis). Required for device health reports in Windows 10, version 1809 or later. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Online Crash Analysis (OCA)](/windows/win32/dxtecharts/crash-dump-analysis). Required to monitor deployment health in Windows 10, version 1803 or earlier. |
| 13 | `https://login.live.com` | Required to provide a more reliable device identity for Desktop Analytics. <br> <br>To disable end-user Microsoft account access, use policy settings instead of blocking this endpoint. For more information, see [The Microsoft account in the enterprise](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Connected user experience and diagnostic component endpoint. |