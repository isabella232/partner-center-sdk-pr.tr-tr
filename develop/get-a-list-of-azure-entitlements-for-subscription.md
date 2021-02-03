---
title: Bir abonelik için Azure yetkilendirmeleri listesini alma
description: Bir aboneliğe ait olan bir Azure yetkilendirme kaynakları koleksiyonunu almak için AzureEntitlement kaynağını kullanabilirsiniz.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: d7d0a10c571dc073bd49e82084f3b7ece7234daf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769118"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="8d061-103">Bir abonelik için Azure yetkilendirmeleri listesini alma</span><span class="sxs-lookup"><span data-stu-id="8d061-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="8d061-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="8d061-104">**Applies to:**</span></span>

- <span data-ttu-id="8d061-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8d061-105">Partner Center</span></span>

<span data-ttu-id="8d061-106">Bir aboneliğe ait kaynakların koleksiyonunu almak için [Azure yetkilendirme kaynağı](subscription-resources.md#azureentitlement) 'nı (**AzureEntitlement**) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d061-106">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d061-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8d061-107">Prerequisites</span></span>

- <span data-ttu-id="8d061-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8d061-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8d061-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8d061-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8d061-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8d061-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8d061-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d061-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8d061-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8d061-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8d061-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="8d061-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8d061-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="8d061-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8d061-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="8d061-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8d061-116">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8d061-116">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8d061-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8d061-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8d061-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8d061-118">Request syntax</span></span>

| <span data-ttu-id="8d061-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8d061-119">Method</span></span>  | <span data-ttu-id="8d061-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8d061-120">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="8d061-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="8d061-121">**GET**</span></span> | <span data-ttu-id="8d061-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/{Subscription-id}/azureentitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="8d061-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8d061-123">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="8d061-123">URI parameters</span></span>

<span data-ttu-id="8d061-124">Aşağıdaki tabloda, bir aboneliğe yönelik tüm Azure yetkilendirmelerini almak için gerekli sorgu parametreleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="8d061-124">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="8d061-125">Ad</span><span class="sxs-lookup"><span data-stu-id="8d061-125">Name</span></span>                   | <span data-ttu-id="8d061-126">Tür</span><span class="sxs-lookup"><span data-stu-id="8d061-126">Type</span></span>     | <span data-ttu-id="8d061-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8d061-127">Required</span></span> | <span data-ttu-id="8d061-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8d061-128">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="8d061-129">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="8d061-129">**customer-tenant-id**</span></span> | <span data-ttu-id="8d061-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="8d061-130">**guid**</span></span> | <span data-ttu-id="8d061-131">Y</span><span class="sxs-lookup"><span data-stu-id="8d061-131">Y</span></span>        | <span data-ttu-id="8d061-132">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="8d061-132">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="8d061-133">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="8d061-133">**subscription-id**</span></span>       | <span data-ttu-id="8d061-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="8d061-134">**guid**</span></span> | <span data-ttu-id="8d061-135">Y</span><span class="sxs-lookup"><span data-stu-id="8d061-135">Y</span></span>        | <span data-ttu-id="8d061-136">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="8d061-136">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="8d061-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8d061-137">Request headers</span></span>

<span data-ttu-id="8d061-138">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8d061-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8d061-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8d061-139">Request body</span></span>

<span data-ttu-id="8d061-140">Yok.</span><span class="sxs-lookup"><span data-stu-id="8d061-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8d061-141">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8d061-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8d061-142">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8d061-142">REST response</span></span>

<span data-ttu-id="8d061-143">Başarılı olursa, bu yöntem yanıt gövdesinde bir [**AzureEntitlement**](subscription-resources.md#azureentitlement) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="8d061-143">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8d061-144">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8d061-144">Response success and error codes</span></span>

<span data-ttu-id="8d061-145">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8d061-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8d061-146">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d061-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8d061-147">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8d061-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8d061-148">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8d061-148">Response example</span></span>

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
