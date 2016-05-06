---
title: How to Create an SSL Certificate for Testing Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8bc784f-c9c7-4601-bf2c-4a6264db7ed1
---
# How to Create an SSL Certificate for Testing Service Provider Foundation
[!INCLUDE[spflong](./Token/spflong_md.md)] requires that a Secure Sockets Layer \(SSL\) server certificate be configured for its website bindings. The [!INCLUDE[spfshort](./Token/spfshort_md.md)] website is the endpoint for the Admin service and the Virtual Machine Manager \(VMM\) service that use Representational State Transfer \(REST\) and Open Data Protocol \(OData\) technology to communicate with clients and portal applications.

> [!NOTE]
> If you are installing [!INCLUDE[spfshort](./Token/spfshort_md.md)] 2012 R2, you do not have to use this procedure because you can select the **Generate a self\-signed certificate** option in the setup wizard instead.

The certificate should conform to the following recommendations:

-   A self\-signed certificate should be used only for testing purposes.

-   The fully qualified domain name \(FQDN\) should be specified for the certification path instead of ”localhost”.

-   A self\-signed certificate should be placed in the personal or webhosting store.

There are several ways to create a self\-signed certificate. The following procedure uses the     [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx) tool to create a self\-signed certificate that is signed with root authority. There are actually two certificates: a self\-signed certificate with root authority that signs the self\-signed certificate that [!INCLUDE[spfshort](./Token/spfshort_md.md)] uses.

### To create a self\-signed certificate for SSL authentication

1.  Open a command prompt as Administrator.

2.  Run the following command to install a self\-signed certificate with root authority in the personal or webhosting store of the local computer:

    ```
    makecert -pe -n "CN=TestRootCA" -ss personal -sr LocalMachine -sky signature -r "TestRootCA.cer"
    ```

3.  Run the following elevated command to create a new certificate that is signed by the test root authority certificate that you just created. Replace `contoso.skyspace.com` in the command with the actual FQDN of the server where you will install [!INCLUDE[spfshort](./Token/spfshort_md.md)]. This is the only change that you must make to the command.

    ```
    makecert -pe -n "CN=contoso.skyspace.com" -ss my -sr LocalMachine -sky exchange -eku 1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2 -in "TestRootCA" -is personal -ir LocalMachine -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12 SPFTestCert.cer
    ```

You can now select your self\-signed certificate in the [!INCLUDE[spfshort](./Token/spfshort_md.md)] setup wizard on the **Specify a Location for the SPF files** page. The certificate name appears in the **Certificate Name** list with the FQDN as its name, for example, `CN=TestRootCA(contoso.skyspace.com)`.

The certificate that is described in this topic should be not confused with a tenant's certificate that is used for claims\-based authentication.

### To verify the certificate configuration in IIS after installing [!INCLUDE[spfshort](./Token/spfshort_md.md)]

1.  Run **Internet Information Services \(IIS\) Manager**.

2.  In the **Connections** pane, under **Sites**, right\-click the **SPF** site, and then click **Edit bindings**.

3.  In the **Site Bindings** dialog box, select the HTTPS binding, and then click the **Edit** button.

4.  In the **Edit Site Binding** dialog box, the **SSL Certificate** should be set to the self\-signed certificate that you created in the previous procedure.

## See Also
[Create a Self\-Signed Server Certificate in IIS 7](http://go.microsoft.com/fwlink/?LinkId=279790)
[Configuring SSL in IIS Manager](http://go.microsoft.com/fwlink/?LinkId=279792)
[How to Install Service Provider Foundation for System Center 2012 SP1](./How-to-Install-Service-Provider-Foundation-for-System-Center-2012-SP1.md)
[System Requirements for Service Provider Foundation for System Center 2012 SP1](./System-Requirements-for-Service-Provider-Foundation-for-System-Center-2012-SP1.md)
[Deploying Service Provider Foundation](./Deploying-Service-Provider-Foundation.md)


