---
title: Belirtilen müşteri için yeni bir yapılandırma ilkesini güncelleştirme
description: Belirtilen müşteri için belirtilen yapılandırma ilkesini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 42c57a92020723415b4621e9f9d7c5c3278bfb77
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505348"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Belirtilen müşteri için yeni bir yapılandırma ilkesini güncelleştirme

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi

Belirtilen müşteri için belirtilen yapılandırma ilkesini güncelleştirme.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- İlke tanımlayıcısı.

## <a name="c"></a>C\#

Belirtilen müşteri için varolan bir yapılandırma ilkesini güncelleştirmek üzere, aşağıdaki kod parçacığında gösterildiği gibi yeni bir [**Configurationpolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) nesnesi örneği oluşturun. Bu yeni nesnedeki değerler varolan nesnede karşılık gelen değerleri değiştirir. Ardından, belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından, belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke KIMLIĞIYLE [**Configurationpolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırın. Son olarak, yapılandırma ilkesini güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) veya [**patchasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) metodunu çağırın.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdateConfigurationPolicy.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies/{Policy-ID} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yol parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| müşteri kimliği | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize.         |
| ilke kimliği   | string | Yes      | Güncelleştirilecek ilkeyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi, ilke bilgilerini sağlayan bir nesne içermelidir.

| Ad            | Tür             | Gerekli | Güncelleştirilebilir | Açıklama                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik              | string           | Yes      | Hayır        | İlkeyi tanımlayan GUID biçimli dize.                                                                                                    |
| name            | string           | Yes      | Yes       | İlkenin kolay adı.                                                                                                                         |
| category        | string           | Yes      | Hayır        | İlke kategorisi.                                                                                                                                     |
| açıklama     | dize           | Hayır       | Yes       | İlke açıklaması.                                                                                                                                  |
| devicesAssigned | sayı           | Hayır       | Hayır        | Cihaz sayısı.                                                                                                                                   |
| policySettings  | dize dizisi | Yes      | Yes       | İlke ayarları: "none", " \_ OEM \_ ön yüklemelerini kaldır", "OOBE \_ user \_ yerel yönetici değil", " \_ \_ \_ hızlı ayarları atla", "OEM kaydını atla", " \_ \_ \_ EULA 'yı atla \_ ". |

### <a name="request-example"></a>İstek örneği

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi yeni ilke için [Configurationpolicy](device-deployment-resources.md#configurationpolicy) kaynağını içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
