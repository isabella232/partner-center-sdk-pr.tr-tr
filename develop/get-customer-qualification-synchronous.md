---
title: Müşterinin nitelemesini alma
description: Iş Ortağı Merkezi API 'SI aracılığıyla bir müşterinin nitelemesini almak için zaman uyumlu doğrulamayı nasıl kullanacağınızı öğrenin. İş ortakları Eğitim müşterilerini doğrulamak için bunu kullanabilir.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e39ace3b598736abed6ab22021a8b93d473486a3
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711923"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="bf1f9-104">Zaman uyumlu doğrulama yoluyla bir müşterinin nitelemesini al</span><span class="sxs-lookup"><span data-stu-id="bf1f9-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="bf1f9-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="bf1f9-105">**Applies To**</span></span>

- <span data-ttu-id="bf1f9-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bf1f9-106">Partner Center</span></span>

<span data-ttu-id="bf1f9-107">Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin nitelemesini eşzamanlı olarak nasıl alabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="bf1f9-108">Bunu zaman uyumsuz yapma hakkında bilgi edinmek için bkz. [zaman uyumsuz doğrulama aracılığıyla Müşterinin nitelemesini alma](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="bf1f9-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf1f9-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bf1f9-109">Prerequisites</span></span>

- <span data-ttu-id="bf1f9-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bf1f9-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bf1f9-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bf1f9-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bf1f9-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bf1f9-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bf1f9-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bf1f9-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bf1f9-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="bf1f9-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="bf1f9-118">C\#</span><span class="sxs-lookup"><span data-stu-id="bf1f9-118">C\#</span></span>

<span data-ttu-id="bf1f9-119">Müşterinin nitelemesini almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="bf1f9-120">Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="bf1f9-121">Son olarak, müşterinin nitelemesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="bf1f9-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="bf1f9-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bf1f9-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="bf1f9-123">Request syntax</span></span>

| <span data-ttu-id="bf1f9-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="bf1f9-124">Method</span></span>  | <span data-ttu-id="bf1f9-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="bf1f9-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bf1f9-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="bf1f9-126">**GET**</span></span> | <span data-ttu-id="bf1f9-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/nitelik http/1.1</span><span class="sxs-lookup"><span data-stu-id="bf1f9-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bf1f9-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="bf1f9-128">URI parameter</span></span>

<span data-ttu-id="bf1f9-129">Bu tabloda, tüm nitelemeyi almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="bf1f9-130">Ad</span><span class="sxs-lookup"><span data-stu-id="bf1f9-130">Name</span></span>               | <span data-ttu-id="bf1f9-131">Tür</span><span class="sxs-lookup"><span data-stu-id="bf1f9-131">Type</span></span>   | <span data-ttu-id="bf1f9-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bf1f9-132">Required</span></span> | <span data-ttu-id="bf1f9-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf1f9-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="bf1f9-134">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="bf1f9-134">**customer-tenant-id**</span></span> | <span data-ttu-id="bf1f9-135">string</span><span class="sxs-lookup"><span data-stu-id="bf1f9-135">string</span></span> | <span data-ttu-id="bf1f9-136">Yes</span><span class="sxs-lookup"><span data-stu-id="bf1f9-136">Yes</span></span>      | <span data-ttu-id="bf1f9-137">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bf1f9-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="bf1f9-138">Request headers</span></span>

<span data-ttu-id="bf1f9-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bf1f9-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bf1f9-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="bf1f9-140">Request body</span></span>

<span data-ttu-id="bf1f9-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bf1f9-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="bf1f9-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="bf1f9-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="bf1f9-143">REST response</span></span>

<span data-ttu-id="bf1f9-144">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelik değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="bf1f9-145">**Eğitim** nitelemesini içeren bir müşterinin **Get** çağrısına bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bf1f9-146">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="bf1f9-146">Response success and error codes</span></span>

<span data-ttu-id="bf1f9-147">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bf1f9-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf1f9-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bf1f9-149">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bf1f9-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bf1f9-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="bf1f9-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="bf1f9-151">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="bf1f9-151">Related articles</span></span>

- [<span data-ttu-id="bf1f9-152">Müşterinin yeterliliğini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bf1f9-152">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)