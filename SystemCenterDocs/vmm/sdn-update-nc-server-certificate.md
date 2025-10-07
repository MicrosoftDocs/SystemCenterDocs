---
ms.assetid: f6500be6-7c8a-46ff-a3d4-b9fada8c5d8d
title: Update the Network Controller Server Certificate
description: This article describes the procedure on how to update the network controller's server certificate.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/07/2025
ms.update-cycle: 1095-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency3, engagement-fy24
---


# Update the network controller server certificate



Network controller (NC) uses a certificate for Northbound communication with REST clients, such as VMM, and Southbound communication with Hyper-V hosts and software load balancers.

You can change or update this certificate in the following scenarios after you deploy the NC:

- The certificate has expired
- You want to move from a self-signed certificate to a certificate that is issued by a certificate authority (CA).

> [!NOTE]
> If you renew the existing certificate with the same key, these steps are not required.

## Before you start

Before you start, ensure that you create a new SSL certificate with the existing network controller's REST name. [Learn more](sdn-controller.md#set-up-the-security-certificates).

## Update the server certificate

To update the server certificate, follow these steps:

1. If the certificate is self-signed, do the following:

   - Certificate with private key - Export the certificate and import it on all the NC nodes' **My** store.
   - Certificate without a private key - Export the certificate and import it on all the NC nodes' **Root** store.

2. If the certificate is a CA issued certificate, import it on all network controller nodes' **My** store.

   > [!NOTE]
   > DO NOT remove the current certificate from the NC nodes. You should validate the updated certificate before you remove the existing one. Proceed with the rest of the steps to update the certificate.

3. Update the server certificate by executing the following PowerShell command on one of the NC nodes.

   ```powershell

   $certificate = Get-ChildItem -Path Cert:\LocalMachine\My | Where {$_.Thumbprint -eq “Thumbprint of new certificate”}
   Set-NetworkController -ServerCertificate $certificate
   ```

4. Update the certificate used for encrypting the credentials stored in the NC by executing the following command on one of the NC nodes.

   ```powershell

   $certificate = Get-ChildItem -Path Cert:\LocalMachine\My | Where {$_.Thumbprint -eq “Thumbprint of new certificate”}
   Set-NetworkControllerCluster -CredentialEncryptionCertificate $certificate
   ```

5. Retrieve a server REST resource by executing the following PowerShell command on one of the NC nodes.

   ```powershell

   Get-NetworkControllerServer -ConnectionUri <REST uri of your deployment>
   ```

6. In the Server REST resource, navigate to the **Credentials** object and check the credential of type **X509Certificate** with a value matching your certificate's thumbprint. Note the credential resource ID.

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
                           "ResourceRef":  "/credentials/<credential resource Id>,
                           "InstanceId":  "00000000-0000-0000-0000-000000000000",
                           …
                           …
                        }
       }   
   }
   ```

7. Update the credential REST resource of type **X509Certificate** retrieved above with the thumbprint of the new certificate.

   Execute this PowerShell cmdlet on any of the NC nodes.

   ```powershell

   $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
   $cred.type="X509Certificate"
   $cred.username=""
   $cred.value="<thumbprint of the new certificate>"
   New-NetworkControllerCredential -ConnectionUri <REST uri of the deployment> -ResourceId <credential resource Id> -Properties
   $cred
   ```

8. If the new certificate is a self-signed certificate, provision the certificate (without the private key) in the trusted root certificate store of all the Hyper-V hosts and software load balancer MUX virtual machines.

9. Provision the NC certificate (without the private key) in the trusted root certificate store of the VMM machine using the following PowerShell cmdlet:

   ```powershell
   $certificate = Get-SCCertificate -ComputerName "NCRestName"
   $networkservice = Get-SCNetworkService | Where {$_.IsNetworkController -eq $true}
   Set-SCNetworkService -ProvisionSelfSignedCertificatesforNetworkService $true -Certificate
   $certificate -NetworkService $networkservice
   ```
   - **NetworkService** is the network controller service, **Certificate** is the new NC server certificate.
   - **ProvisionSelfSignedCertificatesforNetworkService** is **$true** if you're updating to a self-signed certificate.

10. Verify that the connectivity is working fine with the updated certificate.

    You can now remove the previous certificate from the NC nodes.

## Next steps
[Validate the NC deployment](sdn-controller.md#validate-the-deployment) to ensure that the deployment is successful.
