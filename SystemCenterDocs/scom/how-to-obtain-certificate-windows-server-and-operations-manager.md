---
ms.assetid: 
title: How to obtain a certificate for use with Windows Servers and System Center Operations Manager.
description: This article explains How to obtain a certificate for use with Windows Servers and System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 08/11/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# How to obtain a certificate for use with Windows Servers and System Center Operations Manager

*Applies to:* System Center Operations Manager, Windows Server and AD CS 2012 R2 or newer

Using the procedures below, you will be able to obtain a certificate to be used with Operations Manager Management Server, Gateway, or Agent using either a Stand-Alone or Enterprise Active Directory Certificate Services (AD CS) Certificate Authority (CA) server on the Windows platform.

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
>     - `Key Exportable=TRUE`
>     - `HashAlgorithm = SHA256`
>     - `KeyLength=2048`
>     - `KeySpec=1`
>     - `KeyUsage=0xf0`
>     - `MachineKeySet=TRUE`
>
>- `[EnhancedKeyUsageExtension]`
>     - `OID=1.3.6.1.5.5.7.3.1 ; Server Authentication`
>     - `OID=1.3.6.1.5.5.7.3.2 ; Client Authentication`
>
>- `[Compatibility Settings]`
>     - `Compatible with Windows Server 2003 ; (or newer based on environment)`
>
>- `[Cryptography Settings]`
>     - `Provider Category: Legacy Cryptography Service Provider`
>     - `Algorithm name: RSA`
>     - `Minimum Key Size: 2048 ; (2048 or 4096 as per security requirement.)`
>     - `Providers: Microsoft RSA Schannel Cryptographic Provider`

>[!Important]
>The content for this topic is based on the default settings for AD-CS; for example, the standard key length is 2048, and select Microsoft Software Key Storage Provider as CSP and Secure Hash Algorithm 256 (SHA256). Evaluate these selections against the requirements of your company's security policy.

The high-level process to obtain a certificate is:

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

2. Import the Root Certificate to a client server.

3. Create a setup information file to use with the `<certreq>` command-line utility.

4. Create a request file (or use the web portal).

5. Submit a request to the CA using the request file.

6. Approve the pending certificate request.

7. Retrieve the certificate from the CA.

8. Import the certificate into the certificate store.

9. Import the certificate into Operations Manager using `<MOMCertImport>`.

--- 

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

6. Select **Download CA Certificate Chain** link.

7. Select an accessible location for the certificate and give it a friendly file name for later use.

## Import the Trusted Root Certificate from the CA on the client

>[!Note]
>To import a Trusted Root Certificate, you must have administrative privileges on the target machine. 

To import the Trusted Root Certificate, do the following:

1. Copy the file generated in the previous step to the client.
2. Open Certificate Manager.
      1. From the Start menu
          1. Type *mmc* to find the Microsoft Management Console (mmc.exe).
          1. Run this utility.
          1. Go to **File** > **Add/Remove Snap in…**.
          1. On the Add or Remove Snap-ins window, select **Certificates** and then select **Add**.
          1. On the Certificate Snap-in window
              1. Select **Computer Account** and select **Next**.
              1. Select **Local Computer** and select **Finish**.
          1. Select **OK**
      1. From the Command Line, PowerShell, or Run
          1. Type **certlm.msc** and press **enter**.
          1. The steps above also apply if *certlm.msc* cannot be found.
3. Under Console Root, expand **Certificates (Local Computer)**.
4. Expand **Trusted Root Certification Authorities**,
      1. Select and hold **Certificates**.
      1. Select **All Tasks**.
      1. Select **Import**
5. In the Certificate Import Wizard,
      1. Leave the first page as default and select **Next**
      1. Browse to and select the trusted root certificate file copied from the CA.
      1. Select **Next**.
      1. In the Certificate Store location, leave as the default Trusted Root Certification Authorities.
      1. Select **Next**.
      1. Select **Finish**.
6. If successful, the Trusted Root Certificate from the CA should now be visible under **Trusted Root Certification Authorities** > **Certificates**.

## Enterprise CAs: Create a certificate template

**Enterprise CAs** are integrated with Active Directory Domain Services (AD DS). They publish certificates and certificate revocation lists (CRLs) to AD DS. Enterprise CAs use information that is stored in AD DS, including user accounts and security groups, to approve or deny certificate requests. Enterprise CAs use certificate templates. When a certificate is issued, the Enterprise CA uses information in the certificate template to generate a certificate with the appropriate attributes for that certificate type.

**Stand-alone CAs** do not require AD DS, and they do not use certificate templates. If you use stand-alone CAs, all information about the requested certificate type must be included in the certificate request. 

More information, see [certificate templates](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831574(v=ws.11)).

### Create a certificate template for System Center Operations Manager

1. Log onto a domain joined server with AD CS in your environment (your CA).
2. On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3. On the right navigation pane, expand the CA, select and hold **Certificate Templates** and select **Manage**.
4. Select and hold **IPSec (Offline request)** and select **Duplicate Template**.
5. **Properties of New Template** dialog opens, make the selections as below:
      1. Compatibility
          1. **Certification Authority**: Windows Server 2008 (or the lowest AD functional level in the environment)
          1. **Certificate Recipient**: Windows Server 2012 (or the lowest version OS in the environment)
      1. General
          1. **Template display name**: Enter a friendly name, such as *SCOM* or *Operations Manager*
          1. **Template name**: Same as display name
          1. **Validity period**: This should match your organization’s requirements
          1. Check **Publish certificate in Active Directory**
          1. Check **Do not automatically reenroll if a duplicate certificate exists in Active Directory**
      1. Request Handling
          1. **Purpose**: Select **Signature and encryption** from the drop-down
          1. Check **Allow private key to be exported**
      1. Cryptography
          1. **Provider Category**: Legacy Cryptography Service Provider
          1. **Algorithm name**: Determined by CSP
          1. **Minimum Key size**: 2048 or 4096 as per Organization security requirement.
          1. **Providers**: Select **Microsoft RSA Schannel Cryptographic Provider** from the drop-down
      1. Extensions
          1. Under **Extensions included in this template**, select **Application Policies** and then select **Edite
          1. **Edit Application Policies Extension** dialog opens
              1. Under **Application policies:**, select **IP security IKE intermediate** and then select **Remove**
              1. Select **Add** and then select the below policies under Application policies:
                  1. Client Authentication
                  1. Server Authentication
          1. Select **OK**
              1. Select **Key Usage** and Edit
              1. Check **Make this extension critical** and select **OK**
      1. Security
          1. Ensure that the **Authenticated Users** group has **Read** and **Enroll** permissions
6. Select **Apply** to create the template.

### Add the template to the Certificate Templates folder

1. Log onto a domain joined server with AD CS in your environment (your CA).
2. On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
3. On the right navigation pane, expand the CA, select and hold **Certificate Templates** and select **New** > **Certificate Templates to Issue**.
4. Select the new template created in the above steps and select **OK**.

## Request a certificate using a request file

### Create a setup information (.inf) file

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a new text file in a text editor.

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
      ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
      ProviderType = 12
      KeyAlgorithm = RSA

      ; Optionally include the Certificate Template for Enterprise CAs, remove the ; to uncomment
      ; [RequestAttributes]
      ; CertificateTemplate="SystemCenterOperationsManager"

      [EnhancedKeyUsageExtension]
      OID = 1.3.6.1.5.5.7.3.1  ; Server Authentication
      OID = 1.3.6.1.5.5.7.3.2  ; Client Authentication

      ```

3. Save the file with an .inf file name extension.
For example, *CertRequestConfig.inf*.

4. Close text editor.


### Create a Certificate request file

This process encodes the information specified in our config file in Base64 and outputs to a new file.

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open an Administrator command prompt.

2. Navigate to the same directory where the .inf file is located.

3. Run the below command, modifying the *.inf* and *.req* file names as needed (leave the .req extension as-is):

      ```

      CertReq –New –f CertRequestConfig.inf CertRequest.req

      ```

4. Open the newly created file and copy the contents.

## Submit a new certificate request in the AD CS web portal using the request file

# [Enterprise CA](#tab/Enter)

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address
For example, *https://\<servername\>/certsrv*.

2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.

3. On the **Request a Certificate** page, select **advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file**, or **submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure.

6. On the **Certificate Template**, select the certificate template that you created (note that this may take some time to propagate across the environment).
For example, *OperationsManagerCert*, and then select **Submit**.

7. If successful, on the **Certificate Issued** page, select **Base 64 encoded** > **Download certificate**.

8. Save the certificate to an accessible location and give it a friendly name.
For example, save as *SCOM-MS01.cer*.

9. Close the web browser.


# [Stand-Alone CA](#tab/StandAlo)

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address
For example, *https://\<servername\>/certsrv*.


2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.

3. On the **Request a Certificate** page, select **advanced certificate request**.

4. On the **Advanced Certificate Request** page, select **Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file**, or **submit a renewal request by using a base-64-encoded PKCS #7 file**.

5. On the **Submit a Certificate Request or Renewal Request** page, in the **Saved Request** text box, paste the contents of the *CertRequest.req* file that you copied in step 4 in the previous procedure.

6. On the **Certificate Template**, select the certificate template that you created (note that this may take some time to propagate across the environment).
For example, *OperationsManagerCert*, and then select **Submit**.

7. A request will now be submitted to the CA for manual approval before we can download the certificate.

### Approve the pending certificate request on a Stand-Alone CA

1. Log onto an Enterprise Certificate Authority in your environment.
2. Open the **Certification Authority** utility.
      1. This tool can be found in the Start menu under **Windows Administrative Tools** > **Certification Authority**.
3. On the left navigation pane, expand the CA and select  **Pending Requests**.
4. On the right navigation pane, find and select the pending request for the SCOM server
5. Select and hold the **Pending request** > **All Tasks** > **Issue**
6. On the left navigation, select **Issued Certificates**, verify the newly issued certificate is present.
7. Close the Certification Authority console.

### Retrieve the certificate from a Stand-Alone CA

Ideally this step will be completed on the target machine for ease of certificate installation. If that is not possible, that is ok as well, please make sure to export the certificate as indicated below:

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address
For example, *https://\<servername\>/certsrv*.
2. On the Welcome page, select **View the status of a pending certificate request**.
3. On the Certificates Issued page, select **Base 64 encoded**, then **Download Certificate**.
4. If successful, you will be presented with a **Certificate Issued** page with an **Install this certificate link**.
5. Select **Install this certificate**.
6. The certificate will be stored in the Personal certificate store on the server this was run from
7. Load the *MMC* or *CertMgr* consoles.
      1. Navigate to **Personal** > **Certificates**
      1. Locate the newly created certificate
8. If this task was completed on the target server, continue to the next main step.
9. If not on the intended target server, export the certificate:
      1. Select and hold the **new certificate** > **All Tasks** > **Export**
      1. In the **Certificate Export Wizard**, select **Next**
      1. Select **Yes, export the private key** and then select **Next**
      1. Select **Personal Information Exchange – PKCS #12 (.PFX)**
      1. Check **Include all certificates in the certification path if possible**
      1. Check **Export all extended properties**
      1. Select **Next**
      1. Provide a memorable password to encrypt the certificate file at rest, select **Next**
      1. Browse to an accessible path to save the exported file, give the file a friendly name 
      1. Select **Next**, and **Finish**
      1. Find the exported certificate file, inspect the icon for the file
          1. If the icon contains a Key, then we should have the private key attached
          1. If the icon does not contain a key, export the certificate again with the private key as it will be needed later
      1. Copy the exported file to the target machine 
10.	Close the web browser

--- 

## Request a certificate using the AD CS Web Portal

Alternative to the request file, we can create a certificate request directly through the Certificate Services web portal. Ideally this step will be completed on the target machine for ease of certificate installation. If that is not possible, that is ok as well, make sure to export the certificate as indicated below:

1. On the computer hosting the Operations Manager feature for which you are requesting a certificate, open a web browser, and connect to the computer hosting Certificate server web address
For example, *https://\<servername\>/certsrv*.
2. On the **Microsoft Active Directory Certificate Services Welcome** page, select **Request a certificate**.
3. On the **Request a Certificate** page, select **advanced certificate request**.
4. Select **Create and submit a request to this CA**.
5. An Advanced Certificate Request page will load, complete as so:
      1. Certificate Template: use the template created earlier, or one designated for SCOM
      1. Identifying Information for Offline Template:
          1. Name: this should be the FQDN of the server, or how it shows in DNS
          1. Provide other information as appropriate for your organization
      1. Key Options:
          1. Mark keys as exportable – check this box
      1. Additional Options:
          1. Friendly Name: this should be the FQDN of the server, or how it shows in DNS
6. Select **Submit**.
7. If successful, you will be presented with a **Certificate Issued** page with an **Install this certificate link**.
8. Select **Install this certificate**.
9. The certificate will be stored in the Personal certificate store on the server this was run from.
10. Load the *MMC* or *CertMgr* consoles.
      1. Navigate to Personal > Certificates
      1. Locate the newly created certificate
11. If this task was completed on the target server, continue to the next main step
12. If not on the intended target server, export the certificate:
      1. Select and hold the new certificate > All Tasks > Export
      1. In the **Certificate Export Wizard**, select **Next**
      1. Select **Yes, export the private key**, select **Next**
      1. Select **Personal Information Exchange – PKCS #12 (.PFX)**
      1. Check **Include all certificates in the certification path if possible**
      1. Check **Export all extended properties**
      1. Select **Next**
      1. Provide a memorable password to encrypt the certificate file at rest, select **Next**
      1. Browse to an accessible path to save the exported file, give the file a memorable name in 
      1. Select **Next**, and **Finish**
      1. Find the exported certificate file, inspect the icon for the file
          1. If the icon contains a Key, then we should have the private key attached
          1. If the icon does not contain a key, re-export the certificate with the private key as it will be needed later
      1. Copy the exported file to the target machine 
13. Close the web browser

## Request a certificate using Certificate Manager

For Enterprise CAs with a defined certificate template, you may be able to request a new certificate from a domain joined client machine using Certificate Manager. As this uses templates, this method does not apply to Stand-Alone CAs.

1. Log onto the target machine with administrator rights (Management Server, Gateway, Agent, etc.)
2. Open Certificate Manager using an Administrator Command Prompt or PowerShell window
      1. *certlm.msc* – will open the Local Machine certificate store 
      1. *mmc.msc* –will open the Microsoft Management Console 
          1. We will then need to load the Certificate Manager snap-in
          1. Go to File > Add/Remove Snap-In
          1. Select Certificates
          1. Select **Add**
          1. When prompted, select *Computer Account* and select **Next**
          1. Ensure *Local Computer* is selected and select **Finish**
          1. Select **OK** to close the wizard
3. Start the certificate request:
      1. Expand the folders for Personal > Certificates
      1. Select and hold Certificates > All Tasks > Request New Certificate
4. In the Certificate Enrollment wizard:
      1. Select **Next** on the **Before You Begin** page
      1. Select the applicable Certificate Enrollment Policy (default may be the **Active Directory Enrollment Policy**), select **Next**
      1. Find and check the box beside the Enrollment Policy template needed to create the certificate
          1. If the template is not immediately available, check the **Show all templates** box below the list
          1. If the template needed is not unavailable or has a red X beside it, please consult with your Active Directory or Certificate team
      1. In most environments, there will be a warning message in a hyperlink under the certificate template, select this link to continue filling out the information for the certificate
          1. For example:
      1. In the Certificate Properties wizard:
          1. Under the Subject tab
              1. In Subject Name, select the **Common Name** or **Full DN**, provide the value that is the hostname or BIOS name of the target server, Select **Add**
                  1. SCOM will only recognize the first name in the list
              1. If there is an Alternative Name, provide that
                  1. SCOM will only recognize the first name in the list
          1. Under the General tab
              1. Provide a Friendly Name for easy recognition once the certificate is generated
              1. Provide a description of the purpose of this ticket if desired
          1. Under the Extensions tab
              1. Under Key usage
                  1. Ensure that the selected options are “Digital Signature” and “Key encipherment”
                  1. Ensure the “Make these key usages critical” box is checked
          1. Under Extended Key Usage
                  1. Ensure that the selected options are “Server Authentication” and “Client Authentication” 
          1. Under the Private Key tab
              1. Under Key options
                  1. Ensure that the Key Size is at least 1024 or 2048
                  1. Ensure that the “Make private key exportable” box is checked 
          1. Under Key type
              1. Ensure that the Exchange radio button is marked
          1. Under the Certification Authority tab
              1. Ensure that a CA is checked and that there are no errors presented
          1. Under the Signature tab
              1. If your organization requires a registration authority, please provide a signing certificate for this request
              1. Otherwise continue
          1. When completed, Select **OK** to close this wizard
      1. Once the information has been provided in the Certificate Properties wizard, the warning hyperlink from earlier will clear
      1. Select **Enroll to create the certificate**
          1. If there is an error, please consult your AD or certificate team
      1. If successful, the status will read **Succeeded** and a new certificate will be placed in the Personal/Certificates store
5. If these actions were taken on the intended recipient of the certificate, proceed to the next steps
6. Otherwise, the new certificate will need to be exported from this machine, and copied to the next
      1. Open the Certificate Manager window and navigate to Personal > Certificates
      1. Select the certificate to be exported
      1. Select and hold All Tasks > Export
      1. In the Certificate Export Wizard
          1. Select Next on the Welcome page
          1. Ensure that **Yes, export the private key** is selected
          1. Select **Personal Information Exchange – PKCS #12 (.PFX)** from the format options
              1. Check the box for **Include all certificates in the certification path if possible**
              1. Check the box for **Export all extended properties**
          1. Select Next
          1. Provide a known password to encrypt the certificate file 
          1. Select Next
          1. Provide an accessible path and recognizable file name for the certificate
      1. Copy the newly created certificate file to the target machine

## Install the certificate on the target machine

To use the newly created certificate, it will need to be imported into the certificate store on the client machine.

### Add the certificate to the Certificate Store

1. Log onto the computer that we created the certificate for (Management Server, Gateway, or Agent)
2. Copy the certificate created above to an accessible location on this machine
3. Open an Administrator Command Prompt or PowerShell window
4. Navigate to the folder where the certificate file is located
5. Run the below command, be sure to replace “NewCertificate.cer” with the correct name/path of the file:

      `CertReq -Accept -Machine NewCertificate.cer`

6. This certificate should now be present in the Local Machine Personal store on this computer

Alternatively, you may also be able to install the certificate by right-clicking on it, selecting Install, select Local Machine and choosing the destination of personal store.

>[!NOTE]
>If a certificate is added to the certificate store with the private key and is later deleted from the store, when the certificate is re-imported, it may no longer contain the private key. The private key is required for SCOM communications to take place as it is used to encrypt outgoing data. We can repair the certificate using [certutil](/windows-server/administration/windows-commands/certutil#-repairstore), we will need to provide the serial number of the cert. 
>For example, to restore the private key, use the below command in an Administrator Command Prompt or PowerShell window:
>`certutil -repairstore my [certificateSerialNumber]`

## Import the certificate into Operations Manager  

Simply having the certificate installed on the system is not enough, we also need to update Operations Manager to be aware of the certificate that we want it to use. The actions below will restart the Microsoft Monitoring Agent service.

This uses the *MOMCertImport.exe* utility included in the **SupportTools** folder in the Operations Manager installation media. Please copy this file to your server.

To import the certificate into Operations Manager using MOMCertImport, do the following:

1. Log onto the computer that we created the certificate for
2. Open an Administrator Command Prompt or PowerShell window
3. Navigate to the folder where the *MOMCertImport.exe* utility is saved
4. Run the *MomCertImport.exe* utility
      1. In CMD:
          1. *MOMCertImport.exe*
      1. In PowerShell:
          1. *.\MOMCertImport.exe*
5. When ran, a GUI Window will pop up asking to **Select a Certificate**
      1.	There will be a list of certificates, if you do not immediately see a list, select **More choices**.
6. From the list, select the new certificate for this machine
      1.	Select **You can verify the certificate by selecting** to view the certificate properties.
7. Select **OK**
8. If successful, below message will display in the console:

      `Successfully installed the certificate. Please check Operations Manager log in eventviewer to check channel connectivity.`

9. To validate, go to **Event Viewer** > **Applications and Services Logs** > **Operations Manager for an Event ID 20053**. This indicates that the authentication certificate was loaded successfully
10. If Event ID 20053 is not present on the system, look for one of these Event IDs for errors and correct accordingly:
    - 20049 
    - 20050 
    - 20052 
    - 20066 
    - 20069 
    - 20077

11. *MOMCertImport* updates this registry location to contain the value which will match the reverse of the serial number shown on the certificate:
   
      `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\MachineSettings\ChannelCertificateSerialNumber`

## How to Renew a Certificate

Under most cases, Operations Manager itself should generate an alert when an imported certificate it is using is nearing expiration for Management Servers and Gateways. If such an alert is received, please make sure to renew or create a new certificate for the servers before the expiration date. This will only work if the certificate contains template information (from an Enterprise CA).

1. Log onto the server with the expiring certificate
2. Launch the certificate configuration manager (certlm.msc)
3. Locate the expiring SCOM certificate
4. If the certificate could not be found, it may’ve either been removed or imported via file and not the certificate store. A new certificate may need to be issued for this machine from the CA. Please refer to the instructions above to do so.
5. If the certificate was found, there may be a few options to renew the cert: 
      1. Request Certificate with New Key
      1. Renew Certificate with New Key
      1. Renew Certificate with Same Key
6. Select the option that best applies to what you want to do and follow the wizard 
7. Once completed, run the MOMCertImport.exe tool to ensure SCOM has the new serial number (reversed) of the certificate if it changed, see the above section for further details.

If renewing a certificate via this method is not available, you may need to request a new certificate using the steps above, or with the organization’s certificate authority. Then install and import the new certificate for use by SCOM.

### Optional: Configure certificate auto-enrollment and renewal

If using an Enterprise CA and your organization allows it, there is a way to configure certificate auto-enrollment and automatic renewals when they expire, this will also distribute the Trusted Root certificate to all domain-joined systems. This option will not work with Stand-Alone, or third-party CAs. For systems in a Workgroup or separate domain, then certificate renewals and enrollments will still be a manual process.

For more information, please refer to the [Windows Server guide](/windows-server/networking/core-network-guide/cncg/server-certs/configure-server-certificate-autoenrollment)

>[!Note]
>Enabling this setting does not configure SCOM to use certificates, nor does it guarantee that the certificate generated will conform to SCOM’s expected certificate settings for auto-enrollment. However, renewals will use the same template used to create the initial certificate.

