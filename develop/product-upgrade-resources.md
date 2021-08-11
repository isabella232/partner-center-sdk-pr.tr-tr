---
title: Ürün yükseltme kaynakları
description: Azure planına Iş Ortağı Merkezi ürün yükseltmeleri ile ilgili birden çok kaynak kullanabilirsiniz. Bunlar Productyükselderequest, ProductUpgradesEligibility, ProductUpgradesStatus, Upgradeslineıtem, UpgradeProduct ve ErrorDetails içerir.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a251168dbe1e153365beec212feca6fafddaef1700ad8651ec9d459aebf24600
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997405"
---
# <a name="product-upgrade-resources"></a>Ürün yükseltme kaynakları

bir Microsoft Azure (MS-azr-0145p) aboneliğinden bir Azure planına iş ortağı merkezi ürün yükseltmeleri hakkında bilgi edinmek için aşağıdaki kaynakları kullanabilirsiniz.

## <a name="productupgraderequest"></a>Productyükseltildi Derequest

**Productupgradesrequest** kaynağı, ürün yükseltmeleri istek nesnesi hakkında bilgi sağlar.

| Özellik      | Tür                                                          | Description                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | string                                                        | Müşteriyi tanımlayan GUID biçimli bir dize.      |
| productFamily | string                                                        | Yükseltmenin istendiği ürün ailesi. |
| öznitelikler    | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

**ProductUpgradesEligibility** kaynağı, müşterinin bir ürünü yükseltmekte olan uygunluğu hakkında bilgi sağlar.

| Özellik      | Tür                                                          | Description                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | string                                                        | Müşteriyi tanımlayan GUID biçimli bir dize.                            |
| productFamily | string                                                        | Yükseltmenin istendiği ürün ailesi.                       |
| IBir hal    | bool                                                          | Bool değeri, müşterinin istenen yükseltme için uygun olup olmadığını gösterir. |
| Yükseltme kimliği     | string                                                        | Verilen aile için bir ürün yükseltmesi zaten mevcutsa yükseltme KIMLIĞI.        |
| reason        | string                                                        | Müşterinin ürün yükseltmesine uygun olmadığı neden.                |
| productFamily | string                                                        | Yükseltmenin istendiği ürün ailesi.                       |
| öznitelikler    | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

**Productupgradesstatus** kaynağı bir ürün yükseltmesinin durumu hakkında bilgi sağlar.

| Özellik | Tür   | Description                                          |
|----------|--------|------------------------------------------------------|
| Id       | string | Yükseltmeyi tanımlayan GUID biçimli bir dize. |
| productFamily       | string                                                         | Yükseltmenin istendiği ürün ailesi.
| durum              | string                                                         | Ürün yükseltmenin durumu.
| LineItems           | [Upgradeslineitem](#upgradeslineitem) kaynakları dizisi       | İstek gövdesinin parçası olan her bir satır öğesi için Yükseltme ayrıntılarının bilgilerini sağlayan bir nesne dizisi.
| errorDetails        | [ErrorDetails](#errordetails) kaynağı                         | Yükseltme için hata ayrıntıları istendi.
| öznitelikler          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri. |

## <a name="upgradeslineitem"></a>Upgradeslineıtem

**Upgradeslineıtem** kaynağı, isteğin her bir satır öğesi için ürün yükseltme ayrıntılarının durumunu açıklar.

| Özellik      | Tür                                                          | Description                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | [Upgradeproduct](#upgradeproduct) nesnesi                      | Yükseltilen kaynak ürünün bilgileri. |
| targetProduct | [Upgradeproduct](#upgradeproduct) nesnesi                      | Hedef ürün sonrası yükseltme bilgileri.   |
| Yükseltilebilir Deddate  | UTC Tarih-saat biçiminde dize                                | Aboneliğin yükseltilme tarihi.           |
| durum        | string                                                        | Ürün yükseltmenin durumu.                |
| errorDetails  | [ErrorDetails](#errordetails) kaynağı                        | Yükseltme için hata ayrıntıları istendi.          |
| öznitelikler    | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

**Upgradeproduct** kaynağı, yükseltilmekte olan ürünle ilgili bilgiler sağlar.

| Özellik   | Tür                                                          | Description                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| kimlik         | string                                                        | Ürünü tanımlayan GUID biçimli bir dize. |
| name       | string                                                        | Yükseltilen ürünün kolay adı.         |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                             |

## <a name="errordetails"></a>ErrorDetails

**ErrorDetails kaynağı,** yükseltme işlemi sırasındaki hatalar hakkında ayrıntılar sağlar.

| Özellik   | Tür                                                          | Description                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| kod       | string                                                        | Ürün yükseltmesi başarısız olduğunda hata kodu.      |
| message    | string                                                        | Ürün yükseltmesi başarısız olduğunda hata iletisi. |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                          |
