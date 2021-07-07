---
title: Bir müşteriyle kurumsal bayi ilişkisini kaldırma
description: Artık işlem sahibi olmayan bir müşteriyle satıcı ilişkisini kaldırma.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 45eca3564c3b9078e04d1f8155d08849a589d52f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446607"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="f230e-103">Bir müşteriyle kurumsal bayi ilişkisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="f230e-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="f230e-104">Artık işlem sahibi olmayan bir müşteriyle satıcı ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f230e-104">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f230e-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f230e-105">Prerequisites</span></span>

- <span data-ttu-id="f230e-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f230e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f230e-107">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f230e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f230e-108">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f230e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f230e-109">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f230e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f230e-110">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f230e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f230e-111">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f230e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f230e-112">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="f230e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f230e-113">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="f230e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f230e-114">Bir satıcı ilişkisi kaldırılmadan önce tüm Azure ayrılmış VM örneği siparişlerinin iptal edilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f230e-114">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="f230e-115">Açık Azure ayrılmış sanal makine örneği siparişlerinin iptal edilmesi için Azure Desteği ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="f230e-115">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="f230e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="f230e-116">C\#</span></span>

<span data-ttu-id="f230e-117">Bir müşterinin satıcı ilişkisini kaldırmak için, ilk olarak söz konusu müşteriye ait tüm etkin Azure ayrılmış sanal makine örneklerinin iptal edildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f230e-117">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="f230e-118">Ardından, söz konusu müşterinin tüm etkin aboneliklerinin askıya alındığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f230e-118">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="f230e-119">Bunu yapmak için, satıcı ilişkisini silmek istediğiniz müşterinin KIMLIĞINI saptayın.</span><span class="sxs-lookup"><span data-stu-id="f230e-119">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="f230e-120">Aşağıdaki kod örneğinde, kullanıcıdan müşteri tanımlayıcısını sağlaması istenir.</span><span class="sxs-lookup"><span data-stu-id="f230e-120">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="f230e-121">Müşteri için herhangi bir Azure ayrılmış sanal makine örneğinin iptal edilip edilmesinin gerekip gerekmediğini belirlemek için, müşteriyi belirtmek için müşteri tanımlayıcısını kullanarak [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve yetkilendirme toplama işlemlerine bir arabirim almak Için [**yetkilendirmeler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırarak yetkilendirmelerin koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="f230e-121">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="f230e-122">Yetkilendirme koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="f230e-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="f230e-123">Koleksiyonu, [**EntitlementType**](entitlement-resources.md#entitlementtype) değeri [**EntitlementType. Virtualmachinereservedınstance**](entitlement-resources.md#entitlementtype) olan herhangi bir yetkilendirmeden filtreleyin ve varsa, devam etmeden önce destek çağırarak bunları iptal edin.</span><span class="sxs-lookup"><span data-stu-id="f230e-123">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="f230e-124">Ardından, müşteriyi belirtmek için müşteri tanımlayıcısını kullanarak [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve abonelik koleksiyonu işlemlerine bir arabirim almak için [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırarak müşterinin aboneliklerinin bir koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="f230e-124">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="f230e-125">Son olarak, müşterinin abonelikler koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f230e-125">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="f230e-126">Abonelik koleksiyonunda çapraz geçiş yapın ve aboneliklerden hiçbirinin bir abonelikler olduğundan emin olun. [**Subscriptionstatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)öğesinin [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) Özellik değeri.</span><span class="sxs-lookup"><span data-stu-id="f230e-126">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="f230e-127">Abonelik hala etkin ise, nasıl askıya alınacağı hakkında bilgi edinmek için [aboneliği askıya alma](suspend-a-subscription.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f230e-127">If a subscription is still active, see [Suspend a subscription](suspend-a-subscription.md) for information on how to suspend it.</span></span>

<span data-ttu-id="f230e-128">Söz konusu müşteri için tüm etkin Azure ayrılmış sanal makine örneklerinin iptal edildiğini ve tüm etkin aboneliklerinin askıya alındığını doğruladıktan sonra, müşterinin satıcı ilişkisini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f230e-128">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="f230e-129">İlk olarak, [Customer. RelationshipToPartner/DotNet/api/Microsoft. Store. partnercenter. model. Customers. Customer. relationshiptopartner) özelliği [**Customerpartnerrelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)olarak ayarlanmış yeni bir [Customer/DotNet/API/Microsoft. Store. partnercenter. model. Customers. Customer) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f230e-129">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="f230e-130">Ardından müşteriyi belirtmek için müşteri tanımlayıcısını kullanarak [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metodunu çağırın ve yeni müşteri nesnesine geçirerek **Patch** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f230e-130">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="f230e-131">İlişkiyi yeniden oluşturmak için [bir satıcı ilişkisi ve iş ortağı-merkezi/geliştirme/istek-satıcı-ilişki isteği) işlemini tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="f230e-131">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="f230e-132">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f230e-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f230e-133">**Project**: partnersdk. featuresample **sınıfı**: deletepartnercustomerrelationship. cs</span><span class="sxs-lookup"><span data-stu-id="f230e-133">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f230e-134">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f230e-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f230e-135">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f230e-135">Request syntax</span></span>

| <span data-ttu-id="f230e-136">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f230e-136">Method</span></span>     | <span data-ttu-id="f230e-137">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f230e-137">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f230e-138">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="f230e-138">**PATCH**</span></span>  | <span data-ttu-id="f230e-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/http/1.1</span><span class="sxs-lookup"><span data-stu-id="f230e-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f230e-140">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="f230e-140">URI parameter</span></span>

<span data-ttu-id="f230e-141">Bu tablo, satıcı ilişkisini kaldırmak için gerekli sorgu parametrelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="f230e-141">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="f230e-142">Ad</span><span class="sxs-lookup"><span data-stu-id="f230e-142">Name</span></span>                   | <span data-ttu-id="f230e-143">Tür</span><span class="sxs-lookup"><span data-stu-id="f230e-143">Type</span></span>     | <span data-ttu-id="f230e-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f230e-144">Required</span></span> | <span data-ttu-id="f230e-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f230e-145">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="f230e-146">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="f230e-146">**customer-tenant-id**</span></span> | <span data-ttu-id="f230e-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="f230e-147">**guid**</span></span> | <span data-ttu-id="f230e-148">Y</span><span class="sxs-lookup"><span data-stu-id="f230e-148">Y</span></span>        | <span data-ttu-id="f230e-149">Değer, müşteriyi tanımlayan bir GUID biçimli **Müşteri-Kiracı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="f230e-149">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f230e-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f230e-150">Request headers</span></span>

<span data-ttu-id="f230e-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f230e-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f230e-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f230e-152">Request body</span></span>

<span data-ttu-id="f230e-153">İstek gövdesinde bir **Müşteri** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f230e-153">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="f230e-154">**Relationshiptopartner** özelliğinin None olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f230e-154">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="f230e-155">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f230e-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f230e-156">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f230e-156">REST response</span></span>

<span data-ttu-id="f230e-157">Başarılı olursa, bu yöntem belirtilen müşteri için bir satıcı ilişkisini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f230e-157">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f230e-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f230e-158">Response success and error codes</span></span>

<span data-ttu-id="f230e-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f230e-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f230e-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f230e-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f230e-161">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f230e-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f230e-162">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f230e-162">Response example</span></span>

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
