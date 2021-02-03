---
title: Bir kullanıcıya lisans atama
description: C veya REST API 'lerinin kullanımı gibi Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşteri kullanıcısına lisans atamayı öğrenin \# .
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770007"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Iş Ortağı Merkezi API 'Leri aracılığıyla bir kullanıcıya lisans atama

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bir müşteri kullanıcısına lisans atama.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir müşteri Kullanıcı tanımlayıcısı. Bu KIMLIK, lisansın atanacağı kullanıcıyı tanımlar.

- Lisansın ürününü tanımlayan bir Ürün SKU tanımlayıcısı.

## <a name="assigning-licenses-through-code"></a>Kod aracılığıyla lisans atama

Bir kullanıcıya lisans atadığınızda, müşterinin abone olunan SKU 'ların koleksiyonundan seçim yapmanız gerekir. Daha sonra, atamak istediğiniz ürünleri tanımladıktan sonra, atamaları yapabilmek için her bir ürün için Ürün SKU 'su KIMLIĞINI edinmeniz gerekir. Her [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) örneği, [**productsku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) nesnesine başvuralabileceğiniz ve [**kimliği**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)alabileceğiniz bir [**productsku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) özelliği içerir.

Lisans atama isteğinin tek bir lisans grubundan lisans içermesi gerekir. Örneğin, aynı istekte [**grup1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) ve **grup2** 'tan lisans atayamazsınız. Tek bir istekte birden fazla gruptan lisans atama girişimi uygun bir hata ile başarısız olur. Lisans grubuna göre hangi lisansların kullanılabildiğini öğrenmek için bkz. [lisans grubuna göre kullanılabilir lisansların listesini alma](get-a-list-of-available-licenses-by-license-group.md).

Şu kod aracılığıyla lisans atama adımları şunlardır:

1. [**Licenseatama**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) nesnesi örneği oluşturun. Atanacak Ürün SKU 'sunu ve hizmet planlarını belirtmek için bu nesneyi kullanırsınız.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Nesne özelliklerini aşağıda gösterildiği gibi doldurun. Bu kod, zaten Ürün SKU KIMLIĞINIZ olduğunu ve kullanılabilir tüm hizmet planlarının atanacağını (yani, hiçbirinin dışlanmayacağını) varsayar.

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Ürün SKU KIMLIĞINIZ yoksa, abone olunan SKU 'ların koleksiyonunu almanız ve Ürün SKU 'su kimliğini bunlardan birine almanız gerekir. Ürün SKU 'SU adını biliyorsanız bir örnek aşağıda verilmiştir.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Sonra, [**Licenseatama**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)türünde yeni bir liste oluşturun ve lisans nesnesini ekleyin. Her birini listeye ayrı ekleyerek birden fazla lisans atayabilirsiniz. Bu listeye dahil edilen lisanslar aynı lisans grubundan olmalıdır.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. [**Licenseupdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) örneği oluşturun ve lisans atamalarının listesini [**licensestoassign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) özelliğine atayın.

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Lisansları atamak için [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metodunu çağırın ve lisans güncelleştirme nesnesini aşağıda gösterildiği gibi geçirin.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Bir müşteri kullanıcısına lisans atamak için, önce bir [**Licenseatama**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) nesnesi örneği oluşturun ve [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) ve [**excludedplanlar**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) özelliklerini doldurun. Atanacak Ürün SKU 'sunu belirtmek için bu nesneyi kullanırsınız. Sonra, **Licenseatama** türünde yeni bir liste oluşturun ve lisans nesnesini listeye ekleyin. Sonra bir [**Licenseupdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) örneği oluşturun ve lisans atamalarının listesini [**licensestoassign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) özelliğine atayın.

Ardından, müşteriyi tanımlamak için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve kullanıcıyı tanımlamak IÇIN Kullanıcı kimliği ile [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanın. Daha sonra [**Licenseupdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) özelliğinden müşteri Kullanıcı Lisansı güncelleştirme işlemlerine yönelik bir arabirim alın.

Son olarak, [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metodunu çağırın ve lisansı atamak için lisans güncelleştirme nesnesini geçirin.

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

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                       |
|-------------|--------|----------|---------------------------------------------------|
| müşteri kimliği | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir KIMLIK. |
| user-id     | string | Yes      | Kullanıcıyı tanımlayan GUID biçimli bir KIMLIK.     |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Atanacak lisansları belirten istek gövdesine bir [Licenseupdate](license-resources.md#licenseupdate) kaynağı ekleyin.

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

Başarılı olursa, HTTP yanıt durum kodu 201 döndürülür ve yanıt gövdesi lisans bilgilerine sahip bir [Licenseupdate](license-resources.md#licenseupdate) kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
