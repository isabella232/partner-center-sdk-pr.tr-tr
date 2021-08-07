---
title: Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihaz listesini karşıya yükleme
description: Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihazlar hakkında bilgi listesini karşıya yükleme. Bu, sıfır dokunmalı dağıtımda kayıt için bir cihaz toplu işi oluşturur ve cihazları ve cihaz toplu işlerini belirtilen müşteriyle ilişkilendirır.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 104c240ef9a1afefd36fbb558e79ac30a3a66920b802fdc9c6b65023a038af8c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990384"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihaz listesini karşıya yükleme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihazlar hakkında bilgi listesini karşıya yükleme. Bu, sıfır dokunmalı dağıtımda kayıt için bir cihaz toplu işi oluşturur ve cihazları ve cihaz toplu işlerini belirtilen müşteriyle ilişkilendirır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler. [Uygulama+Kullanıcı kimlik doğrulamasını](enable-secure-app-model.md) farklı API'lerle kullanırken güvenli İş Ortağı Merkezi izleyin.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Tek tek cihazlar hakkında bilgi sağlayan cihaz kaynaklarının listesi.

## <a name="c"></a>C\#

Yeni bir cihaz toplu işi oluşturmak için cihazların listesini karşıya yüklemek için:

1. Device türünde yeni bir [List/dotnet/api/system.collections.generic.list-1) örneği açın ve listeyi cihazlarla doldurmak. [](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) Aşağıdaki doldurulmuş özellik birleşimleri, her cihazı tanımlamak için en azından gereklidir:

   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - [**Yalnızca HardwareHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)
   - [**Yalnızca ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)
   - [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

2. [**Bir DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) nesnesi örneği oluşturma ve [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) özelliğini seçtiğiniz benzersiz bir ad olarak, [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) özelliğini ise karşıya yüklenilen cihazlar listesine ayarlayın.

3. Belirtilen müşteri üzerinde işlemlere bir arabirim almak için müşteri tanımlayıcısıyla [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak cihaz toplu iş oluşturma isteğini işin.

4. Toplu işi oluşturmak için cihaz toplu iş oluşturma isteğiyle [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) veya [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) yöntemini çağırma.

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CreateDeviceBatch.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yol parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [DeviceBatchCreationRequest kaynağı içermeli.](device-deployment-resources.md#devicebatchcreationrequest)

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt, cihaz karşıya **yükleme durumunu** almak için URI'ye sahip bir Konum üst bilgisi içerir. Bu URI'yi diğer ilgili REST API'leriyle kullanmak üzere kaydedin.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

#### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
