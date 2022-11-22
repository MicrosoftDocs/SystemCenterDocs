---
ms.assetid: 
title: Azure Monitor SCOM Managed Instance (preview) Data Encryption at rest
description: This article describes how to use Managed identities for Azure with Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/22/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Azure Monitor SCOM Managed Instance (preview) Data Encryption at rest 

Microsoft Azure includes tools to safeguard data according to your company's security and compliance needs. Encryption at Rest is a common security requirement. 

In Azure, organizations can encrypt data at rest without the risk or cost of a custom key management solution. Organizations have the option of letting Azure completely manage Encryption at Rest. Additionally, organizations have various options to closely manage encryption or encryption keys. For more information, see [Azure Data Encryption at rest](/azure/security/fundamentals/encryption-atrest)

This article discusses the SCOM Managed Instance (preview) components protecting the data at various levels.

## SCOM Managed Instance (preview) Components for Azure Encryption at Rest 

The goal of encryption at rest is that data that is persisted on disk is encrypted with a secret encryption key. To achieve that goal secure key creation, storage, access control, and management of the encryption keys must be provided.   

SCOM Managed Instance (preview) service doesn't store any customer details. SCOM Managed Instance (preview) uses different persistence storage such as Key vault, Storage account and Cosmos Database to store service meta data. 

### Azure Key Vault 

The storage location of the encryption keys and access control to those keys is central to an encryption at rest model. The keys need to be highly secured but manageable by specified users and available to specific services. SCOM Managed Instance (preview) uses Azure Key Vault to store service configurations, certificates, and secrets. SCOM Managed Instance (preview) leverages the encryption at Rest capability of Azure Key Vault.

### Azure Storage account 

SCOM Managed Instance (preview) uses storage account to hold service configurations, scripts, and SCOM runtime bits. It is also used to exchange messages (actions on SCOM Managed Instace (preview)) between SCOM RP web service and worker role service. SCOM Managed Instance (preview) meta data is stored in Azure storage blob/Queue uses 256-bit AES encryption. 

## Cosmos database 

SCOM Managed Instance (preview) uses RPaaS Cosmos database to store SCOM Managed Instance (preview) resource details. Azure Cosmos database uses AES-256 encryption on all regions where the account is running. 

## Encryption at Compute 

Though SCOM Managed Instance (preview) doesn't store any customer details, it takes domain user details from your key vault secrets. These domain user details are used for joining SCOM management servers to On-Prem Domain controller. To avoid any data leak at compute, encrypt the compute using VM extension `AzureDiskEncryption`. 