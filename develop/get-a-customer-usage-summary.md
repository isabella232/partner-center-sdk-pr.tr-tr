---
title: Müşterinin aboneliklerinin tümü için Kullanım Özeti alın
description: Müşteri 'nin geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı kullanımını almak için CustomerUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 668176c772ac89cf87189aa00514119340b28963e3abb6ada1717e52536f436b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992628"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>Müşterinin aboneliklerinin tümü için Kullanım Özeti alın

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Müşteri 'nin geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı kullanımını almak için **Customerusagesummary** kaynağını kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

Müşterinin aboneliklerinin tümü için Kullanım Özeti almak üzere:

1. **Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.

2. **Usagesummary** özelliğini çağırın, ardından **Get ()** veya **GetAsync ()** yöntemleri gelir:

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

Bir örnek için aşağıdakilere bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Project: **partnersdk. featuresamples**
- Sınıf: **Getcustomerusagesummary. cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagesummary http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametresi listelenmektedir.

| Ad                   | Tür     | Gerekli | Açıklama                           |
|------------------------|----------|----------|---------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Müşteriye karşılık gelen bir GUID. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir **Customerusagesummary** kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Microsoft Azure için yanıt örneği (MS-azr-0145p) aboneliği

Bu örnekte, müşteri bir **145P Azure PayG** teklifi satın almıştır.

*Microsoft Azure (MS-azr-0145p) aboneliklerine sahip müşteriler için apı yanıtında hiçbir değişiklik olmayacaktır.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a>Azure planına yönelik yanıt örneği

Bu örnekte, müşteri bir Azure planı satın almış.

*Azure planlarına sahip müşteriler için API yanıtında aşağıdaki değişiklikler vardır:*

- **Currencylocale** , **CurrencyCode** ile değiştirilmiştir
- **Usdtotalcost** yeni bir alandır

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
