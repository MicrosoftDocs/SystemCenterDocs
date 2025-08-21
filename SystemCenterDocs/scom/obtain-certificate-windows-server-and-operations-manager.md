---
ms.assetid: 
title: Obtain a certificate for use with Windows Servers and System Center Operations Manager
description: This article explains how to obtain a certificate for use with Windows Servers and System Center Operations Manager.
ms.custom: engagement-fy23, UpdateFrequency2
author: jyothisuri
ms.author: jsuri
ms.date: 01/04/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
---

# Obtain a certificate for use with Windows Servers and System Center Operations Manager

When System Center Operations Manager operates across trust boundaries where Kerberos authentication with Gateway or Windows client machines isn't possible, certificate-based authentication is required. This method is used to establish communication between the Microsoft Monitoring Agent and the Management Servers. The primary use case is to authenticate with Gateway and Windows Client systems in Workgroups, Demilitarized Zones (DMZs), or other domains without a two-way trust.

Certificates generated using this article are **not** for Linux monitoring unless a Gateway server performing the monitoring is across a trust boundary, and then the certificate is only used for Windows-to-Windows authentication for the Gateway and Management Server, separate certificates (SCX-Certificates) are used for Linux authentication and are handled by Operations Manager itself.

This article describes how to obtain a certificate and use with Operations Manager Management Server, Gateway, or Agent using an [Enterprise Active Directory Certificate Services](/windows-server/identity/ad-cs/active-directory-certificate-services-overview) (AD CS) Certificate Authority (CA) server on the Windows platform. If you're using a Stand-Alone or non-Microsoft CA, Consult with your Certificate/PKI team for assistance in creating certificates used for Operations Manager.

## Prerequisites

Ensure you have the following requirements in place:

- Active Directory Certificate Services (AD CS) installed and configured, or a non-Microsoft Certificate Authority (CA). (Note: This guide doesn't cover requesting certificates from a non-Microsoft CA.)
- Domain Administrator privileges.
- Operations Manager Management Servers joined to the domain.

## Certificate Requirements

> [!IMPORTANT]
> Cryptography API Key Storage Provider ([KSP](/windows/win32/secgloss/k-gly?redirectedfrom=MSDN#_security_key_storage_provider_gly)) isn't supported for Operations Manager certificates.

At this time, Operations Manager doesn't support more advanced certificates and relies on legacy providers.

If your organization doesn't use AD CS or uses an external certificate authority, use the instructions provided for that authority to create your certificate, ensuring it meets the following requirements for Operations Manager:

```text
- Subject="CN=server.contoso.com" ; (this should be the FQDN of the target, or how the system shows in DNS)

- [Key Usage]
    Key Exportable = FALE  ; Private key is NOT exportable, unless creating on a domain machine for a non-domain machine, then use TRUE
    HashAlgorithm = SHA256
    KeyLength = 2048  ; (2048 or 4096 as per Organization security requirement.)
    KeySpec = 1  ; AT_KEYEXCHANGE
    KeyUsage = 0xf0  ; Digital Signature, Key Encipherment
    MachineKeySet = TRUE ; The key belongs to the local computer account
    ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
    ProviderType = 12
    KeyAlgorithm = RSA

- [EnhancedKeyUsageExtension]
     - OID=1.3.6.1.5.5.7.3.1 ; Server Authentication
     - OID=1.3.6.1.5.5.7.3.2 ; Client Authentication

- [Compatibility Settings]
     - Compatible with Windows Server 2012 R2 ; (or newer based on environment)

- [Cryptography Settings]
     - Provider Category: Legacy Cryptography Service Provider
     - Algorithm name: RSA
     - Minimum Key Size: 2048 ; (2048 or 4096 as per security requirement.)
     - Providers: "Microsoft RSA Schannel Cryptographic Provider"
```

## High-level process to obtain a certificate

> [!IMPORTANT]
> For this article, the default settings for AD-CS are:
>
> - Standard key length: 2048
> - Cryptography API: Cryptographic Service Provider ([CSP](/windows/win32/secgloss/c-gly?redirectedfrom=MSDN#_security_cryptographic_service_provider_gly))
> - Secure Hash Algorithm: 256 (SHA256)
>
> Evaluate these selections against the requirements of your company's security policy.

# [Enterprise CA](#tab/Enterp)

1. Download the Root Certificate from a CA.
1. Import the Root Certificate to a client server.
1. Create a certificate template.
1. Submit a request to the CA.
1. Approve the request if necessary.
1. Retrieve the certificate.
1. Import the certificate into the certificate store.
1. Import the certificate into Operations Manager using `<MOMCertImport>`.

# [Stand-Alone or non-Microsoft CAs](#tab/Standal)

1. Download the Root Certificate from a CA.
1. Import the Root Certificate to a client-server.
1. Request a certificate from the CA matching the requirements for Operations Manager.
1. Approve the request if necessary.
1. Retrieve the certificate from the CA.
1. Import the certificate into the certificate store.
1. Import the certificate into Operations Manager using `<MOMCertImport>`.

---

## Download and Import the Root Certificate from the CA

> [!TIP]
> If you're using an Enterprise CA and are on a domain-joined system, the root certificates should already be installed in the appropriate stores, and you can skip this step.
>
> To verify the certificates are installed, run the following PowerShell command on the domain-joined system, replacing "Domain" with your partial domain name:
>
> ```powershell
> # Check for Root Certificates
> Get-ChildItem Cert:\LocalMachine\Root\ | Where-Object { $_.Subject -match "Domain" }
>
> # Check for CA Certificates
> Get-ChildItem Cert:\LocalMachine\CA\ | Where-Object { $_.Subject -match "Domain" }
> ```

To trust and validate any certificates created from and Certificate Authorities, the target machine needs to have a copy of the Root Certificate in its Trusted Root Store. Most domain-joined computers already trust the Enterprise CA. However, no machine trusts a certificate from a non-Enterprise CA without the Root Certificate installed for that CA.

If you're using a non-Microsoft CA, the download process is different. However, the import process remains the same.

### To automatically install the Root and CA certificates using Group Policy

1. Sign into the computer where you want to install the certificates as an Administrator.
1. Open an Administrator Command Prompt or PowerShell console.
1. Execute the command `gpupdate /force`
1. Once completed, check for the presence of Root and CA certificates in the certificate store, which should be visible in the Local Machine Certificate Manager under **Trusted Root Certification Authorities** > **Certificates**.

### Manually download the Trusted Root certificate from a CA

To download the Trusted Root certificate, follow these steps:

1. Sign in to the computer where you want to install a certificate.
For example, *a Gateway Server or Management Server*.
2. Open a web browser and connect to the certificate server web address.
For example, `https://<servername>/certsrv`.
3. On the **Welcome** page, select **Download a CA Certificate**, **Certificate chain**, or **CRL**.
   1. If prompted with a **Web Access Confirmation**, verify  the  server and URL, and select **Yes**.
   1. Verify the multiple options under **CA Certificate** and confirm the selection.
4. Change the Encoding method to **Base 64** and then select **Download CA Certificate Chain**.
5. Save the certificate and provide a friendly name.

### Import the Trusted Root Certificate from the CA on the client

> [!NOTE]
> To import a Trusted Root Certificate, you must have administrative privileges on the target machine.

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
6. If successful, the Trusted Root Certificate from the CA is visible under **Trusted Root Certification Authorities** > **Certificates**.

## Create a certificate template for an Enterprise CA

> [!IMPORTANT]
> If you're utilizing Stand-Alone or non-Microsoft CAs, consult with your certificate or PKI team on how to proceed with generating your certificate request.

For more information, see [certificate templates](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831574(v=ws.11)).

### Create a certificate template for System Center Operations Manager

1. Sign in to a domain joined server with AD CS in your environment (your CA).
1. On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
1. On the right navigation pane, expand the CA, right-click **Certificate Templates**, and select **Manage**.
1. Right-click **Computer** and select **Duplicate Template**.
1. The **Properties of New Template** dialog opens; make the selections as indicated:

   |Tab|Description|
   |----|---------------|  
   |Compatibility| 1. **Certification Authority**: Windows Server 2012 R2 (or the lowest AD functional level in the environment).</br> 2. **Certificate Recipient**: Windows Server 2012 R2 (or the lowest version OS in the environment).|
   |General| 1. **Template display name**: Enter a friendly name, such as *Operations Manager*.</br> 2. **Template name**: Enter the same name as display name.</br> 3. **Validity period and Renewal Period**: Enter the validity and renewal periods that align with your organization's certificate policy. The recommendation for validity is to not exceed one-half the life of the CA issuing the certificate. (For example: Four year sub CA, max two year lifetime for the cert.).</br> 4. Select **Publish certificate in Active Directory** and **Do not automatically reenroll if a duplicate certificate exists in Active Directory** checkboxes.|
   |Request Handling| 1. **Purpose**: Select **Signature and encryption** from the dropdown.</br> 2. Select **Allow private key to be exported** checkbox.|
   |Cryptography| 1. **Provider Category**: Select Legacy Cryptography Service Provider</br> 2. **Algorithm name**: Select Determined by CSP from the dropdown.</br> 3. **Minimum Key size**: 2048 or 4096 as per organization security requirement.</br> 4. **Providers**: Select **Microsoft RSA channel Cryptographic Provider** and **Microsoft Enhanced Cryptographic Provider v1.0**.|
   |Security| 1. Remove the user account of the user creating the template, groups should be in place instead.</br>2. Ensure that the **Authenticated Users** group (or Computer object) has **Read** and **Enroll** permissions.</br> 2. Uncheck the **Enroll** permission for **Domain Admins**, and **Enterprise Admins**.</br>3. Add permissions for the Security Group that contains your Operations Manager Servers, and grant this group **Enroll** permission. |
   |Issuance Requirements| 1. Check the box for **CA Certificate manager approval**</br>2. Under "Require the following for reenrollment", select **Valid existing certificate**</br>3. Check the box for **Allow key based renewal** |
   |Subject Name| 1. Select **Supply in the request**</br>2. Check the box for **Use subject information from existing certificates...** |

1. Select **Apply** and **OK** to create the new template.

### Publish the template on all relevant Certification Authorities

1. Sign in to a domain joined server with AD CS in your environment (your CA).
1. On the Windows desktop, select **Start** > **Windows Administrative Tools** > **Certification Authority**.
1. On the right navigation pane, expand the CA, right-click **Certificate Templates**, and select **New** > **Certificate Templates to Issue**.
1. Select the new template created in the above steps and select **OK**.

## Request a certificate using a request file

> [!NOTE]
> Creating certificate requests using an INF file is a legacy method and isn't recommended.

### Create an information (.inf) file

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open a new text file in a text editor.
1. Create a text file containing the following content:

    ```text
    [NewRequest]
    Subject="CN=server.contoso.com"
    Key Exportable = TRUE  ; Private key is exportable, leave if exporting for another machine, otherwise change to FALSE
    HashAlgorithm = SHA256
    KeyLength = 2048  ; (2048 or 4096 as per Organization security requirement.)
    KeySpec = 1  ; AT_KEYEXCHANGE
    KeyUsage = 0xf0  ; Digital Signature, Key Encipherment
    MachineKeySet = TRUE ; The key belongs to the local computer account
    ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
    ProviderType = 12
    KeyAlgorithm = RSA
    
    ; Utilizes the certificate created earlier, ensure to set the name of the template to what yours is named
    [RequestAttributes]
    CertificateTemplate="OperationsManager"
    
    ; Not required if using a template with this defined
    [EnhancedKeyUsageExtension]
    OID = 1.3.6.1.5.5.7.3.1  ; Server Authentication
    OID = 1.3.6.1.5.5.7.3.2  ; Client Authentication
    ```

1. Save the file with an `.inf` file extension. For example, `CertRequestConfig.inf`.
1. Close the text editor.

### Create a certificate request file

This process encodes the information specified in our config file in Base64 and outputs to a new file.

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open an Administrator command prompt.
1. Navigate to the same directory where the `.inf` file is located.
1. Run the following command to modify the `.inf` file name to ensure it matches the file name created earlier. Leave the `.req` file name as-is:

    ```cmd
    CertReq –New –f CertRequestConfig.inf CertRequest.req
    ```

1. Validate the new `.req` file by running the following command and checking the results:

    ```cmd
    CertUtil CertRequest.req
    ```

### Submit a new certificate request

1. On the computer hosting the Operations Manager feature for which you're requesting a certificate, open an Administrator command prompt.
1. Navigate to the same directory where the `.req` file is located.
1. Run the following command to submit a request to your CA:

    ```cmd
    CertReq -Submit CertRequest.req
    ```

1. You can be presented with options to select your CA, if so, select an appropriate CA and continue.
1. Once completed, the results may say the "Certificate request is pending," necessitating your certificate approver to approve the request before continuing.
    1. Otherwise, the certificate is imported to the certificate store.

## Request a certificate using Certificate Manager

For Enterprise CAs with a defined certificate template, you can request a new certificate from a domain-joined client machine using the Certificate Manager. This method is specific to Enterprise CAs and doesn't apply to Stand-Alone CAs.

1. Sign in to the target machine with administrator rights (Management Server, Gateway, Agent, and so on).
1. Use Administrator Command Prompt or PowerShell window to open Certificate Manager.
    1. *certlm.msc* - opens the Local Machine certificate store.
    1. *mmc.msc* - opens the Microsoft Management Console.
        1. Load the Certificate Manager snap-in.
        1. Go to **File** > **Add/Remove Snap-In**.
        1. Select **Certificates**.
        1. Select **Add**.
        1. When prompted, select *Computer Account* and select **Next**
        1. Ensure to select *Local Computer* and select **Finish**.
        1. Select **OK** to close the wizard.
1. Start the certificate request:
    1. Under Certificates, expand the Personal folder.
    1. Right-click  **Certificates** > **All Tasks** > **Request New Certificate**.
1. In the **Certificate Enrollment** wizard
    1. On the **Before You Begin** page, select **Next**.
    2. Select the applicable Certificate Enrollment Policy (default may be the **Active Directory Enrollment Policy**), select **Next**
    3. Select your desired Enrollment Policy template.
    4. If the template isn't immediately available, select **Show all templates** box below the list
    5. If the template needed is available with a red X beside it, consult your Active Directory or Certificate team
    6. As information in the certificate needs to be manually entered, you'll find a warning message under the selected template as a hyperlink that says `⚠️ More Information is required to enroll for this certificate. Click here to configure settings.` 
        1. Select the hyperlink, and continue to fill the information for the certificate in the popup window.
1. In the **Certificate Properties** wizard:

    |Tab|Description|
    |----|---------------|
    |Subject| 1. In Subject Name, select the **Common Name** or **Full DN**, provide the value - hostname or BIOS name of the target server, Select **Add**.</br> 2. Add Alternative Names as desired. If using alternative names in place of a Subject, the *first* name must match the hostname or BIOS name.|
    |General| 1. Provide a Friendly Name to the generated certificate.</br> 2. Provide a description of the purpose of this certificate if desired.|
    |Extensions| 1. Under Key usage, ensure to select **Digital Signature** and **Key encipherment** option, and select the **Make these key usages critical** checkbox.</br> 2. Under Extended Key Usage, ensure to select **Server Authentication** and **Client Authentication** options.|
    |Private Key| 1. Under Key options, ensure that the Key Size is at least 1024 or 2048, and select the **Make private key exportable** checkbox.</br> 2. Under Key type, ensure to select the **Exchange** option.|
    |Certification Authority tab| Ensure to select the CA checkbox.|
    |Signature| If your organization requires a registration authority, provide a signing certificate for this request. |

    1. Once the information is provided in the Certificate Properties wizard, the warning hyperlink from earlier disappears.
    1. Select **Enroll to create the certificate**. If there's an error, consult your AD or certificate team.
        1. If successful, the status reads **Succeeded** and a new certificate is in the Personal/Certificates store.
1. If these actions were taken on the intended recipient of the certificate, proceed to the next steps.
1. If the certificate request needs to approval by a Certificate Manager, continue once the request is validated and approved.
   1. Once approved, if Auto Enrollment is configured, then the certificate will appear on the system after a Group Policy update (`gpupdate /force`).
   1. If it doesn't appear in the Personal store for Local Machine, look in **Certificates - Local Computer** > **Certificate Enrollment Requests** > **Certificates**
       1. If the requested certificate is present here, copy it to the Personal certificate store.
       1. If the requested certificate isn't here, consult with your certificate team.
1. Otherwise, export the new certificate from the machine and copy to the next.
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
2. Copy the certificate created earlier to an accessible location on this machine.
3. Open an Administrator Command Prompt or PowerShell window and navigate to the folder where the certificate file is located.
4. Run the following command, replacing **NewCertificate.cer** with the correct name/path of the file:

      `CertReq -Accept -Machine NewCertificate.cer`

5. This certificate should now be present in the Local Machine Personal store on this computer.

Alternatively, right-click the certificate file > Install > Local machine and choose the destination of the personal store to install the certificate.

> [!TIP]
> If you add a certificate to the certificate store with the private key and later delete it, the certificate loses the private key when reimported. Operations Manager requires the private key for encrypting outgoing data. To restore the private key, use the [certutil](/windows-server/administration/windows-commands/certutil#-repairstore) command with the certificate's serial number. Run the following command in an Administrator Command Prompt or PowerShell window:
>
> ```cmd
> certutil -repairstore my <certificateSerialNumber>
> ```

## Import the certificate into Operations Manager  

In addition to the installation of the certificate on the system, you must update Operations Manager to be aware of the certificate that you want to use. These actions result in a restart of the Microsoft Monitoring Agent service for changes to apply.

We require the **MOMCertImport.exe** utility, which is included in the *SupportTools* folder of the Operations Manager installation media. Copy the file to your server.

To import the certificate into Operations Manager using MOMCertImport, follow these steps:

1. Sign in to the target computer.
1. Open an Administrator Command Prompt or PowerShell window and navigate to the *MOMCertImport.exe* utility folder.
1. Run the *MomCertImport.exe* utility by executing the following command:
      1. In CMD: `MOMCertImport.exe`
      1. In PowerShell: `.\MOMCertImport.exe`
1. A GUI Window appears, prompting to **Select a Certificate**.
      1. You can see a list of certificates, if you don't immediately see your desired certificate listed, select **More choices**.
1. From the list, select the new certificate for the machine.
      1. You can verify the certificate by selecting it. Once selected, you can view the certificate properties.
1. Select **OK**
1. If successful, a pop-up window displays the following message:

      `Successfully installed the certificate. Please check Operations Manager log in eventviewer to check channel connectivity.`

1. To validate, go to **Event Viewer** > **Applications and Services Logs** > **Operations Manager** and look for an Event ID **20053**. This event indicates that the authentication certificate was loaded successfully
1. If Event ID **20053** isn't present on the system, look for one of the following Event IDs as they define any problems with the imported certificate, correct accordingly:
    - **20049**
    - **20050**
    - **20052**
    - **20066**
    - **20069**
    - **20077**

    If none of these event IDs are present in the log, then the certificate import failed, check your certificate and administrative permissions and try again.

1. *MOMCertImport* updates the following registry location to contain a value that matches the serial number of the certificate imported, mirrored:

    ```Registry
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\MachineSettings\ChannelCertificateSerialNumber
    ```

## Renew a Certificate

Operations Manager generates an alert when an imported certificate for Management Servers and Gateways is nearing expiration. If you receive such an alert, renew or create a new certificate for the servers before the expiration date. This alert functionality only works if the certificate contains template information from an Enterprise CA.

1. Sign in to the server with the expiring certificate and launch the certificate configuration manager (*certlm.msc*).
2. Locate the expiring Operations Manager certificate.
3. If you don't find the certificate, it may have been removed or imported via file and not the certificate store. You need to issue a new certificate for this machine from the CA. Refer to earlier instructions on how to do so.
4. If you find the certificate, the following are the options to select to renew the cert:
      1. Request Certificate with New Key
      1. Renew Certificate with New Key
      1. Renew Certificate with Same Key
5. Select the option that best applies to what you want to do and follow the wizard.
6. Once completed, run the `MOMCertImport.exe` tool to ensure Operations Manager has the new serial number of the certificate. For more information, see the [Import the certificate into Operations Manager](#import-the-certificate-into-operations-manager) section.

If certificate renewal via this method isn't available, use the prior steps to request a new certificate or with the organization’s certificate authority. Install and import (MOMCertImport) the new certificate for use by Operations Manager.

### Optional: Configure certificate auto-enrollment and renewal

Use the Enterprise CA to configure certificate auto-enrollment and renewals when they expire. Doing so distributes the Trusted Root certificate to all domain-joined systems.

Configuration of certificate auto-enrollment and renewal doesn't work with Stand-Alone or non-Microsoft CAs. For systems in a Workgroup or separate domain, certificate renewals and enrollments will be a manual process.

For more information, see the [Windows Server Guide](/windows-server/networking/core-network-guide/cncg/server-certs/configure-server-certificate-autoenrollment).

> [!NOTE]
> Auto-enrollment and renewals don't automatically configure Operations Manager to use the new certificate. If the certificate auto renews with the same key, the thumbprint may also stay the same and no action is required by an Administrator. If a new certificate is generated or the thumbprint changes, the updated certificate needs to be re-imported. For more information, see the [Import the certificate into Operations Manager](#import-the-certificate-into-operations-manager) section.
