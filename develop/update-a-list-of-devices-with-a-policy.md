---
title: İlke ile cihaz listesini güncelleştirme
description: Belirtilen müşteri için bir yapılandırma ilkesiyle cihazların listesini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b028c84ae513131d1c754dc59020e40aaf09ce31113cd3964b9144bf155300f8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990061"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>İlke ile cihaz listesini güncelleştirme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Belirtilen müşteri için bir yapılandırma ilkesiyle cihazların listesini güncelleştirme.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- İlke tanımlayıcısı.

- Güncelleştirilen cihazların cihaz tanımlayıcıları.

## <a name="c"></a>C\#

Cihazların listesini belirtilen yapılandırma ilkesiyle güncelleştirmek için, önce [KeyValuePair/dotnet/api/system.collections.generic.list-1) türünde bir [List/dotnet/api/system.collections.generic.keyvaluepair-2)[](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)örneği ve aşağıdaki kod örneğinde gösterildiği gibi uygulanacak ilkeyi ekleyin. İlkenin ilke tanımlayıcısı gerekir.

Ardından, her cihaz [**için**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) cihaz tanımlayıcısını ve uygulanacak ilkeyi içeren listeyi belirterek ilkeyle güncelleştirilen Cihaz nesnelerinin listesini oluşturun. Ardından bir [**DevicePolicyUpdateRequest nesnesi**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) başlatın ve [**Devices özelliğini**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) cihaz nesneleri listesine ayarlayın.

Cihaz ilkesi güncelleştirme isteğini işleme almak için [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri tanımlayıcısıyla çağırarak belirtilen müşteri üzerinde işlemlere bir arabirim alın. Ardından, müşteri cihaz toplama işlemlerine bir arabirim almak için [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) özelliğini alın. Son olarak, [**cihazları ilkeyle**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) güncelleştirmek için DevicePolicyUpdateRequest nesnesiyle Update yöntemini çağırabilirsiniz.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı **Sınıfı:** UpdateDevicesPolicy.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem    | İstek URI'si                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **Yama** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yol parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [DevicePolicyUpdateRequest kaynağı içermeli.](device-deployment-resources.md#devicepolicyupdaterequest)

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt, bu toplu **işlem durumunu** almak için uri'ye sahip bir Konum üst bilgisi içerir. Bu URI'yi diğer ilgili REST API'leriyle kullanmak üzere kaydedin.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
