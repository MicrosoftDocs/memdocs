---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
---

- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

The service connection point makes a long standing outgoing connection to the notification service hosted on `https://*.manage.microsoft.com`. Verify the proxy used for the service connection point doesn't time out outgoing connections too quickly. We recommend 3 minutes for outgoing connections to this internet endpoint. <!--7820969-->