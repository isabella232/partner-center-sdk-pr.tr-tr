---
title: Müşterinin niteliklerini güncelleştirme
description: Profille ilişkili adres de dahil olmak üzere müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572106"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme

Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme.

bir iş ortağı müşterinin niteliklerini zaman uyumsuz olarak "Eğitim" veya "GovernmentCocloud" olacak şekilde güncelleştirin. "Hiçbiri" ve "Kar Amacı Gütmeyen" gibi diğer değerler ayarlanabilir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi menüsünden **CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Müşterinin "Eğitim" niteliğini oluşturmak için önce nitelik türünü temsil eden bir nesne oluşturun. Ardından, [**müşteri tanımlayıcısıyla IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından Bir [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**Nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın. Son olarak, `CreateQualifications()` giriş `CreateQualificationsAsync()` parametresi olarak nite türü nesnesiyle veya çağrısında bulundurabilirsiniz.

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Örnek:** [Konsol Örnek Uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples **Sınıfı:** CreateCustomerQualification.cs

Bir müşterinin yeterliliği olmayan mevcut bir müşteride **KamuCocloud** niteliğini güncelleştirmek için iş ortağının müşterinin ValidationCode kodunu da [**içermesi gerekir.**](utility-resources.md#validationcode) İlk olarak, nitelik türünü temsil eden bir nesne oluşturun. Ardından, [**müşteri tanımlayıcısıyla IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından Bir [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**Nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın. Son olarak, `CreateQualifications()` nitelik `CreateQualificationsAsync()` türü nesnesiyle veya çağrısı ve giriş parametreleri olarak doğrulama kodu.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Örnek:** [Konsol Örnek Uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples **Sınıfı:** CreateCustomerQualificationWithGCC.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Niteliği güncelleştirmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür | Gerekli | Açıklama                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | GUID | Yes      | Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |
| **validationCode**     | int  | No       | Yalnızca Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinin nitelik nesnesini açıklar.

Özellik | Tür | Gerekli | Açıklama
-------- | ---- | -------- | -----------
Eleme | string | Yes | [**CustomerQualification enum değerinden dize**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) değeri.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelik nesnesi döndürür. Aşağıda, Eğitim niteliğine sahip bir müşteriyle ilgili **POST** çağrısının bir örneği (daha önce **Yok** niteliğine sahip) **verilmiştir.**

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>İlgili makaleler:

- [Müşterinin niteliklerini al](./get-customer-qualification-asynchronous.md)
- [İş ortağının doğrulama kodlarını alma](get-a-partner-s-validation-codes.md)
