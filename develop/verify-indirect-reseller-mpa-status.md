---
title: Dolaylı satıcının kurumsal bayinin Microsoft İş Ortağı Sözleşmesi durumunu doğrulama
description: AgreementStatus API'sini kullanarak dolaylı bir kurumsal bayinin sözleşmeyi Microsoft İş Ortağı Sözleşmesi.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 517c99356a4b623b5b46bc3d33f2355cd569f97326e7d9596cff551329d10da7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989857"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Dolaylı satıcının kurumsal bayinin Microsoft İş Ortağı Sözleşmesi durumunu doğrulama

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi için Microsoft Cloud for US Government

Dolaylı bir kurumsal bayinin Microsoft İş Ortağı Sözleşmesi (MPN) Microsoft İş Ortağı Ağı (PGA/PLA) veya Bulut Çözümü Sağlayıcısı (CSP) kiracı kimliğini (Microsoft Kimliği) kullanarak Bulut Çözümü Sağlayıcısı imzaladığı doğrulanabilirsiniz. **AgreementStatus** API'sini kullanarak imzalama durumunu Microsoft İş Ortağı Sözleşmesi bu tanımlayıcılardan birini kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Dolaylı kurumsal bayinin MPN Kimliği (PGA/PLA) veya CSP kiracı kimliği (Microsoft Kimliği). *Bu iki tanımlayıcıdan birini kullan gerekir.*

## <a name="c"></a>C\#

Dolaylı satıcının Microsoft İş Ortağı Sözleşmesi durumunu almak için:

1. **AgreementSignatureStatus** **özelliğini aramak için IAggregatePartner.Compliance** koleksiyonu kullanın.

2. [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) [**GetAsync() yöntemini**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) çağırma.

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Örnek: **[Konsol test uygulaması](console-test-app.md)**
- Project: **PartnerCenterSDK.FeaturesSamples**
- Sınıf: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si |
| ------ | ----------- |
| **Al** | *[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>URI parametreleri

İş ortağını tanımlamak için aşağıdaki iki sorgu parametresini belirtebilirsiniz. Bu iki sorgu parametresini sağlayamazsanız **400 (Hatalı istek) hatası** alırsınız.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | No | Dolaylı Microsoft İş Ortağı Ağı tanımlayan bir kimlik (PGA/PLA). |
| **TenantId** | GUID | No | Dolaylı kurumsal bayinin CSP hesabını tanımlayan bir Microsoft kimliği. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. REST İş Ortağı Merkezi.](headers.md)

### <a name="request-examples"></a>İstek örnekleri

#### <a name="request-using-mpn-id-pgapla"></a>MPN Kimliği (PGA/PLA) kullanarak istek

Aşağıdaki örnek istek, dolaylı kurumsal bayinin Microsoft İş Ortağı Sözleşmesi kimliğini kullanarak dolaylı kurumsal bayinin Microsoft İş Ortağı Ağı alır.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>CSP kiracı kimliğini kullanarak istekte

Aşağıdaki örnek istek dolaylı kurumsal bayinin CSP kiracı Microsoft İş Ortağı Sözleşmesi (Microsoft Kimliği) kullanarak dolaylı kurumsal bayinin oturum açma durumunu alır.

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

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hatası.](error-codes.md)

### <a name="response-example-success"></a>Yanıt örneği (başarılı)

Aşağıdaki örnek yanıt, dolaylı kurumsal bayinin kurumsal bayiyi Microsoft İş Ortağı Sözleşmesi.

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

Dolaylı kurumsal bayinin iş ortağının imzalama durumu döndürülene Microsoft İş Ortağı Sözleşmesi gibi yanıtlar alabilirsiniz.

#### <a name="non-guid-formatted-csp-tenant-id"></a>GUID biçimlendirilmeyen CSP kiracı kimliği

API'ye aktardınız CSP kiracı kimliği GUID değilse aşağıdaki örnek yanıt döndürülür.

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

#### <a name="non-numeric-mpn-id"></a>Sayısal olmayan MPN Kimliği

API'ye aktardınız MPN Kimliği (PGA/PLA) sayısal olmayan olduğunda aşağıdaki örnek yanıt döndürülür.

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>MPN Kimliği veya CSP kiracı kimliği yok

API'ye BIR MPN Kimliği (PGA/PLA) veya CSP kiracı kimliği geçirip geçirip alamamadan aşağıdaki örnek yanıt döndürülür. api'ye iki kimlik türlerinden birini geçmeniz gerekir.

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Hem MPN Kimliği hem de CSP kiracı kimliği geçirildi

API'ye hem MPN Kimliği (PGA/PLA) hem de CSP kiracı kimliğini iletirken aşağıdaki örnek yanıt döndürülür. *API'ye iki tanımlayıcı* türlerinden yalnızca birini geçmelisiniz.

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP Indirect Reseller MPN Kimliği (PGA/PLA) geçersiz veya Partner Membership Center İş Ortağı Merkezi

Dolaylı kurumsal bayi MPN Kimliği (PGA/PLA) geçirilirse veya bu değer bir satıcıdan Partner Membership Center geçirilmezse aşağıdaki İş Ortağı Merkezi. [Daha Fazla Bilgi](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP Indirect Provider bölge CSP Indirect Reseller bölge eşle

Dolaylı kurumsal bayi MPN kimliği (PGA/PLA) bölgesi Dolaylı Sağlayıcının bölgesiyle eşleşmezse aşağıdaki örnek yanıt döndürülür. CSP [Bölgeleri](/partner-center/mpa-indirect-provider-faq) hakkında daha fazla bilgi.

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP Indirect Reseller hesabı İş Ortağı Merkezi MPA'yı imzalamadı

MPA'yı imzalamamış CSP Indirect Reseller aşağıdaki İş Ortağı Merkezi yanıt döndürülür. [Daha Fazla Bilgi](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Belirli CSP Indirect Reseller MPN kimliğiyle ilişkili bir hesap yok

İstekte geçirilen MPN İş Ortağı Merkezi (PGA/PLA) tanıyamıyorum ama verilen MPN kimliğiyle (PGA/PLA) ilişkili CSP kaydı yok olduğunda aşağıdaki örnek yanıt döndürülür. [Daha Fazla Bilgi](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="invalid-tenant-id"></a>Geçersiz Kiracı Kimliği

Aşağıdaki örnek yanıt, istekte İş Ortağı Merkezi kiracı kimliğiyle ilişkili bir hesap bulmazsa döndürülür.

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Verilen Kiracı Kimliği ile MPA bulunamadı

Aşağıdaki örnek yanıt, İş Ortağı Merkezi kiracı kimliğine sahip herhangi bir MPA imzası bulamayarak döndürülür. [Daha Fazla Bilgi](/partner-center/mpa-indirect-provider-faq)

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