---
title: include file
description: include file
author: ErikjeMS  
ms.service: cloudpc
ms.topic: include
ms.date: 03/03/2022
ms.author: erikje
ms.custom: include file
---

## Risks and results of restoring a Cloud PC

Cloud PCs have same risks as all Windows PCs when performing a full disk restore.  These risks and results include:

- All changes made to the Cloud PC between the saved restore point and when the restore is started will be lost. This lost information includes all data, documents, installed applications, configurations, downloads, and other changes. External data stored in cloud services, like OneDrive, won't be lost.
- Various applications, agents and tools also use rolling passwords, secrets, certificates, and keys. If any of these credentials are updated between the current time and the restore point, the associated service or application will be impacted.
- The chances of data loss and automated machine account password updates increase with longer time gaps between the selected restore point and the current time.

## Best practices

- To minimize data loss and the risk of a rolling password conflict, choose a restore point that is as close as possible to the current time.
- After a restoration is complete, the user should immediately sign into their Cloud PC to verify that they can successfully connect. If a user can't connect, or experiences unexpected behavior, try a second restoration to a different restore point that is more recent. On rare occasions you may need to reprovision/reset a Cloud PC if all restore points have obsolete rolling credentials.