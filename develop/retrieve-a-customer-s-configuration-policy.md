---
title: Müşterinin yapılandırma ilkesini alma
description: Belirtilen müşteri için belirtilen yapılandırma ilkesi nasıl alınır?
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f9a8cb435c63d8d02c3b4633abc8723353116f37
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547504"
---
# <a name="retrieve-a-customers-configuration-policy"></a>Müşterinin yapılandırma ilkesini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Belirtilen müşteri için belirtilen yapılandırma ilkesi nasıl alınır?

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- İlke tanımlayıcısı.

## <a name="c"></a>C\#

Belirtilen müşteriye yönelik bir yapılandırma ilkesi almak için, önce [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle çağırarak belirtilen müşteri üzerinde işlemlere bir arabirim alın. Ardından, belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke kimliğiyle [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırabilirsiniz. Son olarak, [**yapılandırma ilkesi almak**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) yöntemini arayın.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Örnekler **Sınıfı:** GetConfigurationPolicy.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |
| policy-id   | string | Yes      | İlkeyi tanımlayan GUID biçimli bir dize.   |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt, istenen [ConfigurationPolicy kaynağını](device-deployment-resources.md#configurationpolicy) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
