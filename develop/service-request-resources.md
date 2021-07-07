---
title: Hizmet isteği kaynakları
description: İş ortakları, Microsoft tarafından sağlanan kesintiler hizmetlerini raporlamak veya sağlanamadığı diğer teknik destek istemek için iş ortakları adına hizmet isteklerini dosya halinde işleyebilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a02e6a873ad8785150368f3d4b89af2b588529
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547368"
---
# <a name="service-request-resources"></a>Hizmet isteği kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

İş ortakları, Microsoft tarafından sağlanan kesintiler hizmetlerini raporlamak veya sağlanamadığı diğer teknik destek istemek için iş ortakları adına hizmet isteklerini dosya halinde işleyebilir.

## <a name="servicerequest"></a>ServiceRequest

Bu isteğin ilerme şekli dahil, bir iş ortağı tarafından dosyalanmış bir hizmet isteğini açıklar.

| Özellik         | Tür                                                          | Açıklama                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Başlık            | string                                                        | Hizmet isteği başlığı.                                                           |
| Description      | dize                                                        | Açıklama.                                                                     |
| Önem derecesi         | string                                                        | Önem derecesi: "bilinmiyor", "kritik", "Orta" veya "minimal".                       |
| Supporttopicıd   | string                                                        | Destek konusunun KIMLIĞI.                                                         |
| SupportTopicName | string                                                        | Destek konusunun adı.                                                       |
| Id               | string                                                        | Hizmet isteğinin Kımlığı.                                                       |
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

| Özellik     | Tür                                                      | Açıklama                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Kuruluş | [Servicerequestorganleştirme](#servicerequestorganization) | Hizmet isteğinin oluşturulduğu kuruluş. |
| Kişi kimliği    | string                                                    | Kişinin benzersiz KIMLIĞI.                               |
| LastName     | string                                                    | Kişinin soyadı.                          |
| FirstName    | string                                                    | Kişinin ilk adı.                         |
| E-posta        | string                                                    | Kişinin e-postası.                              |
| PhoneNumber  | string                                                    | Kişinin telefon numarası.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Bir hizmet isteğine bağlı bir notun olduğunu açıklar.

| Özellik      | Tür   | Açıklama                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | Notu oluşturanın adı.         |
| CreatedDate   | date   | Notun oluşturulma tarihi ve saati. |
| Metin          | string | Notun metni.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Hizmet isteğinin oluşturulacak kuruluşu açıklar.

| Özellik    | Tür   | Açıklama                           |
|-------------|--------|---------------------------------------|
| Id          | string | Kuruluşun benzersiz kimliği.    |
| Name        | string | Kuruluş adı.         |
| PhoneNumber | string | Kuruluşun telefon numarası. |

## <a name="supporttopic"></a>SupportTopic

Bir destek konusunu açıklar. Hizmet istekleri, bunların hızlı ve etkili bir şekilde işlenmesini sağlamak için bir destek konusu belirtir.

| Özellik    | Tür               | Açıklama                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Ad        | string             | Destek konusunun adı.                                |
| Description | dize             | Destek konusunun açıklaması.                         |
| Id          | string             | Destek konusunun benzersiz kimliği.                           |
| Öznitelikler  | Resourceattributes | Hizmet isteğine karşılık gelen meta veri öznitelikleri. |

