---
title: Belirtilen toplu iş ve müşteri için cihazların bir listesini alma
description: Bir müşteri için belirtilen cihaz toplu işleminde cihaz ve cihaz ayrıntıları koleksiyonu alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769550"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>Belirtilen toplu iş ve müşteri için cihazların bir listesini alma

**Uygulama hedefi:**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi

Bu makalede, belirli bir müşteri için belirtilen cihaz toplu işlemindeki cihazların bir koleksiyonunun nasıl alınacağını açıklanır. Her cihaz kaynağı cihaz hakkındaki ayrıntıları içerir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir cihaz toplu iş tanımlayıcısı.

## <a name="c"></a>C\#

Belirtilen müşteri için belirtilen cihaz toplu işlemindeki cihazların bir koleksiyonunu almak için:

1. Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.

2. Belirtilen toplu iş için cihaz toplu işlem koleksiyonu işlemlerine bir arabirim almak üzere [**devicebatch. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırın.

3. Batch için cihaz koleksiyonu işlemlerine bir arabirim almak üzere [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) özelliğini alın.

4. Cihazların koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) yöntemini çağırın.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Bir örnek için aşağıdakilere bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Proje: **Iş ortağı MERKEZI SDK örnekleri**
- Sınıf: **GetDevices.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicebatches/{devicebatch-ID}/Devices http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

İsteği oluştururken aşağıdaki yol parametrelerini kullanın.

| Ad           | Tür   | Gerekli | Açıklama                                           |
|----------------|--------|----------|-------------------------------------------------------|
| müşteri kimliği    | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |
| devicebatch kimliği | string | Yes      | Cihaz toplu işini tanımlayan bir dize tanımlayıcısı. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi [cihaz](device-deployment-resources.md#device) kaynaklarının Sayfalanmış bir koleksiyonunu içerir. Koleksiyonda bir sayfada 100 cihaz bulunur. 100 cihazlarındaki bir sonraki sayfayı almak için, yanıt gövdesinde continuationToken, sonraki isteğe bir MS-ContinuationToken üst bilgisi olarak eklenmelidir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
