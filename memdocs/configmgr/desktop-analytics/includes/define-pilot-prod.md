---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 01/12/2021
---

Use the following definitions to differentiate between pilot and production:  

- **Pilot**: A subset of your devices that you want to validate before you deploy to a larger set. Use Desktop Analytics to add individual devices to the pilot set. Devices in the pilot are ready to upgrade when:

 - All assets that have [Microsoft known issues](../compat-assessment.md#microsoft-known-issues) have been marked with *Ready* or *Ready (with remediation)*.

 - No *critical* or *important* assets have been marked with *unable* to upgrade.  

- **Production**: All other devices enrolled to Desktop Analytics that aren't in the pilot. Production devices are ready to upgrade when all *critical* and *important* assets are marked as *Ready* or *Ready (with remediation)*. Desktop Analytics automatically signs off all other assets.  
