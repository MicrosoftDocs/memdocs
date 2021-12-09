---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 05/28/2021
ms.localizationpriority: medium
---

### <a name="ki_ta"></a> Known issue with tenant attach onboarding

<!--10001852-->

After you upgrade to technical preview branch version 2105.2, if you try to [enable tenant attach](../../../../../tenant-attach/device-sync-actions.md), Configuration Manager immediately offboards the site from tenant attach.

This issue doesn't affect sites that already have tenant attach enabled.

To work around this issue, set the following registry entry on the site system that hosts the service connection point role:

```powershell
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_SERVICE_CONNECTOR" -Name "HeartbeatWorker_IntervalSec" -Value 60
```

After you configure this registry entry, then enable tenant attach.
