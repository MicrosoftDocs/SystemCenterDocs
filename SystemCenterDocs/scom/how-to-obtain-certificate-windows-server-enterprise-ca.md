---
ms.assetid: 
title: How to obtain a Certificate Using Windows Server Enterprise CA.
description: This article explains how to obtain a Certificate Using Windows Server Enterprise CA.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 6/21/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# How to Obtain a Certificate Using Windows Server 2022 Enterprise CA

Applies To: System Center Operations Manager

Use the procedures in this topic to obtain a certificate from a Windows Server computer hosting Enterprise Root Active Directory Certificate Services (AD-CS). You use the certreq command-line utility to request and accept a certificate, and you use a Web interface to submit and retrieve your certificate.

## Prerequisites

- You must have AD-CS installed.
- You mush have a HTTPS binding and its associated certificate has been installed.

For information about creating an HTTPS binding, see How to Configure an HTTPS Binding for a Windows Server CA.

>[!Important]
>The content for this topic is based on the default settings for AD-CS; for example, setting the key length to 2048, selecting Microsoft Software Key Storage Provider as the CSP, and using Secure Hash Algorithm 1 (SHA1). Evaluate these selections against the requirements of your company's security policy.

The high-level process to obtain a certificate from an Enterprise certification authority (CA) is as follows:

1. Download the Trusted Root (CA) certificate.

2. Import the Trusted Root (CA) certificate.

3. Create a certificate template.

4. Add the template to the Certificate Templates folder.

5. Create a setup information file for use with the certreq command-line utility.

6. Create a request file.

7. Submit a request to the CA.

8. Import the certificate into the certificate store.

9. Import the certificate into Operations Manager using MOMCertImport.

## Download the Trusted Root (CA) certificate

To download the Trusted Root (CA) certificate

1. Log on to the computer where you want to install a certificate.
For example, a Gateway Server or Management Server.

2. Open a web brOwser and connect to the computer hosting Certificate Services.
For example, *https://<servername>/certsrv*.

3. On the **Welcome** page, select **Download a CA Certificate**, **Certificate chain**, or **CRL**.

4. On the **Download a CA Certificate**, **Certificate Chain**, or **CRL** page, select **Encoding method** > **Base 64**, and select **Download CA certificate chain**.

5. In the **File Download** dialog, select **Save** and save the certificate.
For example, *Trustedca.p7b*.

6. Close the web browser when the download is completed.

## Import the Trusted Root (CA) certificate

>[!Note]
>To import a Trusted Root Certificate, you must have administrative privileges on the target machine. 

To import the Trusted Root (CA) Certificate

1. On the Windows desktop, select **Start** > **Run**.

2. In the **Run** dialog, enter **mmc**, and select **OK**.

3. In the **Console1** window, select **File** > **Add/Remove Snap-in**.

4. In the **Add/Remove Snap-in** dialog, select **Certificates**, and then select **Next**.

5. In the **Certificates snap-in** dialog, select **Computer account**, and select **Next**.

6. In the **Select Computer** dialog, ensure that **Local computer: (the computer this console is running on)** is selected, and then select **Finish**.

7. In the **Add/Remove Snap-in** dialog, select **OK**.

8. In the **Console1** window, expand **Certificates (Local Computer)**, expand **Trusted Root Certification Authorities**, and then select **Certificates**.

9. Select and hold **Certificates**, select **All Tasks** > **Import**.

10. In the **Certificate Import** Wizard, select **Next**.

11. On the **File to Import** page, select **Browse** and select the location where you have downloaded the CA certificate file.
For example, *TrustedCA.p7b*, and then select **Open**, and **Next**.

12. On the **Certificate Store** page, select **Place all certificates in the following store** and ensure that **Trusted Root Certification Authorities** appears in the **Certificate store** box, and select **Next**.

13. On the **Completing the Certificate Import Wizard** page, select **Finish**.


## Create a certificate template

To create a certificate template

1. On the computer that is hosting your enterprise CA, on the Windows desktop, select **Start** > **Programs** > **Administrative Tools**, and select **Certification Authority**.

2. On the navigation pane, expand the CA name, select and hold **Certificate Templates** > **Manage**.

3. In the **Certificate Templates** console, on the results pane, select and hold **IPsec (Offline request)**, and select **Duplicate Template**.

4. In the **Duplicate Template** dialog, select **Windows Server 2022**, and select **OK**.

5. In the **Properties of New Template** dialog, on the **General** tab, in the **Template display name** text box, enter a new name for this template.
For example, *OperationsManagerCert*.

6. On the **Request Handling** tab, select **Allow private key to be exported**.

7. Select the **Extensions** tab, and in **Extensions included in this template**, select **Application Policies**, and then select **Edit**.

8. In the **Edit Application Policies Extension** dialog, select **IP security IKE intermediate**, and select **Remove**.

9. Select **Add**, and in the **Application policies list**, hold down the ctrl key to select multiple items from the list. Select **Client Authentication** and **Server Authentication**, and select **OK**.

10. In the **Edit Application Policies Extension** dialog, select **OK**.

11. Select the **Security** tab and ensure that the **Authenticated Users** group has **Read** and **Enroll** permissions, and select **OK**.

12. Close the Certificate Templates console.

## Add the template to the Certificate Templates folder

1. On the computer that is hosting your Enterprise CA, in the Certification Authority snap-in, select and hold the **Certificate Templates** folder, select **New** > **Certification Template to Issue**.

2. In the **Enable Certificate Templates** box, select the certificate template that you created.
For example, select *OperationsManagerCert*, and then select **OK**.

## Request a certificate using a request file

**Create a setup information (.inf) file**

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open Notepad.

2. Create a text file containing the following content:
   ```
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

   ```

3. Save the file with an .inf file name extension.
For example, *RequestConfig.inf*.

4. Close Notepad.


## Create a request file

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open an Administrator command prompt.

2. In the command window, enter **CertReq -New -f RequestConfig.inf CertRequest.req**, and select Enter.

3. Open the file using Notepad, (for example, *CertRequest.req*), and copy the contents of this file into the clipboard.

## Submit a request to the CA using the request file

>[!Note]
>HTTPS binding needs to be configured on the Certificate Services Web site of the CA, otherwise we may fail to connect to the website. For more information, see How to Configure an HTTPS Binding for a Windows Server CA.  

To submit a request to an enterprise CA

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate Services. 
For example, *https://<servername>/certsrv*.

2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.

3. On the **Request a Certificate** page, select **advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file**, or **submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure.

6. In the **Certificate Template** select the certificate template that you created.
For example, *OperationsManagerCert*, and then select **Submit**.

7. On the **Certificate Issued** page, select **Base 64 encoded** > **Download certificate**.

8. Name and save the certificate to an accessible location.
For example, save as *SCOM-MS01.cer*.

9. Close the web browser.

## Import the certificate into the certificate store

To import the certificate into the certificate store

1. On the computer hosting the Operations Manager feature for which you are configuring the certificate, select **Start** > **Run**.

2. In the **Run** dialog, enter **cmd**, and select **OK**.

3. In the command window, enter **CertReq -Accept NewCertifiate.cer**, and select Enter.

## Import the certificate into Operations Manager using MOMCertImport 

To import the certificate into Operations Manager using MOMCertImport

1. Log on to the computer where you installed the certificate with an account that is a member of the Administrators group.

2. On the Windows desktop, select **Start** > **Run**.

3. In the **Run** dialog, enter **cmd**, and select **OK**.

4. At the command prompt, enter */<drive_letter/>*: (where */<drive_letter/>* is the drive where the Operations Manager installation media is located), and select Enter.

5. Enter *cd\SupportTools\i386*, and select Enter.

    >[!Note]
    >On 64-bit computers, enter *cd\SupportTools\amd64*

6. Enter the following:

   **MOMCertImport /SubjectName <Certificate Subject Name>**

7. Select Enter.

