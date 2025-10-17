---
author: paolomatarazzo
ms.author: paoloma
ms-topic: include
ms.date: 10/16/2025
---

### Renew the agent

If you don't use the agent for 90 days, the agent authorization expires. As the agent authorization period approaches expiration, Intune raises an alert that's visible to each Copilot owner and Copilot contributor in a warning banner on the agent overview page. The warning alerts Copilot owners and contributors to the end of the authorized period and prompts for the renewal of the agent identity. If the agent authentication expires, subsequent agent runs fail until reauthentication. You can renew the agent authentication before or after expiration. 

To reauthorize the agent identity, select **Renew authentication**. After renewal, the warning banner disappears, and a toast notification appears to validate that renewal is successful. 

> [!IMPORTANT]
> When you renew the agent authentication, the agent uses your credentials. If you don't want the identity to change, make sure the user who authorizes renewal is the same user who the agent identity was already under. 