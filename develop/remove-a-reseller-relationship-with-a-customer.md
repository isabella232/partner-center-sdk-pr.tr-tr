---
title: Bir müşteriyle kurumsal bayi ilişkisini kaldırma
description: Artık işlem sahibi olmayan bir müşteriyle satıcı ilişkisini kaldırma.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 084797997e57c63b5c447379bb08ecb88ebd0cc4
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769604"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Bir müşteriyle kurumsal bayi ilişkisini kaldırma

**Uygulama hedefi**

- İş Ortağı Merkezi

Artık işlem sahibi olmayan bir müşteriyle satıcı ilişkisini kaldırın.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir satıcı ilişkisi kaldırılmadan önce tüm Azure ayrılmış VM örneği siparişlerinin iptal edilmesi gerekir. Açık Azure ayrılmış sanal makine örneği siparişlerinin iptal edilmesi için Azure Desteği ' ni arayın.

## <a name="c"></a>C\#

Bir müşterinin satıcı ilişkisini kaldırmak için, ilk olarak söz konusu müşteriye ait tüm etkin Azure ayrılmış sanal makine örneklerinin iptal edildiğinden emin olun. Ardından, söz konusu müşterinin tüm etkin aboneliklerinin askıya alındığından emin olun. Bunu yapmak için, satıcı ilişkisini silmek istediğiniz müşterinin KIMLIĞINI saptayın. Aşağıdaki kod örneğinde, kullanıcıdan müşteri tanımlayıcısını sağlaması istenir.

Müşteri için herhangi bir Azure ayrılmış sanal makine örneğinin iptal edilip edilmesinin gerekip gerekmediğini belirlemek için, müşteriyi belirtmek için müşteri tanımlayıcısını kullanarak [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve yetkilendirme toplama işlemlerine bir arabirim almak Için [**yetkilendirmeler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırarak yetkilendirmelerin koleksiyonunu alın. Yetkilendirme koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metodunu çağırın. Koleksiyonu, [**EntitlementType**](entitlement-resources.md#entitlementtype) değeri [**EntitlementType. Virtualmachinereservedınstance**](entitlement-resources.md#entitlementtype) olan herhangi bir yetkilendirmeden filtreleyin ve varsa, devam etmeden önce destek çağırarak bunları iptal edin.

Ardından, müşteriyi belirtmek için müşteri tanımlayıcısını kullanarak [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve abonelik koleksiyonu işlemlerine bir arabirim almak için [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırarak müşterinin aboneliklerinin bir koleksiyonunu alın. Son olarak, müşterinin abonelikler koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) yöntemini çağırın. Abonelik koleksiyonunda çapraz geçiş yapın ve aboneliklerden hiçbirinin bir abonelikler olduğundan emin olun. [**Subscriptionstatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)öğesinin [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) Özellik değeri. Abonelik hala etkin ise, nasıl askıya alınacağı hakkında bilgi edinmek için [aboneliği askıya alma](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) bölümüne bakın.

Söz konusu müşteri için tüm etkin Azure ayrılmış sanal makine örneklerinin iptal edildiğini ve tüm etkin aboneliklerinin askıya alındığını doğruladıktan sonra, müşterinin satıcı ilişkisini kaldırabilirsiniz. İlk olarak, [Customer. RelationshipToPartner/DotNet/api/Microsoft. Store. partnercenter. model. Customers. Customer. relationshiptopartner) özelliği [**Customerpartnerrelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)olarak ayarlanmış yeni bir [Customer/DotNet/API/Microsoft. Store. partnercenter. model. Customers. Customer) nesnesi oluşturun. Ardından müşteriyi belirtmek için müşteri tanımlayıcısını kullanarak [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metodunu çağırın ve yeni müşteri nesnesine geçirerek **Patch** yöntemini çağırın.

İlişkiyi yeniden oluşturmak için [bir satıcı ilişkisi ve iş ortağı-merkezi/geliştirme/istek-satıcı-ilişki isteği) işlemini tekrarlayın.

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

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Partnersdk. Featuresample **sınıfı**: DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem     | İstek URI'si                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **DÜZELTMESI**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bu tablo, satıcı ilişkisini kaldırmak için gerekli sorgu parametrelerini listeler.

| Ad                   | Tür     | Gerekli | Açıklama                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Değer, müşteriyi tanımlayan bir GUID biçimli **Müşteri-Kiracı kimliği** olur. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesinde bir **Müşteri** kaynağı gereklidir. **Relationshiptopartner** özelliğinin None olarak ayarlandığından emin olun.

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

Başarılı olursa, bu yöntem belirtilen müşteri için bir satıcı ilişkisini kaldırır.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
