---
title: Müşterinin yeterliliğini güncelleştirme
description: Bir müşterinin niteliklerini, profille ilişkili adres da dahil, zaman uyumlu filtreleme veya dikele aracılığıyla güncelleştirme hakkında bilgi edinin.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 0ffe6d1a236a8a07e1ff71163e7639ef1f3437e1
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030598"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Zaman uyumlu doğrulama ile bir müşterinin nitelemesini güncelleştirme

**Uygulama hedefi**

- İş Ortağı Merkezi

Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin niteliklerini zaman uyumlu olarak güncelleştirme hakkında bilgi edinin. Bunu zaman uyumsuz yapmayı öğrenmek için bkz. [bir müşterinin nitelemesini zaman uyumsuz doğrulama aracılığıyla güncelleştirme](update-customer-qualification-asynchronous.md).

Bir iş ortağı, bir müşterinin nitelemesini "eğitim" veya "kamu bulutu" olacak şekilde güncelleştirebilir. Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

Bir müşterinin nitelemesini "eğitim" olarak güncelleştirmek için mevcut bir [**müşterinin**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) **[Update/DotNet/api/Microsoft. Store. partnercenter. nitelik. ıcustomernitelik. Update)** öğesini çağırın.

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Partnersdk. Featuresamples **sınıfı**: CustomerQualificationOperations. cs

Bir müşterinin nitelemesini, mevcut bir müşteri üzerinde bir nitelik olmadan **Hükümentcommunitycloud** olarak güncelleştirmek için, ortağın müşterinin [**validationcode**](utility-resources.md#validationcode)'u içermesi gerekir.

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/nitelendirme? Code = {validationcode} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Nitelemeyi güncelleştirmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür | Gerekli | Açıklama                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | GUID | Yes      | Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir. |
| **validationCode**     | int  | No       | Yalnızca kamu Community bulutu için gereklidir.                                                                                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

[**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından tamsayı değeri.

### <a name="request-example"></a>İstek örneği

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>İlgili makaleler:

- [Müşterinin nitelemesini alma](./get-customer-qualification-synchronous.md)
- [İş ortağının doğrulama kodlarını alma](get-a-partner-s-validation-codes.md)
