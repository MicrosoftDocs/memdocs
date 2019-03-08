# Windows 10 client AAD authentication workflow while installing



*Applies to: System Center Configuration Manager (Current Branch)*



Installing the Configuration Manager client on Windows 10 devices using Azure AD authentcation workflow details: 
 
 ![AAD CCMSetup Workflow](../comanage/media/AADInstallWF.png)  


###1.  AAD Token Request

Client uses AAD parameters to request AAD token for user.

Getting AAD (user) token with: ClientId = f1f9b14e-55b8-4f17-8c54-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = 649FC29A-ECE3-4A3B-A3C1-680A2F035A6E

(CCMSetup.log)



> [!NOTE] 

> Traffic with invalid token will be blocked upfront on CMG service, We don’t route request to internal roles

> If WPJ certificate is not found, we do not try to request AAD token (client is not properly AAD joined)

> AAD (device) token is available from 1806. Previously, only AAD user token is used but we try Device as well (getting a failed request for device token).

> If AAD token can be retrieved from AAD, we will use it, if not we will try AAD user token.



###2.  CCM Token Request

(Once we get AAD User token, we request CCM token):

    2.1 **CMG Gets request** 

      Getting CCM Token from https://myCMG.cloudapp.net/CCM_Proxy_ServerAuth/9/CCM_STS (CCMSetup.log)

    2.2 **CMG moves request to CMG Connector Point** (IIS log, %CMGHttpHandler.log)

    2.3 **CMG CP transforms CMG client request to MP client request**

     https://myMP.Mylab.com/CCM_STS (SMS_CLOUD_PROXYCONNECTOR.log)

    2.4 **MP runs request against Database to verify user token** (CCM_STS.log)



###Communications Validation

CMG validates client token (via CMG, CMG CP and HTTP(S) and MP database request).

Client verifies CMG service certificate (or management certificate)

PKI for CMG Service certificate: Client requires Root CA of the CMG certificate on local store

Third party CMG service certificate: Clients automatically validates certificate (Root CA published on internet)



Common issues

Root CA not present

CRL check enabled (use the /NoCRLcheck option in command line or publish CRL on internet*)

WPJ cert not found ( client Azure regsitered, not AAD joined)

*Using /NoCRLCheck is only good for ccmsetup bootstrap for this case. For the clients to fully functional, admins need to disable CRL check on that site’s client communication page. Otherwise after security settings refreshed by location service, the clients will not talk to the server anymoreEnvironment
