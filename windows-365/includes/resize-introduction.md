---
title: include file
description: include file
author: ErikjeMS  
ms.service: windows-365
ms.topic: include
ms.date: 09/25/2024
ms.author: erikje
ms.custom: include file
---

The **Resize** remote action, which preserves user and disk data, lets you:

- Upgrade the RAM, CPU, and storage size of a Cloud PC.
- Downgrade the RAM and CPU of Cloud PC. Resizing doesn't let you downsize disk space.

These operations don't require reprovisioning of the Cloud PC.

You might consider resizing a Cloud PC when a user needs:

- Higher RAM and VCPU cores to run CPU intensive applications.
- More disk space for file storing.
- Less RAM and vCPU cores to run their current workload applications.

Resizing supports:

- Direct and group-based licenses.
- Paid, preview, and trial licenses.
- Bulk and single device operations.

Resizing doesn't support:

- GPU Cloud PCs. GPU Cloud PCs might show up in the resize flow, but trying to resize a GPU Cloud PC will result in an error.

Resizing automatically disconnects the user from their session and any unsaved work might be lost. Therefore, it's best to coordinate any resizing with the user before you begin. Contact your end users and have them save their work and sign out before you begin resizing.
