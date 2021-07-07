---
title: API azaltma yönergeleri
description: Api'leri İş Ortağı Merkezi iş ortakları için, hangi API'lerin Microsoft API azaltmadan etkilene olduğunu ve azaltmayı önlemeye veya daha iyi işlemeye yönelik en iyi yöntemleri öğrenin.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: f18518e88b9bb08d4fd248922f4ce2fefdde004f
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025658"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Api'leri çağıran iş ortakları için API İş Ortağı Merkezi azaltma kılavuzu 

Microsoft, API'leri çağıran iş ortaklarının belirli bir zaman aralığı içinde daha tutarlı bir performans elde İş Ortağı Merkezi gerçekleştirmektedir. Azaltma, kaynakların aşırı kullanımına engel olmak için bir zaman aralığı içinde hizmete yapılan istek sayısını sınırlar. Bu İş Ortağı Merkezi, yüksek hacimli istekleri işlemek için tasarlansa da, az sayıda iş ortağı tarafından çok fazla istek oluşursa kısıtlama tüm iş ortakları için en iyi performansın ve güvenilirliğin korunmasına yardımcı olur.  

Azaltma sınırları senaryoya göre değişiklik gösterir. Örneğin, büyük hacimli yazmalar yapıyorsanız azaltma olasılığı yalnızca okumalar yapıyorsanız daha yüksektir.

## <a name="what-happens-when-throttling-occurs"></a>Azaltma oluştuğunda ne olur? 

Bir azaltma eşiği aşılırsa, İş Ortağı Merkezi istemciden gelen diğer tüm istekleri bir süre için sınırlar. Azaltma davranışı istek türüne ve sayısına bağlıdır.   

### <a name="common-throttling-scenarios"></a>Yaygın azaltma senaryoları 

İstemcilerin azaltmanın en yaygın nedenleri şunlardır: 

- **İş Ortağı** Kiracı Kimliği başına çok sayıda API isteği: Bazı İş Ortağı Merkezi API'leri için azaltma İş Ortağı Kiracı Kimliği tarafından belirlenir; aynı İş Ortağı Kiracı Kimliğinde bu API'lere yapılan çok fazla çağrı azaltma eşiğinin aşılır.  

- **Müşteri Kiracı Kimliği** başına İş Ortağı Kiracı Kimliği başına çok sayıda API isteği: Diğer API'ler için azaltma, İş Ortağı Kiracı Kimliği/Müşteri Kiracı Kimliği birleşimine göre belirlenir; Bu durumlarda, aynı müşteri kiracı kimliğine karşı çok fazla çağrı yapmak azaltmaya neden olurken diğer müşterilere yapılan çağrılar başarılı olabilir.

## <a name="best-practices-to-avoid-throttling"></a>Azaltmayı önlemeye yönelik en iyi yöntemler 
 
Güncelleştirmeleri kontrol etmek için bir kaynağı sürekli yoklama ve yeni veya silinmiş kaynakları kontrol etmek için kaynak koleksiyonlarını düzenli olarak tarama gibi programlama uygulamaları, azaltmaya neden olabilir ve genel performansı düşürecektir. Eşzamanlı API çağrıları, birim zamanı başına çok sayıda istekle karşılanabilecek ve isteklerin kısıtlanabilecek şekilde kısıtlanabilecek. Bunun yerine değişiklik izleme ve değişiklik bildirimlerini kullan gerekir. Ayrıca, değişiklikleri algılamak için etkinlik günlüklerini de kullanabilirsiniz. Daha fazla bilgi için [bkz. İş Ortağı Merkezi günlüklerini görüntüleme.](get-a-record-of-partner-center-activity-by-user.md)  İş ortaklarının daha fazla verimlilik ve azaltmayı önlemek için etkinlik günlüğü API'sini kullanmayı göz önünde bulundurmalarını kesinlikle öneririz. Ayrıca aşağıdaki etkinlik günlüklerini kullanma örneğine de bakın.

## <a name="best-practices-to-handle-throttling"></a>Azaltmayı işlemek için en iyi yöntemler

Aşağıda, azaltmayı işlemeye yönelik en iyi yöntemler ve daha iyi yöntemler ve ardından yer alan uygulamalar ve daha fazla bilgi yer amaktadır: 

- Paralellik derecesini azaltma. 
- Çağrı sıklığını azaltma. 
- Tüm istekler kullanım sınırlarınıza göre tahakkuk etti olarak hemen yeniden denemelerden kaçının. 

Hata işleme uyguladığınızda, azaltmayı algılamak için HTTP hata kodu 429’u kullanın. Başarısız yanıt, yanıt üst Retry-After içerir. Yeniden deneme sonrası gecikmeyi kullanarak istekleri geri almanın en hızlı yolu azaltmadan kurtarmaktır. 

Yeniden deneme sonrası gecikmeyi kullanmak için şunları yapın: 

1. Üst bilgisinde belirtilen saniye Retry-After bekleyin. 

2. İsteği yeniden deneyin.  

3. İstek 429 hata koduyla yeniden başarısız olursa, yine de kısıtlamaya devam edersiniz. Üstel geri ödeme ile yeniden deneyin, önerilen gecikmeyi Retry-After ve başarılı olana kadar isteği yeniden deneyin.

4. SDK'yı kullanıyorsanız isteğiniz kısıtlanacaksa durum kodu 429 olan bir özel durum alırsınız. Özel durum içinde RetryAfter özelliğini kullanın ve süre sonra isteği yeniden deneyin.


## <a name="apis-currently-impacted-by-throttling"></a>Şu anda azaltmadan etkilene API'ler

Sonunda, "İş Ortağı Merkezi" uç noktasını çağıran her api api.partnercenter.microsoft.com/ kısıtlar. Şu anda azaltma sınırları yalnızca aşağıda listelenen API'lere uygulanır. İş Ortağı Merkezi API'lerden her biri için telemetri toplayarak azaltma sınırlarını dinamik olarak ayarlar. Aşağıdaki tabloda azaltmanın şu anda zorlanan API'leri listele.  


|**İşlem**| **İş Ortağı Merkezi belgeleri**|
|------------------------|----------------------------|
|{baseURL}/v1/customers/{customer_id}/orders|[sipariş oluşturma](create-an-order.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|[aboneliği geçiş](transition-a-subscription.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}|[abonelik için eklenti satın alma](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[sepet oluşturma](create-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout|[sepete göz at](checkout-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[sepeti güncelleştirme](update-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|[aboneliği kaydetme](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[ürün yükseltme varlığı oluşturma](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions |[deneme aboneliğini ücretli aboneliğe dönüştürme](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{customer-tenant-id}|[Kimliğine göre müşteri al](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/uygunluk|[ürün yükseltmesi için uygunluk elde etmek](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} |[aboneliği yönetme](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions |[get-all-of-a-customer-s-subscriptions](get-all-of-a-customer-s-subscriptions.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Kimliğe göre bir abonelik alma](get-a-subscription-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders|[Tüm müşteri siparişlerini alma](get-all-of-a-customer-s-orders.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}|[Kimliğe göre bir sipariş alma](get-an-order-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|[Abonelik sağlama durumunu alma](get-subscription-provisioning-status.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Siparişleri yönetme ve aboneliği yönetme](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|[Bir abonelik için eklentilerin bir listesini alma](get-a-list-of-add-ons-for-a-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|[Bir abonelik için Azure yetkilendirmelerinin listesini alma](get-a-list-of-azure-entitlements-for-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|[Abonelik kayıt durumunu alma](get-subscription-registration-status.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/transfers|[Müşterinin tüm aktarımlarını al](get-all-of-a-customer-s-transfers.md)|
|{baseURL}/v1/productUpgrades/{upgrade-id}/status|[Ürün yükseltme durumunu alma](get-product-upgrade-status.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|[Deneme dönüştürme tekliflerinin bir listesini alma](get-a-list-of-trial-conversion-offers.md)|


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

Günlük değişiklikleri analiz etmede en iyi yöntem olarak, denetim kaydını belirli bir gün için sorgulamayı öneririz. 

Yanıtta, belirli bir işlem türüne yapılan değişikliklerle bir sonuç elde olur.Filtreyi önemsersiniz işlemi temel alarak filtreleysiniz. Örneğin, yeni oluşturulan bir müşteriyle ilgileniyorsanız operationType = "add_customer".  

operationtype/resources listesi aşağıdaki API belgelerinden bulunabilir.  

- [Kaynakları denetleme](auditing-resources.md)  

- [Kullanıcıya göre Iş Ortağı Merkezi etkinliğinin kaydını al](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Yanıt örneği

**İstek**:  
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

**Yanıt**:    
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
 

