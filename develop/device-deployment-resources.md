---
title: Cihaz dağıtımı kaynakları
description: Iş Ortağı Merkezi cihaz dağıtımıyla ilgili kaynaklar.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8e2429fea88a89873955d9af9253492934e40e5be1a1b7600446485d13f5bd7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994855"
---
# <a name="device-deployment-resources"></a>Cihaz dağıtımı kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi

Aşağıdaki kaynaklar cihaz dağıtımıyla ilgilidir.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**Configurationpolicy** bir yapılandırma ilkesiyle ilgili bilgi sağlar.

| Özellik             | Tür                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| kimlik                   | string                                       | İlkeyi tanımlayan GUID biçimli bir dize.                                  |
| name                 | string                                       | İlke için kolay ad.                                                    |
| category             | string                                       | Kategori.                                                                        |
| açıklama          | string                                       | İlke açıklaması.                                                              |
| devicesAssignedCount | sayı                                       | Bu ilkeye atanan cihazların sayısı.                                       |
| policySettings       | dize dizisi                             | İlke ayarları: "none", " \_ OEM \_ ön yüklemelerini kaldır", "OOBE \_ user \_ yerel yönetici değil", \_ "hızlı ayarları atla", "OEM kaydını atla", \_ \_ \_ \_ \_ "EULA 'yı atla" \_ .    |
| createdDate          | UTC Tarih-saat biçiminde dize               | İlkenin oluşturulduğu tarih ve saat.                                            |
| lastModifiedDate     | UTC Tarih-saat biçiminde dize               | İlkenin en son değiştirildiği tarih ve saat.                                      |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                            |

## <a name="device"></a>Cihaz

**Cihaz** , bir cihaz hakkında bilgi sağlar.

| Özellik            | Tür                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| kimlik                  | string                                                         | Cihazı tanımlayan GUID biçimli bir dize.                      |
| serialNumber        | string                                                         | Cihazla benzersiz olarak ilişkili seri numarası.                   |
| productKey          | string                                                         | Ürün anahtarı cihazla benzersiz bir şekilde ilişkilendirilmiştir.                     |
| Donanım karması        | string                                                         | Donanım karması cihazla benzersiz bir şekilde ilişkilendirilmiştir.                   |
| modelName           | string                                                         | Cihazla ilişkili model adı.                               |
| oemManufacturerName | string                                                         | Cihazla ilişkili OEM üreticisinin adı.             |
| ilkeler            | nesne dizisi                                               | Cihaza atanan ilkelerin listesi.                             |
| uploadedDate        | UTC Tarih-saat biçiminde dize                                 | Cihaz ayrıntılarının karşıya yüklendiği tarih ve saat.                      |
| allowedOperations   | dize dizisi                                               | Bir cihaz eşitlemesine al, yama, SILME olarak izin verilen HTTP yöntemlerinin listesi. |
| öznitelikler          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**Batchuploaddetails** , cihaz listesi içindeki her cihazla ilgili bilgilerin bir cihaz toplu karşıya yükleme durumunu açıklar.

| Özellik        | Tür     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| Batchtrackingıd | string   | Karşıya yüklenen cihaz toplu işi ile ilişkili GUID biçimli bir dize. |
| durum          | string   | Toplu karşıya yükleme durumu: "Unknown", "kuyruğa alındı", "işlem", "bitti", "hatalarla tamamlandı \_ \_ ". |
| startedTime     | UTC Tarih-saat biçiminde dize | Toplu karşıya yükleme işleminin başladığı tarih ve saat.   |
| completedTime   | UTC Tarih-saat biçiminde dize  | Toplu karşıya yükleme işleminin tamamlandığı tarih ve saat.   |
| devicesStatus   | [Deviceuploaddetails](#deviceuploaddetails) kaynakları dizisi | Her cihaz bilgisinin karşıya yükleme durumunu belirten bir nesne dizisi. |
| öznitelikler      | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**Deviceuploaddetails** , bir cihazla ilgili bilgilerin karşıya yüklenmesi durumunu açıklar.

| Özellik         | Tür                    | Description                                 |
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

| Özellik     | Tür                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| kimlik           | string                                                         | Cihaz toplu işi ile ilişkili GUID biçimli bir dize. |
| createdBy    | string                                                         | Koleksiyonu oluşturan kiracının adı.                   |
| creationDate | UTC Tarih-saat biçiminde dize                                 | Koleksiyonun oluşturulduğu veri ve zaman.                    |
| deviceCount  | sayı                                                         | Koleksiyondaki cihaz sayısı.                              |
| devicesLink  | [Bağlantısının](utility-resources.md#link)                              | Bu toplu işte bulunan cihazların bağlantısı.                        |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**Devicebatchcreationrequest** , bir cihaz toplu işi oluşturmak için gereken bilgileri sağlar ve bunları cihazlarla doldurur.

| Özellik     | Tür                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Yığın kimliği      | string                                                         | Cihaz toplu işi ile ilişkili GUID biçimli bir dize. |
| cihazlar      | [cihaz](#device) nesneleri dizisi                             | Her nesne bir cihaz belirtir. Bir cihazı tanımlamaya yönelik aşağıdaki alan birleşimleri kabul edilir: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, yalnızca hardwareHash, productKey yalnızca productKey, serialNumber + oemManufacturerName + modelName. |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**Devicepolicyupdaterequest** bir ilkeyle bir cihaz listesini güncelleştirmek için gereken bilgileri sağlar.

| Özellik     | Tür                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| cihazlar      | [cihaz](#device) nesneleri dizisi                             | Her nesne bir cihaz belirtir. Aşağıdaki özellikler gereklidir: kimlik, Ilkeler. |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |
