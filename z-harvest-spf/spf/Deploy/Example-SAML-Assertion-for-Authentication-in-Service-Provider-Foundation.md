---
title: Example SAML Assertion for Authentication in Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0d8f2b5-7b0e-4853-8072-9801c49ed6ce
author:bwren
manager:cfreemanwa
---
# Example SAML Assertion for Authentication in Service Provider Foundation
  
> [!CAUTION]  
> This topic is outdated. In a [!INCLUDE[katal_1](../../orch/getstarted/includes/katal_1_md.md)] environment, authentication is provided by the REST API. For more information, see [Windows Azure Pack Authentication Overview](http://msdn.microsoft.com/library/dn479300.aspx).  
  
This topic shows an example of using a Security Assertion Markup Language \(SAML\) 2.0 assertion for providing authentication and token information to access tenant resources. In this scenario, this assertion would be provided by a client portal application to [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] to authenticate access to tenant resources by a self\-service\-user \(SSU\).  
  
## SAML 2.0 assertion example  
  
```  
<Assertion ID="_de9f29bd-52ca-4237-95c1-eb53f70fe8e5" IssueInstant="2012-11-06T00:45:30.593Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">  
<Issuer>ADatum</Issuer>  
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">  
<ds:SignedInfo>  
&nbsp; <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />   
&nbsp;&nbsp;<ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />   
<ds:Reference URI="#_de9f29bd-52ca-4237-95c1-eb53f70fe8e5">  
<ds:Transforms>  
&nbsp; <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />   
&nbsp;&nbsp;<ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />   
&nbsp;&nbsp;</ds:Transforms>  
&nbsp; <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />   
&nbsp;&nbsp;<ds:DigestValue>+6OWUn1dFIUJQ6FQ25zgmZvg8zPzfcjnj4ujUvgfmEQ=</ds:DigestValue>   
&nbsp;&nbsp;</ds:Reference>  
&nbsp; </ds:SignedInfo>  
&nbsp; <ds:SignatureValue>O85ytS9fcAhOk/0K25SndyBUbNLrx6J+tv+Uht+HZZ4CzsqjVBU1FpkXjDG03HqZ7xEu3+rMnsyxefDq6Xftw1E926QsG/oPM/afWfbR5dLucjsVaNzXCXzZu+jBmp5KkAv/vv1Es67KnPMr/RDeCVFy9eyxJka6dd8h8RTlatg=</ds:SignatureValue>   
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
<X509Data>  
&nbsp; <X509Certificate>MIICGjCCAYOgAwIBAgIQeJe5qR+4T6VJNZYtWjhErzANBgkqhkiG9w0BAQQFADAgMR4wHAYDVQQDExVBQ1MyQ2xpZW50Q2VydGlmaWNhdGUwHhcNMTExMDEwMDcwMDAwWhcNNDExMjMxMDcwMDAwWjAgMR4wHAYDVQQDExVBQ1MyQ2xpZW50Q2VydGlmaWNhdGUwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAKjtrnJ+bduREosQ9+SH1ocI13wlxStLi8y5heGPo5UBcuf0hYRq4PvjwEY2twebP6iwxjwGqhu224UDUfPWMhQBOh+NFnv9GHAh+W4jFJxvTCcyXTkZRFqgAYRjMvyxzNeHVqn4AJ/ddKGf1fMVCuKhPYteHy2yNacXujucPP6/AgMBAAGjVTBTMFEGA1UdAQRKMEiAEFD3/7uhGcI2nSHZqB0bN66hIjAgMR4wHAYDVQQDExVBQ1MyQ2xpZW50Q2VydGlmaWNhdGWCEHiXuakfuE+lSTWWLVo4RK8wDQYJKoZIhvcNAQEEBQADgYEAkgxktVU5e8TVoigsDRm4qyw6gM/kie3e6dFM0T1BFoQV0PW9W9yKPiP72eTi+331tLFnwDxz5RJLABctAO71plwtREd0k3E0Jsju+Web+u8YcCD43aViQXgXRrY5ghDGwpFRcaNa1PnYY5nk3DYfyZZdz1L+fb30VDiugdf7dBI=</X509Certificate>   
&nbsp;&nbsp;</X509Data>  
&nbsp; </KeyInfo>  
&nbsp; </ds:Signature>  
<Subject>  
&nbsp; <NameID>ADatum</NameID>   
&nbsp;&nbsp;<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />   
&nbsp;&nbsp;</Subject>  
<Conditions NotBefore="2012-11-06T00:45:31.905Z" NotOnOrAfter="9999-12-31T23:59:59.999Z">  
<AudienceRestriction>  
&nbsp; <Audience>https://accesscontrol.adatum.com</Audience>   
&nbsp;&nbsp;</AudienceRestriction>  
&nbsp; </Conditions>  
<AttributeStatement>  
<Attribute Name="http://schemas.microsoft.com/spf/2012/03/claims/tenantname">  
&nbsp; <AttributeValue>Fabrikam</AttributeValue>   
&nbsp;&nbsp;</Attribute>  
&nbsp; </AttributeStatement>  
<AttributeStatement>  
<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">  
&nbsp; <AttributeValue>SSU</AttributeValue>   
&nbsp;&nbsp;</Attribute>  
&nbsp; </AttributeStatement>  
<AttributeStatement>  
<Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn">  
&nbsp; <AttributeValue>accesscontrol@adaum.com</AttributeValue>   
&nbsp;&nbsp;</Attribute>  
&nbsp; </AttributeStatement>  
&nbsp; </Assertion>  
  
```  
  
## See Also  
[Manage Certificates and User Roles in Service Provider Foundation](../../spf/Deploy/Manage-Certificates-and-User-Roles-in-Service-Provider-Foundation.md)  
[Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700)  
  
