---
title: Müşterinin niteliklerini al
description: Iş Ortağı Merkezi API 'SI aracılığıyla bir müşterinin nitelemesini almak için zaman uyumsuz doğrulamayı nasıl kullanacağınızı öğrenin. İş ortakları Eğitim müşterilerini doğrulamak için bunu kullanabilir.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 130ee276461e3390ac78ac7abd8baeefe6a70d7c
ms.sourcegitcommit: 97f93caa57df6c64fe19868e6b2a0f7937226b51
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/21/2021
ms.locfileid: "98636392"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="9852b-104">Müşterinin nitelemesini zaman uyumsuz olarak al</span><span class="sxs-lookup"><span data-stu-id="9852b-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="9852b-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="9852b-105">**Applies To**</span></span>

- <span data-ttu-id="9852b-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9852b-106">Partner Center</span></span>

<span data-ttu-id="9852b-107">Müşterinin niteliklerini zaman uyumsuz olarak alma.</span><span class="sxs-lookup"><span data-stu-id="9852b-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9852b-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9852b-108">Prerequisites</span></span>

- <span data-ttu-id="9852b-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9852b-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9852b-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9852b-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9852b-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9852b-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9852b-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9852b-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9852b-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9852b-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9852b-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9852b-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9852b-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9852b-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9852b-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9852b-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="9852b-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9852b-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9852b-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9852b-118">Request syntax</span></span>

| <span data-ttu-id="9852b-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9852b-119">Method</span></span>  | <span data-ttu-id="9852b-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9852b-120">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9852b-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="9852b-121">**GET**</span></span> | <span data-ttu-id="9852b-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/nitelikler http/1.1</span><span class="sxs-lookup"><span data-stu-id="9852b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9852b-123">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="9852b-123">URI parameter</span></span>

<span data-ttu-id="9852b-124">Bu tabloda, tüm nitelemeyi almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="9852b-124">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="9852b-125">Ad</span><span class="sxs-lookup"><span data-stu-id="9852b-125">Name</span></span>               | <span data-ttu-id="9852b-126">Tür</span><span class="sxs-lookup"><span data-stu-id="9852b-126">Type</span></span>   | <span data-ttu-id="9852b-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9852b-127">Required</span></span> | <span data-ttu-id="9852b-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9852b-128">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="9852b-129">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="9852b-129">**customer-tenant-id**</span></span> | <span data-ttu-id="9852b-130">string</span><span class="sxs-lookup"><span data-stu-id="9852b-130">string</span></span> | <span data-ttu-id="9852b-131">Yes</span><span class="sxs-lookup"><span data-stu-id="9852b-131">Yes</span></span>      | <span data-ttu-id="9852b-132">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="9852b-132">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9852b-133">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9852b-133">Request headers</span></span>

<span data-ttu-id="9852b-134">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9852b-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9852b-135">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9852b-135">Request body</span></span>

<span data-ttu-id="9852b-136">Yok.</span><span class="sxs-lookup"><span data-stu-id="9852b-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9852b-137">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9852b-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="9852b-138">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9852b-138">REST response</span></span>

<span data-ttu-id="9852b-139">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelikler koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="9852b-139">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="9852b-140">**Eğitim** nitelemesini içeren bir müşterinin **Get** çağrısının örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9852b-140">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9852b-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9852b-141">Response success and error codes</span></span>

<span data-ttu-id="9852b-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9852b-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9852b-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9852b-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9852b-144">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9852b-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="9852b-145">Yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="9852b-145">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="9852b-146">Onaylandı</span><span class="sxs-lookup"><span data-stu-id="9852b-146">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a><span data-ttu-id="9852b-147">Gözden Geçiriliyor</span><span class="sxs-lookup"><span data-stu-id="9852b-147">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a><span data-ttu-id="9852b-148">Reddedildi</span><span class="sxs-lookup"><span data-stu-id="9852b-148">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a><span data-ttu-id="9852b-149">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="9852b-149">Related articles</span></span>

- [<span data-ttu-id="9852b-150">Müşterinin niteliklerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9852b-150">Update a customer's qualifications</span></span>](update-a-customer-s-qualifications.md)