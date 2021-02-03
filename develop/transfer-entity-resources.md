---
title: TransferEntity kaynakları
description: Bir müşteri, iş ortağı aboneliğini başka bir iş ortağına aktarmaya istediğinde iş ortağı bir aktarım oluşturur.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96c43d255fcd31e6dc4de50baa0e19f5d8855685
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769220"
---
# <a name="transferentity-resources"></a>TransferEntity kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bir müşteri, iş ortağı aboneliğini başka bir iş ortağına aktarmaya istediğinde iş ortağı bir aktarım oluşturur.

## <a name="transferentity"></a>TransferEntity

Bir transferEntity tanımlar.

| Özellik              | Tür             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | TransferEntity başarıyla oluşturulduktan sonra sağlanan bir transferEntity tanımlayıcısı.                               |
| createdTime           | DateTime         | TransferEntity oluşturulduğu tarih-saat biçiminde. TransferEntity başarıyla oluşturulduktan sonra uygulandı.      |
| Zamanı      | DateTime         | TransferEntity 'ın son güncelleştirilme tarihi, tarih-saat biçiminde. TransferEntity başarıyla oluşturulduktan sonra uygulandı. |
| lastModifiedUser      | string           | Transfer varlığını son güncelleştiren Kullanıcı. TransferEntity başarıyla oluşturulduktan sonra uygulandı.                          |
| customerName          | string           | İsteğe bağlı. Abonelikleri aktarılmakta olan müşterinin adı.                                              |
| Customertenantıd      | string           | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği. TransferEntity başarıyla oluşturulduktan sonra uygulandı.         |
| partnertenantıd       | string           | Ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.                                                                   |
| sourcePartnerName     | string           | İsteğe bağlı. Aktarımı başlatan iş ortağının kuruluşun adı.                                           |
| Sourcepartnertenantıd | string           | Aktarımı başlatan ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.                                           |
| targetPartnerName     | string           | İsteğe bağlı. Aktarımın hedeflediği iş ortağının kuruluşun adı.                                         |
| Targetpartnertenantıd | string           | Aktarımın hedeflediği ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.                                  |
| LineItems             | Nesne dizisi | Bir [Transferlineıtem](#transferlineitem) kaynakları dizisi.                                                   |
| durum                | string           | TransferEntity durumu. Olası değerler şunlardır. "etkin" (silinebilir/gönderilebilir) ve "tamamlandı" (daha önce tamamlanmış). TransferEntity başarıyla oluşturulduktan sonra uygulandı.|

## <a name="transferlineitem"></a>Transferlineıtem

Bir transferEntity içinde bulunan bir öğeyi temsil eder.

| Özellik             | Tür                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Aktarım satırı öğesi için benzersiz bir tanımlayıcı. TransferEntity başarıyla oluşturulduktan sonra uygulandı.   |
| subscriptionId       | string                           | Abonelik tanımlayıcısı.                                                                            |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                    |
| Bilimlingcycle         | Nesne                           | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                   |
| friendlyName         | string                           | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                   |
| partnerIdOnRecord    | string                           | Aktarım kabul edildiğinde gerçekleşen Satınalmadaki iş ortağı kimliği (MPNıD).                 |
| OfferId              | string                           | Teklif tanımlayıcısı.    |
| Addonıtems           | **Transferlineıtem** nesnelerinin listesi | Aktarılmakta olan, aktarılan temel abonelikle birlikte aktarılacak olan bir transferEntity satır öğeleri koleksiyonu. TransferEntity başarıyla oluşturulduktan sonra uygulandı.|
| Transferhatası        | string                           | Bir hata durumunda transferEntity kabul edildikten sonra uygulandı.                |
| durum               | string           | TransferEntity içindeki LineItem 'ın durumu.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Bir aktarım kabul etme sonucunu temsil eder.

| Özellik          | Tür                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| siparişler            | [Sıra](order-resources.md#order) nesnelerinin listesi.    | Siparişlerin koleksiyonu.          |
| transferErrors    | [Transfererror](#transfererror) nesnelerinin listesi.      | Aktarım hataları koleksiyonu. |

## <a name="transfererror"></a>Transferhatası

Bir aktarım kabul edildiğinde oluşan bir hatayı gösterir.

| Özellik          | Tür   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| Transfergroupıd   | string | Hatanın sipariş Grup KIMLIĞI. |
| kod              | int    | Hata kodu.                                 |
| açıklama       | string | Hatanın açıklaması.                   |
| LineItems         | **Transferlineıtem** nesnelerinin listesi | Aktarım hatasının parçası olan bir transferEntity satırı öğeleri koleksiyonu.|

## <a name="transfererrorcode"></a>TransferErrorCode

Bir sıra hatası türünü belirten değerler içeren bir [enum/DotNet/api/System. Enum).

| Değer | Konum | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | İstek bağlamında ortak belirteç yok. |
| Invalidınput | 800002 | Geçersiz istek girişi. |
| ServiceException | 800003 | Beklenmeyen hizmet hatası. |
| InvalidOfferId | 800004 | Geçersiz teklif KIMLIĞI. |
| CreateOrderError | 800005 | Sipariş oluşturma başarılı değil. |
| Mpnıdnotfound | 800015 | MPN kimliği bulunamadı. |
| Notvalidındirectresellermpnıd | 800016 | MPN kimliği geçerli bir dolaylı satıcı değil. |
| Transferıdnotfound | 900100   | Aktarım isteği bulunamadı.   |
| Transfernotallowedıstatusisınprogress | 900101 | Aktarım isteği zaten devam ediyor.|
| Transfernotallowedıstatusıscompleted | 900102 | Aktarım isteği zaten tamamlanmış.|
| TransferCreateOrderError | 900103 | Aktarım sırası başarılı değil.|
| TransferProcessedByAnotherRequest | 900104 | Aktarım, başka bir istek tarafından işleniyor.|