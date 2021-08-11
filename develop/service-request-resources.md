---
title: Hizmet isteği kaynakları
description: İş ortakları, Microsoft tarafından sağlanan kesinti hizmetlerini bildirmeleri veya sağlanamıyor olmaları durumunda başka teknik destek talep etmek için iş ortakları adına hizmet isteklerinde bulunabilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f919b3c34ff179a7a6cd0541f34c53737ec4148e44791419d2252fae64b0658d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993240"
---
# <a name="service-request-resources"></a>Hizmet isteği kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş ortakları, Microsoft tarafından sağlanan kesinti hizmetlerini bildirmeleri veya sağlanamıyor olmaları durumunda başka teknik destek talep etmek için iş ortakları adına hizmet isteklerinde bulunabilir.

## <a name="servicerequest"></a>ServiceRequest

İsteğin nasıl ilerler olduğu da dahil olmak üzere bir iş ortağı tarafından dosyalama yapılan bir hizmet isteğini açıklar.

| Özellik         | Tür                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Başlık            | string                                                        | Hizmet isteği başlığı.                                                           |
| Description      | dize                                                        | Açıklama.                                                                     |
| Önem Derecesi         | string                                                        | Önem derecesi: "unknown", "critical", "moderate" veya "minimal".                       |
| SupportTopicId   | string                                                        | Destek konusunun kimliği.                                                         |
| SupportTopicName | string                                                        | Destek konusunun adı.                                                       |
| Id               | string                                                        | Hizmet isteğinin kimliği.                                                       |
| Durum           | string                                                        | Hizmet isteğinin durumu: "none", "open", "closed" veya "attention \_ needed". |
| Kuruluş     | [ServiceRequestOrganization](#servicerequestorganization)     | Hizmet isteğinin oluşturulacak kuruluş.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Hizmet isteğiyle ilgili Birincil Kişi.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | Hizmet isteğinde yapılan değişiklikler için "Son Güncelleştirme Tarihi" ilgili kişisi.                        |
| ProductName      | string                                                        | Hizmet isteğine karşılık gelen ürünün adı.                     |
| ProductId        | string                                                        | Ürünün kimliği.                                                               |
| CreatedDate      | date                                                          | Hizmet isteğinin oluşturulma tarihi.                                          |
| LastModifiedDate olarak ayarlayın | date                                                          | Hizmet isteğinin en son değiştiril olduğu tarih.                                 |
| LastClosedDate   | date                                                          | Hizmet isteğinin en son kapatılan tarih.                                   |
| Dosya Bağlantıları        | [FileInfo kaynakları](utility-resources.md#fileinfo) dizisi | Hizmet isteğiyle ilgili Dosya Bağlantıları koleksiyonu.                    |
| YeniNot          | [ServiceRequestNote](#servicerequestnote)                     | Mevcut hizmet isteğine bir not eklenebilir.                                  |
| Notlar            | [ServiceRequestNotes dizisi](#servicerequestnote)           | Hizmet isteğine eklenen notlar koleksiyonu.                                  |
| CountryCode      | string                                                        | Hizmet isteğine karşılık gelen ülke.                                    |
| Öznitelikler       | Resourceattributes                                            | Hizmet isteğine karşılık gelen meta veri öznitelikleri.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Hizmet isteği oluşturan veya değiştiren bir kişiyi açıklar.

| Özellik     | Tür                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Kuruluş | [ServiceRequestOrganization](#servicerequestorganization) | Hizmet isteğinin oluşturulacak kuruluş. |
| Contactıd    | string                                                    | Kişinin benzersiz kimliği.                               |
| LastName     | string                                                    | Kişinin soyadı.                          |
| FirstName    | string                                                    | Kişinin adı.                         |
| E-posta        | string                                                    | Kişinin e-postası.                              |
| PhoneNumber  | string                                                    | Kişinin telefon numarası.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Hizmet isteğine eklenmiş bir notu açıklar.

| Özellik      | Tür   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | Notu oluşturanın adı.         |
| CreatedDate   | date   | Notun oluşturulma tarihi ve saati. |
| Metin          | string | Notun metni.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Hizmet isteğinin oluşturulacak kuruluşu açıklar.

| Özellik    | Tür   | Description                           |
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

