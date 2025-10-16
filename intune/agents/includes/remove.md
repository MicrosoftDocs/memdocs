---
author: paolomatarazzo
ms.author: paoloma
ms-topic: include
ms.date: 10/16/2025
---

## Remove the agent instance

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To remove an agent instance in Security Copilot, your account must have the *Owner* role.\
> Accounts with the *Contributor* role can run agents and view results, but they cannot manage or remove agent instances.
:::column-end:::
:::row-end:::

Steps to remove an agent instance:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents**.
1. Select the agent instance you want to remove.
1. Select **Remove agent** and confirm the removal.

> [!WARNING]
> Removing an agent deletes all existing suggestions, including those marked as complete. Previously applied suggestions will remain unchanged.

After removal:

- The agent pane returns to its original state.
- An admin can reinstall the agent later by repeating the setup process.

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431