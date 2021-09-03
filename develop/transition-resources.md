---
title: Geçiş kaynakları
description: Yeni ticari abonelikleri geçiş yapmak için kullanılan kaynakları açıklar.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 44867be3823414ab43957e789c0cd29aef44d956
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457325"
---
# <a name="transition-resources"></a>Geçiş kaynakları

**Uygulandığı Yer**

- İş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetici aracısı

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir.

Yeni bir ticari abonelikten diğerine geçiş yapmak için kullanılan kaynakları açıklar.

## <a name="transitioneliblity"></a>TransitionBlity

Tek bir abonelik geçiş kaynağının davranışını açıklar.

| Özellik          | Tür                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| CatalogItemId | string                  | Denetlenen katalog öğesi kimliği. |
| Başlık  | string                  | SKU başlığı. |
| Description | dize                  | SKU açıklaması. |
| Miktar | tamsayı                 | Satın alınacak yeni teklifin miktarı. |
| Uygunluklar | TransitionEligibilityDetail listesi | Geçiş uygunluğu ayrıntılarının listesi. | 

## <a name="transitioneligibilitydetail"></a>TransitionEligibilityDetail

Tek bir geçiş uygunluğu ayrıntıları kaynağının davranışını açıklar.

| Özellik          | Tür                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| Önemsiz | boolean | Uygunluk geçerli olup olmadığını döndürür. |
| TransitionType | TransitionType | Geçiş türü. Bu, transition_with_license_transfer veya transition_only. |
| Hatalar | TransitionErrors Listesi | Hataya karşılık gelen meta veri öznitelikleri. |

## <a name="transition"></a>Transition

Tek bir abonelik geçiş kaynağının davranışını açıklar.

| Özellik          | Tür                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| FromCatalogItemId | string                  | Katalog öğesi kimliğinden. |
| ToCatalogItemId   | string                  | To catalog item id. |
| ToSubscriptionId  | string                  | To abonelik kimliği. Bu yalnızca abonelik değişirse doldurulur. Şu anda yalnızca Eski Yükseltme bunu gerektirse de modern kısmi geçiş de gerekir. |
| Miktar          | tamsayı                 | Hedef katalog öğesine geçiş yapılan miktar. |
| TransitionType    | string              | Geçiş türü. Olası değerler - transition_only, transition_with_license_transfer.   |
| Ekinlikler            | TransitionEvents listesi | Geçiş olayları. |

## <a name="transitionevent"></a>TransitionEvent

Yükseltmenin gerçekleştirilema nedenini açıklar.

| Özellik          | Tür               | Açıklama                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|------------------------------------------------------------------------------|
| Ad | string | Geçiş olayı adı. Dönüştürme veya LicenseReassignment olası değerleri. |
| Durum | string  | Geçiş olayı durumu. Olası InProgress, Completed veya Failed değerleri.  |
| Timestamp | DateTime | Olayın UTC zaman damgası. |
| Hatalar | TransitionErrors Listesi | Hataya karşılık gelen meta veri öznitelikleri. |

## <a name="transitionerror"></a>TransitionError

Abonelik aktarımı uygunluğuyla ilgili bir hatayı temsil eder. Bir geçişin gerçekleştirilemama nedenini sağlar.

| Özellik          | Tür               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|--------------------------------------------------------------|
| Kod | TransitionErrorCode | Sorunla ilişkili hata kodu. |
| Description | dize  | Hatayı açıklayan kolay metin. |

