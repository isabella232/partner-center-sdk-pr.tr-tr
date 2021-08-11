---
title: Müşterinin kullanıcı hesabını silme
description: Müşteri için mevcut bir kullanıcı hesabını silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 64e9175a2a4545022175b326a2d765ecd6a1106242b8926fe19e32c7e2ab6ec2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994889"
---
# <a name="delete-a-user-account-for-a-customer"></a>Müşterinin kullanıcı hesabını silme

Bu makalede, bir müşteri için mevcut bir kullanıcı hesabının nasıl silinecekleri açıklanmıştır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Kullanıcı kimliği. Kullanıcı kimliğiniz yoksa [bkz. Müşteri için tüm kullanıcı hesaplarının listesini al.](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="deleting-a-user-account"></a>Kullanıcı hesabını silme

Bir kullanıcı hesabını silebilirsiniz. Kullanıcı durumu 30 **gün boyunca** devre dışı olarak ayarlanır. Otuz 30 gün sonra kullanıcı hesabı ve ilişkili verileri temizlenebilir ve kurtarılamaz hale geldi.

Etkin olmayan hesap 30 [günlük süre](restore-a-user-for-a-customer.md) içinde ise, silinmiş bir kullanıcı hesabını bir müşteri için geri yükleyebilirsiniz. Ancak silinmiş ve etkin değil olarak işaretlenmiş bir hesabı geri yükledikten sonra hesap artık kullanıcı koleksiyonunun bir üyesi olarak döndürülemez (örneğin, bir müşterinin tüm kullanıcı hesaplarının listesini [alırsanız).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Mevcut bir müşteri kullanıcı hesabını silmek için:

1. Müşteriyi [**tanımlamak için IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanın.

2. Kullanıcı tanımlamak [**için Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırma.

3. Delete [**yöntemini**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) çağırarak kullanıcı silin ve kullanıcı durumunu etkin değil olarak ayarlayın.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** DeleteCustomerUser.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem     | İstek URI'si                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | Değer, kurumsal bayinin belirli bir **müşteri için** sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |
| user-id                | GUID     | Y        | Değer, tek bir kullanıcı hesabına **ait OLAN** GUID biçimli bir kullanıcı kimliğidir.                                          |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem **204 İçerik Yok durum** kodunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [REST İş Ortağı Merkezi Kodları.](error-codes.md)

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
