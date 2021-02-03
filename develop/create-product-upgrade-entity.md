---
title: Müşteri için ürün yükseltme varlığı oluşturma
description: Bir müşteriyi belirli bir ürün ailesine yükseltmek üzere ürün yükseltme varlığı oluşturmak için Productyükselderequest kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768813"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Müşteri için ürün yükseltme varlığı oluşturma

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bir müşteriyi, **Productyükselderequest** kaynağını kullanarak belirli bir ürün ailesine (örneğin, Azure planı) yükseltmek için bir ürün yükseltme varlığı oluşturabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler. Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Müşteriyi yükseltmek istediğiniz ürün ailesi.

## <a name="c"></a>C\#

Bir müşteriyi Azure planına yükseltmek için:

1. **Productupgradesrequest** nesnesi oluşturun ve ürün ailesi olarak müşteri tanımlayıcısını ve "Azure" i belirtin.

2. **Iaggregatepartner. Productyükseltmeleri** koleksiyonunu kullanın.

3. **Create** metodunu çağırın ve bir **konum üst bilgi** dizesi döndürecek **productupgradesrequest** nesnesini geçirin.

4. Yükseltme [durumunu sorgulamak](get-product-upgrade-status.md)için kullanılabilecek konum üst bilgisi dizesinden **Upgrade-ID** ' i ayıklayın.

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/productyükseltmeleri http/1.1 |

#### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

#### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [Productyükseltilebilir Derequest](product-upgrade-resources.md#productupgraderequest) kaynağı içermelidir.

#### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt ürün yükseltme durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir. Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
