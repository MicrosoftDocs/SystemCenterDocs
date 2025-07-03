---
ms.assetid: cf56de7b-757b-4639-89b7-d819130d02fb
title: Configure Authentication with the Web console
description: This article describes how to configure Secure Sockets Layer (SSL) encryption for the web server running the Operations Manager Web Console.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy23, UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Configure authentication with the Web console



## Configure SSL encryption

The following steps are necessary to configure Secure Sockets Layer (SSL) encryption after the Operations Manager Web console server has been installed on an Internet Information Services (IIS) 7.0 and higher web server.  Before performing these steps, you should first review  [Configuring Secure Sockets Layer in IIS 7](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis) and configure IIS to enable SSL for the web server hosting the Web console.  

>[!NOTE]
>When creating the certificate, you must provide the fully qualified domain name (FQDN) of the host and domain name in the **Common name** field to match the address users would enter in their web browser to access the Web console.  

>[!IMPORTANT]
>If you are experiencing issues with authentication prompts when attempting to access the Web console, check that the fully qualified domain name (FQDN) URL is included in **Control Panel** -> **Internet Options** -> **Security Tab** -> **Local Intranet Sites** -> **Sites** -> **Advanced**.

1. Ensure that the SSL certificates are installed and configured on the management server.

2. Add an https binding in the IIS website wherever the Operations Manager Web console is installed.

3. After completing the above steps, reset the Web site hosting the Operations Manager Web console.

>[!NOTE]
> Enable SSL check box in the installer only works if you're using an https binding for the web console. For more information, see [How to set up SSL on IIS 7](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

::: moniker range="<sc-om-2019"

1. Use a plain text editor to open the **web.config** in `<PATH>:\Program Files\Microsoft System Center 2016\Operations Manager\WebConsole\WebHost`.
2. In the `<services>` root element, modify the following in the `<!– Logon Service –>`element:

     ```
     <endpoint address=”” binding=”customBinding” contract=”Microsoft.EnterpriseManagement.Presentation.Security.Services.ILogonService” bindingConfiguration=”DefaultHttpsBinding”/>
     ```

3. In the `<services>` root element, modify the following in the `<!– Data Access service –>` element:

     ```
      <endpoint address=”” binding=”customBinding” contract=”Microsoft.EnterpriseManagement.Presentation.DataAccess.Server.IDataAccessService” bindingConfiguration=”DefaultHttpsBinding”/>
      ```

4. Save and close the file when finished.
5. Select **Start**, select **Run**, type **regedit**, and select **OK**.

6. Under **HKEY_LOCAL_MACHINE\Software\Microsoft\System Center Operations Manager\12\Setup\WebConsole\\**, double-click the value **HTTP_GET_ENABLED** and change its value to **false**. Double-click the value **BINDING_CONFIGURATION** and change its value to **DefaultHttpsBinding**.

7. After completing the above steps, reset the Web site hosting the Operations Manager Web console.  

::: moniker-end

## Configure FIPS compliance

Follow these steps for the Operations Manager Web console server component to use algorithms that are compliant with Federal Information Processing Standards (FIPS). Enabling FIPS compliance for System Center - Operations Manager requires that the underlying infrastructure used (Server OS, Active Directory, etc.), also be FIPS compliant.

### Install the cryptography DLL

1. On the system hosting the Web console, use the Run as Administrator option to open a Command Prompt window.
2. Change directories to the SupportTools directory of your installation media, and then change directory to **AMD64**.  
3. Run the following **gacutil** command: `gacutil.exe –i Microsoft.EnterpriseManagement.Cryptography.dll`.

### Edit the machine.config files

1. Use a plain text editor to open the **machine.config** file in *%WinDir%\Microsoft.NET\Framework\v2.0.50727\CONFIG\\*.
2. If the following content doesn't exist within the `<Configuration>` root element, add as follows:

    ```
     <mscorlib>
      <cryptographySettings>
        <cryptoNameMapping>
            <cryptoClasses>
                <cryptoClass
    SHA256CSP="System.Security.Cryptography.SHA256CryptoServiceProvider, System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
                <cryptoClass HMACSHA256CSP
    ="Microsoft.EnterpriseManagement.Cryptography.HMACSHA256, Microsoft.EnterpriseManagement.Cryptography, Version=7.0.5000.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </cryptoClasses>
            <nameEntry name="SHA256" class="SHA256CSP"/>
            <nameEntry name="HMACSHA256" class="HMACSHA256CSP"/>  
        </cryptoNameMapping>
      </cryptographySettings>
     </mscorlib>
    ```
3. Save and close the file when finished.

Repeat the preceding step on the following files:

- %WinDir%\Microsoft.NET\Framework\v4.0.30319\Config\machine.config
- %WinDir%\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config

::: moniker range="<sc-om-2019"

### Edit the web.config file in WebHost folder

1. Use a plain text editor to open the web.config file in `<Path>:\Program Files\System Center 2016\Operations Manager\WebConsole\WebHost\web.config`.
2. In the \<encryption\> element, add the following element if it doesn't exist: `<symmetricAlgorithm  iv="SHA256"/>`
3. In the `<connection autoSignIn="true" autoSignOutInterval="30">` element, in the `<session>` tag, add the following attribute if it doesn't exist: **tokenAlgorithm="SHA256"**

     ```
     <connection autoSignIn="True" autoSignOutInterval="30">  
     <session encryptionKey="SessionEncryptionKey" tokenAlgorithm="SHA256">  
     ```

4. Modify the following element by changing its value from true to false: `<serviceMetadata httpGetEnabled="false"/>`
5. Modify the following two elements by changing their values from **DefaultHttpBinding** to **DefaultHttpsBinding**:

     ```
     <endpoint address="" binding="customBinding" contract="Microsoft.EnterpriseManagement.Presentation.Security.Services.ILogonService" bindingConfiguration="DefaultHttpsBinding"/>
     <endpoint address="" binding="customBinding" contract="Microsoft.EnterpriseManagement.Presentation.DataAccess.Server.IDataAccessService" bindingConfiguration="DefaultHttpsBinding"/>
     ```

6. Save and close the file.

### Edit the web.config file in MonitoringView folder

1. Use a plain text editor to open the web.config file in `<PATH>:\Program Files\System Center 2012\Operations Manager\WebConsole\MonitoringView\web.config`.
2. In the `<encryption>` element, add the following element if it doesn't exist: `<symmetricAlgorithm  iv="SHA256"/>`.
3. In the `<connection>` element, In the `<connection autoSignIn="true" autoSignOutInterval="30">` element, in the `<session>` tag, add the following attribute if it doesn't exist: **tokenAlgorithm="SHA256"**

     ```
     <connection autoSignIn="True" autoSignOutInterval="30">
     <session encryptionKey="SessionEncryptionKey" tokenAlgorithm="SHA256">
     ```

4. In the `<system.web>` element, add the following element if it doesn't exist:

     ```
     <machineKey validationKey="AutoGenerate,IsolateApps" decryptionKey="AutoGenerate,IsolateApps" validation="3DES" decryption="3DES"/>
     ```

5. Save and close the file.

::: moniker-end

::: moniker range=">=sc-om-2019"

## Configure sign in session

>[!NOTE]
>The web console uses windows authentication by default, if available to sign into the website. The default session timeout interval for web console is 1 day and this is the maximum value.

1. To edit the value, use a plain text editor to open the web.config in `<PATH>:\Program Files\Microsoft System Center\Operations Manager\WebConsole\Dashboard`.
2. In the `<appSettings>` root element, modify the following session timeout value in minutes.
    ```
	  <add key="SessionTimeout" value="1440"/>
    ```
3. After completing the above steps, reset the Web site hosting the Operations Manager Web console.

::: moniker-end

## Next steps

- To configure FIPS compliance for the Reporting server, see [Configure Authentication for Reporting server](manage-config-authentication-reporting-server.md)
