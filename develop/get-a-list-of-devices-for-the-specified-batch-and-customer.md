---
title: Belirtilen toplu iş ve müşteri için cihazların bir listesini alma
description: Bir müşteri için belirtilen cihaz toplu işsinde cihaz koleksiyonunu ve cihaz ayrıntılarını alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 28af1f568f755ba4c50cfac21529d6c677656c8e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874270"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>Belirtilen toplu iş ve müşteri için cihazların bir listesini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Bu makalede, belirtilen bir müşteri için belirtilen bir cihaz toplu iş içinde cihaz koleksiyonunun nasıl alın açıklanmıştır. Her cihaz kaynağı, cihazla ilgili ayrıntıları içerir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Cihaz toplu iş tanımlayıcısı.

## <a name="c"></a>C\#

Belirtilen müşteri için belirtilen bir cihaz toplu iş içinde cihazların koleksiyonunu almak için:

1. Belirtilen müşteri üzerinde işlemlere bir arabirim almak için müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.

2. Belirtilen toplu iş için cihaz toplu toplama işlemlerine arabirim almak üzere [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırma.

3. Toplu iş için cihaz toplama işlemlerine bir arabirim almak için [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) özelliğini alın.

4. Cihaz koleksiyonunu [**almak**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) [**için Get veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) yöntemini çağırma.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Bir örnek için aşağıdakilere bakın:

- Örnek: [Konsol test uygulaması](console-test-app.md)
- Project: **İş Ortağı Merkezi SDK'sı Örnekleri**
- Sınıf: **GetDevices.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

İsteği oluştururken aşağıdaki yol parametrelerini kullanın.

| Ad           | Tür   | Gerekli | Açıklama                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |
| devicebatch-id | string | Yes      | Cihaz toplu işlemini tanımlayan bir dize tanımlayıcısı. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

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

Başarılı olursa, yanıt gövdesi Cihaz kaynaklarının sayfalı [bir koleksiyonunu](device-deployment-resources.md#device) içerir. Koleksiyon, bir sayfada 100 cihaz içerir. 100 cihazların sonraki sayfasını almak için yanıt gövdesinde continuationToken, sonraki istekte bir üst bilgi olarak MS-ContinuationToken gerekir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
