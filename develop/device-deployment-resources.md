---
title: Cihaz dağıtım kaynakları
description: Cihaz dağıtımıyla İş Ortağı Merkezi kaynaklar.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c85f0bd6a633ac18aa8e56e5a89bfc5c8f0398cc
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906507"
---
# <a name="device-deployment-resources"></a>Cihaz dağıtım kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Aşağıdaki kaynaklar cihaz dağıtımıyla ilgilidir.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** bir yapılandırma ilkesi hakkında bilgi sağlar.

| Özellik             | Tür                                                           | Açıklama                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| kimlik                   | string                                       | İlkeyi tanımlayan GUID biçimli bir dize.                                  |
| name                 | string                                       | İlkenin kolay adı.                                                    |
| category             | string                                       | Kategori.                                                                        |
| açıklama          | string                                       | İlke açıklaması.                                                              |
| devicesAssignedCount | sayı                                       | Bu ilkeye atanan cihazların sayısı.                                       |
| policySettings       | dize dizisi                             | İlke ayarları: "none","remove \_ oem \_ preinstalls","oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration", "skip \_ eula".    |
| createdDate          | UTC tarih-saat biçiminde dize               | İlkenin oluşturulma tarihi ve saati.                                            |
| lastModifiedDate     | UTC tarih-saat biçiminde dize               | İlkenin son değiştiril olduğu tarih ve saat.                                      |
| öznitelikler           | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                            |

## <a name="device"></a>Cihaz

**Cihaz,** bir cihaz hakkında bilgi sağlar.

| Özellik            | Tür                                                           | Açıklama                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| kimlik                  | string                                                         | Cihazı tanımlayan GUID biçimli bir dize.                      |
| serialNumber        | string                                                         | Cihazla benzersiz olarak ilişkilendirilen seri numarası.                   |
| Productkey          | string                                                         | Cihazla benzersiz olarak ilişkili ürün anahtarı.                     |
| hardwareHash        | string                                                         | Cihazla benzersiz olarak ilişkili donanım karması.                   |
| Modelname           | string                                                         | Cihazla ilişkili model adı.                               |
| oemManufacturerName | string                                                         | Cihazla ilişkili OEM üreticisinin adı.             |
| ilkeler            | nesne dizisi                                               | Cihaza atanan ilkelerin listesi.                             |
| uploadedDate        | UTC tarih-saat biçiminde dize                                 | Cihaz ayrıntılarının karşıya yük olduğu tarih ve saat.                      |
| allowedOperations   | dize dizisi                                               | Cihaz eşitlemesinde GET, PATCH, DELETE olarak izin verilen HTTP yöntemlerinin listesi. |
| öznitelikler          | [Resourceattributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails,** cihaz listesinde her cihazla ilgili bilgilerin cihaz toplu karşıya yükleme durumunu açıklar.

| Özellik        | Tür     | Açıklama                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | Karşıya yüklenen cihaz toplu işiyle ilişkili GUID biçimli bir dize. |
| durum          | string   | Toplu karşıya yüklemenin durumu: "unknown","queued","processing","finished","finished \_ with \_ errors". |
| startedTime     | UTC tarih-saat biçiminde dize | Toplu karşıya yükleme işleminin başladığı tarih ve saat.   |
| completedTime   | UTC tarih-saat biçiminde dize  | Toplu karşıya yükleme işleminin tamam olduğu tarih ve saat.   |
| devicesStatus   | [DeviceUploadDetails kaynakları](#deviceuploaddetails) dizisi | Her cihaz bilgisinin karşıya yükleme durumunu belirten bir nesne dizisi. |
| öznitelikler      | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails,** bir cihazla ilgili bilgilerin karşıya yükleme durumunu açıklar.

| Özellik         | Tür                    | Açıklama                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | Cihazla ilişkili GUID biçimli bir dize. |
| serialNumber     | string                  | Cihazla benzersiz olarak ilişkili seri numarası. |
| productKey       | string                  | Ürün anahtarı cihazla benzersiz bir şekilde ilişkilendirilmiştir. |
| durum           | string                  | Cihaz bilgilerini karşıya yükleme durumu: "devam ediyor", "tamamlandı", " \_ \_ hatalarla tamamlandı". |
| Raporladı        | string                  | Cihaz yüklemesi başarısız olursa döndürülen HTTP durum hata kodu. |
| errorDescription | string                  | Cihaz yüklemesi başarısız olursa HTTP hatası açıklaması. |
| öznitelikler       | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.   |

## <a name="devicebatch"></a>DeviceBatch

**Devicebatch** bir cihaz koleksiyonunu temsil eder.

| Özellik     | Tür                                                           | Açıklama                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| kimlik           | string                                                         | Cihaz toplu işi ile ilişkili GUID biçimli bir dize. |
| createdBy    | string                                                         | Koleksiyonu oluşturan kiracının adı.                   |
| creationDate | UTC Tarih-saat biçiminde dize                                 | Koleksiyonun oluşturulduğu veri ve zaman.                    |
| deviceCount  | sayı                                                         | Koleksiyondaki cihaz sayısı.                              |
| devicesLink  | [Bağlantısının](utility-resources.md#link)                              | Bu toplu işte bulunan cihazların bağlantısı.                        |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**Devicebatchcreationrequest** , bir cihaz toplu işi oluşturmak için gereken bilgileri sağlar ve bunları cihazlarla doldurur.

| Özellik     | Tür                                                           | Açıklama                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Yığın kimliği      | string                                                         | Cihaz toplu işi ile ilişkili GUID biçimli bir dize. |
| cihazlar      | [cihaz](#device) nesneleri dizisi                             | Her nesne bir cihaz belirtir. Bir cihazı tanımlamaya yönelik aşağıdaki alan birleşimleri kabul edilir: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, yalnızca hardwareHash, productKey yalnızca productKey, serialNumber + oemManufacturerName + modelName. |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**Devicepolicyupdaterequest** bir ilkeyle bir cihaz listesini güncelleştirmek için gereken bilgileri sağlar.

| Özellik     | Tür                                                           | Açıklama                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| cihazlar      | [cihaz](#device) nesneleri dizisi                             | Her nesne bir cihaz belirtir. Aşağıdaki özellikler gereklidir: kimlik, Ilkeler. |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |
