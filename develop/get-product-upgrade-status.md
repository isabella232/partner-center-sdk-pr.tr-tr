---
title: Müşterinin ürün yükseltme durumunu al
description: ProductUpgradeRequest kaynağını kullanarak müşterinin yeni bir ürün ailesine (örneğin, bir Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına ürün yükseltme durumunu tespit edebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e33ac61d77fc4e14ff6f7801e2c15a968cf9f1a667087df612c0f76b216f891a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995756"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Müşterinin ürün yükseltme durumunu al

Yeni bir ürün ailesine yükseltme durumunu almak için [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanabilirsiniz. Bu kaynak, bir müşteriyi Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına yükseltirken geçerlidir. Başarılı bir istek [**ProductUpgradesEligibility kaynağını**](product-upgrade-resources.md#productupgradeseligibility) döndürür.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler. [Uygulama+Kullanıcı kimlik doğrulamasını](enable-secure-app-model.md) farklı API'lerle kullanırken güvenli İş Ortağı Merkezi izleyin.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Ürün ailesi.

- Yükseltme isteğinin upgrade-id.

## <a name="c"></a>C\#

Bir müşterinin Azure planına yükseltmeye uygun olup olduğunu kontrol etmek için:

1. Bir **ProductUpgradesRequest nesnesi** oluşturun ve müşteri tanımlayıcısını ve ürün ailesi olarak "Azure" belirtin.

2. **IAggregatePartner.ProductUpgrades koleksiyonunu** kullanın.

3. **ById yöntemini** çağırın ve **upgrade-id girin.**

4. **CheckStatus** yöntemini çağırarak **ProductUpgradesRequest** nesnesini **(productUpgradeStatus** nesnesi) iade eder.

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si |
|----------|-----------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Ürün yükseltme durumunu almak istediğiniz müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad               | Tür | Gerekli | Açıklama                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **upgrade-id** | GUID | Yes | Değer, GUID biçimli bir yükseltme tanımlayıcısıdır. bu tanımlayıcıyı, izılacak bir yükseltme belirtmek için kullanabilirsiniz. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [**ProductUpgradeRequest kaynağı içermeli.**](product-upgrade-resources.md#productupgraderequest)

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem gövdede [**bir ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
