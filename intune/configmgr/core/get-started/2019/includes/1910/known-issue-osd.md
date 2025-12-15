---
author: Banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 10/17/2019


---

### <a name="ki_osd"></a> Task sequences aren't available to PXE or media

<!--5578298-->
If you deploy a task sequence for PXE or media (USB or DVD), the client doesn't receive the policy. The following message is in **smsts.log**:

`There are no task sequences available to this computer.`

#### Workaround

Start the task sequence from Software Center.
