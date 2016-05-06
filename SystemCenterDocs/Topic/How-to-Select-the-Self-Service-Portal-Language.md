---
title: How to Select the Self Service Portal Language
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0b0d41f-a5cd-493a-a489-18c307e4c846
---
# How to Select the Self Service Portal Language
[!INCLUDE[smshort](../Token/smshort_md.md)] does not include a localized Self Service Portal SharePoint template. As a result, after you install the [!INCLUDE[smssp](../Token/smssp_md.md)] on a non\-English SharePoint site, it will contain content that is not localized. In order to display the [!INCLUDE[smssp](../Token/smssp_md.md)] in a fully localized language, you must modify the Self Service Portal to suit your organization’s needs.

In System Center 2012, because the portal is based on SharePoint 2010, it is possible for your end\-users to choose the languages they want displayed by themselves, subject to the SharePoint administrator’s configuration.

You can also set up multiple SharePoint sites for the [!INCLUDE[smssp](../Token/smssp_md.md)] which can have different default languages and then you can direct users to a particular portal if you want.  End\-users can still change their language to whatever language they want, as long as the administrator has enabled it on the site.

### To select the [!INCLUDE[smssp](../Token/smssp_md.md)] language

1.  Install whatever language packs you want for your SharePoint product site and then follow instructions to install and deploy them using of the following options.

    -   Download [SharePoint 2010 Server Language packs](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=3411) and then read and follow the [installation and deployment instructions](http://technet.microsoft.com/library/cc262108.aspx).

    -   Download [SharePoint 2010 Foundation language packs](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=4731) and then read and follow the [installation and deployment instructions](http://technet.microsoft.com/library/cc288518.aspx).

2.  Once you have the language packs deployed you can configure the language settings. As a SharePoint site administrator, open the [!INCLUDE[smssp](../Token/smssp_md.md)] home page, click **Site Actions** and then select **Site Settings**.

3.  Under **Site Administration**, click **Language settings** and select your default language and additional languages you want to enable and then click **OK**.

4.  Click **Site Actions**, select **Site Settings** and then click **Quick Launch** and then modify items such as **Home**, **Help Articles**, **My Requests**, and **My Activities** for your language.

5.  Click **Site Actions**, select **Site Settings** and then click **Site Libraries and lists** and open each item, such as **Customize Calendar** and then modify items such as title, description and navigation and associated columns headings.

6.  Separately, each individual user can choose the language they want to display in the [!INCLUDE[smssp](../Token/smssp_md.md)], under <Account Name> by selecting **Select Display Language** and then click the language they want to display.

