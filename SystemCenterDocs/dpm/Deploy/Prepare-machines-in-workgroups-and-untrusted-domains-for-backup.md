---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Prepare machines in workgroups and untrusted domains for backup
ms.technology:  data-protection-manager
ms.assetid:  e63b86d4-1f83-48ef-82bb-636b9dc745e2
---

# Prepare machines in workgroups and untrusted domains for backup

>Applies To: System Center 2016 Technical Preview - Data Protection Manager

DPM can protect computers that are in untrusted domains or workgroups. You can authenticate these computers using a local user account (NTLM authentication), or using certificates. For both types of authentication you'll need to prepare the infrastructure before you can set up a protection group that contains the sources you want to back up.

1.  **Install a certificate**—If you want to use certificate authentication install a certificate on the DPM server and on the computer you want to protect.

2.  **Install the agent**—Install the agent on the computer you want to protect.

3.  **Recognize the DPM server**—Configure the computer to recognize the DPM server for performing backups. To do this you'll run the SetDPMServer command.

4.  **Attach the computer**—Lastly you'll need to attach the protected computer to the DPM server.

## Before you start
Before you started check the supported protection scenarios and required network settings

### Supported scenarios

||Support|
|-|-----------|
|Files|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />NTLM and certificate authentication for single server. Certificate authentication only for cluster.|
|System State|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />NTLM authentication only|
|SQL Server|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />Mirroring not supported.<br /><br />NTLM and certificate authentication for single server. Certificate authentication only for cluster.|
|Hyper-V server|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />NTLM and certificate authentication|
|Hyper-V cluster|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />CSV not supported.<br /><br />Certificate authentication only|
|Exchange Server|Workgroup: Not applicable<br /><br />Untrusted: Supported for single server only. Cluster not supported. CCR, SCR, DAG not supported. LCR supported.<br /><br />NTLM authentication only|
|Secondary DPM server (For backup of primary DPM server|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />Certificate authentication only|
|SharePoint|Workgroup: Not supported<br /><br />Untrusted: Not supported|
|Client computers|Workgroup: Not supported<br /><br />Untrusted: Not supported|
|Bare metal recovery (BMR)|Workgroup: Not supported<br /><br />Untrusted: Not supported|
|End-user recovery|Workgroup: Not supported<br /><br />Untrusted: Not supported|

### Network settings

|Settings|Computer in workgroup or untrusted domain|
|------------|---------------------------------------------|
|Control data|Protocol: DCOM<br /><br />Default port: 135<br /><br />Authentication: NTLM/certificate|
|File transfer|Protocol: Winsock<br /><br />Default port: 5718 and 5719<br /><br />Authentication: NTLM/certificate|
|DPM account requirements|Local account without admin rights on DPM server. Uses NTLM v2 communication|
|Certificate requirements||
|Agent installation|Agent installed on protected computer|
|Perimeter network|Perimeter network protection not supported.|
|IPSEC|Ensure IPSEC doesn't block communications.|

## Back up using  NTLM authentication
Here's what you'll need to do:

1.  Install the agent — Install the agent on the computer you want to protect.

2.  Configure the agent — Configure the computer to recognize the DPM server for performing backups. To do this you'll run the SetDPMServer command.

3.  Attach the computer — Lastly you'll need to attach the protected computer to the DPM server.

### <a name="BKMK_Config"></a>Install and configure the agent

1.  On the computer you want to protect, run DPMAgentInstaller_X64.exe from the DPM installation CD to install the agent.

2.  Configure the agent by running SetDpmServer as follows:

    ```
    SetDpmServer.exe -dpmServerName <serverName> -isNonDomainServer -userName <userName> [-productionServerDnsSuffix <DnsSuffix>]
    ```

3.  Specify the parameters as follows:

    -   **-DpmServerName**—Specify the name of the DPM server. Use either an FQDN if the server and computer are accessible to each other using FQDNs, or a NETBIOS name.

    -   **-IsNonDomainServer**—Use to indicate that the server is in a workgroup or untrusted domain in relation to the computer you want to protect. Firewall exceptions are created for required ports.

    -   **-UserName**—Specify the name of the account you want to use for NTLM authentication. To use this option you should have the -isNonDomainServer flag specified. A local user account will be created and the DPM protection agent will be configured to use this account for authentication.

    -   **-ProductionServerDnsSuffix**—Use this switch if the server has multiple DNS suffixes configured. This switch represents the DNS suffix that the server uses to connect to the computer you're protecting.

4.  When the command completes successfully open the DPM console.

#### Update the password
If at any point you want to update the password for the NTLM credentials, run the following on the protected computer:

```
SetDpmServer.exe -dpmServerName <serverName> -isNonDomainServer -updatePassword
```

You'll need to use the same naming convention (FQDN or NETBIOS) that you did when you configured protection. On the DPM server you'll need to run the Update -NonDomainServerInfo PowerShell cmdlet. Then you'll need to refresh the agent information for the protected computer.

NetBIOS example: Protected computer: `SetDpmServer.exe -dpmServerName Server01 -isNonDomainServer -UpdatePassword` DPM server: `Update-NonDomainServerInfo -PSName Finance01 -dpmServerName Server01`

FQDN example: Protected computer: `SetDpmServer.exe -dpmServerName Server01.corp.contoso.com -isNonDomainServer -UpdatePassword` DPM server: `Update-NonDomainServerInfo -PSName  Finance01.worlwideimporters.com -dpmServerName Server01.contoso.com`

### <a name="BKMK_Attach"></a>Attach the computer

1.  In the DPM console, run the Protection Agent Installation wizard.

2.  In **Select agent deployment method**, select **Attach agents**.

3.  Enter the computer name, user name, and password for the computer that you want to attach to. These should be the credentials you specified when you installed the agent.

4.  Review the **Summary** page, and click **Attach**.

You can optionally run the Windows PowerShell Attach-NonDomainServer.ps1 command instead of running the wizard. To do this take a look at the example in the next section.

### Examples
**Example 1**

Example to configure a workgroup computer after the agent is installed:

1.  On the computer, run `SetDpmServer.exe -DpmServerName Server01 -isNonDomainServer -UserName mark`.

2.  On the DPM server, run `Attach-NonDomainServer.ps1 -DpmServername Server01 -PSName Finance01 -Username mark`.

Because the workgroup computers are typically accessible only by using NetBIOS name, the value for DPMServerName must be the NetBIOS name.

**Example 2**

Example to configure a workgroup computer with conflicting NetBIOS names after the agent is installed.

1.  On the workgroup computer, run `SetDpmServer.exe -dpmServerName Server01.corp.contoso.com -isNonDomainServer -userName mark -productionServerDnsSuffix widgets.corp.com`.

2.  On the DPM server, run `Attach-NonDomainServer.ps1 -DPMServername Server01.corp.contoso.com -PSName Finance01.widgets.corp.com -Username mark`.

## Back up using certificate authentication
Here's how to set up protection with certificate authentication.

-   Each computer you want to protect should have at least .NET Framework 3.5 with SP1 installed.

-   The certificate you use for authentication must comply with the following:

    -   X.509 V3 certificate

    -   Enhanced Key Usage (EKU) should have client authentication and server authentication.

    -   Key length should be at least 1024 bits.

    -   Key type should be **exchange**.

    -   The subject name of the certificate and the root certificate should not be empty.

    -   The revocation servers of the associated Certificate Authorities are online and accessible by both the protected server and DPM server

    -   The certificate should have associated private key

    -   DPM doesn't support certificates with CNG Keys

    -   DPM doesn't support self-signed certificates.

-   Each computer you want to protect (including virtual machines) must have its own certificate.

### Set up protection

1.  [Create a DPM certificate template](#BKMK_Template)

2.  [Configure a certificate on the DPM server](#BKMK_CertDPM).

3.  [Install the agent](#BKMK_Agent)

4.  [Configure a certificate on the protected computer](#BKMK_Protected)

5.  [Attach the computer](#BKMK_AttachComputer)

### <a name="BKMK_Template"></a>Create a DPM certificate template
You can optionally set up a DPM template for web enrollment. If you do want to do this, select a template that has Client Authentication and Server Authentication as its intended purpose. For example:

1.  In the **Certificate Templates** MMC snap-in you could select the **RAS and IAS Server** template. Right-click it and select **Duplicate Template**.

2.  In **Duplicate Template**, leave the default setting **Windows Server 2003 Enterprise**.

3.  In the **General** tab, change the template display name to something recognizable. For example **DPM Authentication**. Make sure the setting **Publish certificate in Active Directory** is enabled.

4.  In the **Request Handling** tab, make sure **Allow private key to be exported** is enabled.

5.  After you've created the template make it available for use. Open the Certificate Authority snap-in. Right-click **Certificate Templates**, select **New**, and choose **Certificate Template to Issue**. In **Enable Certificate Template** select the template and click OK. Now the template will be available when you obtain a certificate.

#### Enable enrollment or autoenrollment
If you want to optionally configure the template for enrollment or autoenrollment, click the Subject Name tab in the template properties. When you configure enrollment the template can be selected in the MMC. If you configure autoenrollment the certificate is automatically assigned to all computers in the domain.

-   For enrollment, in the **Subject Name** tab of the template properties, enable **Select Build from this Active Directory information**. In **Subject name format** select **Common Name** and enable **DNS name**. Then go to the Security tab and assign the **Enroll** permission to authenticated users.

-   For autoenrollment, go to the **Security** tab and assign the **Autoenroll** permission to authenticated users. With this setting enabled the certificate will be automatically assigned to all computers in the domain.

-   If you've configured enrollment you'll be able to request a new certificate in the MMC, based on the template. To do this, on the protected computer, in **Certificates (Local Computer)** > **Personal**, right-click **Certificates**. Select **All Tasks** > **Request New Certificate**. In the **Select Certificate Enrollment Policy** page of the wizard select **Active Directory Enrollment Policy**. In **Request Certificates** you'll see the template. Expand **Details** and click **Properties**. Select the **General** tab and provide a friendly name. After you apply the settings you should receive a message that the certificate was installed successfully.

### <a name="BKMK_CertDPM"></a>Configure a certificate on the DPM server

1.  Generate a certificate from a CA for the DPM server, via web enrollment or some other method. In web enrollment, select **advanced certificate required**, and **Create and Submit a request to this CA**. Make sure the key size is 1024 or higher, and that **Mark key as exportable** is selected.

2.  The certificate is placed in the User store. We need to move it to the Local Computer store.

3.  To do this export the certificate from the User store. Make sure you export it with the private key. You can export it in the default .pfx format. Specify a password for the export.

4.  In Local Computer\Personal\Certificate run the Certificate Import Wizard to imported the exported file from its saved location. Specify the password you used to export it and make sure **Mark this key as exportable** is selected. On the Certificate Store page leave the default setting **Place all certificates in the following store**, and ensure **Personal** is displayed.

5.  After the import set the DPM credentials to use the certificate, as follows:

    1.  Obtain the thumbprint for the certificate. In the **Certificates** store double-click on the certificate. Select the **Details** tab and scroll down to the thumbprint. Click it, highlight and copy it. Paste the thumbprint into Notepad and remove any spaces.

    2.  Run **Set-DPMCredentials** to configure the DPM server:

        ```
        Set-DPMCredentials [-DPMServerName <String>] [-Type <AuthenticationType>] [Action <Action>] [-OutputFilePath <String>] [-Thumbprint <String>] [-AuthCAThumbprint <String>]
        ```

    -   **-Type**—Indicates the type of authentication. Value: **certificate**.

    -   **-Action**—Specify whether you want to perform the command for the first time, or regenerate the credentials. Possible values: **regenerate** or **configure**.

    -   -**OutputFilePath**— Location of the output file used in Set-DPMServer on the protected computer.

    -   **-Thumbprint**—Copy from the Notepad file.

    -   **-AuthCAThumbprint**—Thumbprint of the CA in the trust chain of the certificate. Optional. If not specified, Root will be used.

6.  This generates a metadata file (.bin) that is required at the time of each agent install in untrusted domain. Make sure that the C:\Temp folder exists before  you run the command. Note that if the file is lost or deleted you can recreate it by running the script with the **-action regenerate** option.

7.  Retrieve the .bin file and copy it to the C:\Program Files\Microsoft Data Protection Manager\DPM\bin folder on the computer you want to protect. You don't have to do this, but if you don't you'll need to specify the full path of the file for the -DPMcredential parameter when you …

8.  Repeat these steps on every DPM server that will protect a computer in a workgroup or in an untrusted domain.

### <a name="BKMK_Agent"></a>Install the agent

1.  On each computer you want to protect, run DPMAgentInstaller_X64.exe from the DPM installation CD to install the agent.

### <a name="BKMK_Protected"></a>Configure a certificate on the protected computer

1.  Generate a certificate from a CA for the protected computer, via web enrollment or some other method. In web enrollment, select **advanced certificate required**, and **Create and Submit a request to this CA**. Make sure the key size is 1024 or higher, and that **Mark key as exportable** is selected.

2.  The certificate is placed in the User store. We need to move it to the Local Computer store.

3.  To do this export the certificate from the User store. Make sure you export it with the private key. You can export it in the default .pfx format. Specify a password for the export.

4.  In Local Computer\Personal\Certificate run the Certificate Import Wizard to imported the exported file from its saved location. Specify the password you used to export it and make sure **Mark this key as exportable** is selected. On the Certificate Store page leave the default setting **Place all certificates in the following store**, and ensure **Personal** is displayed.

5.  After the import configure the computer to recognize the DPM server as authorized to perform backups, as follows

    1.  Obtain the thumbprint for the certificate. In the **Certificates** store double-click on the certificate. Select the **Details** tab and scroll down to the thumbprint. Click it, highlight and copy it. Paste the thumbprint into Notepad and remove any spaces.

    2.  Navigate to the C:\Program files\Microsoft Data Protection anager\DPM\bin folder. And run **setdpmserver** as follows:

        ```
        setdpmserver -dpmCredential CertificateConfiguration_DPM01.contoso.com.bin -OutputFilePath c:\Temp -Thumbprint <ClientThumbprintWithNoSpaces
        ```

        Where ClientThumbprintWithNoSpaces is copied from the Notepad file.

    3.  You should get output to confirm that the configuration was completed successfully.

6.  Retrieve the .bin file and copy it to the DPM server. We suggest you copy it to the default location in which the Attach process will check for the file (Windows\System32) so you can just specify the filename instead of the full path when you run the Attach command.

### <a name="BKMK_AttachComputer"></a>Attach the computer
You attach the computer to the DPM server using the Attach-ProductionServerWithCertificate.ps1 PowerShell script, using the syntax.

```
Attach-ProductionServerWithCertificate.ps1 [-DPMServerName <String>] [-PSCredential <String>] [<CommonParameters>]
```

-   -DPMServerName—Name of the DPM server

-   PSCredential—Name of the .bin file. If you placed it in the Windows\System32 folder you can specify the file name only. Be careful to specify the .bin file created o nthe protected server. If you specify the .bin file created on the DPM server you'll remove all the protected computers that are configured for certificate-based authentication.

After the attach process completes the protected computer should appear in the DPM console.

### Examples
**Example 1**

Generates a file in `c:\\CertMetaData\\` with name `CertificateConfiguration\_<DPM SERVER FQDN>.bin`

```
Set-DPMCredentials -DPMServerName dpmserver.contoso.com -Type Certificate -Action Configure -OutputFilePath c:\CertMetaData\ -Thumbprint "cf822d9ba1c801ef40d4b31de0cfcb200a8a2496"
```

Where dpmserver.contoso.com is the name of the DPM server and "cf822d9ba1c801ef40d4b31de0cfcb200a8a2496" is the thumbprint of the DPM server certificate.

**Example 2**

Regenerates a lost configuration file in the folder c:\CertMetaData\

```
Set-DPMCredentials -DPMServerName dpmserver.contoso.com -Type Certificate "-OutputFilePath c:\CertMetaData\ -Action Regenerate
```



