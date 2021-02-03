---
title: Müşterinin niteliklerini al
description: Iş Ortağı Merkezi API 'SI aracılığıyla bir müşterinin nitelemesini almak için zaman uyumsuz doğrulamayı nasıl kullanacağınızı öğrenin. İş ortakları Eğitim müşterilerini doğrulamak için bunu kullanabilir.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 9f9b9aaddde0d66caf9c7ef32e8fba6d5e3aba36
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770189"
---
# <a name="get-a-customers-qualifications-via-asynchronous-validation"></a><span data-ttu-id="84c8c-104">Zaman uyumsuz doğrulama aracılığıyla bir müşterinin niteliklerini al</span><span class="sxs-lookup"><span data-stu-id="84c8c-104">Get a customer's qualifications via asynchronous validation</span></span>

<span data-ttu-id="84c8c-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="84c8c-105">**Applies To**</span></span>

- <span data-ttu-id="84c8c-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="84c8c-106">Partner Center</span></span>

<span data-ttu-id="84c8c-107">Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin niteliklerini zaman uyumsuz olarak almayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="84c8c-107">Learn how to get a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="84c8c-108">Bunu eşzamanlı olarak nasıl yapacağınızı öğrenmek için bkz. [zaman uyumlu doğrulama aracılığıyla bir müşterinin nitelemesini alma](get-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="84c8c-108">To learn how to do this synchronously, see [Get a customer's qualification via synchronous validation](get-customer-qualification-synchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84c8c-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="84c8c-109">Prerequisites</span></span>

- <span data-ttu-id="84c8c-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="84c8c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="84c8c-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="84c8c-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="84c8c-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="84c8c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="84c8c-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84c8c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="84c8c-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="84c8c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="84c8c-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="84c8c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="84c8c-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="84c8c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="84c8c-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="84c8c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="84c8c-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="84c8c-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="84c8c-119">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="84c8c-119">Request syntax</span></span>

| <span data-ttu-id="84c8c-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="84c8c-120">Method</span></span>  | <span data-ttu-id="84c8c-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="84c8c-121">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="84c8c-122">**Al**</span><span class="sxs-lookup"><span data-stu-id="84c8c-122">**GET**</span></span> | <span data-ttu-id="84c8c-123">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/nitelikler http/1.1</span><span class="sxs-lookup"><span data-stu-id="84c8c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="84c8c-124">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="84c8c-124">URI parameter</span></span>

<span data-ttu-id="84c8c-125">Bu tabloda, tüm nitelemeyi almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="84c8c-125">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="84c8c-126">Ad</span><span class="sxs-lookup"><span data-stu-id="84c8c-126">Name</span></span>               | <span data-ttu-id="84c8c-127">Tür</span><span class="sxs-lookup"><span data-stu-id="84c8c-127">Type</span></span>   | <span data-ttu-id="84c8c-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="84c8c-128">Required</span></span> | <span data-ttu-id="84c8c-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84c8c-129">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="84c8c-130">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="84c8c-130">**customer-tenant-id**</span></span> | <span data-ttu-id="84c8c-131">string</span><span class="sxs-lookup"><span data-stu-id="84c8c-131">string</span></span> | <span data-ttu-id="84c8c-132">Yes</span><span class="sxs-lookup"><span data-stu-id="84c8c-132">Yes</span></span>      | <span data-ttu-id="84c8c-133">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="84c8c-133">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="84c8c-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="84c8c-134">Request headers</span></span>

<span data-ttu-id="84c8c-135">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="84c8c-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="84c8c-136">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="84c8c-136">Request body</span></span>

<span data-ttu-id="84c8c-137">Yok.</span><span class="sxs-lookup"><span data-stu-id="84c8c-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="84c8c-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="84c8c-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="84c8c-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="84c8c-139">REST response</span></span>

<span data-ttu-id="84c8c-140">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelikler koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="84c8c-140">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="84c8c-141">**Eğitim** nitelemesini içeren bir müşterinin **Get** çağrısının örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="84c8c-141">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="84c8c-142">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="84c8c-142">Response success and error codes</span></span>

<span data-ttu-id="84c8c-143">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="84c8c-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="84c8c-144">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="84c8c-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="84c8c-145">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="84c8c-145">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="84c8c-146">Yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="84c8c-146">Response examples</span></span>

<span data-ttu-id="84c8c-147">Bu bölümde, bir müşteri olduğunda alacağınız yanıtlar gösterilmektedir `vettingStatus` :</span><span class="sxs-lookup"><span data-stu-id="84c8c-147">This section shows responses you might receive when a customer's `vettingStatus` is:</span></span>

- <span data-ttu-id="84c8c-148">Onaylandı</span><span class="sxs-lookup"><span data-stu-id="84c8c-148">Approved</span></span>
- <span data-ttu-id="84c8c-149">Gözden Geçiriliyor</span><span class="sxs-lookup"><span data-stu-id="84c8c-149">In Review</span></span>
- <span data-ttu-id="84c8c-150">Reddedildi</span><span class="sxs-lookup"><span data-stu-id="84c8c-150">Denied</span></span>

<span data-ttu-id="84c8c-151">**Onaylanan** örnek:</span><span class="sxs-lookup"><span data-stu-id="84c8c-151">**Approved** example:</span></span>

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

<span data-ttu-id="84c8c-152">**İnceleme** örneği:</span><span class="sxs-lookup"><span data-stu-id="84c8c-152">**In Review** example:</span></span>

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

<span data-ttu-id="84c8c-153">**Engellenen** örnek:</span><span class="sxs-lookup"><span data-stu-id="84c8c-153">**Denied** example:</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="84c8c-154">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="84c8c-154">Related articles</span></span>

- [<span data-ttu-id="84c8c-155">Müşterinin niteliklerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="84c8c-155">Update a customer's qualifications</span></span>](update-a-customer-s-qualifications.md)