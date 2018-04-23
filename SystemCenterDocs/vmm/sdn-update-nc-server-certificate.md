---
ms.assetid: f6500be6-7c8a-46ff-a3d4-b9fada8c5d8d
title: Update the network controller server certificate
description: This article describes the procedure on how to update the network controller's server certificate.
author:  JYOTHIRMAISURI
ms.author: V-jysur
manager:  vvithal
ms.date:  04/23/2018
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Update the network controller server certificate
  Network controller (NC) uses a certificate for Northbound communication with REST clients (such as VMM) and Southbound communication with Hyper-V hosts and software load balancers.

  You can change or update this certificate in the following scenarios, after you deploy the NC.

  1.	The certificate has expired
  2.	You want to move from a self-signed certificate to a certificate that is issued by a certificate authority (CA).

  > [!NOTE]

  > If you renew the existing certificate with the same key, these steps are not required.

## Before you start

 Make sure you create a new SSL certificate with existing network controller's REST name. [Learn more](sdn-controller.md#set-up-the-security-certificates).

## Update the server certificate

1.	Export the certificate with private key and import it on the all NC nodes **My** and **Root** store if it is a self-signed certificate.

  For a CA issued certificate, import it in all network controller nodes' **My** store.

  > [!NOTE]

  > DO NOT remove the current certificate from the NC nodes. You should validate the updated certificate before you remove the existing one. Proceed with rest of the steps to update the certificate.

2.	Update the server certificate by executing the following PowerShell command on one of the NC nodes.

  ```powershell

  $certificate = Get-ChildItem -Path Cert:\LocalMachine\My | Where {$_.Thumbprint -eq “Thumbprint of new certificate”}
  Set-NetworkController -ServerCertificate $certificate

   ```

3.	Update the certificate used for encrypting the credentials stored in the NC by executing the following command on one of the NC nodes.

  ```powershell

  $certificate = Get-ChildItem -Path Cert:\LocalMachine\My | Where {$_.Thumbprint -eq “Thumbprint of new certificate”}
  Set-NetworkControllerCluster -CredentialEncryptionCertificate $certificate

  ```

4.	Retrieve a server REST resource by executing the following PowerShell command on one of the NC nodes.

  ```powershell

  Get-NetworkControllerServer -ConnectionUri <REST uri of your deployment>

  ```

5.	In the Server REST resource, navigate to the **Connections** object and retrieve the credential resource ID with type **X509Certificate**.

  ```powershell

  "Connections":
    {
       {
          "ManagementAddresses":[ “contoso.com" ],                  
          "CredentialType":  "X509Certificate",
          "Protocol":  null,
          "Port":  null,
          "Credential": {
                            "Tags":  null,
                            "ResourceRef":  "/credentials/41229069-85d4-4352-be85-034d0c5f4658",
                            "InstanceId":  "00000000-0000-0000-0000-000000000000",
                            …
                            …
                         }
        }   
    }

    ```

6. Update the credential REST resource of type **X509Certificate** retrieved above with the thumbprint of the new certificate.

  Execute these PowerShell cmdlet on any of the NC Node.

  ```powershell

  $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
  $cred.type="X509Certificate"
  $cred.username=""
  $cred.value="<thumbprint of the new certificate>"
  New-NetworkControllerCredential -ConnectionUri <REST uri of the deployment> -ResourceId 41229069-85d4-4352-be85-034d0c5f4658 -Properties
  $cred

 ```
7. If the new certificate is a self-signed certificate, provision the certificate (without the private key) in the trusted root certificate store of all the Hyper-V hosts and software load balancer MUX virtual machines.

8. Provision the NC certificate (without the private key) in the trusted root certificate store of the VMM machine using the following PowerShell cmdlet:

  ```powershell
  $certificate = Get-SCCertificate -ComputerName "NCRestName"
  $networkservice = Get-SCNetworkService | Where {$_.IsNetworkController -eq $true}
  Set-SCNetworkService -ProvisionSelfSignedCertificatesforNetworkService $true -Certificate
  $certificate -NetworkService $networkservice

 ```
  - **NetworkService** is the network controller service, **Certificate** is the new NC server certificate.
  - **ProvisionSelfSignedCertificatesforNetworkService** is **$true** if you are updating to a self-signed certificate.

9. Verify  that the connectivity is working fine with the updated certificate.

  You can now remove the previous certificate from the NC nodes.


## Next steps

-[Configure the VM settings](vm-settings.md)
