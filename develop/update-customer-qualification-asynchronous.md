---
title: Müşterinin niteliklerini güncelleştirme
description: Profille ilişkili adres da dahil olmak üzere müşterinin niteliklerini zaman uyumsuz olarak güncelleştirir.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 6d46d6a170e4ebcd441e678c482469c4041b2435bf7ee946dc91db554ec4932a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997966"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme

Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirir.

Bir iş ortağı, zaman uyumsuz olarak "eğitim" veya "Hükümentcommunıcloud" olarak bir müşterinin niteliklerini güncelleştirebilir. Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

"Eğitim" için bir müşterinin nitelemesini oluşturmak için, önce nitelik türünü temsil eden bir nesne oluşturun. Ardından, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın. Son olarak, `CreateQualifications()` `CreateQualificationsAsync()` bir giriş parametresi olarak nitelendirme türü nesnesini çağırın.

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project**: sdksamples **sınıfı**: createcustomernitelik. cs

Bir müşterinin nitelemesini, mevcut bir müşteri üzerinde bir nitelik olmadan **Hükümentcommunitycloud** olarak güncelleştirmek için, ortağın ayrıca müşterinin [**validationcode**](utility-resources.md#validationcode)'u içermesi gerekir. İlk olarak, nitelik türünü temsil eden bir nesne oluşturun. Ardından, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın. Son olarak, `CreateQualifications()` ya da `CreateQualificationsAsync()` nitelik türü nesnesini ve doğrulama kodunu giriş parametreleri olarak çağırın.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project**: sdksamples **sınıfı**: CreateCustomerQualificationWithGCC. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/nitelikler? Code = {validationcode} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Nitelemeyi güncelleştirmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür | Gerekli | Açıklama                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | GUID | Yes      | Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir. |
| **validationCode**     | int  | No       | Yalnızca Government Community Cloud için gereklidir.                                                                                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde nitelik nesnesini açıklar.

Özellik | Tür | Gerekli | Açıklama
-------- | ---- | -------- | -----------
Eleme | string | Yes | [**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından dize değeri.

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

Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelikler nesnesi döndürür. **Eğitim** nitelemesini içeren bir müşterinin (önceki bir niteliğe sahip **olmayan)** **gönderme** çağrısının bir örneği aşağıda verilmiştir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

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
