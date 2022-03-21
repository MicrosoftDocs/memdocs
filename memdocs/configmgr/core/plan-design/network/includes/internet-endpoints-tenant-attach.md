---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/02/2021
ms.localizationpriority: medium
---

- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742--> _for Azure public cloud customers_

- `https://*.manage.microsoft.us` <!-- 8353823 --> _for US Government cloud customers on version 2107 or later_

- `https://dc.services.visualstudio.com` <!--7541816-->

The service connection point makes a long standing outgoing connection to the notification service hosted on `https://*.manage.microsoft.com`. Verify the proxy used for the service connection point doesn't time out outgoing connections too quickly. We recommend 3 minutes for outgoing connections to this internet endpoint. <!--7820969-->

If your environment has proxy rules to allow only specific certificate revocation lists (CRLs) or online certificate status protocol (OCSP) verification locations, also allow the following CRL and OCSP URLs:<!-- 8974697 -->

- `http://crl3.digicert.com`
- `http://crl4.digicert.com`
- `http://ocsp.digicert.com`
- `http://www.d-trust.net`
- `http://root-c3-ca2-2009.ocsp.d-trust.net`
- `http://crl.microsoft.com`
- `http://oneocsp.microsoft.com`
- `http://ocsp.msocsp.com`
- `http://www.microsoft.com/pkiops`

<!-- list from https://docs.microsoft.com/azure/security/fundamentals/tls-certificate-changes#will-this-change-affect-me -->
