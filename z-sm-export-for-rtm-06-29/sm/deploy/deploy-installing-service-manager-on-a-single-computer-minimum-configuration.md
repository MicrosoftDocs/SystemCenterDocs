---
title: Installing Service Manager on a Single Computer (Minimum Configuration)
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08c888e1-57cb-4f94-8b9e-041a54204c09
---

# Installing Service Manager on a Single Computer (Minimum Configuration)

If you want to evaluate System Center 2012 - Service Manager and you have a minimal amount of hardware available, install Service Manager on one computer. A sample single\-computer configuration is shown in figure&nbsp;1. This configuration will not support a production environment, and no scalability or performance estimates are provided. Because you cannot install both the Service Manager management server and the data warehouse management server on the same computer, use Hyper\-V to create a virtual computer to host the data warehouse management server. For more information about the hardware requirements for Hyper\-V, see [Hyper\-V Server&nbsp;2008&nbsp;R2 system requirements](http://go.microsoft.com/fwlink/p/?LinkId=231898).  

 To install Service Manager on a single computer, start with a physical computer that is running Windows&nbsp;Server&nbsp;2008 and Hyper\-V, and make sure that the CPU on the physical computer is compatible with Hyper\-V. Of the 8&nbsp;gigabytes \(GB\) of RAM on the host computer, 3&nbsp;GB is used for the virtual computer that hosts the data warehouse management server. Make sure that at least 200&nbsp;GB of free space is available on the hard disk drive.  

 **Figure 1: Single\-computer installation in which you use a physical computer that is running Windows&nbsp;Server&nbsp;2008 and Hyper\-V**  

 ![Minimum Configuration for Service Manager2012](../media/deploy-minimumconfiguration.png)  

 If your organization's best practice guidelines do not allow you to install applications on a Hyper\-V host, you can create a second virtual computer to host the Service Manager management server, the Service Manager database, and the data warehouse databases. Use the following procedures to install Service Manager on a single computer.  

## Installing Service Manager on a single computer topics  

-   [How to Install Service Manager on a Single Computer](../../../sm/deploy/deploy-guide/How-to-Install-Service-Manager-on-a-Single-Computer.md)  

     Describes how to install Service Manager on a single computer.  

-   [How to Validate the Single\-Computer Installation](../../../sm/deploy/deploy-guide/How-to-Validate-the-Single-Computer-Installation.md)  

     Describes how to validate the installation.  

## Other resources for this component  

-   TechNet Library main page for [System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  

-   [Operations Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)  

-   [Administrator's Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  

-   [Planning Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)
