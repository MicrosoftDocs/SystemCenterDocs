---
ms.assetid: 
title: How to Obtain a Certificate Using Windows Server Stand-Alone CA.
description: This article describes How to Obtain a Certificate Using Windows Server Stand-Alone CA.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 06/21/2022
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to Obtain a Certificate Using Windows Server Stand-Alone CA

Applies To: System Center Operations Manager

Use the procedures in this topic to obtain a certificate from a stand-alone Windows Server computer hosting Active Directory Certificate Services (AD-CS). You use the command-line utility to request and accept a certificate, and you use a Web interface to submit and retrieve your certificate.

It is assumed that you have AD-CS installed, an HTTPS binding is being used, and its associated certificate has been installed. For more information about creating an HTTPS binding see How to Configure an HTTPS Binding for a Windows Server CA.

>[!Important]
>The content for this topic is based on the default settings for AD-CS; for example, setting the key length to 2048, selecting Microsoft Software Key Storage Provider as the CSP, and using Secure Hash Algorithm 1 (SHA1). Evaluate these selections against the requirements of your company's security policy.

The high-level process to obtain a certificate from a stand-alone certification authority (CA) is as follows:

1. Download the Trusted Root (CA) certificate.

2. Import the Trusted Root (CA) certificate

3. Create a setup information file to use with the certreq command-line utility.

4. Create a request file.

5. Submit a request to the CA using the request file.

6. Approve the pending certificate request.

7. Retrieve the certificate from the CA.

8. Import the certificate into the certificate store.

9. Import the certificate into Operations Manager using MOMCertImport.

## Download the Trusted Root (CA) certificate

To download the Trusted Root (CA) certificate

1. Log on to the computer where you want to install a certificate. 
For example, a Gateway Server or Management Server.

2. Open a web browser and connect to the computer hosting Certificate Services.
For example, *https://<servername>/certsrv*.

3. On the **Welcome** page, select **Download a CA Certificate**, **Certificate chain**, or **CRL**.

4. On the **Download a CA Certificate**, **Certificate Chain**, or **CRL** page, select **Encoding method** > **Base 64**, and then select **Download CA certificate chain**.

5. Save the certificate to an accessible location and give it a friendly name, such as SCOM-MS01.cer.

6. Close the browser window.

## Import the Trusted Root (CA) certificate

>[!Note]
>To import a Trusted Root Certificate, you must have administrative privileges on the target machine. 

To import the Trusted Root (CA) Certificate

1. On the Windows desktop, select **Start** > **Run**.

2. In the **Run** dialog, enter **mmc**, and select **OK**.

3. In the **Console1** window, select **File** > **Add/Remove Snap-in**.

4. In the **Add/Remove Snap-in** dialog, select **Certificates** > **Add**.

5. In the **Certificates snap-in** dialog, select **Computer account**, and then select **Next**.

6. In the **Select Computer** dialog, ensure that **Local computer: (the computer this console is running on)** is selected, and then select Finish.

7. In the **Add/Remove Snap-in** dialog, select **OK**.

8. In the **Console1** window, expand **Certificates (Local Computer)**, expand **Trusted Root Certification Authorities**, and then select **Certificates**.

9. Select and hold the **Certificates**, select **All Tasks** > **Import**.

10. In the **Certificate Import** Wizard, select **Next**.

11. On the **File to Import** page, browse to the location where you downloaded the CA certificate file, change the file type to **PKCS #7 Certificates** and select the root certificate file. 
For example, *TrustedCA.p7b*, select **Open** and **Next**.

12. On the **Certificate Store** page, select **Place all certificates in the following store** and ensure that **Trusted Root Certification Authorities** appears in the **Certificate store** box, and then select **Next**.

13. On the **Completing the Certificate Import Wizard** page, select **Finish**.

## Request a certificate using a request file

To create a setup information (.inf) file

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, select **Start** > **Run**.

2. In the **Run** dialog, enter Notepad, and select **OK**.

3. Create a text file containing the following content:
   
   [NewRequest]

   Subject="CN=<FQDN of computer you are creating the certificate, for example, the gateway server or management server.>"

   Exportable=TRUE

   KeyLength=2048

   KeySpec=1

   KeyUsage=0xf0

   MachineKeySet=TRUE

   [EnhancedKeyUsageExtension]

   OID=1.3.6.1.5.5.7.3.1

   OID=1.3.6.1.5.5.7.3.2

4. Save the file with an .inf file name extension.
For example, *RequestConfig.inf*.

5. Close Notepad.

## Create a request file

To create a request file to use with a stand-alone CA

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open an Administrator Command Prompt.

2. In the command window, enter **CertReq –New –f RequestConfig.inf CertRequest.req**, and select Enter.

4. Open the resulting file (for example, CertRequest.req) with Notepad. Copy the contents of this file onto the clipboard.

## Submit a request to the CA using the request file

>[!Note]
>HTTPS binding needs to be configured on the Certificate Services Web site of the CA, otherwise we may fail to connect to the website. For more information, see How to Configure an HTTPS Binding for a Windows Server CA.  

To submit a request to a stand-alone CA

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate Services.
For example, *https://<servername>/certsrv*. 

2. On the **Microsoft Active Directory Certificate Services Welcome** screen, select **Request a certificate**.

3. On the **Request a Certificate** page, select **Advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file**, or **Submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure, and then select **Submit**.

## Approve the pending certificate request

To approve the pending certificate request

1. Log on to the CA server as a certification authority administrator.

2. On the Windows desktop, select **Start** > **Programs** > **Administrative Tools**, and select **Certification Authority**.

3. In **Certification Authority**, expand the node for your certification authority name, and then slect **Pending Requests**.

4. On the results pane, select and hold the pending request from the previous procedure, point to **All Tasks**, and select **Issue**.

5. Select **Issued Certificates**, and confirm the certificate you just issued is listed.

6. Close Certification Authority.


## Retrieve the certificate from the CA

To retrieve the certificate

1. Log on to the computer where you want to install a certificate. 
For example, the gateway server or management server.

2. Start a web browser, and connect to the computer hosting Certificate Services.
For example, *https://<servername>/certsrv*.

3. On the **Microsoft Active Directory Certificate Services Welcome** page, select **View the status of a pending certificate request**.

4. On the **View the Status of a Pending Certificate Request** page, select the certificate you requested.

5. On the **Certificate Issued** page, select **Base 64 encoded**, and then select **Download certificate**.

6. In the **File Download – Security Warning** dialog, select Save, and save the certificate.
For example, as *NewCertificate.cer*.

7. On the **Certificate Installed** page, after you see the message that **Your new certificate has been successfully installed**, close the browser.

8. Close the web browser.

## Import the certificate into the certificate store

To import the certificate into the certificate store

1. On the computer hosting the Operations Manager feature for which you are configuring the certificate, select **Start** > **Run**.

2. In the **Run** dialog, enter **cmd**, and select **OK**.

3. In the command window, enter *CertReq –Accept NewCertifiate.cer*, and select Enter.

## Import the certificate into Operations Manager using MOMCertImport

To import the certificate into Operations Manager using MOMCertImport

1. Log on to the computer where you installed the certificate with an account that is a member of the Administrators group.

2. On the Windows desktop, select **Start** > **Run**.

3. In the **Run** dialog, enter **cmd**, and select **OK**.

4. At the command prompt, enter <drive_letter>: (where <drive_letter> is the drive where the Operations Manager installation media is located), and then select Enter.

5. Enter *cd\SupportTools\i386*, and select Enter.

>[!Note]
>On 64-bit computers, enter *cd\SupportTools\amd64*

6. Enter the following:

   ```
   MOMCertImport /SubjectName <Certificate Subject Name>
   ```

7. Select Enter.