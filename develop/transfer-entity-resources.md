---
title: TransferEntity kaynakları
description: Müşteri, iş ortağıyla olan aboneliğinin başka bir iş ortağına devredsini isterse iş ortağı bir aktarım oluşturur.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 544b9682bb0e1428fad088c818a62492198897b2
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530149"
---
# <a name="transferentity-resources"></a>TransferEntity kaynakları

Müşteri, iş ortağıyla olan aboneliğinin başka bir iş ortağına devredsini isterse iş ortağı bir aktarım oluşturur.

## <a name="transferentity"></a>TransferEntity

transferEntity'i açıklar.

| Özellik              | Tür             | Açıklama                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | transferEntity'nin başarıyla oluşturulmasının ardından sağlanan bir transferEntity tanımlayıcısı.                               |
| createdTime           | DateTime         | transferEntity'nin tarih-saat biçiminde oluşturulma tarihi. transferEntity başarıyla oluşturularak uygulanır.      |
| lastModifiedTime      | DateTime         | transferEntity'nin en son güncelleştirilen tarih-saat biçiminde olduğu tarih. transferEntity başarıyla oluşturularak uygulanır. |
| lastModifiedUser      | string           | transferEntity'i en son güncelleştirilen kullanıcı. transferEntity başarıyla 1.000.000'in oluşturulmasının ardından uygulanır.                          |
| Müşteriadı          | string           | İsteğe bağlı. Abonelikleri aktarılan müşterinin adı.                                              |
| customerTenantId      | string           | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id. transferEntity başarıyla oluşturularak uygulanır.         |
| partnertenantid       | string           | İş ortağını tanımlayan GUID biçimlendirilmiş iş ortağı kimliği.                                                                   |
| sourcePartnerName     | string           | İsteğe bağlı. Aktarımı başlatan iş ortağının kuruluş adı.                                           |
| sourcePartnerTenantId | string           | Aktarımı başlatan iş ortağını tanımlayan GUID biçimli iş ortağı kimliği.                                           |
| targetPartnerName     | string           | İsteğe bağlı. Aktarımın hedeflen olduğu iş ortağının kuruluş adı.                                         |
| targetPartnerTenantId | string           | Aktarımın hedeflene iş ortağını tanımlayan GUID biçimli iş ortağı kimliği.                                  |
| lineItems             | Nesne dizisi | [TransferLineItem kaynakları](#transferlineitem) dizisi.                                                   |
| durum                | string           | transferEntity durumu. Olası değerler "Etkin" (silinebilir/gönderebilirsiniz) ve "Tamamlandı" (zaten tamamlandı) değerleridir. transferEntity başarıyla oluşturularak uygulanır.|

## <a name="transferlineitem"></a>TransferLineItem

transferEntity içinde yer alan bir öğeyi temsil eder.

| Özellik             | Tür                             | Açıklama                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Aktarım satırı öğesi için benzersiz tanımlayıcı. transferEntity başarıyla oluşturularak uygulanır.   |
| subscriptionId       | string                           | Abonelik tanımlayıcısı.                                                                            |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                    |
| billingCycle         | Nesne                           | Geçerli dönem için ayarlanmış faturalama dönemi türü.                                                   |
| Friendlyname         | string                           | İsteğe bağlı. Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                   |
| partnerIdOnRecord    | string                           | Aktarım kabul edilirken yapılan satın almada Kayıtta PartnerId (MPNID).                 |
| offerId              | string                           | Teklif tanımlayıcısı.    |
| addonItems           | **TransferLineItem nesnelerinin** listesi | Aktarılan temel abonelikle birlikte aktaracak eklentiler için transferEntity satır öğeleri koleksiyonu. transferEntity başarıyla oluşturularak uygulanır.|
| transferError        | string                           | Hata durumunda transferEntity kabul edildikten sonra uygulanır.                |
| durum               | string           | transferEntity'de lineitem durumu.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Aktarım kabul etme sonucu temsil eder.

| Özellik          | Tür                                                  | Açıklama                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| siparişler            | [Sıra](order-resources.md#order) nesnelerinin listesi.    | Siparişlerin koleksiyonu.          |
| transferErrors    | [Transfererror](#transfererror) nesnelerinin listesi.      | Aktarım hataları koleksiyonu. |

## <a name="transfererror"></a>Transferhatası

Bir aktarım kabul edildiğinde oluşan bir hatayı gösterir.

| Özellik          | Tür   | Açıklama                                     |
|-------------------|--------|-------------------------------------------------|
| Transfergroupıd   | string | Hatanın sipariş Grup KIMLIĞI. |
| kod              | int    | Hata kodu.                                 |
| açıklama       | string | Hatanın açıklaması.                   |
| LineItems         | **Transferlineıtem** nesnelerinin listesi | Aktarım hatasının parçası olan bir transferEntity satırı öğeleri koleksiyonu.|

## <a name="transfererrorcode"></a>TransferErrorCode

Bir sıra hatası türünü belirten değerler içeren bir [enum/DotNet/api/System. Enum).

| Değer | Konum | Açıklama |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | İstek bağlamında ortak belirteç yok. |
| Invalidınput | 800002 | Geçersiz istek girişi. |
| ServiceException | 800003 | Beklenmeyen hizmet hatası. |
| InvalidOfferId | 800004 | Geçersiz teklif KIMLIĞI. |
| CreateOrderError | 800005 | Sipariş oluşturma başarılı değil. |
| Mpnıdnotfound | 800015 | MPN KIMLIĞI bulunamadı. |
| Notvalidındirectresellermpnıd | 800016 | MPN KIMLIĞI geçerli bir dolaylı satıcı değil. |
| Transferıdnotfound | 900100   | Aktarım isteği bulunamadı.   |
| Transfernotallowedıstatusisınprogress | 900101 | Aktarım isteği zaten devam ediyor.|
| Transfernotallowedıstatusıscompleted | 900102 | Aktarım isteği zaten tamamlanmış.|
| TransferCreateOrderError | 900103 | Aktarım sırası başarılı değil.|
| TransferProcessedByAnotherRequest | 900104 | Aktarım, başka bir istek tarafından işleniyor.|