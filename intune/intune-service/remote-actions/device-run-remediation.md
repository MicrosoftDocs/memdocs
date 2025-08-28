---
# required metadata

title: Run Remediation
description: Learn how to initiate on demand proactive remediation with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---


# Run remediation



> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Run Remediation**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Managed devices/Read, Update)



## Reference links

- Microsoft Graph API reference: [initiateOnDemandProactiveRemediation action][GRAPH-1]


<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-initiateondemandproactiveremediation
