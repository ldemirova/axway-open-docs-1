{
"title": "Certificate chain check",
"linkTitle": "Certificate chain check",
"date": "2019-10-17",
"description": "It is a trivial task for a user to generate a structurally sound X.509 certificate, and use it to negotiate mutually authenticated connections to publicly available services. However, this scenario is a security nightmare for IT administrators. You cannot allow every user to generate their own certificate and use it on the Internet. For this reason, API Gateway can establish the authenticity of the client certificate by ensuring that the certificate originated from a trusted source. To do this, a server can perform a *certificate chain check*\\n on the client certificate."
}
﻿
<div id="p_certificate_cert_chain_over">

Overview
--------

It is a trivial task for a user to generate a structurally sound X.509 certificate, and use it to negotiate mutually authenticated connections to publicly available services. However, this scenario is a security nightmare for IT administrators. You cannot allow every user to generate their own certificate and use it on the Internet. For this reason, API Gateway can establish the authenticity of the client certificate by ensuring that the certificate originated from a trusted source. To do this, a server can perform a *certificate chain check*
on the client certificate.

The main purpose of certificate chain validation is to ensure that a certificate has been issued by a trusted source. Typically, in a Public Key Infrastructure (PKI), a Certificate Authority (CA) is responsible for issuing and distributing certificates. This infrastructure is based on the premise of *transitive trust*
—if everybody trusts the CA, everybody transitively trusts the certificates issued by that CA. If entities only trust certificates that have been issued by the CA, they can reject certificates that have been self-generated by clients.

When a CA issues a certificate, it digitally signs the certificate and inserts a copy of its own certificate into it. This is called a certificate chain. Whenever an application (such as API Gateway) receives a client certificate, it can extract the issuing CA certificate from it, and run a certificate chain check to determine whether it should trust the CA. If it trusts the CA, it also trusts the client certificate.

API Gateway maintains a repository of trusted CA certificates, which is known as the certificate store. To *trust*
a specific CA, that CA certificate must be imported into the certificate store.

</div>

<div id="p_certificate_cert_chain_conf">

Configuration
-------------

You can configure the following settings on the **Certificate Chain Check**
window:

**Name**:\
Enter an appropriate name for this filter to display in a policy.

**Certificates Message Attribute**:\
You can specify a message attribute that contains the certificate or certificates to check. The message attribute type can be an `X509Certificate`
object, or an `ArrayList`
of `X509Certificate`
objects.

**Distinguished Name**:\
This table lists the Distinguished Names of the certificates currently in the certificate store. Select the check box beside a CA to enable this filter to consider it as *trusted*
when performing the certificate chain check. You can select multiple CAs in the table.

</div>