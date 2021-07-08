---
title: Bir abonelik için Azure yetkilendirmeleri listesini alma
description: Bir aboneliğe ait Azure yetkilendirme kaynaklarının koleksiyonunu almak için AzureEntitlement kaynağını kullanabilirsiniz.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 280da155122ed9efd99838d7819fb34f8f7ec52c
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874372"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="a42c2-103">Bir abonelik için Azure yetkilendirmeleri listesini alma</span><span class="sxs-lookup"><span data-stu-id="a42c2-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="a42c2-104">Bir aboneliğe [ait kaynak koleksiyonunu almak için](subscription-resources.md#azureentitlement) Azure yetkilendirme kaynağını (**AzureEntitlement**) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a42c2-104">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a42c2-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a42c2-105">Prerequisites</span></span>

- <span data-ttu-id="a42c2-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a42c2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a42c2-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a42c2-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a42c2-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a42c2-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a42c2-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a42c2-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a42c2-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="a42c2-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a42c2-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="a42c2-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a42c2-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="a42c2-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a42c2-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="a42c2-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a42c2-114">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a42c2-114">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a42c2-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a42c2-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a42c2-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="a42c2-116">Request syntax</span></span>

| <span data-ttu-id="a42c2-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a42c2-117">Method</span></span>  | <span data-ttu-id="a42c2-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a42c2-118">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="a42c2-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="a42c2-119">**GET**</span></span> | <span data-ttu-id="a42c2-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a42c2-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a42c2-121">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a42c2-121">URI parameters</span></span>

<span data-ttu-id="a42c2-122">Aşağıdaki tabloda, bir aboneliğin tüm Azure yetkilendirmelerini almak için gerekli sorgu parametreleri listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="a42c2-122">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="a42c2-123">Ad</span><span class="sxs-lookup"><span data-stu-id="a42c2-123">Name</span></span>                   | <span data-ttu-id="a42c2-124">Tür</span><span class="sxs-lookup"><span data-stu-id="a42c2-124">Type</span></span>     | <span data-ttu-id="a42c2-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a42c2-125">Required</span></span> | <span data-ttu-id="a42c2-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a42c2-126">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="a42c2-127">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="a42c2-127">**customer-tenant-id**</span></span> | <span data-ttu-id="a42c2-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="a42c2-128">**guid**</span></span> | <span data-ttu-id="a42c2-129">Y</span><span class="sxs-lookup"><span data-stu-id="a42c2-129">Y</span></span>        | <span data-ttu-id="a42c2-130">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="a42c2-130">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="a42c2-131">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="a42c2-131">**subscription-id**</span></span>       | <span data-ttu-id="a42c2-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="a42c2-132">**guid**</span></span> | <span data-ttu-id="a42c2-133">Y</span><span class="sxs-lookup"><span data-stu-id="a42c2-133">Y</span></span>        | <span data-ttu-id="a42c2-134">Aboneliğe karşılık gelen BIR GUID.</span><span class="sxs-lookup"><span data-stu-id="a42c2-134">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="a42c2-135">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a42c2-135">Request headers</span></span>

<span data-ttu-id="a42c2-136">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a42c2-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a42c2-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a42c2-137">Request body</span></span>

<span data-ttu-id="a42c2-138">Yok.</span><span class="sxs-lookup"><span data-stu-id="a42c2-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a42c2-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a42c2-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a42c2-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a42c2-140">REST response</span></span>

<span data-ttu-id="a42c2-141">Başarılı olursa, bu yöntem yanıt gövdesinde [**AzureEntitlement**](subscription-resources.md#azureentitlement) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a42c2-141">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a42c2-142">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a42c2-142">Response success and error codes</span></span>

<span data-ttu-id="a42c2-143">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a42c2-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a42c2-144">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a42c2-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a42c2-145">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a42c2-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a42c2-146">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a42c2-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
```
