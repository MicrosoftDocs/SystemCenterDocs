---
title: Set up protection with NTLM authentication
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a31fc374-1662-4984-834b-ef3c67e20666
---
# Set up protection with NTLM authentication
[!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] can protect computers in workgroups and untrusted domains. You can handle authentication using NTLM or certificates. This topic describes how to configure protection using NTLM.

1.  **[Install the agent](#BKMK_Install)**—Install the agent on the computer you want to protect.

2.  **[Configure the agent](#BKMK_Config)**—Configure the computer to recognize the DPM server for performing backups. To do this you’ll run the SetDPMServer command.

3.  **[Attach the computer](#BKMK_Attach)**—Lastly you’ll need to attach the protected computer to the DPM server.

## <a name="BKMK_Install"></a>Install the agent
On the computer you want to protect, run DPMAgentInstaller\_X64.exe from the DPM installation CD to install the agent.

## <a name="BKMK_Config"></a>Configure the agent

1.  Configure the agent by running SetDpmServer as follows:

    ```
    SetDpmServer.exe -dpmServerName <serverName> -isNonDomainServer -userName <userName> [-productionServerDnsSuffix <DnsSuffix>]
    ```

2.  Specify the parameters as follows:

    -   **\-DpmServerName**—Specify the name of the DPM server. Use either an FQDN if the server and computer are accessible to each other using FQDNs, or a NETBIOS name.

    -   **\-IsNonDomainServer**—Use to indicate that the server is in a workgroup or untrusted domain in relation to the computer you want to protect. Firewall exceptions are created for required ports.

    -   **\-UserName**—Specify the name of the account you want to use for NTLM authentication. To use this option you should have the –isNonDomainServer flag specified. A local user account will be created and the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] protection agent will be configured to use this account for authentication.

    -   **\-ProductionServerDnsSuffix**—Use this switch if the server has multiple DNS suffixes configured. This switch represents the DNS suffix that the server uses to connect to the computer you’re protecting.

3.  When the command completes successfully open the DPM console.

### Update the password
If at any point you want to update the password for the NTLM credentials, run the following on the protected computer:

```
SetDpmServer.exe -dpmServerName <serverName> -isNonDomainServer -updatePassword
```

You’ll need to use the same naming convention \(FQDN or NETBIOS\) that you did when you configured protection. On the DPM server you’ll need to run the Update –NonDomainServerInfo PowerShell cmdlet. Then you’ll need to refresh the agent information for the protected computer.

NetBIOS example: Protected computer: `SetDpmServer.exe -dpmServerName Server01 -isNonDomainServer –UpdatePassword` DPM server: `Update-NonDomainServerInfo –PSName Finance01 –dpmServerName Server01`

FQDN example: Protected computer: `SetDpmServer.exe -dpmServerName Server01.corp.contoso.com -isNonDomainServer -UpdatePassword` DPM server: `Update-NonDomainServerInfo –PSName  Finance01.worlwideimporters.com –dpmServerName Server01.contoso.com`

## <a name="BKMK_Attach"></a>Attach the computer

1.  In the DPM console, run the Protection Agent Installation wizard.

2.  In **Select agent deployment method**, select **Attach agents**.

3.  Enter the computer name, user name, and password for the computer that you want to attach to. These should be the credentials you specified when you installed the agent.

4.  Review the **Summary** page, and click **Attach**.

You can optionally run the Windows PowerShell Attach\-NonDomainServer.ps1 command instead of running the wizard. To do this take a look at the example in the next section.

## Examples
**Example 1**

Example to configure a workgroup computer after the agent is installed:

1.  On the computer, run `SetDpmServer.exe -DpmServerName Server01 -isNonDomainServer -UserName mark`.

2.  On the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, run `Attach-NonDomainServer.ps1 –DpmServername Server01 -PSName Finance01 -Username mark`.

Because the workgroup computers are typically accessible only by using NetBIOS name, the value for DPMServerName must be the NetBIOS name.

**Example 2**

Example to configure a workgroup computer with conflicting NetBIOS names after the agent is installed.

1.  On the workgroup computer, run `SetDpmServer.exe -dpmServerName Server01.corp.contoso.com -isNonDomainServer -userName mark -productionServerDnsSuffix widgets.corp.com`.

2.  On the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, run `Attach-NonDomainServer.ps1 -DPMServername Server01.corp.contoso.com -PSName Finance01.widgets.corp.com -Username mark`.

