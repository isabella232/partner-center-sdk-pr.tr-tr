---
title: Müşterinin kullanıcı hesabını silme
description: Bir müşterinin mevcut kullanıcı hesabını silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c45646da43b8926f911942374de5da07f318c526
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973069"
---
# <a name="delete-a-user-account-for-a-customer"></a>Müşterinin kullanıcı hesabını silme

Bu makalede, bir müşterinin mevcut kullanıcı hesabının nasıl silineceği açıklanır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir kullanıcı KIMLIĞI. Kullanıcı KIMLIĞINIZ yoksa, bkz. [bir müşterinin tüm Kullanıcı hesaplarının listesini alın](get-a-list-of-all-user-accounts-for-a-customer.md).

## <a name="deleting-a-user-account"></a>Kullanıcı hesabını silme

Bir kullanıcı hesabını sildiğinizde, Kullanıcı durumu 30 gün boyunca **etkin değil** olarak ayarlanır. 30 30 gün sonra, Kullanıcı hesabı ve onunla ilişkili veriler temizlenir ve kurtarılamaz hale getirilir.

Etkin olmayan hesap 30 günlük bir pencere içindeyse, [bir müşterinin silinen kullanıcı hesabını geri yükleyebilirsiniz](restore-a-user-for-a-customer.md) . Ancak, silinmiş ve devre dışı olarak işaretlenen bir hesabı geri yüklediğinizde, hesap artık kullanıcı koleksiyonunun bir üyesi olarak döndürülmez (örneğin, [bir müşterinin tüm Kullanıcı hesaplarının bir listesini](get-a-list-of-all-user-accounts-for-a-customer.md)aldığınızda).

## <a name="c"></a>C\#

Mevcut bir müşteri Kullanıcı hesabını silmek için:

1. Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.

2. Kullanıcıyı tanımlamak için [**Users. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırın.

3. Kullanıcıyı silmek ve Kullanıcı durumunu devre dışı olarak ayarlamak için [**silme**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: deletecustomeruser. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem     | İstek URI'si                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| Müşteri-Kiracı kimliği     | GUID     | Y        | Değer, satıcının belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-kiracı kimliğidir** . |
| user-id                | GUID     | Y        | Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliğidir** .                                          |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem bir **204 içerik** durum kodu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
