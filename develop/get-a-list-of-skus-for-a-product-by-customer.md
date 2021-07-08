---
title: Bir ürüne ait SKU 'ların listesini alın (müşteriye göre)
description: Müşteri tarafından belirtilen ürün için SKU 'ların bir koleksiyonunu alır.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b76526d97ba9027897fc88954ba45186d58aefb8
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874168"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="6b1eb-103">Bir ürüne ait SKU 'ların listesini alın (müşteriye göre)</span><span class="sxs-lookup"><span data-stu-id="6b1eb-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="6b1eb-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6b1eb-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6b1eb-105">Mevcut bir müşterinin kullanabildiği belirli bir ürün için SKU 'ların bir koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-105">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b1eb-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6b1eb-106">Prerequisites</span></span>

- <span data-ttu-id="6b1eb-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6b1eb-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6b1eb-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6b1eb-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6b1eb-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6b1eb-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6b1eb-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6b1eb-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6b1eb-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="6b1eb-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6b1eb-115">Ürün KIMLIĞI (**ürün kimliği**).</span><span class="sxs-lookup"><span data-stu-id="6b1eb-115">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="6b1eb-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6b1eb-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6b1eb-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6b1eb-117">Request syntax</span></span>

| <span data-ttu-id="6b1eb-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6b1eb-118">Method</span></span> | <span data-ttu-id="6b1eb-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6b1eb-119">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6b1eb-120">POST</span><span class="sxs-lookup"><span data-stu-id="6b1eb-120">POST</span></span>   | <span data-ttu-id="6b1eb-121">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products/{product-id}/SKU http/1.1</span><span class="sxs-lookup"><span data-stu-id="6b1eb-121">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="6b1eb-122">İstek URI 'SI parametresi</span><span class="sxs-lookup"><span data-stu-id="6b1eb-122">Request URI parameter</span></span>

| <span data-ttu-id="6b1eb-123">Ad</span><span class="sxs-lookup"><span data-stu-id="6b1eb-123">Name</span></span>               | <span data-ttu-id="6b1eb-124">Tür</span><span class="sxs-lookup"><span data-stu-id="6b1eb-124">Type</span></span> | <span data-ttu-id="6b1eb-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6b1eb-125">Required</span></span> | <span data-ttu-id="6b1eb-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b1eb-126">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="6b1eb-127">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="6b1eb-127">customer-tenant-id</span></span> | <span data-ttu-id="6b1eb-128">GUID</span><span class="sxs-lookup"><span data-stu-id="6b1eb-128">GUID</span></span> | <span data-ttu-id="6b1eb-129">Yes</span><span class="sxs-lookup"><span data-stu-id="6b1eb-129">Yes</span></span> | <span data-ttu-id="6b1eb-130">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-130">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="6b1eb-131">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="6b1eb-131">product-id</span></span> | <span data-ttu-id="6b1eb-132">string</span><span class="sxs-lookup"><span data-stu-id="6b1eb-132">string</span></span> | <span data-ttu-id="6b1eb-133">Yes</span><span class="sxs-lookup"><span data-stu-id="6b1eb-133">Yes</span></span> | <span data-ttu-id="6b1eb-134">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-134">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="6b1eb-135">İstek üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="6b1eb-135">Request header</span></span>

<span data-ttu-id="6b1eb-136">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6b1eb-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6b1eb-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6b1eb-137">Request body</span></span>

<span data-ttu-id="6b1eb-138">Yok.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6b1eb-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6b1eb-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="6b1eb-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6b1eb-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6b1eb-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6b1eb-141">Response success and error codes</span></span>

<span data-ttu-id="6b1eb-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6b1eb-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6b1eb-144">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6b1eb-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="6b1eb-145">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="6b1eb-145">This method returns the following error codes:</span></span>

| <span data-ttu-id="6b1eb-146">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="6b1eb-146">HTTP Status Code</span></span> | <span data-ttu-id="6b1eb-147">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="6b1eb-147">Error code</span></span> | <span data-ttu-id="6b1eb-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b1eb-148">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="6b1eb-149">404</span><span class="sxs-lookup"><span data-stu-id="6b1eb-149">404</span></span> | <span data-ttu-id="6b1eb-150">400013</span><span class="sxs-lookup"><span data-stu-id="6b1eb-150">400013</span></span> | <span data-ttu-id="6b1eb-151">Üst ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-151">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="6b1eb-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6b1eb-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```
