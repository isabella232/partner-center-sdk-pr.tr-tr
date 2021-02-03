---
title: Bir rolden bir müşteri kullanıcısını kaldırma
description: Bir kullanıcıyı bir müşteri hesabı içindeki dizin rolünden kaldırma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253e86f3733bbf2b9c593c5ca3f3e2fccce7c2c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769647"
---
# <a name="remove-a-customer-user-from-a-role"></a>Bir rolden bir müşteri kullanıcısını kaldırma

**Uygulama hedefi**

- İş Ortağı Merkezi

Bir kullanıcıyı bir müşteri hesabı içindeki dizin rolünden kaldırma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

Bir kullanıcıyı bir dizin rolünden kaldırmak için, Kullanıcı tarafından değiştirilecek [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemine bir çağrı ile, DIZIN rolü kimliğiyle [**Directoryroles. byıd**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metodunu kullanarak rolü belirtin. Ardından, kaldırılacak kullanıcıyı belirlemek için [**Usermembers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) yöntemine erişin ve kullanıcıyı rolden kaldırmak için silme yöntemini ve [**silin**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) .

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem     | İstek URI'si                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **SILMELI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers/{User-id} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Doğru müşteri, rol ve kullanıcıyı tanımlamak için aşağıdaki URI parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Değer, müşteriyi tanımlayan bir GUID biçimli **Müşteri-Kiracı kimliği** olur. |
| **rol kimliği**            | **guid** | Y        | Değer, rolü tanımlayan bir GUID biçimli **rol kimliği** olur.                |
| **Kullanıcı kimliği**            | **guid** | Y        | Değer, tek bir kullanıcı hesabını tanımlayan GUID biçimli bir **Kullanıcı kimliği** ' dir.   |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Kullanıcı rolden başarıyla kaldırılırsa, yanıt gövdesi boştur.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
