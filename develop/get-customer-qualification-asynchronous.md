---
title: Müşterinin niteliklerini al
description: Iş Ortağı Merkezi API 'SI aracılığıyla bir müşterinin nitelemesini almak için zaman uyumsuz doğrulamayı nasıl kullanacağınızı öğrenin. İş ortakları Eğitim müşterilerini doğrulamak için bunu kullanabilir.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: df605e4d400d29e14fd0b44bef34f88bbc7ca8b2
ms.sourcegitcommit: 7d59c58ee36b217bd5cac089f918059e9dbb8a62
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/19/2021
ms.locfileid: "110027937"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="b7846-104">Müşterinin nitelemesini zaman uyumsuz olarak al</span><span class="sxs-lookup"><span data-stu-id="b7846-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="b7846-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="b7846-105">**Applies To**</span></span>

- <span data-ttu-id="b7846-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b7846-106">Partner Center</span></span>

<span data-ttu-id="b7846-107">Müşterinin niteliklerini zaman uyumsuz olarak alma.</span><span class="sxs-lookup"><span data-stu-id="b7846-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7846-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b7846-108">Prerequisites</span></span>

- <span data-ttu-id="b7846-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b7846-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b7846-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="b7846-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b7846-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b7846-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b7846-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7846-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b7846-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b7846-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b7846-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b7846-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b7846-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="b7846-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b7846-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="b7846-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b7846-117">C\#</span><span class="sxs-lookup"><span data-stu-id="b7846-117">C\#</span></span>

<span data-ttu-id="b7846-118">Müşterinin niteliklerini almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="b7846-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="b7846-119">Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7846-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="b7846-120">Son olarak, `GetQualifications()` `GetQualificationsAsync()` müşterinin niteliklerini almak için veya öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="b7846-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="b7846-121">**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="b7846-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="b7846-122">**Proje**: Sdksamples **sınıfı**: getcustomernitelikler. cs</span><span class="sxs-lookup"><span data-stu-id="b7846-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b7846-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="b7846-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b7846-124">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="b7846-124">Request syntax</span></span>

| <span data-ttu-id="b7846-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b7846-125">Method</span></span>  | <span data-ttu-id="b7846-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="b7846-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b7846-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="b7846-127">**GET**</span></span> | <span data-ttu-id="b7846-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b7846-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b7846-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="b7846-129">URI parameter</span></span>

<span data-ttu-id="b7846-130">Bu tabloda tüm niteliği almak için gerekli sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="b7846-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="b7846-131">Ad</span><span class="sxs-lookup"><span data-stu-id="b7846-131">Name</span></span>               | <span data-ttu-id="b7846-132">Tür</span><span class="sxs-lookup"><span data-stu-id="b7846-132">Type</span></span>   | <span data-ttu-id="b7846-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b7846-133">Required</span></span> | <span data-ttu-id="b7846-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7846-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="b7846-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="b7846-135">**customer-tenant-id**</span></span> | <span data-ttu-id="b7846-136">string</span><span class="sxs-lookup"><span data-stu-id="b7846-136">string</span></span> | <span data-ttu-id="b7846-137">Yes</span><span class="sxs-lookup"><span data-stu-id="b7846-137">Yes</span></span>      | <span data-ttu-id="b7846-138">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="b7846-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b7846-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="b7846-139">Request headers</span></span>

<span data-ttu-id="b7846-140">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b7846-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b7846-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b7846-141">Request body</span></span>

<span data-ttu-id="b7846-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="b7846-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b7846-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="b7846-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="b7846-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="b7846-144">REST response</span></span>

<span data-ttu-id="b7846-145">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelik koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="b7846-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="b7846-146">Aşağıda, Eğitim niteliğine sahip bir müşteri için **GET** çağrısı örnekleri **verilmiştir.**</span><span class="sxs-lookup"><span data-stu-id="b7846-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b7846-147">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="b7846-147">Response success and error codes</span></span>

<span data-ttu-id="b7846-148">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="b7846-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b7846-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7846-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b7846-150">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b7846-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="b7846-151">Yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="b7846-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="b7846-152">Onaylandı</span><span class="sxs-lookup"><span data-stu-id="b7846-152">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

#### <a name="in-review"></a><span data-ttu-id="b7846-153">Gözden Geçiriliyor</span><span class="sxs-lookup"><span data-stu-id="b7846-153">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

#### <a name="denied"></a><span data-ttu-id="b7846-154">Reddedildi</span><span class="sxs-lookup"><span data-stu-id="b7846-154">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="b7846-155">Eyalete Ait Varlık Örnekleri</span><span class="sxs-lookup"><span data-stu-id="b7846-155">State Owned Entity Samples</span></span>

<span data-ttu-id="b7846-156">**POST örneği aracılığıyla Eyalete Ait Varlık**</span><span class="sxs-lookup"><span data-stu-id="b7846-156">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="b7846-157">**Nitelik Al örneği aracılığıyla Eyalete Ait Varlık**</span><span class="sxs-lookup"><span data-stu-id="b7846-157">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="b7846-158">**Eğitimle Nitelik Al aracılığıyla Eyalete Ait Varlık**</span><span class="sxs-lookup"><span data-stu-id="b7846-158">**State Owned Entity via Get Qualifications with Education**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “Education”,
        “vettingStatus”: “Approved”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="b7846-159">**GCC ile Get nitelikleri aracılığıyla durum sahibi olan varlık**</span><span class="sxs-lookup"><span data-stu-id="b7846-159">**State Owned Entity via Get Qualifications with GCC**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “GovernmentCommunityCloud”,
        “vettingStatus”: “Approved”,
        “vettingCreateDate”: “2021-05-06T19:59:56.6832021+00:00”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="b7846-160">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="b7846-160">Related articles</span></span>

- [<span data-ttu-id="b7846-161">Müşterinin niteliklerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b7846-161">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
