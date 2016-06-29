---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Hardware Requirements for Service Manager
ms.technology:  service-manager
ms.assetid:  e13218d6-05f1-46d1-8f10-068a2497aacb
---

# Hardware Requirements for Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic describes the hardware requirements for <token>scsm_threshold_Token>.</para>
  </introduction>
  <section>
    <title>Hardware Requirements</title>
    <content>
      <para>The following table lists the recommended hardware requirements for the individual parts of <token>scsm_threshold_Token>. These computers can be physical servers or virtual servers.</para>
      <para>
        The hardware requirements for <token>smshort1Token> in  are unchanged from its initial release.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>
          <?Comment j: PAGE # "'Page: '#''"169361 2012-08-29T14:08:00Z  Id='1?>Hardware requirements table<?CommentEnd Id='1'
    ?></caption>
        <tbody>
          <tr>
            <TD>
              <para>
                <token>scsm_threshold_Token> database</para>
            </TD>
            <TD>
              <para>8-core 2.66 gigahertz (GHz) CPU</para>
              <para>
                <?Comment j: PAGE # "'Page: '#''"174421 2012-08-29T14:08:00Z  Id='2?>8 gigabytes (GB) of RAM for 20,000 users, 32 GB of RAM for 50,000 users<?CommentEnd Id='2'
    ?></para>
              <para>80 GB of available disk space</para>
              <para>RAID Level 1 or Level 10 drive*</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <token>scsm_threshold_Token> management server</para>
            </TD>
            <TD>
              <para>
                <?Comment JD: PAGE # "'Page: '#''"238454 2012-08-29T14:08:00Z  Id='3?>4-Core 2.66 GHz CPU<?CommentEnd Id='3'
    ?></para>
              <para>
                <?Comment j: PAGE # "'Page: '#''"174421 2012-08-29T14:08:00Z  Id='4?>8 GB of RAM<?CommentEnd Id='4'
    ?></para>
              <para>10 GB of available disk space</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <token>smconToken>
              </para>
            </TD>
            <TD>
              <para>2-core 2.0 GHz CPU</para>
              <para>4 GB of RAM</para>
              <para>10 GB of available disk space</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Data warehouse management server</para>
            </TD>
            <TD>
              <para>
                <?Comment JD: PAGE # "'Page: '#''"238454 2012-08-29T14:08:00Z  Id='5?>4-Core 2.66 GHz CPU<?CommentEnd Id='5'
    ?></para>
              <para>
                <?Comment j: PAGE # "'Page: '#''"174421 2012-08-29T14:08:00Z  Id='6?>8 GB of RAM <!--Removed broken links to Hardware Performance--><?CommentEnd Id='6'
    ?></para>
              <para>When a data warehouse management group and SQL Server Analysis Services are hosted on a single server, it should contain at least 16 GB RAM.</para>
              <para>10 GB of available disk space</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Data warehouse databases</para>
            </TD>
            <TD>
              <para>8-core 2.66 GHz CPU</para>
              <para>
                <?Comment j: PAGE # "'Page: '#''"174421 2012-08-29T14:08:00Z  Id='7?>8 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users<?CommentEnd Id='7'
    ?></para>
              <para>400 GB of available disk space</para>
              <para>RAID Level 1 or Level (1+0) drive</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <token>smssToken>: Web Content Server with SharePoint Web Parts</para>
            </TD>
            <TD>
              <para>
                <?Comment JD: PAGE # "'Page: '#''"238454 2012-08-29T14:08:00Z  Id='8?>
                <?Comment j: PAGE # "'Page: '#''"Per discussion with Jim Truher, we are using the same hardware specs at the SM MS for the WCS. 2012-08-29T14:08:00Z  Id='9?>8-Core 2.66 GHz CPU<?CommentEnd Id='9'
    ?><?CommentEnd Id='8'
    ?></para>
              <para>8-core, 64-bit CPU for medium deployments</para>
              <para>
                <?Comment j: PAGE # "'Page: '#''"174421 2012-08-29T14:08:00Z  Id='10?>16 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users.<?CommentEnd Id='10'
    ?></para>
              <para>80 GB of available hard disk space</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <para>* For more information, see <externalLink><linkText>RAID levels and Microsoft SQL Server</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=134073</linkUri></externalLink>.</para>
      <para>** Hardware requirements are based on SharePoint specifications. For more information, see <externalLink><linkText>Hardware and Software Requirements (SharePoint Server 2010)</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=219606</linkUri></externalLink>.</para>
    </content>
  </section>
  <relatedTopics/>
</developerConceptualDocument>


