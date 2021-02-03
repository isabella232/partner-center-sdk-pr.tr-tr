---
title: Müşterinin bir Azure planına yükseltmeye uygunluğunu denetleme
description: Bir müşterinin bir Microsoft Azure (MS-AZR-0145P) aboneliğinden bir Azure planına yükseltme için uygun olup olmadığını öğrenmek üzere Productyükselderequest kaynağını kullanarak bir ProductUpgradesEligibility kaynağı döndürebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768723"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Müşterinin bir Azure planına yükseltmeye uygunluğunu denetleme

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bir müşterinin bir Microsoft Azure (MS-AZR-0145P) aboneliğinden bir Azure planına yükseltme için uygun olup olmadığını denetlemek için [**productyükseltileequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanabilirsiniz. Bu yöntem, müşterinin ürün yükseltme uygunluğuyla bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler. Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Ürün ailesi.

## <a name="c"></a>C\#

Müşterinin Azure planına yükseltmeye uygun olup olmadığını denetlemek için:

1. **Productupgradesrequest** nesnesi oluşturun ve ürün ailesi olarak müşteri tanımlayıcısını ve "Azure" i belirtin.

2. **Iaggregatepartner. Productyükseltmeleri** koleksiyonunu kullanın.
3. **CheckEligibility** yöntemini çağırın ve bir **ProductUpgradesEligibility** nesnesi döndüren **productupgradesrequest** nesnesini geçirin.

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/productupgrades/uygunluk http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [**Productyükseltilebilir Derequest**](product-upgrade-resources.md#productupgraderequest) kaynağı içermelidir.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
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
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem gövdede bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
