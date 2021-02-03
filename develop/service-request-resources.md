---
title: Hizmet isteği kaynakları
description: İş ortakları, Microsoft tarafından sağlanan kesintiler hizmetlerini raporlamak veya sağlanamadığı diğer teknik destek istemek için iş ortakları adına hizmet isteklerini dosya halinde işleyebilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 072f9eddaf9d854f1dcc8cc65f7928b6c95700fa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768926"
---
# <a name="service-request-resources"></a>Hizmet isteği kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

İş ortakları, Microsoft tarafından sağlanan kesintiler hizmetlerini raporlamak veya sağlanamadığı diğer teknik destek istemek için iş ortakları adına hizmet isteklerini dosya halinde işleyebilir.

## <a name="servicerequest"></a>ServiceRequest

Bu isteğin ilerme şekli dahil, bir iş ortağı tarafından dosyalanmış bir hizmet isteğini açıklar.

| Özellik         | Tür                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Başlık            | string                                                        | Hizmet isteği başlığı.                                                           |
| Description      | dize                                                        | Açıklama.                                                                     |
| Önem derecesi         | string                                                        | Önem derecesi: "bilinmiyor", "kritik", "Orta" veya "minimal".                       |
| Supporttopicıd   | string                                                        | Destek konusunun kimliği.                                                         |
| SupportTopicName | string                                                        | Destek konusunun adı.                                                       |
| Id               | string                                                        | Hizmet isteğinin kimliği.                                                       |
| Durum           | string                                                        | Hizmet isteğinin durumu: "none", "Open", "Closed" veya "ilgilenilmesi \_ gerekiyor". |
| Kuruluş     | [Servicerequestorganleştirme](#servicerequestorganization)     | Hizmet isteğinin oluşturulduğu kuruluş.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Hizmet isteğindeki birincil Iletişim.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Son güncelleme tarihi" hizmet isteğindeki değişiklikler için ilgili kişi.                        |
| ProductName      | string                                                        | Hizmet isteğine karşılık gelen ürünün adı.                     |
| ProductId        | string                                                        | Ürünün kimliği.                                                               |
| CreatedDate      | date                                                          | Hizmet isteği oluşturma tarihi.                                          |
| LastModifiedDate olarak ayarlayın | date                                                          | Hizmet isteğinin son değiştirilme tarihi.                                 |
| LastClosedDate   | date                                                          | Hizmet isteğinin son kapatıldığı tarih.                                   |
| Dosya bağlantıları        | [FileInfo](utility-resources.md#fileinfo) kaynakları dizisi | Hizmet isteğiyle ilgili dosya bağlantıları koleksiyonu.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Mevcut bir hizmet isteğine bir Note eklenebilir.                                  |
| Notlar            | [Servicerequestnotes](#servicerequestnote) dizisi           | Hizmet isteğine eklenen notların bir koleksiyonu.                                  |
| CountryCode      | string                                                        | Hizmet isteğine karşılık gelen ülke.                                    |
| Öznitelikler       | ResourceAttributes                                            | Hizmet isteğine karşılık gelen meta veri öznitelikleri.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Bir hizmet isteği oluşturan veya değiştiren bir kişiyi açıklar.

| Özellik     | Tür                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Kuruluş | [Servicerequestorganleştirme](#servicerequestorganization) | Hizmet isteğinin oluşturulduğu kuruluş. |
| Kişi kimliği    | string                                                    | Kişinin benzersiz kimliği.                               |
| LastName     | string                                                    | Kişinin soyadı.                          |
| FirstName    | string                                                    | Kişinin ilk adı.                         |
| E-posta        | string                                                    | Kişinin e-postası.                              |
| PhoneNumber  | string                                                    | Kişinin telefon numarası.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Bir hizmet isteğine bağlı bir notun olduğunu açıklar.

| Özellik      | Tür   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | Notun oluşturucusunun adı.         |
| CreatedDate   | date   | Notun oluşturulduğu tarih ve saat. |
| Metin          | string | Notun metni.                        |

## <a name="servicerequestorganization"></a>Servicerequestorganleştirme

Hizmet isteğinin oluşturulduğu organizasyonu açıklar.

| Özellik    | Tür   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | string | Kuruluşun benzersiz kimliği.    |
| Name        | string | Kuruluş adı.         |
| PhoneNumber | string | Kuruluşun telefon numarası. |

## <a name="supporttopic"></a>SupportTopic

Bir destek konusunu açıklar. Hizmet istekleri, hızlı ve etkili bir şekilde işlenmesini sağlamak için bir destek konusu belirler.

| Özellik    | Tür               | Açıklama                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Ad        | string             | Destek konusunun adı.                                |
| Description | dize             | Destek konusunun açıklaması.                         |
| Id          | string             | Destek konusunun benzersiz kimliği.                           |
| Öznitelikler  | ResourceAttributes | Hizmet isteğine karşılık gelen meta veri öznitelikleri. |

