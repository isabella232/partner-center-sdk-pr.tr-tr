---
title: API azaltma yönergeleri
description: Iş Ortağı Merkezi API 'Lerini çağıran iş ortakları için, hangi API 'Lerin Microsoft API daraltma ve en iyi uygulamalardan etkilendiğinin ve daha iyi bir şekilde azaltılmasını önlemek için
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: 4eead16c5bb2b01f0fba85e30ea35fbcdae9d5a6682872eecfeeb9e47f43d324
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993767"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerini çağıran iş ortakları için API azaltma Kılavuzu 

Microsoft, Iş Ortağı Merkezi API 'Lerini çağıran iş ortakları için zaman dilimi içinde daha tutarlı performans sağlamak üzere API daraltma işlemi yapıyor. Azaltma, kaynakların aşırı kullanımını engellemek için bir zaman dilimi içindeki bir hizmete yönelik isteklerin sayısını sınırlar. Iş ortağı merkezi yüksek bir istek hacmi işleyecek şekilde tasarlandığından, birkaç iş ortağı tarafından çok sayıda istek oluşursa, azaltma işlemi tüm iş ortakları için en iyi performansı ve güvenilirliği korumanıza yardımcı olur.  

Azaltma limitleri senaryoya göre farklılık gösterir. Örneğin, büyük bir yazma hacmi gerçekleştiriyorsanız, yalnızca okuma işlemi gerçekleştirmekten daha yüksektir.

## <a name="what-happens-when-throttling-occurs"></a>Kısıtlama gerçekleştiğinde ne olur? 

Bir azaltma eşiği aşıldığında, Iş ortağı merkezi bir süre için o istemciden gelen diğer istekleri sınırlandırır. Kısıtlama davranışı, istek türüne ve sayısına bağlıdır.   

### <a name="common-throttling-scenarios"></a>Yaygın kısıtlama senaryoları 

İstemcilerin azaltmasının en yaygın nedenleri şunlardır: 

- **BIR API Için Iş ortağı KIRACı kimliği başına çok sayıda istek** vardır: bazı Iş Ortağı Merkezi API 'leri Için azaltma Iş ortağı kiracı kimliğine göre belirlenir, aynı Iş ortağı kiracı kimliğinde bu API 'lere çok fazla çağrı azaltma eşiğini aşarak sonuçlanır.  

- Her **Müşteri KIRACı kimliği Için Iş ortağı KIRACı kimliği başına BIR API için çok sayıda istek** vardır: diğer API 'ler için, azaltma Iş ortağı Kiracı kimliği/MÜŞTERI Kiracı kimliği birleşimine göre belirlenir; Bu durumlarda, aynı müşteri kiracı KIMLIĞINE karşı çok fazla çağrı yapmak, diğer müşterilerle yapılan çağrıların başarılı olabileceği azaltma ile sonuçlanır.

## <a name="best-practices-to-avoid-throttling"></a>Azaltmayı önlemek için en iyi uygulamalar 
 
Güncelleştirmeleri denetlemek için bir kaynağı sürekli yoklamak ve yeni veya silinmiş kaynakları denetlemek için düzenli olarak kaynak koleksiyonlarını taramak, azaltmaya neden olabilir ve genel performansı düşürür. Eşzamanlı API çağrıları, birim zamanı başına yüksek sayıda isteğe yol açabilir, bu da isteklerin kısıtlanmasına neden olur. Bunun yerine değişiklik izleme ve değişiklik bildirimlerini kullanmanız gerekir. Ayrıca, değişiklikleri algılamak için etkinlik günlüklerini kullanabilmeniz gerekir. Daha fazla bilgi için bkz. [Iş ortağı merkezi etkinlik günlükleri](get-a-record-of-partner-center-activity-by-user.md).  İş ortaklarının, daha fazla verimlilik için etkinlik günlüğü API 'sini kullanmayı ve azaltmasını önlemek için kullanılması önerilir. Ayrıca aşağıdaki etkinlik günlüklerini kullanma örneğine bakın.

## <a name="best-practices-to-handle-throttling"></a>Azaltmayı işlemek için en iyi uygulamalar

Azaltma işlemi için en iyi uygulamalar şunlardır: 

- Paralellik derecesini azaltın. 
- Çağrıların sıklığını azaltın. 
- Tüm istekler kullanım sınırlarınıza göre tahakkuk ettiğinden anında denemeler yapmaktan kaçının. 

Hata işleme uyguladığınızda, azaltmayı algılamak için HTTP hata kodu 429’u kullanın. Başarısız yanıt Retry-After yanıt üst bilgisini içerir. Yeniden deneme-sonrası gecikmesini kullanarak istekleri kapatmak, azaltmayı kurtarmanın en hızlı yoludur. 

Retry-After gecikmesini kullanmak için şunları yapın: 

1. Retry-After üstbilgisinde belirtilen saniye sayısını bekleyin. 

2. İsteği yeniden deneyin.  

3. İstek bir 429 hata koduyla yeniden başarısız olursa, hala kısıtlanıyor olursunuz. Üstel geri alma ile yeniden deneyin, önerilen Retry-After gecikmesini kullanın ve başarılı olana kadar isteği yeniden deneyin.

4. SDK kullanıyorsanız, isteğiniz kısıtlandığınızda 429 durum koduyla bir özel durum alırsınız. Özel durumda RetryAfter özelliğini kullanın ve zaman geçtikten sonra isteği yeniden deneyin.


## <a name="apis-currently-impacted-by-throttling"></a>Daraltma tarafından şu anda etkilenen API 'Ler

Sonunda, "api.partnercenter.microsoft.com/" uç noktasını çağıran her tek Iş Ortağı Merkezi API 'SI kısıtlanacak. Şu anda azaltma sınırları yalnızca aşağıda listelenen API 'lerde zorlanır. İş Ortağı Merkezi, her API için telemetri toplar ve azaltma sınırlarını dinamik olarak ayarlar. Aşağıdaki tabloda, azaltma 'nın Şu anda zorlandığı API 'Ler listelenmektedir.  


|**İşlem**| **İş Ortağı Merkezi belgeleri**|
|------------------------|----------------------------|
|{baseURL}/v1/Customers/{customer_id}/Orders|[sipariş oluşturma](create-an-order.md)|
|{baseURL}/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/yükseltmeler|[abonelik geçişi](transition-a-subscription.md)|
|{baseURL}/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID}|[bir aboneliğe eklenti satın alma](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/Customers/{Customer-id}/Carts/{cart-id}|[sepet oluşturma](create-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-id}/Carts/{cart-id}/Checkout|[sepet kullanıma alma](checkout-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-id}/Carts/{cart-id}|[sepetini güncelleştirme](update-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/kayıtları|[abonelik kaydetme](register-a-subscription.md)|
|{baseURL}/v1/productyükseltmeleri|[ürün yükseltme varlığı oluştur](create-product-upgrade-entity.md)|
|{baseURL}/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/dönüşümler |[deneme aboneliğini ücretli olarak dönüştürme](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/Customers/{Customer-Tenant-ID}|[KIMLIĞE göre müşteri al](get-a-customer-by-id.md)|
|{baseURL}/v1/productupgrades/uygunluk|[ürün yükseltmesine uygunluk sağlayın](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} |[aboneliği Yönet](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/Customers/{customer_id}/abonelikler |[tüm a-a-a-a-](get-all-of-a-customer-s-subscriptions.md)|
|{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}|[Kimliğe göre bir abonelik alma](get-a-subscription-by-id.md)|
|{baseURL}/v1/Customers/{customer_id}/Orders|[Tüm müşteri siparişlerini al](get-all-of-a-customer-s-orders.md)|
|{baseURL}/v1/Customers/{customer_id}/Orders/{order_id}|[Kimliğe göre bir sipariş alma](get-an-order-by-id.md)|
|{baseURL}/v1/Customers/{customer_id}/Orders/{order_id}/provisioningstatus|[Abonelik sağlama durumunu alma](get-subscription-provisioning-status.md)|
|{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}|[Siparişleri yönetme ve bir aboneliği yönetme](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}/addons|[Bir abonelik için eklentilerin bir listesini alma](get-a-list-of-add-ons-for-a-subscription.md)|
|{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}/azureEntitlements|[Bir abonelik için Azure yetkilendirmeleri listesini alın](get-a-list-of-azure-entitlements-for-subscription.md)|
|{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}/registrationstatus|[Abonelik kayıt durumunu alma](get-subscription-registration-status.md)|
|{baseURL}/v1/Customers/{Customer-Tenant-ID}/aktarmaları|[Müşterinin tüm aktarımlarını al](get-all-of-a-customer-s-transfers.md)|
|{baseURL}/v1/productUpgrades/{upgrade-id}/status|[Ürün yükseltme durumunu alma](get-product-upgrade-status.md)|
|{baseURL}/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/dönüşümler|[Deneme dönüştürme tekliflerinin bir listesini alma](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a>Hata kodu yanıtı:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Etkinlik günlüğü örneği

Günlük değişiklikleri çözümlemede en iyi yöntem için, belirli bir gün için denetim kaydını sorgulamanızı öneririz. 

Yanıtta, belirli işlem türünde değişikliklerle bir sonuç alacaksınız.İlgilendiğiniz işleme göre filtreleyebilirsiniz. Örneğin, yeni oluşturulan bir müşteriyle ilgileniyorsanız, operationType = "add_customer" adresinden bakabilirsiniz.  

OperationType/Resources listesi aşağıdaki API belgeleri altında bulunabilir.  

- [Kaynakları denetleme](auditing-resources.md)  

- [Kullanıcıya göre bir İş Ortağı Merkezi kaydını al](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Yanıt örneği

**İstek:**  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

**Yanıt:**    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

