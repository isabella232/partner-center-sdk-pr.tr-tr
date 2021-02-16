---
title: Dolaylı bir satıcının Microsoft Iş ortağı sözleşmesi imza durumunu doğrulama
description: AgreementStatus API 'sini kullanarak dolaylı bir satıcının Microsoft Iş ortağı sözleşmesinin imzalanıp imzalanmadığını doğrulayabilirsiniz.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9501f245a6c98fa90e77de7bc0caed8ca51fa4f2
ms.sourcegitcommit: 40baf4d825ce0ca6a254b5f368c308f025be7034
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100537585"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Dolaylı bir satıcının Microsoft Iş ortağı sözleşmesi imza durumunu doğrulama

**Uygulama hedefi:**

- İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir dolaylı satıcının, Microsoft İş Ortağı Ağı (MPN) KIMLIĞI (PGA/PLA) veya bulut çözümü sağlayıcısı (CSP) kiracı KIMLIĞI (Microsoft ID) kullanarak Microsoft Iş ortağı sözleşmesi 'Ni imzaladığını doğrulayabilirsiniz. **AgreementStatus** API 'Sini kullanarak Microsoft Iş ortağı sözleşmesi imza durumunu denetlemek için bu tanımlayıcılardan birini kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- MPN KIMLIĞI (PGA/PLA) veya dolaylı satıcıdan oluşan CSP kiracı KIMLIĞI (Microsoft ID). *Bu iki tanımlayıcıdan birini kullanmalısınız.*

## <a name="c"></a>C\#

Dolaylı bir satıcının Microsoft Iş ortağı sözleşmesi imza durumunu almak için:

1. **AgreementSignatureStatus** özelliğini çağırmak Için **ıaggregatepartner. uyum** koleksiyonunuzu kullanın.

2. [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Örnek: **[konsol test uygulaması](console-test-app.md)**
- Proje: **Partnercentersdk. FeaturesSamples**
- Sınıf: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si |
| ------ | ----------- |
| **Al** | *[{BaseUrl}](partner-center-rest-urls.md)*/v1/Compliance/{programname}/agreementstatus? mpnıd = {mpnıd} &tenantıd = {tenantıd} |

#### <a name="uri-parameters"></a>URI parametreleri

İş ortağını tanımlamak için aşağıdaki iki sorgu parametresini sağlamanız gerekir. Bu iki sorgu parametrelerinden birini sağlamazsanız, **400 (hatalı istek)** hatası alırsınız.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| **Mpnıd** | int | Hayır | Dolaylı Bayi tanımlayan bir Microsoft İş Ortağı Ağı KIMLIĞI (PGA/PLA). |
| **Değerine** | GUID | Hayır | Dolaylı satıcıdan oluşan CSP hesabını tanımlayan bir Microsoft KIMLIĞI. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI kalanı](headers.md).

### <a name="request-examples"></a>İstek örnekleri

#### <a name="request-using-mpn-id-pgapla"></a>MPN KIMLIĞI (PGA/PLA) kullanarak istek

Aşağıdaki örnek istek dolaylı satıcının Microsoft Iş ortağı sözleşmesi imza durumunu dolaylı Bayi Microsoft İş Ortağı Ağı KIMLIĞINI kullanarak alır.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>CSP kiracı KIMLIĞI kullanarak istek

Aşağıdaki örnek istek, dolaylı satıcının CSP kiracı KIMLIĞINI (Microsoft ID) kullanarak dolaylı satıcının Microsoft Iş ortağı sözleşmesi imza durumunu alır.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hatası](error-codes.md).

### <a name="response-example-success"></a>Yanıt örneği (başarılı)

Aşağıdaki örnek yanıt başarıyla dolaylı satıcının Microsoft Iş ortağı sözleşmesi 'Ni imzaladığı olup olmadığını döndürür.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a>Yanıt örnekleri (hata)

Dolaylı satıcının Microsoft Iş ortağı sözleşmesinin imzalama durumu döndürülemeyebilir, aşağıdaki örneklere benzer yanıtlar alabilirsiniz.

#### <a name="non-guid-formatted-csp-tenant-id"></a>GUID olmayan biçimli CSP kiracı KIMLIĞI

Aşağıdaki örnek yanıt, API 'ye geçirilen CSP kiracı KIMLIĞI bir GUID olmadığında döndürülür.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a>Sayısal olmayan MPN KIMLIĞI

Aşağıdaki örnek yanıt, API 'ye geçirilen MPN KIMLIĞI (PGA/PLA) sayısal olmayan bir değer olarak döndürülür.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a>MPN KIMLIĞI veya CSP kiracı KIMLIĞI yok

Aşağıdaki örnek yanıt, API 'ye bir MPN KIMLIĞI (PGA/PLA) veya CSP kiracı KIMLIĞI geçirmedikçe döndürülür. İki KIMLIK türünden birini API 'ye geçirmeniz gerekir.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>MPN KIMLIĞI ve CSP kiracı KIMLIĞI geçildi

Aşağıdaki örnek yanıt, hem MPN KIMLIĞI (PGA/PLA) hem de CSP kiracı KIMLIĞINI API 'ye geçirdiğinizde döndürülür. API 'ye iki tanımlayıcı türünden *yalnızca birini* geçirmeniz gerekir.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP dolaylı Bayi MPN kimliği (PGA/PLA) geçersiz ya da Iş ortağı üyeliği merkezinden Iş Ortağı Merkezi 'ne geçirilmedi

Geçirilen dolaylı satıcı MPN KIMLIĞI (PGA/PLA) geçersiz olduğunda veya Iş ortağı üyeliği merkezinden Iş Ortağı Merkezi 'ne geçirilmediğinde aşağıdaki örnek yanıt döndürülür. [Daha Fazla Bilgi](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP dolaylı sağlayıcı bölgesi ve CSP dolaylı satıcı bölgesi eşleşmiyor

Dolaylı satıcı MPN KIMLIĞI (PGA/PLA) bölgesi dolaylı sağlayıcının bölgesiyle eşleşmediği zaman aşağıdaki örnek yanıt döndürülür. CSP bölgeleri hakkında [daha fazla bilgi edinin](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq) .

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP dolaylı satıcı hesabı Iş Ortağı Merkezi 'nde var, ancak MPA imzasız

Aşağıdaki örnek yanıt, Iş ortağı merkezindeki CSP dolaylı satıcı hesabı MPA 'yı imzaladığı zaman döndürülür. [Daha Fazla Bilgi](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Belirtilen MPN KIMLIĞIYLE ilişkili CSP dolaylı satıcı hesabı yok

Iş Ortağı Merkezi, istekte geçirilen MPN KIMLIĞINI (PGA/PLA) tanıyabileceği halde, belirtilen MPN KIMLIĞI (PGA/PLA) ile ilişkili CSP kaydı yoksa, aşağıdaki örnek yanıt döndürülür. [Daha Fazla Bilgi](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>Geçersiz kiracı KIMLIĞI

Iş Ortağı Merkezi, istekte geçirilen kiracı KIMLIĞIYLE ilişkili herhangi bir hesap bulamadığında aşağıdaki örnek yanıt döndürülür.

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Verilen kiracı KIMLIĞINE sahip bir MPA bulunamadı

Aşağıdaki örnek yanıt, Iş Ortağı Merkezi belirtilen kiracı KIMLIĞINE sahip herhangi bir MPA imzasını bulamadığında döndürülür. [Daha Fazla Bilgi](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```
