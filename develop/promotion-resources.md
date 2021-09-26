---
title: Yükseltme kaynakları
description: Yeni ticari abonelikler için işlemlere uygulanan promosyonların kaynaklarını açıklar.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6a0b38576f5756a127fe6ba787f970db9ac59be3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716013"
---
# <a name="promotions-resources"></a>Yükseltme kaynakları

**Uygulandığı Yer**

- İş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetici aracısı

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca Microsoft 365 ve Dynamics 365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortakları tarafından kullanılabilir.

Yeni ticari abonelikler için işlemlere uygulanan promosyonların kaynaklarını açıklar.

## <a name="promotion"></a>Promosyon

Uygunluk ölçütleri karşılandı ise ürün SKU'su satın alırken uygulanan indirim.

| Özellik          | Tür                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| kimlik | string                  | Yükseltme tanımlayıcısı. |
| name | string                  | Yükseltmenin kolay adı. |
| açıklama | string                  | Yükseltmenin açıklaması. |
| Startdate | string | Yükseltmenin geçerli olduğu başlangıç tarihi. |
| Bitiştarihi | string  | Yükseltmenin geçerli olduğu bitiş tarihi. |
| requiredProducts | requiredProducts listesi | Promosyon için geçerli olan ürün, SKU ayrıntıları ve fiyatlandırma ilkeleri. | 
| properties | özellik listesi | Yükseltmenin otomatik olarak uygulanabilir olup olmadığı da dahil olmak üzere yükseltmenin özellikleri. | 

## <a name="requiredproducts"></a>RequiredProducts

Promosyon için geçerli olan ürün, SKU ayrıntıları ve fiyatlandırma ilkeleri.

| Özellik          | Tür                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| string | Yükseltmenin kullanılabilir olduğu ürünün tanımlayıcısı. |
| skuId | string | Yükseltmenin kullanılabilir olduğu SKU'nun tanımlayıcısı. |
| terimi | Süre | Promosyon için kullanılabilir olan süre ve faturalama döngüsü de dahil olmak üzere bir süre. |
| pricingPolicies| pricingPolicies listesi | Promosyon indirimi türlerini ve değerlerini tanımlayan ilkelerin listesi. |

## <a name="term"></a>Süre

Promosyon satın alınarak satın alına bir dönemi temsil eder.

| Özellik          | Tür                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| süre          | string                  | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler P1M (bir ay), P1Y (bir yıl) ve P3Y (üç yıl) değerleridir. 
| billingCycle      | string | Yükseltmenin faturalamaya ne sıklıkta uygulan olacağını açıklar. Değerler Aylık, Yıllık, OneTime veya Bilinmeyen değerlerini içerebilir. | 

## <a name="pricingpolicies"></a>PricingPolicies

Promosyon indirimi türlerini ve değerlerini açıklama.

| Özellik          | Tür               | Description                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| tür | string | İndirimin yüzdelere mi yoksa sabit fiyat indirimlerine mi bağlı olduğunu açıklama. |
| değer | string  | Uygulanan indirim miktarını tanımlar. |

## <a name="properties"></a>Özellikler

Yükseltmenin özellikleri.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| isAutoApplicable  | bool  | Yükseltmenin otomatik olarak uygulanıp uygulanmay olmadığını veya iş ortağı tarafından geçirip geçirilemayacaklarını gösterir. |


## <a name="promotioneligibilitiesrequestitem"></a>PromotionEligibilitiesRequestItem

Bir işlemi ve yükseltmenin uygunluğunu temsil eden özellikler.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| kimlik | int| Yükseltmelere uygunluk öğe tanımlayıcısı. |
| catalogItemId | string | Yükseltmenin uygulanacak katalog öğesi tanımlayıcısı. Ürün kimliğini, SKU kimliğini ve kullanılabilirlik kimliğini içerir. |
| miktar | int | Lisans veya örnek sayısı. |
| termDuration | string | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler P1M (bir ay), P1Y (bir yıl) ve P3Y (üç yıl). |
| Bilimlingcycle | string | Yükseltmenin faturalandırmaya ne sıklıkta uygulanacağını açıklar. Değerler aylık, yıllık, OneTime veya Unknown içerebilir. | 
| Promotionıd | string | Yükseltme tanımlayıcısı. |

## <a name="promotioneligibilities"></a>Promotioneligılıklara

Ürünlerin, SKU 'Ların ve promosyon eliklerinden oluşan bir liste.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| kimlik | int| Promosyonlar öğe tanımlayıcısı. |
| Catalogıtemıd | string | Yükseltmenin uygulanacağı Katalog öğesi tanımlayıcısı. Ürün KIMLIĞI, SKU KIMLIĞI ve kullanılabilirlik KIMLIĞINI içerir. |
| miktar | int | Lisans veya örnek sayısı. |
| termDuration | string | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler P1M (bir ay), P1Y (bir yıl) ve P3Y (üç yıl). |
| Bilimlingcycle | string | Yükseltmenin faturalandırmaya ne sıklıkta uygulanacağını açıklar. Değerler aylık, yıllık, OneTime veya Unknown içerebilir. | 
| eligilıklara | Promotioneligılıklara listesi | Promosyon uygunluk sonuçlarının listesini temsil eder. |

## <a name="promotioneligibility"></a>Promotionuygunluğu

Ürünlerin, SKU 'Ların ve promosyon eliklerinden oluşan bir liste.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| Promotionıd | string | Yükseltme tanımlayıcısı. |
| IBir hal | bool | Yükseltmenin verilen uygunluk isteği öğesine uygun olup olmadığını açıklar. |
| hatalar | PromotionEligibilityErrors listesi | Bir promosyon isteğiniz öğe için neden uygun olmayan bir şekilde hata oluştu. | 

## <a name="promotioneligibilityerror"></a>PromotionEligibilityError

Bir promosyon uygunluğu istek öğesinin neden uygun olmadığı açıklanmaktadır. 

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| tür | string | Yükseltme uygunluğu hata türleri ınvalidcatalogıtemıd, ınvalidpromosyonu, PrerequisiteProductOwnership, Mptionlimit, SeatCount, OfferPurchasedPreviously veya Term içerebilir. |
| açıklama | string | Yükseltmenin verilen uygunluk isteği öğesine uygun olup olmadığını açıklar. |

## <a name="redemptionlimitpromotioneligibilityerror"></a>RedemptionLimitPromotionEligibilityError

Kullanım sınırının neden aşıldığına ilişkin ayrıntıları içerir.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| Maxpromotiono Mptioncount | int | Bir yükseltmenin en fazla kaç kez elde edilebilir. |
| remainingPromotionRedemptionCount| int | Bir yükseltmenin elde edilebilir kalan sayısı. |

## <a name="seatcountpromotioneligibilityerror"></a>SeatCountPromotionEligibilityError

Bilgisayar sayısı sınırının neden aşıldığına ilişkin ayrıntıları içerir. Her iki değer de null olabilir.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| Minimumrequiredkoltuk | 'tir? | Bir yükseltmenin destekleyeceği en düşük lisans. |
| Maximumrequiredkoltuk | 'tir? | Bir yükseltmenin destekleyeceği maksimum lisans. |

## <a name="termpromotioneligibilityerror"></a>TermPromotionEligibilityError

Yükseltme koşulunun neden kabul edilmediğini içeren ayrıntıları içerir.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| eligibleTerms | PromotionTerm | Bir yükseltmenin destekleyeceği uygun koşullar. |

## <a name="promotionterm"></a>PromotionTerm

Bilgisayar sayısı sınırının neden aşıldığına ilişkin ayrıntıları içerir.

| Özellik          | Tür               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| Bilimlingcycle | string | Yükseltmenin faturalandırmaya ne sıklıkta uygulanacağını açıklar. Değerler aylık, yıllık, OneTime veya Unknown içerebilir. |
| süre | string | Satın alınan dönem süresi. |




