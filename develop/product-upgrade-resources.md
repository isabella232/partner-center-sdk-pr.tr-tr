---
title: Ürün yükseltme kaynakları
description: Bir Azure planına ürün yükseltmesi İş Ortağı Merkezi birden çok kaynak kullanabilirsiniz. Bunlar ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct ve ErrorDetails'tir.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c995ac44dbe22000f7bc86991cb973ed31a5c018
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445349"
---
# <a name="product-upgrade-resources"></a>Ürün yükseltme kaynakları

Bir İş Ortağı Merkezi Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına yapılan ürün yükseltmeleri hakkında bilgi için aşağıdaki kaynakları kullanabilirsiniz.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

**ProductUpgradesRequest** kaynağı, ürün yükseltme isteği nesnesi hakkında bilgi sağlar.

| Özellik      | Tür                                                          | Açıklama                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | string                                                        | Müşteriyi tanımlayan GUID biçimli bir dize.      |
| productFamily | string                                                        | Yükseltmenin isten olduğu ürün ailesi. |
| öznitelikler    | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

**ProductUpgradesEligibility** kaynağı, müşterinin bir ürünü yükseltmeye uygunluğu hakkında bilgi sağlar.

| Özellik      | Tür                                                          | Açıklama                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | string                                                        | Müşteriyi tanımlayan GUID biçimli bir dize.                            |
| productFamily | string                                                        | Yükseltmenin isten olduğu ürün ailesi.                       |
| isEligible    | bool                                                          | Bool değeri müşterinin istenen yükseltme için uygun olup olmadığını gösterir. |
| upgradeId     | string                                                        | Verilen aile için bir ürün yükseltmesi zaten varsa yükseltme kimliği.        |
| reason        | string                                                        | Müşterinin ürün yükseltmesi için uygun olmadığının nedeni.                |
| productFamily | string                                                        | Yükseltmenin isten olduğu ürün ailesi.                       |
| öznitelikler    | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

**ProductUpgradesStatus** kaynağı, ürün yükseltme durumu hakkında bilgi sağlar.

| Özellik | Tür   | Açıklama                                          |
|----------|--------|------------------------------------------------------|
| Id       | string | Yükseltmeyi tanımlayan GUID biçimli bir dize. |
| productFamily       | string                                                         | Yükseltmenin isten olduğu ürün ailesi.
| durum              | string                                                         | Ürün yükseltme durumu.
| lineItems           | [UpgradesLineItem kaynakları](#upgradeslineitem) dizisi       | İstek gövdesinin parçası olan her satır öğesi için yükseltme ayrıntılarıyla ilgili bilgi sağlayan bir nesne dizisi.
| errorDetails        | [ErrorDetails](#errordetails) kaynağı                         | İstenen yükseltme için hata ayrıntıları.
| öznitelikler          | [Resourceattributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

**UpgradesLineItem kaynağı,** isteğin her satır öğesi için ürün yükseltme ayrıntılarının durumunu açıklar.

| Özellik      | Tür                                                          | Açıklama                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | [UpgradeProduct](#upgradeproduct) nesnesi                      | Yükseltilen kaynak ürünle ilgili bilgiler. |
| targetProduct | [UpgradeProduct](#upgradeproduct) nesnesi                      | Yükseltme sonrası hedef ürünle ilgili bilgiler.   |
| upgradedDate  | UTC tarih-saat biçiminde dize                                | Aboneliğin yükseltil olduğu tarih.           |
| durum        | string                                                        | Ürün yükseltme durumu.                |
| errorDetails  | [ErrorDetails](#errordetails) kaynağı                        | İstenen yükseltme için hata ayrıntıları.          |
| öznitelikler    | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

**UpgradeProduct kaynağı** yükseltilen ürün hakkında bilgi sağlar.

| Özellik   | Tür                                                          | Açıklama                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| kimlik         | string                                                        | Ürünü tanımlayan GUID biçimli bir dize. |
| name       | string                                                        | Yükseltilen ürünün kolay adı.         |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                             |

## <a name="errordetails"></a>ErrorDetails

**ErrorDetails kaynağı,** yükseltme işlemi sırasındaki hatalar hakkında ayrıntılar sağlar.

| Özellik   | Tür                                                          | Açıklama                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| kod       | string                                                        | Ürün yükseltmesi başarısız olduğunda hata kodu.      |
| message    | string                                                        | Ürün yükseltmesi başarısız olduğunda hata iletisi. |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                          |
