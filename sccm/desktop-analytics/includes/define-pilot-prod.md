---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
---

Use the following definitions to differentiate between pilot and production:  

- **Pilot**: A subset of your devices that you want to validate before you deploy to a larger set. Use Desktop Analytics to mark devices as unique to the pilot set. Devices in the pilot are ready to upgrade when no assets are blocking. A blocking asset is marked as *critical* and *unable* to upgrade.  

- **Production**: All other devices enrolled to Desktop Analytics that aren't in the pilot. Production devices are ready to upgrade when all assets are signed-off. Desktop Analytics automatically signs off any non-critical assets.  

