
# Windows 10 client AAD authentication workflow while installing



*Applies to: System Center Configuration Manager (Current Branch)*


Installing the Configuration Manager client on Windows 10 devices using Azure AD authentcation workflow details: 
 



### 1. AAD Token Request

Windows 10 AADJ client uses AAD parameters to request AAD token.

1.1 Request AAD Device token:

    Getting AAD (device) token with: ClientId = 22ed38d9-ba21-4036-be67-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token

1.2 If Device token is not retrieved, we request AAD user token:

    Getting AAD (user) token with: ClientId = f1f9b14e-55b8-4f17-8c54-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = 649FC29A-ECE3-4A3B-A3C1-680A2F035A6E

**LOGS: ccmsetup.log**


> [!NOTE] 

> If WPJ certificate is not found, we do not try to request AAD token (client is not properly AAD joined)
> Traffic with invalid token will be blocked upfront on CMG service, We will not route  the request to internal role.
> AAD (device) token is available from 1806. If AAD token can be retrieved from AAD, we will use it. otherwise we try AAD user token.


### 2.  CCM Token Request

With AAD token, we create new request  to obtain CCM Token:

    Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
    Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
 
 **LOGS: CCMSetup.log**
 
   **2.1 CMG Gets request** 
   
   **2.2 CMG moves request to CMG Connectoion Point** 
   
    RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms

   **2.3 CMG Connector Point transforms CMG client request to MP client request**
   
    MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms 


   **2.4 MP runs request against Database to verify user token** 
   
    Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0aebad80-77d2-4f0a-9639-676ee4764bb7 OnPrem_UserSid:  OnPrem_DeviceSid: 

    Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX	

**LOGS:  %CMGService.log, SMS_CLOUD_PROXYCONNECTOR.log, CCM_STS.log**


### 3. Content location request

Once we get response with the CCM token, we cache and use it to request site information and content location through Cloud Management Gateway:

    Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
    Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
    Appending CCM Token to the header.

**LOGS: Ccmsetup.logs**


### 4.Client installation

We download the client files and installation starts.

> [!NOTE] Communications Validation

 >CMG validates client token (via CMG, CMG CP and HTTP(S) and MP database request).
 >Client verifies CMG service certificate (or management certificate)
 >PKI for CMG Service certificate: Client requires Root CA of the CMG certificate on local store
 >Third party CMG service certificate: Clients automatically validates certificate (Root CA published on internet)


### AAD Token Request Workflow

 ![AAD CCMSetup Workflow](../comanage/media/AADInstallWF.png)  

> [!Common issues] 

> - Root CA not present
> - CRL check enabled (use the /NoCRLcheck* option in command line or publish CRL on internet*)
> - WPJ cert not found ( client Azure regsitered, not AAD joined)
>
>*Using /NoCRLCheck is only good for ccmsetup bootstrap for this case. For the clients to fully functional, admins need to disable CRL >check on that site’s client communication page. Otherwise after security settings refreshed by location service, the clients will not >talk to the server anymoreEnvironment
