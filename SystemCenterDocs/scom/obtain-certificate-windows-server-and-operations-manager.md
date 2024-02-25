---
ms.assetid: 
title: Obtain a certificate for use with Windows Servers and System Center Operations Manager
description: This article explains how to obtain a certificate for use with Windows Servers and System Center Operations Manager.
ms.custom: engagement-fy23, UpdateFrequency2
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 01/28/2023
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# Obtain a certificate for use with Windows Servers and System Center Operations Manager

This article describes how to obtain a certificate and use with Operations Manager Management Server, Gateway, or Agent using either a Stand-Alone or Enterprise Active Directory Certificate Services (AD CS) Certificate Authority (CA) server on the Windows platform.

- To request and accept a certificate, use the [certreq](/windows-server/administration/windows-commands/certreq_1) command-line utility. To submit and retrieve a certificate, use a web interface.

## Prerequisites

Ensure you've the following:

- AD-CS installed and configured in the environment with web services **or** a third party Certificate Authority with certificates that match the required settings shown.
- HTTPS binding and its associated certificate installed. For information about creating an HTTPS binding, see [How to Configure an HTTPS Binding for a Windows Server CA](/system-center/scom/configure-https-binding-windows-server-ca).
- A typical desktop experience and not Core servers.

  >[!NOTE]
  >If your organization doesn't use AD CS or uses an external certificate authority, use the instructions provided for that application to create a certificate and ensure it meets the following requirements for Operations Manager, and then follow the Import and Installation steps provided:
  >```
  >- Subject="CN=server.contoso.com" ; (this should be the FQDN or how the system shows in DNS)
  >
  >- [Key Usage]
  >     - Key Exportable=TRUE ; This setting is required for Server Authentication 
  >     - HashAlgorithm = SHA256
  >     - KeyLength=2048
  >     - KeySpec=1
  >     - KeyUsage=0xf0
  >     - MachineKeySet=TRUE
  >
  >- [EnhancedKeyUsageExtension]
  >     - OID=1.3.6.1.5.5.7.3.1 ; Server Authentication
  >     - OID=1.3.6.1.5.5.7.3.2 ; Client Authentication
  >
  >- [Compatibility Settings]
  >     - Compatible with Windows Server 2003 ; (or newer based on environment)
  >
  >- [Cryptography Settings]
  >     - Provider Category: Legacy Cryptography Service Provider
  >     - Algorithm name: RSA
  >     - Minimum Key Size: 2048 ; (2048 or 4096 as per security requirement.)
  >     - Providers: "Microsoft RSA Schannel Cryptographic Provider and Microsoft Enhanced Cryptographic Provider v1.0"
  >```

>[!Important]
>For this topic, the default settings for AD-CS are as below: 
> - Standard key length: 2048
> - Microsoft Software Key Storage Provider: CSP 
> - Secure Hash Algorithm: 256 (SHA256)
>Evaluate these selections against the requirements of your company's security policy.


High-level process to obtain a certificate:

# [Enterprise CA](#tab/Enterp)

1. Download the Root Certificate from a CA.

2. Import the Root Certificate to a client server.

3. Create a certificate template.

4. Add the template to the Certificate Templates folder.

5. Create a setup information file for use with the `<certreq>` command-line utility.

6. Create a request file (or use the web portal).

7. Submit a request to the CA.

8. Import the certificate into the certificate store.

9. Import the certificate into Operations Manager using `<MOMCertImport>`.

# [Stand-Alone CA](#tab/Standal)

1. Download the Root Certificate from a CA.

2. Import the Root Certificate to a client-server.

3. Create a setup information file to use with the `<certreq>` command-line utility.

4. Create a request file (or use the web portal).

5. Submit a request to the CA using the request file.

6. Approve the pending certificate request.

7. Retrieve the certificate from the CA.

8. Import the certificate into the certificate store.

9. Import the certificate into Operations Manager using `<MOMCertImport>`.

--- 

## Download and Import the Root Certificate from the CA

To trust and validate any certificates created from Enterprise or Stand-Alone CAs, the target machine needs to have a copy of the Root Certificate in its Trusted Root Store. Most domain-joined computers must trust the Enterprise CA. However, no machine will trust a certificate from a Stand-Alone CA without the Root Certificate installed.

If you're using a third-party CA, the download process will be different. However, the import process remains the same.

### Download the Trusted Root certificate from a CA

To download the Trusted Root certificate, follow these steps:

1. Sign in to the computer where you want to install a certificate.
For example, *a Gateway Server or Management Server*.

2. Open a web browser and connect to the certificate server web address.
For example, `https://<servername>/certsrv`.

3. On the **Welcome** page, select **Download a CA Certificate**, **Certificate chain**, or **CRL**.
   
   a.	If prompted with a **Web Access Confirmation**, verify  the  server and URL, and select **Yes**.

   b. Verify the multiple options under **CA Certificate** and confirm the selection.

4. Change the Encoding method to **Base 64** and then select **Download CA Certificate Chain**.

5. Save the certificate and provide a friendly name.

### Import the Trusted Root Certificate from the CA on the client

>[!Note]
>To import a Trusted Root Certificate, you must have administrative privileges on the target machine.

To import the Trusted Root Certificate, follow these steps:

1. Copy the file generated in the previous step to the client.
2. Open Certificate Manager.
   1. From the Command Line, PowerShell, or Run, type *certlm.msc* and press **enter**. 
   1. Select Start > Run and type *mmc* to find the Microsoft Management Console (mmc.exe).
      1. Go to **File** > **Add/Remove Snap in…**.
      1. On the Add or Remove Snap-ins dialog, select **Certificates**, and then select **Add**.
      1. On the Certificate Snap-in dialog,
         1. Select **Computer Account** and select **Next**. Select Computer dialog opens.
         1. Select **Local Computer** and select **Finish**.
      1. Select **OK**.
      1. Under Console Root, expand **Certificates (Local Computer)**
3. Expand **Trusted Root Certification Authorities**, and then select Certificates.
4. Select **All Tasks**.
5. In the Certificate Import Wizard, leave the first page as default and select **Next**.
      1. Browse to the location where you downloaded the CA certificate file and select the trusted root certificate file copied from the CA.
      1. Select **Next**.
      1. In the Certificate Store location, leave the Trusted Root Certification Authorities as default.
      1. Select **Next** and **Finish**.
6. If successful, the Trusted Root Certificate from the CA will be visible under **Trusted Root Certification Authorities** > **Certificates**.

## Create a certificate template: Enterprise CAs

**Enterprise CAs:**

 - Integrates with Active Directory Domain Services (AD-DS).
 - Publishes certificates and certificate revocation lists (CRLs) to AD-DS. 
 - Uses user accounts and security groups information that is stored in AD-DS to approve or deny certificate requests.
 - Uses certificate templates.

To issue a certificate, the Enterprise CA uses information in the certificate template to generate a certificate with the appropriate attributes for that certificate type.

**Stand-alone CAs:**

 - Don't require AD-DS.
 - Don't use certificate templates. 

If you use stand-alone CAs, include all the information about the requested certificate type in the certificate request.

For more information, see [certificate templates](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831574(v=ws.11)).

### Create a certificate template for System Center Operations Manager

1. Sign in to a domain joined server with AD CS in your environment (your CA).
2. On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3. On the right navigation pane, expand the CA, right-click **Certificate Templates**, and select **Manage**.
4. Right-click **IPSec (Offline request)** and select **Duplicate Template**.
5. The **Properties of New Template** dialog opens; make the selections as below:
     
   |Tab|Description|
   |----|---------------|  
   |Compatibility| 1. **Certification Authority**: Windows Server 2008 (or the lowest AD functional level in the environment).</br> 2. **Certificate Recipient**: Windows Server 2012 (or the lowest version OS in the environment).|
   |General| 1. **Template display name**: Enter a friendly name, such as *Operations Manager*.</br> 2. **Template name**: Enter the same name as display name.</br> 3. **Validity period**: Enter the validity period to match your organization’s requirements.</br> 4. Select **Publish certificate in Active Directory** and **Do not automatically reenroll if a duplicate certificate exists in Active Directory** checkboxes.|
   |Request Handling| 1. **Purpose**: Select **Signature and encryption** from the dropdown.</br> 2. Select **Allow private key to be exported** checkbox.|
   |Cryptography| 1. **Provider Category**: Select Legacy Cryptography Service Provider</br> 2. **Algorithm name**: Select Determined by CSP from the dropdown.</br> 3. **Minimum Key size**: 2048 or 4096 as per Organization security requirement.</br> 4. **Providers**: Select **Microsoft RSA channel Cryptographic Provider** and **Microsoft Enhanced Cryptographic Provider v1.0** from the dropdown.|
   |Extensions| 1. Under **Extensions included in this template**, select **Application Policies** and then select **Edit**</br> 2. **Edit Application Policies Extension** dialog opens.</br> 3. Under **Application policies:**, select **IP security IKE intermediate** and then select **Remove**</br> 4. Select **Add** and then select the **Client Authentication** and **Server Authentication** under **Application policies**.</br> 5. Select **OK**.</br> 6. Select **Key Usage** and **Edit**.</br> 7. Ensure **Digital signature** and **Allow key exchange only with key encryption (key encipherment)** are selected. </br>8. Select **Make this extension critical** checkbox and select **OK**.|
   |Security| 1. Ensure that the **Authenticated Users** group (or Computer object) has **Read** and **Enroll** permissions and select **Apply** to create the template.|

### Add the template to the Certificate Templates folder

1. Sign in to a domain joined server with AD CS in your environment (your CA).
2. On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3. On the right navigation pane, expand the CA, right-click **Certificate Templates**, and select **New** > **Certificate Templates to Issue**.
4. Select the new template created in the above steps and select **OK**.

## Request a certificate using a request file

### Create a setup information (.inf) file

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open a new text file in a text editor.

2. Create a text file containing the following content:

      ```

      [NewRequest]
      Subject=”CN=server.contoso.com”
      Key Exportable = TRUE  ; Private key is exportable
      HashAlgorithm = SHA256
      KeyLength = 2048  ; (2048 or 4096 as per Organization security requirement.)
      KeySpec = 1  ; Key Exchange – Required for encryption
      KeyUsage = 0xf0  ; Digital Signature, Key Encipherment
      MachineKeySet = TRUE
      ProviderName = "Microsoft RSA SChannel Cryptographic Provider and Microsoft Enhanced Cryptographic Provider v1.0"
      ProviderType = 12
      KeyAlgorithm = RSA

      ; Optionally include the Certificate Template for Enterprise CAs, remove the ; to uncomment
      ; [RequestAttributes]
      ; CertificateTemplate="SystemCenterOperationsManager"

      [EnhancedKeyUsageExtension]
      OID = 1.3.6.1.5.5.7.3.1  ; Server Authentication
      OID = 1.3.6.1.5.5.7.3.2  ; Client Authentication

      ```

3. Save the file with an *.inf* file extension.
For example, `CertRequestConfig.inf`.

4. Close the text editor.


### Create a Certificate request file

This process encodes the information specified in our config file in Base64 and outputs to a new file.

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open an Administrator command prompt.

2. Navigate to the same directory where the *.inf* file is located.

3. Run the below command to modify the *.inf* file name to ensure it matches the file name created earlier. Leave the *.req* file name as-is:

      ```
      CertReq –New –f CertRequestConfig.inf CertRequest.req
      ```

4. Open the newly created file and copy the contents.

## Submit a new certificate request in the AD CS web portal using the request file

# [Enterprise CA](#tab/Enter)

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open a web browser and connect to the computer hosting Certificate server web address.
For example, `https://<servername>/certsrv`.

2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.

3. On the **Request a Certificate** page, select **advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file** or **submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure.

6. On the **Certificate Template**, select the certificate template that you created.
For example, *OperationsManagerCert*, and then select **Submit**.

7. If successful, on the **Certificate Issued** page, select **Base 64 encoded** > **Download certificate**.

8. Save the certificate and provide a friendly name.
For example, save as *SCOM-MS01.cer*.

9. Close the web browser.


# [Stand-Alone CA](#tab/StandAlo)

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address.
For example, `https://<servername>/certsrv`.


2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.

3. On the **Request a Certificate** page, select **Advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file**, or **Submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure.

6. On the **Certificate Template**, select the certificate template that you created.
For example, *OperationsManagerCert*, and then select **Submit**.

7. A request will now be submitted to the CA for manual approval before we can download the certificate.

### Approve the pending certificate request on a Stand-Alone CA

1. Sign in to an Enterprise Certificate Authority in your environment.
2. Select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3. On the left navigation pane, expand the CA and select  **Pending Requests**.
4. On the right navigation pane, find and select the pending request for the Operations Manager server.
5. Right-click the **Pending request** > **All Tasks** > **Issue**
6. On the left navigation, select **Issued Certificates**, verify the presence of newly issued certificate.
7. Close the Certification Authority console.

### Retrieve the certificate from a Stand-Alone CA

A certificate from a Stand-Alone CA will be retrieved on the target machine for ease of certificate installation. If the CA isn't reached from the target machine, ensure to export the certificate as indicated below:

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address.
For example, `https://<servername>/certsrv`.
2. On the Welcome page, select **View the status of a pending certificate request**.
3. On the Certificates Issued page, select **Base 64 encoded**, and select **Download Certificate**.
4. If successful, the **Certificate Issued** page opens with a link to **Install this certificate**.
5. Select **Install this certificate**.
6. On the server, *Personal certificate store* stores the certificate.
7. Load the *MMC* or *CertMgr* consoles and navigate to **Personal** > **Certificates**, and locate the newly created certificate.
8. Upon the successful completion of the task on the target server, continue to the next main step. Else, export the certificate:
      1. Right-click the new certificate > **All Tasks** > **Export**.
      1. In the **Certificate Export Wizard**, select **Next**.
      1. Select **Yes, export the private key** and select **Next**.
      1. Select **Personal Information Exchange – PKCS #12 (.PFX)**.
      1. Check **Include all certificates in the certification path if possible**.
      1. Check **Export all extended properties** and select **Next**.
      1. Provide a password to encrypt the certificate file at rest and select Next.
      1. Save the exported file and provide a friendly name.
      1. Select **Next**, and **Finish**.
      1. Locate the exported certificate file and inspect the icon of the file.
          1. If the icon contains a Key, then you must have the private key attached.
          1. If the icon doesn't contain a key, export the certificate again with the private key as you need it for later use.
      1. Copy the exported file to the target machine.
10.	Close the web browser.

--- 

## Use the AD-CS web portal to request a certificate 

Apart from the request file, you can create a certificate request through the Certificate services web portal. This step completes on the target machine for ease of certificate installation. If the certificate request using the AD-CS web portal isn't possible, ensure to export the certificate as indicated below:

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address.
For example, `https://<servername>/certsrv`.
2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.
3. On the **Request a Certificate** page, select **advanced certificate request**.
4. Select **Create and submit a request to this CA**.
5. An Advanced Certificate Request opens. Do the following:
      1. Certificate Template: Use the template created earlier, or one designated for Operations Manager.
      1. Identifying Information for Offline Template:
          1. Name: FQDN of the server, or as it appears in DNS
          1. Provide other information as appropriate for your organization
      1. Key Options:
          1. Select the checkbox for Mark keys as exportable
      1. Additional Options:
          1. Friendly Name: FQDN of the server, or as it appears in DNS
6. Select **Submit**.
7. Upon the successful completion of the task, **Certificate Issued** page opens with a link to **Install this certificate**.
8. Select **Install this certificate**.
9. On the server, the *Personal certificate store* stores the certificate.
10. Load the *MMC* or *CertMgr* consoles, and go to **Personal** > **Certificates** and locate the newly created certificate.
11. If this task isn't completed on the target server, export the certificate:
      1. Right-click the new certificate > All Tasks > Export.
      1. In the **Certificate Export Wizard**, select **Next**.
      1. Select **Yes, export the private key**, select **Next**.
      1. Select **Personal Information Exchange – PKCS #12 (.PFX)**.
      1. Select **Include all certificates in the certification path if possible** and **Export all extended properties** checkboxes, and select **Next**.
      1. Provide a password to encrypt the certificate file at rest, and select **Next**.
      1. Save the exported file and provide a friendly name.
      1. Select **Next**, and **Finish**.
      1. Locate the exported certificate file and inspect the icon for the file.
          1. If the icon contains a Key, then you must have the private key attached.
          1. If the icon doesn't contain a key, re-export the certificate with the private key as you need it for later use.
      1. Copy the exported file to the target machine.
13. Close the web browser.

## Request a certificate using Certificate Manager

For Enterprise CAs with a defined certificate template, you may be able to request a new certificate from a domain joined client machine using the Certificate Manager. As this uses templates, this method doesn't apply to Stand-Alone CAs.

1. Sign in to the target machine with administrator rights (Management Server, Gateway, Agent, and so on).
2. Use Administrator Command Prompt or PowerShell window to open Certificate Manager.
      1. *certlm.msc* – opens the Local Machine certificate store.
      1. *mmc.msc* – opens the Microsoft Management Console.
          1. Load the Certificate Manager snap-in.
          1. Go to **File** > **Add/Remove Snap-In**.
          1. Select **Certificates**.
          1. Select **Add**.
          1. When prompted, select *Computer Account* and select **Next**
          1. Ensure to select *Local Computer* and select **Finish**.
          1. Select **OK** to close the wizard.
3. Start the certificate request:
      1. Under Certificates, expand the Personal folder.
      1. Right-click  **Certificates** > **All Tasks** > **Request New Certificate**.
4. **Certificate Enrollment wizard**
      1. On the **Before You Begin** page, select **Next**.
      1. Select the applicable Certificate Enrollment Policy (default may be the **Active Directory Enrollment Policy**), select **Next**
      1. Select the desired Enrollment Policy template to create the certificate
          1. If the template isn't immediately available, select **Show all templates** box below the list
          1. If the template needed is available with a red X beside it, consult your Active Directory or Certificate team
      1. In most environments, you can find a warning message with a hyperlink under the certificate template, select the link and continue to fill the information for the certificate.
          
      1. **Certificate Properties wizard:**
         
         |Tab|Description|
         |----|---------------|
         |Subject| 1. In Subject Name, select the **Common Name** or **Full DN**, provide the value - hostname or BIOS name of the target server, Select **Add**.|
         |General| 1. Provide a Friendly Name to the generated certificate.</br> 2. Provide a description of the purpose of this ticket if desired.|
         |Extensions| 1. Under Key usage, ensure to select **Digital Signature** and **Key encipherment** option, and select the **Make these key usages critical** checkbox.<br> 2. Under Extended Key Usage, ensure to select **Server Authentication** and **Client Authentication** options.|
         |Private Key| 1. Under Key options, ensure that the Key Size is at least 1024 or 2048, and select the **Make private key exportable** checkbox.</br> 2. Under Key type, ensure to select the **Exchange** option.|
         |Certification Authority tab| Ensure to select the CA checkbox.|
         |Signature| If your organization requires a registration authority, provide a signing certificate for this request. |

      1. Once the information has been provided in the Certificate Properties wizard, the warning hyperlink from earlier disappears.
      1. Select **Enroll to create the certificate**. If there's an error, consult your AD or certificate team.
      1. If successful, the status will read **Succeeded** and a new certificate will be placed in the Personal/Certificates store.
5. If these actions were taken on the intended recipient of the certificate, proceed to the next steps.
6. Otherwise, export the new certificate from the machine and copy to the next.
      1. Open the Certificate Manager window and navigate to **Personal** > **Certificates**.
      1. Select the certificate to be exported.
      1. Right-click All **Tasks** > **Export**.
      1. In the Certificate Export Wizard.
          1. Select **Next** on the Welcome page.
          1. Ensure to select **Yes, export the private key**.
          1. Select **Personal Information Exchange – PKCS #12 (.PFX)** from the format options.
              1. Select **Include all certificates in the certification path if possible** and **Export all extended properties** checkboxes.
          1. Select **Next**.
          1. Provide a known password to encrypt the certificate file.
          1. Select **Next**.
          1. Provide an accessible path and recognizable file name for the certificate.
      1. Copy the newly created certificate file to the target machine.

## Install the certificate on the target machine

To use the newly created certificate, import it into the certificate store on the client machine.

### Add the certificate to the Certificate Store

1. Sign in to the computer where the certificates are created for Management Server, Gateway, or Agent.
2. Copy the certificate created above to an accessible location on this machine.
3. Open an Administrator Command Prompt or PowerShell window and navigate to the folder where the certificate file is located.
4. Run the below command, ensure to replace *NewCertificate.cer* with the correct name/path of the file:

      `CertReq -Accept -Machine NewCertificate.cer`

5. This certificate should now be present in the Local Machine Personal store on this computer.

Alternatively, right-click the certificate file > Install > Local machine and choose the destination of the personal store to install the certificate.

>[!NOTE]
>If you add a certificate to the certificate store with the private key and delete it from the store at a later point, the certificate will no longer contain the private key when re-imported. Operations Manager communications requires private key as the outgoing data needs to be encrypted. You can repair the certificate using [certutil](/windows-server/administration/windows-commands/certutil#-repairstore); you need to provide the serial number of the cert. For example, to restore the private key, use the below command in an Administrator Command Prompt or PowerShell window:
>```
>certutil -repairstore my <certificateSerialNumber>
>```

## Import the certificate into Operations Manager  

Apart from installation of certificate on the system, you must update Operations Manager to be aware of the certificate that you want to use. The actions below will restart the Microsoft Monitoring Agent service.

Use the MOMCertImport.exe utility included in the **SupportTools** folder in the Operations Manager installation media. Copy the file to your server.


To import the certificate into Operations Manager using MOMCertImport, follow these steps:

1. Sign in to the target computer.
2. Open an Administrator Command Prompt or PowerShell window and navigate to the *MOMCertImport.exe* utility folder.
3. Run the *MomCertImport.exe* utility
      1. In CMD: `MOMCertImport.exe`
      1. In PowerShell: `.\MOMCertImport.exe`
4. A GUI Window appears to **Select a Certificate**
      1. You can see a list of certificates, if you don't immediately see a list, select **More choices**.
5. From the list, select the new certificate for the machine
      1. You can verify the certificate by selecting it. Once selected, you can view the certificate properties.
6. Select **OK**
7. If successful, a pop-up window will display the following message:

      `Successfully installed the certificate. Please check Operations Manager log in eventviewer to check channel connectivity.`

8. To validate, go to **Event Viewer** > **Applications and Services Logs** > **Operations Manager for an Event ID 20053**. This indicates that the authentication certificate was loaded successfully
9. If Event ID **20053** isn't present on the system, look for one of these Event IDs for errors and correct accordingly:
    - **20049** 
    - **20050** 
    - **20052**
    - **20066**
    - **20069**
    - **20077**

11. *MOMCertImport* updates this registry location to contain the value that matches the reverse of the serial number shown on the certificate:
      ```
      HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\MachineSettings\ChannelCertificateSerialNumber
      ```

## Renew a Certificate

The Operations Manager generates an alert when an imported certificate for Management Servers and Gateways is nearing expiration. If you receive an alert, renew or create a new certificate for the servers before the expiration date. This will only work if the certificate contains template information (from an Enterprise CA).

1. Sign in to the server with the expiring certificate and launch the certificate configuration manager (*certlm.msc*).
2. Locate the expiring Operations Manager certificate.
3. If you don't find the certificate, it may have either been removed or imported via file and not the certificate store. You may need to issue a new certificate for this machine from the CA. Refer to the instructions above to do so.
4. If you find the certificate, below are the options to renew the cert:
      1. Request Certificate with New Key
      1. Renew Certificate with New Key
      1. Renew Certificate with Same Key
5. Select the option that best applies to what you want to do and follow the wizard.
6. Once completed, run the `MOMCertImport.exe` tool to ensure Operations Manager has the new serial number (reversed) of the certificate if it changed; see the above section for further details.

If certificate renewal via this method isn't available, use the prior steps to request a new certificate or with the organization’s certificate authority. Install and import (MOMCertImport) the new certificate for use by Operations Manager.

### Optional: Configure certificate auto-enrollment and renewal

Use the Enterprise CA to configure certificate auto-enrollment and renewals when they expire. This will distribute the Trusted Root certificate to all domain-joined systems.

Configuration of certificate auto-enrollment and renewal won't work with Stand-Alone or third-party CAs. For systems in a Workgroup or separate domain, certificate renewals and enrollments will still be a manual process.


For more information, see [Windows Server guide](/windows-server/networking/core-network-guide/cncg/server-certs/configure-server-certificate-autoenrollment).

>[!Note]
>Auto-enrollment and renewal doesn't automatically configure Operations Manager to use the new certificate. If the certificate auto renews with the same key, the thumbprint may also stay the same and no action is required by an Administrator. If a new certificate is generated or the thumbprint changes, the updated certificate will need to be imported into Operations Manager using the MOMCertImport tool as outlined above.
