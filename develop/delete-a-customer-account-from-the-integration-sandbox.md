---
title: Tümleştirme korumalı alandan bir müşteri hesabını silme
description: Bir müşteri hesabını Üretimde Test (İpucu) tümleştirme korumalı alandan silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973137"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Tümleştirme korumalı alandan bir müşteri hesabını silme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede iş ortağı ile müşteri hesabı arasındaki ilişkiyi kesme ve Üretimde Test (İpucu) tümleştirme korumalı alanı kotasını geri kazanma açıklanmıştır.

> [!IMPORTANT]
> Bir müşteri hesabını silebilirsiniz. Bu müşteri kiracısı ile ilişkili tüm kaynaklar temiz olur.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- İpucu Azure Ayrılmış Sanal Makine Örnekleri alanından müşteri silmeden önce tüm yazılım satın alma siparişlerini ve yazılım satın alma siparişlerini iptal etmeniz gerekir.

## <a name="c"></a>C\#

İpucu tümleştirme korumalı alandan bir müşteri silmek için:

1. İş ortağı işlemlerine bir [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) arabirimi almak için İpucu hesabı kimlik bilgilerinizi [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) yöntemine girin.

2. Yetkilendirme koleksiyonunu almak için iş ortağı işlemleri arabirimini kullanın:

    1. Müşteriyi [**belirtmek için müşteri tanımlayıcısıyla Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.

    2. **Yetkilendirmeler özelliğini** çağırma.

    3. Yetkilendirme koleksiyonunu almak için **Get** **veya GetAsync** [**yöntemini**](entitlement-resources.md) çağırma.

3. Bu müşteriye Azure Ayrılmış Sanal Makine Örnekleri satın alma siparişlerini iptal etmelerini sağlar. Koleksiyonda [**her Yetkilendirme**](entitlement-resources.md) için:

    1. Yetkilendirmeyi [**kullanın. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) sipariş koleksiyonundan ilgili [Siparişin](order-resources.md#order) yerel bir kopyasını almak için kullanın.

    2. [**Order.Status özelliğini**](order-resources.md#order) "Cancelled" olarak ayarlayın.

    3. Siparişi **güncelleştirmek için Patch()** yöntemini kullanın.

4. Tüm siparişleri iptal edin. Örneğin, aşağıdaki kod örneği durumu "İptal Edildi" olana kadar her siparişi yoklama amacıyla bir döngü kullanır.

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
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
        // Check if all the orders were canceled.
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

5. Müşteri için Delete yöntemi çağrılarak tüm siparişlerin **iptal** edildiğine emin olun.

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi PartnerCenterSDK.FeaturesSamples **Sınıfı:** DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
