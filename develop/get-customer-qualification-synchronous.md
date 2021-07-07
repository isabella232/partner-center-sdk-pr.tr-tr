---
title: Müşterinin nitelemesini alma
description: İş Ortağı Merkezi API aracılığıyla müşterinin niteliğini almak için zaman uyumlu doğrulamayı kullanmayı öğrenin. İş ortakları Eğitim müşterilerini doğrulamak için bunu kullanabilir.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446352"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="34f78-104">Zaman uyumlu doğrulama yoluyla müşterinin niteliğini elde etmek</span><span class="sxs-lookup"><span data-stu-id="34f78-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="34f78-105">Api'leri kullanarak müşterinin niteliğini zaman uyumlu olarak İş Ortağı Merkezi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="34f78-105">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="34f78-106">Bu işlemi zaman uyumsuz olarak yapmayı öğrenmek için bkz. Zaman uyumsuz doğrulama [yoluyla müşterinin niteliğini al.](get-customer-qualification-asynchronous.md)</span><span class="sxs-lookup"><span data-stu-id="34f78-106">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34f78-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="34f78-107">Prerequisites</span></span>

- <span data-ttu-id="34f78-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="34f78-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="34f78-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="34f78-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="34f78-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="34f78-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="34f78-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="34f78-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="34f78-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="34f78-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="34f78-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="34f78-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="34f78-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="34f78-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="34f78-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="34f78-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="34f78-116">C\#</span><span class="sxs-lookup"><span data-stu-id="34f78-116">C\#</span></span>

<span data-ttu-id="34f78-117">Müşterinin niteliğini almak için müşteri tanımlayıcısıyla [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="34f78-117">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="34f78-118">Ardından Bir [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**Nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="34f78-118">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="34f78-119">Son olarak, [**müşterinin niteliğini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) almak için Get veya [**GetAsync'i**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) arayın.</span><span class="sxs-lookup"><span data-stu-id="34f78-119">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="34f78-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="34f78-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="34f78-121">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="34f78-121">Request syntax</span></span>

| <span data-ttu-id="34f78-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="34f78-122">Method</span></span>  | <span data-ttu-id="34f78-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="34f78-123">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="34f78-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="34f78-124">**GET**</span></span> | <span data-ttu-id="34f78-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="34f78-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="34f78-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="34f78-126">URI parameter</span></span>

<span data-ttu-id="34f78-127">Bu tabloda tüm niteliği almak için gerekli sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="34f78-127">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="34f78-128">Ad</span><span class="sxs-lookup"><span data-stu-id="34f78-128">Name</span></span>               | <span data-ttu-id="34f78-129">Tür</span><span class="sxs-lookup"><span data-stu-id="34f78-129">Type</span></span>   | <span data-ttu-id="34f78-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34f78-130">Required</span></span> | <span data-ttu-id="34f78-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34f78-131">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="34f78-132">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="34f78-132">**customer-tenant-id**</span></span> | <span data-ttu-id="34f78-133">string</span><span class="sxs-lookup"><span data-stu-id="34f78-133">string</span></span> | <span data-ttu-id="34f78-134">Yes</span><span class="sxs-lookup"><span data-stu-id="34f78-134">Yes</span></span>      | <span data-ttu-id="34f78-135">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="34f78-135">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="34f78-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="34f78-136">Request headers</span></span>

<span data-ttu-id="34f78-137">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="34f78-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="34f78-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="34f78-138">Request body</span></span>

<span data-ttu-id="34f78-139">Yok.</span><span class="sxs-lookup"><span data-stu-id="34f78-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="34f78-140">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="34f78-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="34f78-141">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="34f78-141">REST response</span></span>

<span data-ttu-id="34f78-142">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelik değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="34f78-142">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="34f78-143">Aşağıda, eğitim niteliğine sahip bir müşteriye yapılan **GET** çağrısının **bir örneği verilmiştir.**</span><span class="sxs-lookup"><span data-stu-id="34f78-143">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="34f78-144">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="34f78-144">Response success and error codes</span></span>

<span data-ttu-id="34f78-145">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="34f78-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="34f78-146">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="34f78-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="34f78-147">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="34f78-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="34f78-148">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="34f78-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="34f78-149">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="34f78-149">Related articles</span></span>

- [<span data-ttu-id="34f78-150">Müşterinin yeterliliğini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="34f78-150">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)