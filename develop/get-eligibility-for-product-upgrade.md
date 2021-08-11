---
title: Azure planına yükseltme için müşterinin uygunluğunu denetleme
description: ProductUpgradeRequest kaynağını kullanarak bir Müşterinin bir Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına yükseltmeye uygun olup olmadığını belirlemek üzere bir ProductUpgradesEligibility kaynağı iade edebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a72a9f2f3909ac4b3b74754b58a8d8d4745fbb2cadd101ad18cf487b1b02267a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996044"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Azure planına yükseltme için müşterinin uygunluğunu denetleme

[**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanarak müşterinin bir Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına yükseltmeye uygun olup oluğunu kontrol edebilirsiniz. Bu yöntem müşterinin ürün yükseltme uygunluğuyla [**bir ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler. [Uygulama+Kullanıcı kimlik doğrulamasını](enable-secure-app-model.md) farklı API'lerle kullanırken güvenli İş Ortağı Merkezi izleyin.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Ürün ailesi.

## <a name="c"></a>C\#

Bir müşterinin Azure planına yükseltmeye uygun olup olduğunu kontrol etmek için:

1. Bir **ProductUpgradesRequest nesnesi** oluşturun ve müşteri tanımlayıcısını ve ürün ailesi olarak "Azure" belirtin.

2. **IAggregatePartner.ProductUpgrades koleksiyonunu** kullanın.
3. **CheckEligibility yöntemini** çağırarak **Bir ProductUpgradesEligibility nesnesi dönecek ProductUpgradesRequest** **nesnesini** iletir.

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

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/uygunluk HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [**ProductUpgradeRequest kaynağı içermeli.**](product-upgrade-resources.md#productupgraderequest)

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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
