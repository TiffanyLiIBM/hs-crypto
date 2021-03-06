---

copyright:
  years: 2018
lastupdated: "2018-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}

> _**Disclaimer: {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is still in experimental phase and it might change at anytime.**_

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) helps you encrypt your data at the safety and security level of System z cryptography in a convenient and cost competitive manner.
{:shortdesc}

{{site.data.keyword.hscrypto}} is the industry's first crypto service that provides access to cryptographic hardware that is FIPS 140-2 Level 4 certified technology, the highest level attainable of security. {{site.data.keyword.hscrypto}} offers network addressable hardware security modules (HSMs) and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on.  You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources. For more information about {{site.data.keyword.hscrypto}}, see [About {{site.data.keyword.hscrypto}}](overview.html).  

{{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/hypersecure-platform/index.html){:new_window}.

This tutorial guides you to set up your environment to use the {{site.data.keyword.hscrypto}} service.


## Provisioning the service

Before you begin, you must have a instance of {{site.data.keyword.hscrypto}} in {{site.data.keyword.cloud_notm}}. For more information, see [Provisioning a {{site.data.keyword.hscrypto}} instance](overview.html#provision).


## Installing ACSP client libraries

Complete the following steps to install the ACSP client libraries in your local environment.

1. Download the installation package from the [GitHub repository ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:new_window}. In the **packages** folder, choose the installation package file that is suitable for your operation system and CPU architecture. For example, for Ubuntu on x86, choose `acsp-pkcs11-client_1.5-3.5_amd64.deb`.
2. Install the package to install the ACSP client libraries with the `dpkg` command. For example, `dpkg -i acsp-pkcs11-client_1.5-3.5_amd64.deb`.



## Configuring ACSP client

> _**Disclaimer: At the current stage, {{site.data.keyword.hscrypto}} provides only self-signed certificates.**_

You need to configure the ACSP client to enable a proper secure communication channel (mutual TLS) to your service instance in the cloud.

1. In your {{site.data.keyword.hscrypto}} service instance in {{site.data.keyword.cloud_notm}}, select **Manage** from the left navigator.
2. On the "Manage" screen, click the **Download Config** button to download the `acsp_client_credentials.uue` file.
3. Copy the `acsp_client_credentials.uue` file to the `/opt/ibm/acsp-pkcs11-client/config` directory in your local environment.
4. In the `/opt/ibm/acsp-pkcs11-client/config` directory, decode the file with the following command:
       `base64 --decode acsp_client_credentials.uue > acsp_client_credentials.tar`
5. Extract the client credentials file with the following command:
       `tar xf acsp_client_credentials.tar`
6. Move the `server-config` files into the default place with the following command:
       `mv server-config/* ./`
7. Rename the client credentials file with the following command:
       `mv acsp.properties.client acsp.properties`
8. (Optional:) Change group ID of the files with the following command:
       `chown root.pkcs11 *`
9. Enable ACSP to use the proper config for the service instance in the cloud:
       `export ACSP_P11=/opt/ibm/acsp-pkcs11-client/config/acsp.properties`

Now your ACSP client is operational and your {{site.data.keyword.hscrypto}} is ready to use!

For more information about ACSP client installation and configureation, see [ACSP Client Installation and Configuration Guide ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/blob/master/doc/ACSP-client-config-guide.pdf){:new_window}.


## Getting support

There are several mechanisms available to obtain support and troubleshoot problems that are associated with {{site.data.keyword.hscrypto}}. Search for your problems in the following forums. If you don't find an answer there, submit your questions and ensure that you add the **hyperprotect-crypto** tag to your questions.

- [dwAnswers](https://developer.ibm.com/answers/index.html)
- [StackOverflow](https://stackoverflow.com/)
