---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### When the SMS provider is remote from the CAS, you may encounter an internal server error from the admin console

**Error message:** On-prem error code: 500 internal server error

**Scenario 1:** When running Configuration Manager version 2002 and there is a remote provider for the CAS, then you may encounter an internal server error from the admin console.

**Scenario 2:** When running Configuration Manager version 2006, you may also encounter this error if the service connection point fails to connect to the provider on the primary site and falls back to the provider for the CAS. 

**Scenario 3:** If the CAS has been upgraded to version 2006 but the primary server hasn't been upgraded yet, then the requests will be routed through the CAS provider. If the provider is remote, you may encounter an internal server error from the admin console. 

**Workaround:** Follow the instructions for the [CAS has a remote provider](../../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) scenario in the CMPivot article to work around this "double hop" scenario.

### When multi-factor authentication is enabled, most tenant attach features don't work

**Scenario:** If the [SMS provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider) machine that communicates with the [service connection point](../../core/servers/deploy/configure/about-the-service-connection-point.md) are configured to use multi-factor authentication, you'll be unable to install applications, run CMPivot queries, and perform other actions from the admin console.

**Workaround:** Configure the hierarchy to the default authentication level of **Windows authentication**. For more information, see the [Authentication section in the SMS provider article](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth).

