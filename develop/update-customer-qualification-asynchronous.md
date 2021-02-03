---
title: Müşterinin niteliklerini güncelleştirme
description: Bir müşterinin niteliklerini, profille ilişkili adres dahil, zaman uyumsuz filtreleme veya diting aracılığıyla güncelleştirmeyi öğrenin.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: e0390e8a9c2a277dcb9e18b026f12625400ae176
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770202"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme

**Uygulama hedefi**

- İş Ortağı Merkezi

Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme hakkında bilgi edinin. Bunu eşzamanlı olarak nasıl yapacağınızı öğrenmek için bkz. [zaman uyumlu doğrulama ile bir müşterinin nitelemesini güncelleştirme](update-customer-qualification-synchronous.md).

Bir iş ortağı, zaman uyumsuz olarak "eğitim" veya "Hükümentcommunıcloud" olarak bir müşterinin niteliklerini güncelleştirebilir. Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

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
| **validationCode**     | int  | No       | Yalnızca kamu Community bulutu için gereklidir.                                                                                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

[**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından tamsayı değeri.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

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

- [Müşterinin niteliklerini al](get-a-customer-s-qualifications.md)
- [İş ortağının doğrulama kodlarını alma](get-a-partner-s-validation-codes.md)