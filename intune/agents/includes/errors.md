---
author: paolomatarazzo
ms.author: paoloma
ms-topic: include
ms.date: 10/16/2025
---

## Common errors

###  You don't have access to this agent - Licenses

**Details:** You don't have the licenses needed to access this agent.\
Check the licensing and plugins requirements for this agent, and make sure the necessary licenses and configurations are assigned in your tenant.

###  You don't have access to this agent - Workspace

**Details:** You aren't part of the workspace needed to access this agent.\
This message indicates that your account doesn't have permission to view or use the [Security Copilot workspace](/copilot/security/workspaces-overview), which is configured at the time Security Copilot is added to your Tenant. Contact the administrator who installed or manages your Security Copilot subscription for assistance in gaining access, and see [Understand authentication in Microsoft Security Copilot](/copilot/security/authentication).

###  You don't have access to this agent - Permissions

**Details:** You don't have the permissions needed to access this agent.\
Review the roles requirements to use the agent. Work with an Intune Administrator to assign your account the required permissions.

###  The agent encountered an error and didn't finish the run. Try running the agent again.

**Details:** The agent instance failed to start or successfully complete its run. Details of the failure can't be identified. Despite failing to run or complete, admins can continue to view and manage the agent suggestions from past runs.\
If the agent continues to fail, it's possible that its lost authorization for its identity account and can't run until it's reauthorized. Possible reasons for a loss of authorization include but aren't limited to:
- The agent's authorization period of 90 days was reached.
- The user account that the agent was installed with is subject to a policy that requires periodic reauthentication.
- An access token has been revoked.

Agent reauthorization requires that the agent is removed and then set up again.
> [!WARNING]
> When an agent is removed, all existing agent suggestions are deleted. This includes details about suggestions that were marked as *Applied*.