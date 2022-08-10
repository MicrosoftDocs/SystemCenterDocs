---
ms.assetid: 
title: How to obtain a Certificate Using Windows Server Enterprise CA.
description: This article explains how to obtain a Certificate Using Windows Server Enterprise CA.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 08/09/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# How to Obtain a Certificate Using Windows Server Enterprise CA

*Applies to:* System Center Operations Manager, Windows Server and AD CS 2012 R2 or newer

Use the procedures in this topic to obtain a certificate to be used with Operations Manager Management Server, Gateway, or Agent using Enterprise Active Directory Certificate Services (AD CS) Certificate Authority (CA) server on the Windows platform. 

You use the [certreq](/windows-server/administration/windows-commands/certreq_1) command-line utility to request and accept a certificate, and you use a Web interface to submit and retrieve your certificate.

## Prerequisites

You must have the following:

- AD-CS installed and configured in the environment with web services.
- a HTTPS binding and its associated certificate has been installed.
- typical desktop experience and are not Core servers. 

For information about creating an HTTPS binding, see [How to Configure an HTTPS Binding for a Windows Server CA](/system-center/scom/how-to-configure-https-binding-windows-server-ca).

>[!NOTE]
>
>If your organization is not using AD CS or does not use the accompanying web services, the steps below will not completely apply to your environment. If you are using an external certificate authority, these steps will not cover that scenario.
>
>If you are covered by one of these scenarios and wish to create a certificate using means outside these instructions, or just need the certificate specifications, please make sure the certificate meets these requirements for SCOM to use the certificate:
>
>- `Subject="CN=server.contoso.com" ; (this should be the FQDN or how the system shows in DNS)`
>
>- `[Key Usage]`
>- `Key Exportable=TRUE`
>- `HashAlgorithm = SHA256`
>- `KeyLength=2048`
>- `KeySpec=1`
>- `KeyUsage=0xf0`
>- `MachineKeySet=TRUE`
>
>- `[EnhancedKeyUsageExtension]`
>- `OID=1.3.6.1.5.5.7.3.1 ; Server Authentication`
>- `OID=1.3.6.1.5.5.7.3.2 ; Client Authentication`
>
>- `[Compatibility Settings]`
>- `Compatible with Windows Server 2003 ; (or newer based on environment)`
>
>- `[Cryptography Settings]`
>- `Provider Category: Legacy Cryptography Service Provider`
>- `Algorithm name: RSA`
>- `Minimum Key Size: 2048 ; (2048 or 4096 as per security requirement.)`
>- `Providers: Microsoft RSA Schannel Cryptographic Provider`

>[!Important]
>The content for this topic is based on the default settings for AD-CS; for example, the standard key length is 2048, and select Microsoft Software Key Storage Provider as CSP and Secure Hash Algorithm 256 (SHA256). Evaluate these selections against the requirements of your company's security policy.

The high-level process to obtain a certificate from an Enterprise certification authority (CA) is as follows:

1. Download the Root Certificate from a CA.

2. Import the Root Certificate to a client server.

3. Create a certificate template.

4. Add the template to the Certificate Templates folder.

5. Create a setup information file for use with the \<certreq\> command-line utility.

6. Create a request file (or use the web portal).

7. Submit a request to the CA.

8. Import the certificate into the certificate store.

9. Import the certificate into Operations Manager using \<MOMCertImport\>.

## Download and Import the Root Certificate from the CA

To trust and validate any certificates created from Enterprise or Stand-Alone CAs, the target machine needs to have a copy of the Root Certificate in its Trusted Root Store. Most domain-joined computers should already trust the Enterprise CA, however no machine will trust a certificate from a Stand-Alone CA without the Root Certificate installed.

If using a third-party CA, the download process will be different, however the import process should still be similar.

### Download the Trusted Root certificate from a CA

To download the Trusted Root certificate, do the following:

1. Log on to the computer where you want to install a certificate.
For example, a Gateway Server or Management Server.

2. Open a web browser and connect to the certificate server web address.
   
   a. *https://\<servername\>/certsrv*.

3. On the **Welcome** page, select **Download a CA Certificate**, **Certificate chain**, or **CRL**.
   
   a.	If prompted with a **Web Access Confirmation**, verify that you have the correct server and URL, and select **Yes**.

4. If presented with multiple options under **CA Certificate**, confirm the correct selection, else select the default.

5. Change the Encoding Method to **Base 64**.

6.	Click the **Download CA Certificate Chain** link.

7.	Select an accessible location for the certificate and give it a friendly file name for later use.

## Import the Trusted Root Certificate from the CA on the client

>[!Note]
>To import a Trusted Root Certificate, you must have administrative privileges on the target machine. 

To import the Trusted Root Certificate, do the following:

1. Copy the file generated in the previous step to the client.
2. Open Certificate Manager
   a. From the Start menu
      i. Type *mmc* to find the Microsoft Management Console (mmc.exe).
      ii. Run this utility.
      iii. Go to **File** > **Add/Remove Snap in…**.
      iv. On the Add or Remove Snap-ins window, select **Certificates** and then select **Add**.
      v.	On the Certificate Snap-in window
         1.	Select **Computer Account** and select **Next**.
         2.	Select **Local Computer** and select **Finish**.
      vi. Select **OK**
   b.	From the Command Line, PowerShell, or Run
      i.	Type **certlm.msc** and press **enter**.
      ii. The steps above also apply if *certlm.msc* cannot be found.
3.	Under Console Root, expand **Certificates (Local Computer)**.
4.	Expand **Trusted Root Certification Authorities**,
   a.	Select and hold **Certificates**.
   b.	Select **All Tasks**.
   c.	Select **Import**
5.	In the Certificate Import Wizard,
   a.	Leave the first page as default and select **Next**
   b.	Browse to and select the trusted root certificate file copied from the CA.
   c.	Select **Next**.
   d.	In the Certificate Store location, leave as the default Trusted Root Certification Authorities.
   e.	Select **Next**.
   f.	Select **Finish**.
6.	If successful, the Trusted Root Certificate from the CA should now be visible under **Trusted Root Certification Authorities** > **Certificates**.

## Create a certificate template

Enterprise CAs are integrated with Active Directory Domain Services (AD DS). They publish certificates and certificate revocation lists (CRLs) to AD DS. Enterprise CAs use information that is stored in AD DS, including user accounts and security groups, to approve or deny certificate requests. Enterprise CAs use certificate templates. When a certificate is issued, the Enterprise CA uses information in the certificate template to generate a certificate with the appropriate attributes for that certificate type.

More information, see [certificate templates](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831574(v=ws.11)).

### Create a certificate template for System Center Operations Manager

1.	Log onto a domain joined server with AD CS in your environment (your CA).
2.	On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3.	On the right navigation pane, expand the CA, select and hold **Certificate Templates** and select **Manage**.
4.	Select and hold **IPSec (Offline request)** and select **Duplicate Template**.
5.	**Properties of New Template** dialog opens, make the selections as below:
   a.	Compatibility
      i.	**Certification Authority**: Windows Server 2008 (or the lowest AD functional level in the environment)
      ii. **Certificate Recipient**: Windows Server 2012 (or the lowest version OS in the environment)
   b.	General
      i.	**Template display name**: Enter a friendly name, such as *SCOM* or *Operations Manager*
      ii. **Template name**: Same as display name
      iii. **Validity period**: This should match your organization’s requirements
      iv. Check **Publish certificate in Active Directory**
      v.	Check **Do not automatically reenroll if a duplicate certificate exists in Active Directory**
   c.	Request Handling
      i.	**Purpose**: Select **Signature and encryption** from the drop-down
      ii. Check **Allow private key to be exported**
    d. Cryptography
      i.	**Provider Category**: Legacy Cryptography Service Provider
      ii. **Algorithm name**: Determined by CSP
      iii. **Minimum Key size**: 2048 or 4096 as per Organization security requirement.
      iv. **Providers**: Select **Microsoft RSA Schannel Cryptographic Provider** from the drop-down
   e.	Extensions
      i.	Under **Extensions included in this template**, select **Application Policies** and then select **Edite
      ii. **Edit Application Policies Extension** dialog opens
         1.	Under **Application policies:**, select **IP security IKE intermediate** and then select **Remove**
         2.	Select **Add** and then select the below policies under Application policies:
            a.	Client Authentication
            b.	Server Authentication
         3.	Select **OK**
      iii.	Select **Key Usage** and Edit
         1.	Check **Make this extension critical** and select **OK**
   f.	Security
      i.	Ensure that the **Authenticated Users** group has **Read** and **Enroll** permissions
6. Select **Apply** to create the template.

### Add the template to the Certificate Templates folder

1.	Log onto a domain joined server with AD CS in your environment (your CA).
2.	On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3.	On the right navigation pane, expand the CA, select and hold **Certificate Templates** and select **New** > **Certificate Templates to Issue**.
4. Select the new template created in the above steps and select **OK**.

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
>HTTPS binding needs to be configured on the Certificate Services Web site of the CA, otherwise we may fail to connect to the website. For more information, see [How to Configure an HTTPS Binding for a Windows Server CA](/system-center/scom/how-to-configure-https-binding-windows-server-ca).  

To submit a request to an enterprise CA, do the following:

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate Services. 
For example, *https://\<servername\>/certsrv*.

2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.

3. On the **Request a Certificate** page, select **advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file**, or **submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure.

6. In the **Certificate Template**, select the certificate template that you created.
For example, *OperationsManagerCert*, and then select **Submit**.

7. On the **Certificate Issued** page, select **Base 64 encoded** > **Download certificate**.

8. Name and save the certificate to an accessible location.
For example, save as *SCOM-MS01.cer*.

9. Close the web browser.

## Import the certificate into the certificate store

To import the certificate into the certificate store, do the following:

1. On the computer hosting the Operations Manager feature for which you are configuring the certificate, select **Start** > **Run**.

2. In the **Run** dialog, enter **cmd**, and select **OK**.

3. In the command window, enter **CertReq -Accept NewCertifiate.cer**, and select Enter.

## Import the certificate into Operations Manager using MOMCertImport 

To import the certificate into Operations Manager using MOMCertImport, do the following:

1. Log on to the computer where you installed the certificate with an account that is a member of the Administrators group.

2. On the Windows desktop, select **Start** > **Run**.

3. In the **Run** dialog, enter **cmd**, and select **OK**.

4. At the command prompt, enter */<drive_letter/>*: (where */<drive_letter/>* is the drive where the Operations Manager installation media is located), and select Enter.

5. Enter *cd\SupportTools\i386*, and select Enter.

    >[!Note]
    >On 64-bit computers, enter *cd\SupportTools\amd64*

6. Enter the following:

   **MOMCertImport /SubjectName \<Certificate Subject Name\>**

7. Select Enter.

