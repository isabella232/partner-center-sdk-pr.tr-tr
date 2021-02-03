---
title: Tümleştirme korumalı alandan bir müşteri hesabını silme
description: Üretim (tıp) tümleştirme korumalı alanındaki sınamadan bir müşteri hesabını silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97769424"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Tümleştirme korumalı alandan bir müşteri hesabını silme

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, iş ortağı ile müşteri hesabı arasındaki ilişkiyi bölmek ve üretim (tıp) tümleştirme korumalı alanında test için kotayı geri kazanmak açıklanmaktadır.

> [!IMPORTANT]
> Bir müşteri hesabını sildiğinizde, bu müşteri kiracısıyla ilişkili tüm kaynaklar temizlenir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir müşteri, tıp tümleştirme korumalı alanından silinmeden önce tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edilmesi gerekir.

## <a name="c"></a>C\#

Bir müşteriyi tıp tümleştirme korumalı alanından silmek için:

1. İş ortağı işlemlerine bir [**ıpartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) arabirimi almak için tıp hesabı kimlik bilgilerinizi [**createpartneroperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metoduna geçirin.

2. Yetkilendirmeler koleksiyonunu almak için iş ortağı işlemler arabirimini kullanın:

    1. Müşteriyi belirtmek için müşteri tanımlayıcısı ile [**Customers. byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.

    2. **Yetkilendirmeler** özelliğini çağırın.

    3. [**Yetkilendirme**](entitlement-resources.md) koleksiyonunu almak için **Get** veya **GetAsync** metodunu çağırın.

3. Söz konusu müşteriye ait tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edildiğinden emin olun. Koleksiyondaki her [**Yetkilendirme**](entitlement-resources.md) için:

    1. [**Yetkilendirme kullanın. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) , müşterinin sipariş koleksiyonundan Ilgili [siparişin](order-resources.md#order) yerel bir kopyasını almak için.

    2. [**Order. Status**](order-resources.md#order) özelliğini "iptal edildi" olarak ayarlayın.

    3. Sıralamayı güncelleştirmek için **Patch ()** metodunu kullanın.

4. Tüm siparişleri iptal et. Örneğin, aşağıdaki kod örneği, durumu "Iptal edildi" olana kadar her sırayı yoklamak için bir döngü kullanır.

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. Müşterinin **silme** yöntemini çağırarak tüm siparişlerin iptal edildiğinden emin olun.

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş ortağı Center PartnerCenterSDK. FeaturesSamples **sınıfı**: DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| Müşteri-Kiracı kimliği     | GUID     | Y        | Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem boş bir yanıt döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
