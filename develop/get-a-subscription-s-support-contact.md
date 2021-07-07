---
title: Bir aboneliğin destek kişisini alma
description: Aboneliğin destek kişisi alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b6c98e5ed96f2ca4787e93504c9e094bd46ae783
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760768"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="236d0-103">Bir aboneliğin destek kişisini alma</span><span class="sxs-lookup"><span data-stu-id="236d0-103">Get a subscription's support contact</span></span>

<span data-ttu-id="236d0-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="236d0-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="236d0-105">Aboneliğin destek kişisi alma.</span><span class="sxs-lookup"><span data-stu-id="236d0-105">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="236d0-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="236d0-106">Prerequisites</span></span>

- <span data-ttu-id="236d0-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="236d0-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="236d0-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="236d0-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="236d0-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="236d0-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="236d0-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="236d0-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="236d0-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="236d0-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="236d0-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="236d0-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="236d0-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="236d0-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="236d0-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="236d0-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="236d0-115">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="236d0-115">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="236d0-116">C\#</span><span class="sxs-lookup"><span data-stu-id="236d0-116">C\#</span></span>

<span data-ttu-id="236d0-117">Bir aboneliğin destek ilgili kişisi almak için müşteri kimliğini kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak müşteriyi tanıyın.</span><span class="sxs-lookup"><span data-stu-id="236d0-117">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="236d0-118">Ardından abonelik kimliğiyle [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="236d0-118">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="236d0-119">Ardından, kişi işlemlerini desteklemek üzere bir arabirim elde etmek için [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) özelliğini kullanın ve ardından [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="236d0-119">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="236d0-120">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="236d0-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="236d0-121">**Project:** İş Ortağı Merkezi SDK'sı **Sınıfı:** GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="236d0-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="236d0-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="236d0-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="236d0-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="236d0-123">Request syntax</span></span>

| <span data-ttu-id="236d0-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="236d0-124">Method</span></span>  | <span data-ttu-id="236d0-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="236d0-125">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="236d0-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="236d0-126">**GET**</span></span> | <span data-ttu-id="236d0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="236d0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="236d0-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="236d0-128">URI parameter</span></span>

<span data-ttu-id="236d0-129">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="236d0-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="236d0-130">Ad</span><span class="sxs-lookup"><span data-stu-id="236d0-130">Name</span></span>            | <span data-ttu-id="236d0-131">Tür</span><span class="sxs-lookup"><span data-stu-id="236d0-131">Type</span></span>   | <span data-ttu-id="236d0-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="236d0-132">Required</span></span> | <span data-ttu-id="236d0-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="236d0-133">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="236d0-134">customer-id</span><span class="sxs-lookup"><span data-stu-id="236d0-134">customer-id</span></span>     | <span data-ttu-id="236d0-135">string</span><span class="sxs-lookup"><span data-stu-id="236d0-135">string</span></span> | <span data-ttu-id="236d0-136">Yes</span><span class="sxs-lookup"><span data-stu-id="236d0-136">Yes</span></span>      | <span data-ttu-id="236d0-137">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="236d0-137">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="236d0-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="236d0-138">subscription-id</span></span> | <span data-ttu-id="236d0-139">string</span><span class="sxs-lookup"><span data-stu-id="236d0-139">string</span></span> | <span data-ttu-id="236d0-140">Yes</span><span class="sxs-lookup"><span data-stu-id="236d0-140">Yes</span></span>      | <span data-ttu-id="236d0-141">Deneme aboneliğini tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="236d0-141">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="236d0-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="236d0-142">Request headers</span></span>

<span data-ttu-id="236d0-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="236d0-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="236d0-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="236d0-144">Request body</span></span>

<span data-ttu-id="236d0-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="236d0-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="236d0-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="236d0-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="236d0-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="236d0-147">REST response</span></span>

<span data-ttu-id="236d0-148">Başarılı olursa yanıt gövdesi [SupportContact kaynağını](subscription-resources.md#supportcontact) içerir.</span><span class="sxs-lookup"><span data-stu-id="236d0-148">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="236d0-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="236d0-149">Response success and error codes</span></span>

<span data-ttu-id="236d0-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="236d0-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="236d0-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="236d0-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="236d0-152">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="236d0-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="236d0-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="236d0-153">Response example</span></span>

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
