---
ms.assetid: 
title: Azure Monitor SCOM Managed Instance (preview) Data Encryption at Rest
description: This article provides an overview of SCOM Managed Instance (preview) Data Encryption at Rest.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 02/13/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Azure Monitor SCOM Managed Instance (preview) Data Encryption at Rest 

Microsoft Azure includes tools to safeguard the data according to your company's security and compliance needs. Encryption at Rest is a common security requirement. 

In Azure, organizations can encrypt data at rest without the risk or cost of a custom key management solution. Organizations have the option of letting Azure completely manage Encryption at Rest. Additionally, organizations have various options to closely manage encryption or encryption keys. For more information, see [Azure Data Encryption at rest](/azure/security/fundamentals/encryption-atrest).

This article discusses the SCOM Managed Instance (preview) components protecting the data at various levels.

## SCOM Managed Instance (preview) components for Azure Encryption at Rest 

The goal of encryption at rest is that data that is persisted on disk is encrypted with a secret encryption key. To achieve that goal, secure key creation, storage, access control, and management of the encryption keys must be provided.

SCOM Managed Instance (preview) service doesn't store any customer details. SCOM Managed Instance (preview) uses different persistence storage, such as Key vault, Storage account, and Cosmos Database, to store service metadata.

### Azure Key Vault 

The storage location of the encryption keys and access control to those keys is central to an Encryption at Rest model. The keys need to be highly secure but manageable by specified users and available to specific services. SCOM Managed Instance (preview) uses Azure Key Vault to store service configurations, certificates, and secrets. SCOM Managed Instance (preview) uses the Encryption at Rest capability of Azure Key Vault.

### Azure Storage account 

SCOM Managed Instance (preview) uses a storage account to hold service configurations, scripts, and System Center Operations Manager runtime bits. It's also used to exchange messages (actions on SCOM Managed Instance (preview)) between System Center Operations Manager RP web service and the worker role service. SCOM Managed Instance (preview) metadata that is stored in Azure storage blob/Queue uses 256-bit AES encryption. 

## Cosmos database 

SCOM Managed Instance (preview) uses RPaaS Cosmos database to store SCOM Managed Instance (preview) resource details. Azure Cosmos database uses AES-256 encryption on all regions where the account is running. 

## Encryption at Compute 

Though SCOM Managed Instance (preview) doesn't store any customer details, it takes domain user details from your key vault secrets. These domain user details are used for adding System Center Operations Manager management servers to on-premises Domain controller. To avoid any data leak at compute, encrypt it using the VM extension `AzureDiskEncryption`. 

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).

