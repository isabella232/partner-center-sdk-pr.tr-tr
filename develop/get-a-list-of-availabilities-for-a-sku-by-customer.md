---
title: Bir SKU (müşteriye göre) için kullanılabilirlik listesini alma
description: Müşteri, ürün ve SKU tanımlayıcılarını kullanarak, müşteri tarafından belirtilen ürün ve SKU için bir kullanılabilirlik koleksiyonu edinebilirsiniz.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b237bbd17a6108bbcb4e23529cf476a6b8306f68
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874559"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="42a3f-103">Bir SKU (müşteriye göre) için kullanılabilirlik listesini alma</span><span class="sxs-lookup"><span data-stu-id="42a3f-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="42a3f-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="42a3f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42a3f-105">Belirli bir müşteri tarafından kullanılabilen belirli bir ürün ve SKU 'nun kullanılabilirliği koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42a3f-105">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42a3f-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="42a3f-106">Prerequisites</span></span>

- <span data-ttu-id="42a3f-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="42a3f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42a3f-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="42a3f-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="42a3f-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="42a3f-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="42a3f-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42a3f-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="42a3f-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="42a3f-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="42a3f-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="42a3f-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="42a3f-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="42a3f-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="42a3f-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="42a3f-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="42a3f-115">Ürün tanımlayıcısı (**ürün kimliği**).</span><span class="sxs-lookup"><span data-stu-id="42a3f-115">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="42a3f-116">Bir SKU tanımlayıcısı (**SKU kimliği**).</span><span class="sxs-lookup"><span data-stu-id="42a3f-116">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="42a3f-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="42a3f-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42a3f-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="42a3f-118">Request syntax</span></span>

| <span data-ttu-id="42a3f-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="42a3f-119">Method</span></span> | <span data-ttu-id="42a3f-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="42a3f-120">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42a3f-121">POST</span><span class="sxs-lookup"><span data-stu-id="42a3f-121">POST</span></span>   | <span data-ttu-id="42a3f-122">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products/{product-id}/SKUs/{SKU-id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="42a3f-122">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="42a3f-123">İstek URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="42a3f-123">Request URI parameters</span></span>

| <span data-ttu-id="42a3f-124">Ad</span><span class="sxs-lookup"><span data-stu-id="42a3f-124">Name</span></span>               | <span data-ttu-id="42a3f-125">Tür</span><span class="sxs-lookup"><span data-stu-id="42a3f-125">Type</span></span> | <span data-ttu-id="42a3f-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="42a3f-126">Required</span></span> | <span data-ttu-id="42a3f-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="42a3f-127">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="42a3f-128">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="42a3f-128">customer-tenant-id</span></span> | <span data-ttu-id="42a3f-129">GUID</span><span class="sxs-lookup"><span data-stu-id="42a3f-129">GUID</span></span> | <span data-ttu-id="42a3f-130">Yes</span><span class="sxs-lookup"><span data-stu-id="42a3f-130">Yes</span></span> | <span data-ttu-id="42a3f-131">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="42a3f-131">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="42a3f-132">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="42a3f-132">product-id</span></span> | <span data-ttu-id="42a3f-133">string</span><span class="sxs-lookup"><span data-stu-id="42a3f-133">string</span></span> | <span data-ttu-id="42a3f-134">Yes</span><span class="sxs-lookup"><span data-stu-id="42a3f-134">Yes</span></span> | <span data-ttu-id="42a3f-135">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="42a3f-135">A string that identifies the product.</span></span> |
| <span data-ttu-id="42a3f-136">SKU kimliği</span><span class="sxs-lookup"><span data-stu-id="42a3f-136">sku-id</span></span> | <span data-ttu-id="42a3f-137">string</span><span class="sxs-lookup"><span data-stu-id="42a3f-137">string</span></span> | <span data-ttu-id="42a3f-138">Yes</span><span class="sxs-lookup"><span data-stu-id="42a3f-138">Yes</span></span> | <span data-ttu-id="42a3f-139">SKU 'YU tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="42a3f-139">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="42a3f-140">İstek üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="42a3f-140">Request header</span></span>

<span data-ttu-id="42a3f-141">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="42a3f-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42a3f-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="42a3f-142">Request body</span></span>

<span data-ttu-id="42a3f-143">Yok.</span><span class="sxs-lookup"><span data-stu-id="42a3f-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="42a3f-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="42a3f-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="42a3f-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="42a3f-145">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42a3f-146">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="42a3f-146">Response success and error codes</span></span>

<span data-ttu-id="42a3f-147">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="42a3f-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42a3f-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="42a3f-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42a3f-149">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="42a3f-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="42a3f-150">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="42a3f-150">This method returns the following error codes:</span></span>

| <span data-ttu-id="42a3f-151">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="42a3f-151">HTTP Status Code</span></span> | <span data-ttu-id="42a3f-152">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="42a3f-152">Error code</span></span> | <span data-ttu-id="42a3f-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="42a3f-153">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="42a3f-154">404</span><span class="sxs-lookup"><span data-stu-id="42a3f-154">404</span></span> | <span data-ttu-id="42a3f-155">400013</span><span class="sxs-lookup"><span data-stu-id="42a3f-155">400013</span></span> | <span data-ttu-id="42a3f-156">Üst ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="42a3f-156">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="42a3f-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="42a3f-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
