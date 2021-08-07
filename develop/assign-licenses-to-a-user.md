---
title: Bir kullanıcıya lisans atama
description: C veya REST API'leri kullanımı gibi İş Ortağı Merkezi API'ler aracılığıyla bir müşteri kullanıcıya \# lisans atamayı öğrenin.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8263f7f274e453603305324cc7ac6e8b25820561ade3136b873c65ffa21e94fc
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989075"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Api'leri kullanarak kullanıcıya lisans İş Ortağı Merkezi atama

Bir müşteri kullanıcıya lisans atama.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Müşteri kullanıcı tanımlayıcısı. Bu kimlik, lisansın atanma kullanıcısını tanımlar.

- Lisansın ürününü tanımlayan ürün SKU tanımlayıcısı.

## <a name="assigning-licenses-through-code"></a>Kod aracılığıyla lisans atama

Bir kullanıcıya lisans atadığınız zaman müşterinin abone olunan SKU koleksiyonundan birini seçmeniz gerekir. Ardından, atamak istediğiniz ürünleri belirlediniz, atamaları yapmak için her ürün için ürün SKU Kimliğini elde edinirsiniz. Her [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) örneği, [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) nesnesine başvurarak kimliğini almak için [**bir ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) özelliği [**içerir.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)

Lisans ataması isteği tek bir lisans grubundan lisanslar içermeli. Örneğin, aynı istekte [**Grup1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) ve **Grup2'den lisans** atayamazsiniz. Tek bir istekte birden fazla gruptan lisans atama girişimi uygun bir hatayla başarısız olur. Lisans grubuna göre hangi lisansların kullanılabilir olduğunu bulmak için [bkz. Lisans grubuna göre kullanılabilir lisansların listesini alın.](get-a-list-of-available-licenses-by-license-group.md)

Kod aracılığıyla lisans atama adımları şu şekildedir:

1. [**LicenseAssignment nesnesinin örneğini**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) oluşturma. Bu nesneyi, atanma ürün SKU'su ve hizmet planlarını belirtmek için kullanırsiniz.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Nesne özelliklerini aşağıda gösterildiği gibi girin. Bu kod, ürün SKU kimliğine zaten sahip olduğunu ve tüm kullanılabilir hizmet planlarının atandığı varsayar (başka bir şey yoktur).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Ürün SKU Kimliğiniz yoksa, abone olunan SKU'ların koleksiyonunu almalı ve ürün SKU Kimliğini bunlardan birini al gerekir. Ürün SKU'su adını biliyorsanız bir örnek burada vetir.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Ardından [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)türünde yeni bir liste örneği ekleyin ve lisans nesnesini ekleyin. Her birini listeye tek tek ekleyerek birden fazla lisans atabilirsiniz. Bu listeye dahil edilen lisansların aynı lisans grubundan olması gerekir.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Bir [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) örneği oluşturun ve lisans atamalarının listesini [**LicensesToAssign özelliğine**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) attayabilirsiniz.

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) veya [**CreateAsync yöntemini**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) çağırarak lisansları atamak için aşağıda gösterildiği gibi lisans güncelleştirme nesnesini geçin.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Bir müşteri kullanıcıya lisans atamak için, önce [**bir LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) nesnesi örneği oluşturma ve [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) ve [**ExcludedPlans özelliklerini**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) doldurmak. Bu nesneyi, atanacak ürün SKU'larını ve hariç tutulacak hizmet planlarını belirtmek için kullanırsiniz. Ardından **LicenseAssignment** türünde yeni bir liste örneği ekleyin ve lisans nesnesini listeye ekleyin. Ardından bir [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) örneği oluşturun ve lisans atamalarının listesini [**LicensesToAssign özelliğine**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) attayabilirsiniz.

Ardından [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanarak müşteriyi ve kullanıcı kimliğiyle [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanarak kullanıcı kimliğini tanımlayabilirsiniz. Ardından [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) özelliğinden müşteri kullanıcı lisansı güncelleştirme işlemlerine bir arabirim alın.

Son olarak, [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) veya [**CreateAsync yöntemini**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) çağırarak lisansa atamak için lisans güncelleştirme nesnesinin geçişine geçebilirsiniz.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı **Örnekler Sınıfı:** CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                       |
|-------------|--------|----------|---------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir kimlik. |
| user-id     | string | Yes      | Kullanıcıyı tanımlayan GUID biçimlendirilmiş bir kimlik.     |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek [gövdesine,](license-resources.md#licenseupdate) atanma lisanslarını belirten bir LicenseUpdate kaynağı dahil etme.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, 201 HTTP yanıt durum kodu döndürülür ve yanıt gövdesi lisans bilgilerini içeren [bir LicenseUpdate](license-resources.md#licenseupdate) kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example-success"></a>Yanıt örneği (başarılı)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a>Yanıt örneği (lisans kullanılamıyor)

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
