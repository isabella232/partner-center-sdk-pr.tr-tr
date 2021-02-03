---
title: Müşteri için doğrulanmış bir etki alanı ekleme
description: Iş Ortağı Merkezi 'nde bir müşterinin onaylanan etki alanları listesine doğrulanmış bir etki alanı eklemeyi öğrenin. Iş Ortağı Merkezi API 'Leri ve REST API 'Leri kullanarak bunu yapın.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d0ea9998324e99c7986645dc90fdfba0a2a71571
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769965"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Mevcut bir müşterinin onaylanan etki alanları listesine doğrulanmış etki alanı ekleme 

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Mevcut bir müşterinin onaylanan etki alanları listesine doğrulanmış etki alanı ekleme.

## <a name="prerequisites"></a>Önkoşullar

- Etki alanı kaydedicisi olan bir Iş ortağı olmanız gerekir.

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="adding-a-verified-domain"></a>Doğrulanmış etki alanı ekleme

Etki alanı kaydedicisi olan bir Iş ortağıysanız, API 'yi kullanarak mevcut bir `verifieddomain` müşterinin etki alanları listesine yeni bir [etki alanı](#domain) kaynağı gönderebilirsiniz. Bunu yapmak için Customertenantıd 'sini kullanarak müşteriyi tanımayın. VerifiedDomainName özelliği için bir değer belirtin. Istekte gerekli ad, yetenek, AuthenticationType, durum ve doğrulama Icationmethod özelliklerine sahip bir [etki alanı](#domain) kaynağı geçirin. Yeni [etki alanının](#domain) bir Federasyon etki alanı olduğunu belirtmek Için, [etki alanı](#domain) kaynağındaki AuthenticationType özelliğini olarak ayarlayın `Federated` ve isteğe bir [domainfederationsettings](#domain-federation-settings) kaynağı ekleyin. Yöntem başarılı olursa, yanıt yeni doğrulanmış etki alanı için bir [etki alanı](#domain) kaynağı içerecektir.

### <a name="custom-verified-domains"></a>Özel doğrulanmış etki alanları

**Onmicrosoft.com**' de kayıtlı olmayan özel bir doğrulanmış etki alanı eklediğinizde, [Customeruser. ImmutableID](user-resources.md#customeruser) özelliğini, etki alanını eklediğiniz MÜŞTERIYE ait benzersiz bir kimlik değeri olarak ayarlamanız gerekir. Bu benzersiz tanımlayıcı, etki alanı doğrulanırken doğrulama işlemi sırasında gereklidir. Müşteri Kullanıcı hesapları hakkında daha fazla bilgi için bkz. [müşteri için Kullanıcı hesapları oluşturma](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{CustomerTenantId}/verifieddomain http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

İçin doğrulanmış bir etki alanı eklediğiniz müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Değer, bir müşteriyi belirtmenizi sağlayan bir GUID biçimli **Customertenantıd** 'dir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad                                                  | Tür   | Gerekli                                      | Açıklama                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | Yes                                           | Doğrulanan etki alanı adı. |
| [Etki alanı](#domain)                                     | object | Yes                                           | Etki alanı bilgilerini içerir. |
| [DomainFederationSettings](#domain-federation-settings) | object | Evet (IF AuthenticationType = `Federated` )     | Etki alanı etki alanı değil, etki alanı ise kullanılacak etki alanı Federasyon ayarları `Federated` `Managed` . |

### <a name="domain"></a>Etki alanı

Bu tablo, istek gövdesinde gerekli ve isteğe bağlı **etki alanı** özelliklerini açıklar.

| Ad               | Tür                                     | Gerekli | Açıklama                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | string           | Yes      | Etki alanının bir etki alanı mı yoksa etki alanı mı olduğunu tanımlar `Managed` `Federated` . Desteklenen değerler: `Managed` , `Federated` .|
| Özellik                                            | string           | Yes      | Etki alanı özelliğini belirtir. Örneğin, `Email`.                  |
| IsDefault                                             | null yapılabilir Boole | No       | Etki alanının kiracı için varsayılan etki alanı olup olmadığını gösterir. Desteklenen değerler: `True` , `False` , `Null` .        |
| Isınıtıal                                             | null yapılabilir Boole | No       | Etki alanının bir ilk etki alanı olup olmadığını gösterir. Desteklenen değerler: `True` , `False` , `Null` .                       |
| Name                                                  | string           | Yes      | Etki alanı adı.                                                          |
| RootDomain                                            | dize           | No       | Kök etki alanının adı.                                              |
| Durum                                                | string           | Yes      | Etki alanı durumu. Örneğin, `Verified`. Desteklenen değerler:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| Doğrulamaları Icationmethod                                    | string           | Yes      | Etki alanı doğrulama yöntemi türü. Desteklenen değerler: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Etki alanı Federasyon ayarları

Bu tabloda, istek gövdesinde gerekli ve isteğe bağlı **Domainfederationsettings** özellikleri açıklanmaktadır.

| Ad   | Tür   | Gerekli | Açıklama                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | dize           | No      | Zengin istemciler tarafından kullanılan oturum açma URI 'SI. Bu özellik, ortağın STS kimlik doğrulama URL 'sidir. |
| Defaultınteractiveauthenticationmethod | dize           | No      | Bir uygulama kullanıcının etkileşimli oturum açmasını gerektirdiğinde kullanılması gereken varsayılan kimlik doğrulama yöntemini gösterir. |
| FederationBrandName                    | dize           | No      | Federasyon markası adı.        |
| Issueruri                              | string           | Yes     | Sertifika verenin adı.                        |
| LogOffUri                              | string           | Yes     | Oturum kapatma URI 'SI. Bu özellik, Federasyon etki alanı oturum açma URI 'sini açıklar.        |
| MetadataExchangeUri                    | dize           | No      | Zengin istemci uygulamalarından kimlik doğrulaması için kullanılan meta veri değişim uç noktasını belirten URL. |
| NextSigningCertificate                 | dize           | No      | Daha sonra gelen ve ADFS v2 STS tarafından talepleri imzalamak için kullanılan sertifika. Bu özellik, sertifikanın Base64 olarak kodlanmış bir gösterimidir. |
| Openıdconnectdiscoveryendpoint         | dize           | No      | Federal ıDP STS 'nin OpenID Connect bulma uç noktası. |
| PassiveLogOnUri                        | string           | Yes     | Eski pasif Istemciler tarafından kullanılan oturum açma URI 'SI. Bu özellik, Federasyon oturum açma isteklerini göndermek için olan adrestir. |
| PreferredAuthenticationProtocol        | string           | Yes     | Kimlik doğrulama belirtecinin biçimi. Örneğin, `WsFed`. Desteklenen değerler: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | string           | Yes     | İstem oturum açma davranışı türü.  Örneğin, `TranslateToFreshPasswordAuth`. Desteklenen değerler: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | string           | Yes     | Şu anda ADFS v2 STS tarafından talepleri imzalamak için kullanılan sertifika. Bu özellik, sertifikanın Base64 olarak kodlanmış bir gösterimidir. |
| SigningCertificateUpdateStatus         | dize           | No      | Imzalama sertifikasının güncelleştirme durumunu gösterir. |
| SigningCertificateUpdateStatus         | null yapılabilir Boole | No      | IDP STS 'nin MFA 'yı destekleyip desteklemediğini gösterir. Desteklenen değerler: `True` , `False` , `Null` .|

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu API yeni doğrulanmış etki alanı için bir [etki alanı](#domain) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```
