---
title: Müşteri için doğrulanmış bir etki alanı ekleme
description: İş Ortağı Merkezi'daki bir müşteri için onaylı etki alanları listesine doğrulanmış etki alanı İş Ortağı Merkezi. Bunu api'İş Ortağı Merkezi REST API'lerini kullanarak yapma.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 570008c955ce3242b02c1df4c87df52aea3627abb6c86a069cc7c4c0d1d6f799
ms.sourcegitcommit: ac8f5f8bedaddba5110dd4e562fbd9a2b24837df
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/08/2021
ms.locfileid: "116885586"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Mevcut bir müşteri için onaylanmış etki alanları listesine doğrulanmış bir etki alanı ekleme 

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Mevcut bir müşteri için onaylı etki alanları listesine doğrulanmış etki alanı ekleme.

## <a name="prerequisites"></a>Önkoşullar

- Etki alanı kayıt şirketi olan bir İş Ortağınız olmalıdır.

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="adding-a-verified-domain"></a>Doğrulanmış etki alanı ekleme

Etki alanı kayıt şirketi olan bir İş Ortağınız varsa API'yi kullanarak mevcut müşteri için etki alanları listesine yeni bir Etki alanı `verifieddomain` kaynağı ekleyebilirsiniz. [](#domain) Bunu yapmak için CustomerTenantId'sini kullanarak müşteriyi tanıyın. VerifiedDomainName özelliği için bir değer belirtin. İstekte [gerekli](#domain) Ad, Yetenek, AuthenticationType, Durum ve VerificationMethod özelliklerine sahip bir Etki alanı kaynağı girin. Yeni Etki Alanının federasyon [etki](#domain) alanı olduğunu belirtmek için, Etki [](#domain) alanı kaynağında AuthenticationType özelliğini olarak ayarlayın ve `Federated` [İstek'e bir DomainFederationSettings](#domain-federation-settings) kaynağı dahil ederek. Yöntem başarılı olursa Yanıt, yeni doğrulanmış etki [alanı için](#domain) bir Etki alanı kaynağı içerir.

### <a name="custom-verified-domains"></a>Özel doğrulanmış etki alanları

Özel bir doğrulanmış etki alanı eklerken, **onmicrosoft.com** üzerinde kayıtlı olmayan bir etki alanı, [CustomerUser.immutableId](user-resources.md#customeruser) özelliğini etki alanını eklemekte olan müşteri için benzersiz bir kimlik değerine ayarlamış olur. Bu benzersiz tanımlayıcı, etki alanı doğrulandığında doğrulama işlemi sırasında gereklidir. Müşteri kullanıcı hesapları hakkında daha fazla bilgi için [bkz. Müşteri için kullanıcı hesapları oluşturma.](create-user-accounts-for-a-customer.md)

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Doğrulanmış bir etki alanı eklemekte olduğunu müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Değer, müşteri belirtmenize olanak sağlayan GUID biçiminde bir **CustomerTenantId** değeridir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde gerekli özellikleri açıklar.

| Ad                                                  | Tür   | Gerekli                                      | Açıklama                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | Yes                                           | Doğrulanmış etki alanı adı. |
| [Etki alanı](#domain)                                     | object | Yes                                           | Etki alanı bilgilerini içerir. |
| [DomainFederationSettings](#domain-federation-settings) | object | Evet (AuthenticationType = `Federated` ise)     | Etki alanı bir etki alanı değil etki alanı ise `Federated` kullanılacak etki alanı federasyon `Managed` ayarları. |

### <a name="domain"></a>Etki alanı

Bu tablo, istek gövdesinde gerekli **ve isteğe** bağlı Etki alanı özelliklerini açıklar.

| Ad               | Tür                                     | Gerekli | Açıklama                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authenticationtype                                    | string           | Yes      | Etki alanının bir etki alanı mı `Managed` yoksa etki alanı mı olduğunu `Federated` tanımlar. Desteklenen değerler: `Managed` , `Federated` .|
| Özellik                                            | string           | Yes      | Etki alanı özelliğini belirtir. Örneğin, `Email`.                  |
| ısdefault                                             | null değere sahip boole değeri | No       | Etki alanının kiracı için varsayılan etki alanı olup olmadığını gösterir. Desteklenen değerler: `True` , `False` , `Null` .        |
| IsInitial                                             | null değere sahip boole değeri | No       | Etki alanının bir ilk etki alanı olup olmadığını gösterir. Desteklenen değerler: `True` , `False` , `Null` .                       |
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
| Openıdconnectdiscoveryendpoint         | dize           | No      | federal ıdp STS 'nin openıd Bağlan bulma uç noktası. |
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
