---
author: paolomatarazzo
ms.author: paoloma
ms-topic: include
ms.date: 11/10/2025
---

## Renew the agent

Agents expire after 90 days of inactivity. When authentication expires, agent runs fail until you reauthenticate. You can renew authentication at any time.

As expiration approaches, Intune displays a warning on the agent overview page. Both **Copilot owners** and **Copilot contributors** can see this banner, which prompts you to renew the agent identity.

**To renew the agent:**

1. Open the [Microsoft Security Copilot admin center][COP-PORTAL] and sign in with an account that has the required permissions.
2. Select **Agents**.
3. Find the agent that needs renewal and select **Go to agent**.
4. On the agent details page, select **...**, then select **Edit**.
5. Select **Renew authentication**. The agent uses your signed-in credentials by default. To use different credentials, select **Re-authenticate** and provide them.

After renewal, the warning banner disappears and a toast notification confirms success.

[COP-PORTAL]: https://go.microsoft.com/fwlink/?linkid=2247989