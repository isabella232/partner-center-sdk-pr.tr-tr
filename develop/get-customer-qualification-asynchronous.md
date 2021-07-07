---
title: Müşterinin niteliklerini al
description: Iş Ortağı Merkezi API 'SI aracılığıyla bir müşterinin nitelemesini almak için zaman uyumsuz doğrulamayı nasıl kullanacağınızı öğrenin. İş ortakları Eğitim müşterilerini doğrulamak için bunu kullanabilir.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 4795b6e1ad008f9d854dc7efbee0c2099aefa609
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446318"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="08ebd-104">Müşterinin nitelemesini zaman uyumsuz olarak al</span><span class="sxs-lookup"><span data-stu-id="08ebd-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="08ebd-105">Müşterinin niteliklerini zaman uyumsuz olarak alma.</span><span class="sxs-lookup"><span data-stu-id="08ebd-105">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08ebd-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="08ebd-106">Prerequisites</span></span>

- <span data-ttu-id="08ebd-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="08ebd-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="08ebd-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="08ebd-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="08ebd-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="08ebd-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="08ebd-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08ebd-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="08ebd-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="08ebd-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="08ebd-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="08ebd-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="08ebd-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="08ebd-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="08ebd-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="08ebd-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="08ebd-115">C\#</span><span class="sxs-lookup"><span data-stu-id="08ebd-115">C\#</span></span>

<span data-ttu-id="08ebd-116">Müşterinin niteliklerini almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="08ebd-116">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="08ebd-117">Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="08ebd-117">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="08ebd-118">Son olarak, `GetQualifications()` `GetQualificationsAsync()` müşterinin niteliklerini almak için veya öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="08ebd-118">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="08ebd-119">**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="08ebd-119">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="08ebd-120">**Project**: sdksamples **sınıfı**: getcustomernitelikler. cs</span><span class="sxs-lookup"><span data-stu-id="08ebd-120">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="08ebd-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="08ebd-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="08ebd-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="08ebd-122">Request syntax</span></span>

| <span data-ttu-id="08ebd-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="08ebd-123">Method</span></span>  | <span data-ttu-id="08ebd-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="08ebd-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="08ebd-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="08ebd-125">**GET**</span></span> | <span data-ttu-id="08ebd-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/nitelikler http/1.1</span><span class="sxs-lookup"><span data-stu-id="08ebd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="08ebd-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="08ebd-127">URI parameter</span></span>

<span data-ttu-id="08ebd-128">Bu tabloda, tüm nitelemeyi almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="08ebd-128">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="08ebd-129">Ad</span><span class="sxs-lookup"><span data-stu-id="08ebd-129">Name</span></span>               | <span data-ttu-id="08ebd-130">Tür</span><span class="sxs-lookup"><span data-stu-id="08ebd-130">Type</span></span>   | <span data-ttu-id="08ebd-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08ebd-131">Required</span></span> | <span data-ttu-id="08ebd-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08ebd-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="08ebd-133">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="08ebd-133">**customer-tenant-id**</span></span> | <span data-ttu-id="08ebd-134">string</span><span class="sxs-lookup"><span data-stu-id="08ebd-134">string</span></span> | <span data-ttu-id="08ebd-135">Yes</span><span class="sxs-lookup"><span data-stu-id="08ebd-135">Yes</span></span>      | <span data-ttu-id="08ebd-136">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="08ebd-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="08ebd-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="08ebd-137">Request headers</span></span>

<span data-ttu-id="08ebd-138">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="08ebd-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="08ebd-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="08ebd-139">Request body</span></span>

<span data-ttu-id="08ebd-140">Yok.</span><span class="sxs-lookup"><span data-stu-id="08ebd-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="08ebd-141">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="08ebd-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="08ebd-142">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="08ebd-142">REST response</span></span>

<span data-ttu-id="08ebd-143">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelikler koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="08ebd-143">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="08ebd-144">**Eğitim** nitelemesini içeren bir müşterinin **Get** çağrısının örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="08ebd-144">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="08ebd-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="08ebd-145">Response success and error codes</span></span>

<span data-ttu-id="08ebd-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="08ebd-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="08ebd-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="08ebd-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="08ebd-148">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="08ebd-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="08ebd-149">Yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="08ebd-149">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="08ebd-150">Onaylandı</span><span class="sxs-lookup"><span data-stu-id="08ebd-150">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="08ebd-151">Gözden Geçiriliyor</span><span class="sxs-lookup"><span data-stu-id="08ebd-151">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="08ebd-152">Reddedildi</span><span class="sxs-lookup"><span data-stu-id="08ebd-152">Denied</span></span>

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

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="08ebd-153">Eyalet ait varlık örnekleri</span><span class="sxs-lookup"><span data-stu-id="08ebd-153">State Owned Entity Samples</span></span>

<span data-ttu-id="08ebd-154">**GÖNDERI örneği aracılığıyla durum sahibi olan varlık**</span><span class="sxs-lookup"><span data-stu-id="08ebd-154">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="08ebd-155">**Get nitelikleri örneği aracılığıyla durum sahibi olan varlık**</span><span class="sxs-lookup"><span data-stu-id="08ebd-155">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="08ebd-156">**Eğitim ile Get nitelikleri aracılığıyla durum sahibi olan varlık**</span><span class="sxs-lookup"><span data-stu-id="08ebd-156">**State Owned Entity via Get Qualifications with Education**</span></span>

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

<span data-ttu-id="08ebd-157">**GCC ile sahip olan varlık, Get nitelikleri aracılığıyla**</span><span class="sxs-lookup"><span data-stu-id="08ebd-157">**State Owned Entity via Get Qualifications with GCC**</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="08ebd-158">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="08ebd-158">Related articles</span></span>

- [<span data-ttu-id="08ebd-159">Müşterinin niteliklerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="08ebd-159">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
