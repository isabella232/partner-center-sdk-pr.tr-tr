---
title: Bir aboneliğin destek kişisini alma
description: Aboneliğin destek kişisini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df3bce48902d95dc541c4a45e4e633569fc4406e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769274"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="60041-103">Bir aboneliğin destek kişisini alma</span><span class="sxs-lookup"><span data-stu-id="60041-103">Get a subscription's support contact</span></span>

<span data-ttu-id="60041-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="60041-104">**Applies To**</span></span>

- <span data-ttu-id="60041-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="60041-105">Partner Center</span></span>
- <span data-ttu-id="60041-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="60041-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="60041-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="60041-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="60041-108">Aboneliğin destek kişisini alma.</span><span class="sxs-lookup"><span data-stu-id="60041-108">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60041-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="60041-109">Prerequisites</span></span>

- <span data-ttu-id="60041-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="60041-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="60041-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="60041-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="60041-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60041-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="60041-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60041-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="60041-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="60041-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="60041-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="60041-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="60041-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="60041-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="60041-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="60041-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="60041-118">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="60041-118">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="60041-119">C\#</span><span class="sxs-lookup"><span data-stu-id="60041-119">C\#</span></span>

<span data-ttu-id="60041-120">Bir aboneliğin destek ilgili kişisini almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="60041-120">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="60041-121">Ardından, abonelik KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="60041-121">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="60041-122">Ardından, iletişim işlemlerini desteklemek için bir arabirim elde etmek üzere [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) özelliğini kullanın ve ardından [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) nesnesini almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="60041-122">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="60041-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="60041-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="60041-124">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="60041-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="60041-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="60041-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="60041-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="60041-126">Request syntax</span></span>

| <span data-ttu-id="60041-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="60041-127">Method</span></span>  | <span data-ttu-id="60041-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="60041-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="60041-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="60041-129">**GET**</span></span> | <span data-ttu-id="60041-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="60041-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="60041-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="60041-131">URI parameter</span></span>

<span data-ttu-id="60041-132">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="60041-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="60041-133">Ad</span><span class="sxs-lookup"><span data-stu-id="60041-133">Name</span></span>            | <span data-ttu-id="60041-134">Tür</span><span class="sxs-lookup"><span data-stu-id="60041-134">Type</span></span>   | <span data-ttu-id="60041-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="60041-135">Required</span></span> | <span data-ttu-id="60041-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="60041-136">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="60041-137">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="60041-137">customer-id</span></span>     | <span data-ttu-id="60041-138">string</span><span class="sxs-lookup"><span data-stu-id="60041-138">string</span></span> | <span data-ttu-id="60041-139">Yes</span><span class="sxs-lookup"><span data-stu-id="60041-139">Yes</span></span>      | <span data-ttu-id="60041-140">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="60041-140">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="60041-141">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="60041-141">subscription-id</span></span> | <span data-ttu-id="60041-142">string</span><span class="sxs-lookup"><span data-stu-id="60041-142">string</span></span> | <span data-ttu-id="60041-143">Yes</span><span class="sxs-lookup"><span data-stu-id="60041-143">Yes</span></span>      | <span data-ttu-id="60041-144">Deneme aboneliğini tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="60041-144">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="60041-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="60041-145">Request headers</span></span>

<span data-ttu-id="60041-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="60041-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="60041-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="60041-147">Request body</span></span>

<span data-ttu-id="60041-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="60041-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="60041-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="60041-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="60041-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="60041-150">REST response</span></span>

<span data-ttu-id="60041-151">Başarılı olursa, yanıt gövdesi [Supportcontact](subscription-resources.md#supportcontact) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="60041-151">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="60041-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="60041-152">Response success and error codes</span></span>

<span data-ttu-id="60041-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="60041-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="60041-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="60041-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="60041-155">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="60041-155">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="60041-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="60041-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

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
