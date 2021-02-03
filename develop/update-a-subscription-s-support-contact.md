---
title: Bir aboneliğin destek kişisini güncelleştirme
description: Bir aboneliğin destek kişisini iş ortağının değer eklenmiş satıcılarından biriyle güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769587"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="a9e2c-103">Bir aboneliğin destek kişisini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a9e2c-103">Update a subscription's support contact</span></span>

<span data-ttu-id="a9e2c-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="a9e2c-104">**Applies To**</span></span>

- <span data-ttu-id="a9e2c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9e2c-105">Partner Center</span></span>
- <span data-ttu-id="a9e2c-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9e2c-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a9e2c-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9e2c-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a9e2c-108">Bir aboneliğin destek kişisini iş ortağının değer eklenmiş satıcılarından biriyle güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-108">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9e2c-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a9e2c-109">Prerequisites</span></span>

- <span data-ttu-id="a9e2c-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a9e2c-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a9e2c-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a9e2c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a9e2c-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a9e2c-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a9e2c-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a9e2c-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a9e2c-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="a9e2c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a9e2c-118">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-118">A subscription identifier.</span></span>

- <span data-ttu-id="a9e2c-119">Yeni destek kişisi hakkında bilgi: kiracı tanımlayıcı, Microsoft İş Ortağı Ağı tanımlayıcı ve ad.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-119">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="a9e2c-120">Destek kişisi, ortağın değer eklenmiş satıcılarından biri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-120">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="a9e2c-121">C\#</span><span class="sxs-lookup"><span data-stu-id="a9e2c-121">C\#</span></span>

<span data-ttu-id="a9e2c-122">Bir aboneliğin destek ilgili kişisini güncelleştirmek için ilk olarak bir [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) nesnesi oluşturun ve yeni değerlerle doldurun.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-122">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="a9e2c-123">Ardından müşteriyi tanımlamak için [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-123">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="a9e2c-124">Ardından, abonelik KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-124">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="a9e2c-125">Ardından, iletişim işlemlerini desteklemek için bir arabirim elde etmek üzere [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-125">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="a9e2c-126">Son olarak, destek kişisini güncelleştirmek için, doldurulmuş SupportContact nesnesiyle [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) veya [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

<span data-ttu-id="a9e2c-127">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9e2c-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a9e2c-128">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="a9e2c-128">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a9e2c-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a9e2c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a9e2c-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a9e2c-130">Request syntax</span></span>

| <span data-ttu-id="a9e2c-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a9e2c-131">Method</span></span>  | <span data-ttu-id="a9e2c-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a9e2c-132">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a9e2c-133">**PUT**</span><span class="sxs-lookup"><span data-stu-id="a9e2c-133">**PUT**</span></span> | <span data-ttu-id="a9e2c-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="a9e2c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a9e2c-135">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="a9e2c-135">URI parameter</span></span>

<span data-ttu-id="a9e2c-136">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-136">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="a9e2c-137">Ad</span><span class="sxs-lookup"><span data-stu-id="a9e2c-137">Name</span></span>            | <span data-ttu-id="a9e2c-138">Tür</span><span class="sxs-lookup"><span data-stu-id="a9e2c-138">Type</span></span>   | <span data-ttu-id="a9e2c-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a9e2c-139">Required</span></span> | <span data-ttu-id="a9e2c-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a9e2c-140">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="a9e2c-141">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="a9e2c-141">customer-id</span></span>     | <span data-ttu-id="a9e2c-142">string</span><span class="sxs-lookup"><span data-stu-id="a9e2c-142">string</span></span> | <span data-ttu-id="a9e2c-143">Yes</span><span class="sxs-lookup"><span data-stu-id="a9e2c-143">Yes</span></span>      | <span data-ttu-id="a9e2c-144">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-144">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="a9e2c-145">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="a9e2c-145">subscription-id</span></span> | <span data-ttu-id="a9e2c-146">string</span><span class="sxs-lookup"><span data-stu-id="a9e2c-146">string</span></span> | <span data-ttu-id="a9e2c-147">Yes</span><span class="sxs-lookup"><span data-stu-id="a9e2c-147">Yes</span></span>      | <span data-ttu-id="a9e2c-148">Deneme aboneliğini tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-148">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a9e2c-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a9e2c-149">Request headers</span></span>

<span data-ttu-id="a9e2c-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a9e2c-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a9e2c-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a9e2c-151">Request body</span></span>

<span data-ttu-id="a9e2c-152">İstek gövdesine doldurulmuş bir [Supportcontact](subscription-resources.md#supportcontact) kaynağı dahil etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-152">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="a9e2c-153">Destek ilgili kişisi, iş ortağıyla ilişkisi olan mevcut bir satıcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-153">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="a9e2c-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a9e2c-154">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="a9e2c-155">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a9e2c-155">REST response</span></span>

<span data-ttu-id="a9e2c-156">Başarılı olursa, yanıt gövdesi [Supportcontact](subscription-resources.md#supportcontact) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-156">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a9e2c-157">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a9e2c-157">Response success and error codes</span></span>

<span data-ttu-id="a9e2c-158">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a9e2c-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9e2c-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a9e2c-160">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a9e2c-160">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a9e2c-161">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a9e2c-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
