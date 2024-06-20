---
author: banreet
ms.author: banreetkaur
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: include
ms.date: 08/02/2021
ms.localizationpriority: medium
---

Unless otherwise noted, this guidance is the same for all deployment models and VM sizes.

- You can install multiple instances of the cloud management gateway (CMG) at primary sites, or the central administration site (CAS).

    > [!TIP]
    > In a hierarchy, create the CMG at the CAS.

- One CMG supports up to 16 virtual machine (VM) instances in the Azure cloud service.

- Simultaneous client connections per each CMG VM instance depend upon the deployment model and VM size. When the CMG is under high load with more than the supported number of clients, it still handles requests but there may be delay.

  - **Virtual machine scale-set** _(version 2107 and later)_<!-- 3555749 -->

    - **Lab (B2s)**: 10
    - **Standard (A2_v2)**: 6,000
    - **Large (A4_v2)**: 10,000

    > [!IMPORTANT]
    > The **Lab (B2s)** size VM is only intended for lab testing and small proof-of-concept environments. They aren't intended for production use with the CMG. The B2s VMs are low cost and low performing. The Configuration Manager technical preview branch only supports 10 clients, which is why this size supports that number of clients.

  - **Virtual machine scale set** _(version 2010 and 2103 for Cloud Service Provider (CSP) subscriptions)_: 2,000

  - **Cloud service (classic)** _(version 2111 and earlier)_: 6,000

    > [!IMPORTANT]
    > Starting in version 2203, the option to deploy a CMG as a **cloud service (classic)** is removed.<!-- 13235079 --> All CMG deployments should use a [virtual machine scale set](../../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets).<!--10966586--> For more information, see [Removed and deprecated features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).
