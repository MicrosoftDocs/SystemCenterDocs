---
title: How to Obtain a Certificate Using Windows Server 2008 Enterprise CA
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02c53794-e0d3-4bdb-8d7e-6ed2f94e247c
---
# How to Obtain a Certificate Using Windows Server 2008 Enterprise CA
Use the procedures in this topic to obtain a certificate from Windows Server 2008 R2, or Windows Server 2008 R2 SP1 computer hosting Enterprise Root Active Directory Certificate Services \(AD CS\). You use the CertReq command\-line utility to request and accept a certificate, and you use a Web interface to submit and retrieve your certificate.

It is assumed that you have AD CS installed, an HTTPS binding has been created, and its associated certificate has been installed. Information about creating an HTTPS binding is available in the topic [How to Configure an HTTPS Binding for a Windows Server 2008 CA](assetId:///3b251849-d501-40af-a3c7-43da0f1236f5).

> [!IMPORTANT]
> The content for this topic is based on the default settings for Windows Server 2008 AD CS; for example, setting the key length to 2048, selecting Microsoft Software Key Storage Provider as the CSP, and using Secure Hash Algorithm 1 \(SHA1\). Evaluate these selections against the requirements of your company’s security policy.

The high\-level process to obtain a certificate from an Enterprise certification authority \(CA\) is as follows:

1.  [Download the Trusted Root \(CA\) certificate](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_DownloadCert).

2.  [Import the Trusted Root \(CA\) certificate](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_ImportCert).

3.  [Create a certificate template](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_CreateTemplate).

4.  [Add the template to the Certificate Templates folder](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_AddTemplateToFolder).

5.  [Create a setup information file for use with the CertReq command\-line utility](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_CreateSetupInfoFile).

6.  [Create a request file](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_CreateRequestFile).

7.  [Submit a request to the CA](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_SubmitRequest).

8.  [Import the certificate into the certificate store](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_ImportCertStore).

9. [Import the certificate into Operations Manager using MOMCertImport](assetId:///cd585e5a-b9ec-458e-8bcf-87e8a30e0967#BKMK_ImportMOMCertImport).

## <a name="BKMK_DownloadCert"></a>Download the Trusted Root \(CA\) certificate

#### To download the Trusted Root \(CA\) certificate

1.  Log on to the computer where you want to install a certificate; for example, the gateway server or management server.

2.  Start Internet Explorer, and connect to the computer hosting Certificate Services; for example, https:\/\/<servername>\/certsrv.

3.  On the **Welcome** page, click **Download a CA Certificate, certificate chain, or CRL**.

4.  On the **Download a CA Certificate, Certificate Chain, or CRL** page, click **Encoding method**, click **Base 64**, and then click **Download CA certificate chain**.

5.  In the **File Download** dialog box, click **Save** and save the certificate; for example, **Trustedca.p7b**.

6.  When the download has finished, close Internet Explorer.

### <a name="BKMK_ImportCert"></a>Import the Trusted Root \(CA\) certificate

##### To import the Trusted Root \(CA\) Certificate

1.  On the Windows desktop, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, type **mmc**, and then click **OK**.

3.  In the **Console1** window, click **File**, and then click **Add\/Remove Snap\-in**.

4.  In the **Add\/Remove Snap\-in** dialog box, click **Add**.

5.  In the **Add Standalone Snap\-in** dialog box, click **Certificates**, and then click **Add**.

6.  In the **Certificates snap\-in** dialog box, select **Computer account**, and then click **Next**.

7.  In the **Select Computer** dialog box, ensure that **Local computer: \(the computer this console is running on\)** is selected, and then click **Finish**.

8.  In the **Add Standalone Snap\-in** dialog box, click **Close**.

9. In the **Add\/Remove Snap\-in** dialog box, click **OK**.

10. In the **Console1** window, expand **Certificates \(Local Computer\)**, expand **Trusted Root Certification Authorities**, and then click **Certificates**.

11. Right\-click **Certificates**, select **All Tasks**, and then click **Import**.

12. In the Certificate Import Wizard, click **Next**.

13. On the **File to Import** page, click **Browse** and select the location where you downloaded the CA certificate file, for example, TrustedCA.p7b, select the file, and then click **Open**.

14. On the **File to Import** page, select **Place all certificates in the following store** and ensure that **Trusted Root Certification Authorities** appears in the **Certificate store** box, and then click **Next**.

15. On the **Completing the Certificate Import Wizard** page, click **Finish**.

### <a name="BKMK_CreateTemplate"></a>Create a certificate template

##### To create a certificate template

1.  On the computer that is hosting your enterprise CA, on the Windows desktop, click **Start**, point to **Programs**, point to **AdministrativeTools**, and then click **Certification Authority**.

2.  In the navigation pane, expand the CA name, right\-click **CertificateTemplates**, and then click **Manage**.

3.  In the **Certificate Templates** console, in the results pane, right\-click **IPsec \(Offline request\)**, and then click **Duplicate Template**.

4.  In the **Duplicate Template** dialog box, select **Windows Server 2008 Enterprise Edition**, and then click **OK**.

5.  In the **Properties of New Template** dialog box, on the **General** tab, in the **Template display name** text box, type a new name for this template; for example, **OperationsManagerCert**.

6.  On the **Request Handling** tab, select **Allow private key to be exported**.

7.  Click the **Extensions** tab, and in **Extensions included in this template**, click **Application Policies**, and then click **Edit**.

8.  In the **Edit Application Policies Extension** dialog box, click **IP security IKE intermediate,** and then click **Remove**.

9. Click **Add**, and in the **Application policies list**, hold down the CTRL key to multi\-select items from the list, click **Client Authentication** and **Server Authentication**, and then click **OK**.

10. In the **Edit Application Policies Extension** dialog box, click **OK**.

11. Click the **Security** tab and ensure that the **Authenticated Users** group has **Read** and **Enroll** permissions, and then click **OK**.

12. Close the Certificate Templates console.

### <a name="BKMK_AddTemplateToFolder"></a>Add the template to the Certificate Templates folder

##### To add the template to the Certificate Templates folder

1.  On the computer that is hosting your Enterprise CA, in the Certification Authority snap\-in, right\-click the **Certificate Templates** folder, point to **New**, and then click **Certification Template to Issue**.

2.  In the **Enable Certificate Templates** box, select the certificate template that you created; for example, click **OperationsManagerCert**, and then click **OK**.

### <a name="BKMK_CreateSetupInfoFile"></a>Create a setup information file for use with the CertReq command\-line utility

##### To create a setup information \(.inf\) file

1.  On the computer hosting the Operations Manager feature for which you are requesting a certificate, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, type **Notepad**, and then click **OK**.

3.  Create a text file containing the following content:

    **\[NewRequest\]**

    **Subject\="CN\=<FQDN of computer you are creating the certificate, for example, the gateway server or management server.>"**

    **Exportable\=TRUE**

    **KeyLength\=2048**

    **KeySpec\=1**

    **KeyUsage\=0xf0**

    **MachineKeySet\=TRUE**

    **\[EnhancedKeyUsageExtension\]**

    **OID\=1.3.6.1.5.5.7.3.1**

    **OID\=1.3.6.1.5.5.7.3.2**

4.  Save the file with an .inf file name extension; for example, RequestConfig.inf.

5.  Close Notepad.

### <a name="BKMK_CreateRequestFile"></a>Create a request file

##### To create a request file to use with an enterprise CA

1.  On the computer hosting the Operations Manager feature for which you are requesting a certificate, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, type **cmd**, and then click **OK**.

3.  In the command window, type **CertReq –New –f RequestConfig.inf CertRequest.req**, and then press ENTER.

4.  Using Notepad, open the resulting file \(for example, CertRequest.req\), and copy the contents of this file into the clipboard.

### <a name="BKMK_SubmitRequest"></a>Submit a request to the CA

##### To submit a request to an enterprise CA

1.  On the computer hosting the Operations Manager feature for which you are requesting a certificate, start Internet Explorer, and then connect to the computer hosting Certificate Services; for example, https:\/\/<servername>\/certsrv.

    > [!NOTE]
    > If an HTTPS binding has not been configured on the Certificate Services Web site, the browser will fail to connect. See the topic [How to Configure an HTTPS Binding for a Windows Server 2008 CA](assetId:///8b74f9c4-22fd-495c-ac9e-61f2e2a0d719) in this guide.

2.  On the **Microsoft Active Directory Certificate Services Welcome** screen, click **Request a certificate**.

3.  On the **Request a Certificate** page, click **advanced certificate request**.

4.  On the **Advanced Certificate Request** page, click **Submit a certificate request by using a base\-64\-encoded CMC or PKCS \#10 file, or submit a renewal request by using a base\-64\-encoded PKCS \#7 file.**

5.  On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the CertRequest.req file that you copied in step 4 in the previous procedure.

6.  In the **Certificate Template** select the certificate template that you created, for example, OperationsManagerCert, and then click **Submit**.

7.  On the **Certificate Issued** page, select **Base 64 encoded**, and then click **Download certificate**.

8.  In the **File Download – Security Warning** dialog box, click **Save**, and save the certificate; for example, save as NewCertificate.cer.

9. Close Internet Explorer.

### <a name="BKMK_ImportCertStore"></a>Import the certificate into the certificate store

##### To import the certificate into the certificate store

1.  On the computer hosting the Operations Manager feature for which you are configuring the certificate, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, type **cmd**, and then click **OK**.

3.  In the command window, type **CertReq –Accept NewCertifiate.cer**, and then press ENTER.

### <a name="BKMK_ImportMOMCertImport"></a>Import the certificate into Operations Manager using MOMCertImport

##### To import the certificate into Operations Manager using MOMCertImport

1.  Log on to the computer where you installed the certificate with an account that is a member of the Administrators group.

2.  On the Windows desktop, click **Start**, and then click **Run**.

3.  In the **Run** dialog box, type **cmd**, and then click **OK**.

4.  At the command prompt, type **<***drive\_letter***>:** \(where <*drive\_letter*> is the drive where the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media is located\), and then press ENTER.

5.  Type **cd\\SupportTools\\i386**, and then press ENTER.

    > [!NOTE]
    > On 64\-bit computers, type **cd\\SupportTools\\amd64**

6.  Type the following:

    **MOMCertImport \/SubjectName <Certificate Subject Name>**

7.  Press ENTER.

## See Also
[Authentication and Data Encryption for Windows Computers](assetId:///8ee895a9-7bac-4274-80b8-092475a83c67)


