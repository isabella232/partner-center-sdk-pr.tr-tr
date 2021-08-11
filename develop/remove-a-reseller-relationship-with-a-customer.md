---
title: Bir müşteriyle kurumsal bayi ilişkisini kaldırma
description: Artık işlem sahip olmadığınız bir müşteriyle kurumsal bayi ilişkisini kaldırma.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bcfba544bd1647ba0f3eb360d5ace14c7223b38837cb858198cf95c4e82dd594
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997082"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Bir müşteriyle kurumsal bayi ilişkisini kaldırma

Artık işlem sahip olmadığınız bir müşteriyle kurumsal bayi ilişkisini kaldırın.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Kurumsal bayi ilişkisi kaldırılana kadar tüm Azure Ayrılmış VM Örneği siparişlerini iptal etmeniz gerekir. Açık Azure desteği Azure Ayrılmış SANAL Makine Örneği siparişlerini iptal etmek için sanal makineyi arayın.

## <a name="c"></a>C\#

Bir müşterinin kurumsal bayi ilişkisini kaldırmak için önce bu müşteri için etkin Azure Ayrılmış VM Örnekleri iptal edildiklerini emin olun. Ardından, bu müşteri için tüm etkin aboneliklerin askıya alınmış olduğundan emin olun. Bunu yapmak için kurumsal bayi ilişkisini silmek istediğiniz müşterinin kimliğini belirleme. Aşağıdaki kod örneğinde, kullanıcıdan müşteri tanımlayıcısını sağlaması istenir.

Müşterinin Azure Ayrılmış VM Örnekleri olup olmadığını belirlemek için müşteri tanımlayıcısını kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak yetkilendirme koleksiyonunu alın ve yetkilendirme toplama işlemlerine yönelik bir arabirim almak için [**Yetkilendirmeler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini kullanın. Yetkilendirme koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) [**veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) yöntemini çağırma. [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) [**entitlementType**](entitlement-resources.md#entitlementtype) değerine sahip tüm yetkilendirmeler için koleksiyonu filtrelenin ve varsa devam etmeden önce desteği çağırarak bunları iptal edin.

Ardından müşteriyi belirtmek için müşteri tanımlayıcısını [**kullanarak IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak müşterinin aboneliklerinin koleksiyonunu ve abonelik toplama işlemlerine bir arabirim almak için [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini alın. Son olarak, [**müşterinin abonelik**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) koleksiyonunu almak için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) yöntemini çağırabilirsiniz. Abonelik koleksiyonunu çapraz geçişe geçin ve aboneliklerin hiçbirinin [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**subscriptionStatus.Status özellik değerine sahip olduğundan emin olun.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) Abonelik hala etkinse, askıya alma [hakkında bilgi için bkz.](suspend-a-subscription.md) Aboneliği askıya alma.

Tüm etkin aboneliklerin Azure Ayrılmış VM Örnekleri iptal edildiğini ve tüm etkin aboneliklerin askıya alınarak müşteri için kurumsal bayi ilişkisini kaldırabilirsiniz. İlk olarak, [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)olarak ayarlanmış [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.relationshiptopartner) özelliğiyle yeni bir [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) nesnesi oluşturun. Ardından müşteri tanımlayıcısını kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın ve yeni müşteri nesnesini geçerek **Patch** yöntemini çağırın.

İlişkiyi yeniden oluşturmak için [kurumsal bayi ilişkisi/iş ortağı-merkezi/geliştirme/istek-kurumsal bayi-ilişkisi isteği) işlemini tekrarlayın.

``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** PartnerSDK.FeatureSample **Sınıfı:** DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem     | İstek URI'si                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Yama**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda bayi ilişkisini kaldırmak için gerekli sorgu parametreleri listelemektedir.

| Ad                   | Tür     | Gerekli | Açıklama                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, müşteriyi tanımlayan GUID **biçimli bir customer-tenant-id** değeridir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek **gövdesinde** bir Müşteri kaynağı gereklidir. **RelationshipToPartner özelliğinin** yok olarak ayarlanmış olduğundan emin olmak.

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem belirtilen müşteri için bir kurumsal bayi ilişkisini kaldırır.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
