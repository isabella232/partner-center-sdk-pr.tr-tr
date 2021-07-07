---
title: Belirtilen müşteri için mevcut bir toplu işe ait cihaz listesini karşıya yükleme
description: Belirtilen müşteri için mevcut bir toplu işe cihaz hakkındaki bilgilerin bir listesini karşıya yükleme. Bu, cihazları zaten oluşturulmuş bir cihaz toplu işi ile ilişkilendirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3fa9cff39113130c54cecfaef1f8ca28e0ac5adf
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530319"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>Belirtilen müşteri için mevcut bir toplu işe ait cihaz listesini karşıya yükleme

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi

Belirtilen müşteri için mevcut bir toplu işe cihaz hakkındaki bilgilerin bir listesini karşıya yükleme. Bu, cihazları zaten oluşturulmuş bir cihaz toplu işi ile ilişkilendirir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Cihaz toplu işlem tanımlayıcısı.

- Ayrı cihazlarla ilgili bilgileri sağlayan cihaz kaynaklarının listesi.

## <a name="c"></a>C\#

Mevcut bir cihaz toplu işinde cihaz listesini karşıya yüklemek için, [**cihaz**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) türünde yeni bir [list/DotNet/api/System. Collections. Generic. List -1) örneği oluşturun ve listeyi cihazlarla doldurun. Doldurulmuş özelliklerin aşağıdaki birleşimleri, her bir cihazı tanımlamak için en azından gereklidir:

- [**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).

- [**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- [**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- Yalnızca [**Hardwarehash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .

- Yalnızca [**ürün**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .

- [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

Ardından, belirtilen müşterideki işlemlere bir arabirim almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından, belirtilen toplu işlem için bir arabirim almak üzere cihaz toplu kimliğiyle [**devicebatch. byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırın. Son olarak, cihazları cihaz toplu işe eklemek için cihazların listesiyle birlikte Device [**. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) yöntemini çağırın.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: createdevices. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicebatches/{devicebatch-ID}/Devices http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad           | Tür   | Gerekli | Açıklama                                           |
|----------------|--------|----------|-------------------------------------------------------|
| müşteri kimliği    | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |
| devicebatch kimliği | string | Yes      | Cihaz toplu işini tanımlayan bir dize tanımlayıcısı. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [cihaz](device-deployment-resources.md#device) nesneleri dizisi içermelidir. Bir cihazı tanımlamaya yönelik aşağıdaki alan birleşimleri kabul edilir:

- hardwareHash + productKey.
- hardwareHash + serialNumber.
- hardwareHash + productKey + serialNumber.
- yalnızca hardwareHash.
- Yalnızca ürün.
- serialNumber + oemManufacturerName + modelName.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt, cihaz yükleme durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir. Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
