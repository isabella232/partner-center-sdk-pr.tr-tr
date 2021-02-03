---
title: Ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirin
description: Ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirmek üzere C/# ve Iş Ortağı Merkezi REST API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769952"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="e9a52-103">Faturalandırmayı etkinleştirmek için ticari Market SaaS ürünleri için bir korumalı alan aboneliği etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e9a52-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="e9a52-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="e9a52-104">**Applies to:**</span></span>

- <span data-ttu-id="e9a52-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e9a52-105">Partner Center</span></span>

<span data-ttu-id="e9a52-106">Faturalandırmayı etkinleştirmek için tümleştirme korumalı alanı hesaplarından hizmet olarak satılan ticari Market yazılım (SaaS) ürünleri için bir abonelik etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="e9a52-106">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="e9a52-107">Yalnızca tümleştirme korumalı alanı hesaplarından ticari Market SaaS ürünleri için bir abonelik etkinleştirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e9a52-107">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="e9a52-108">Üretim aboneliğiniz varsa, kurulum işlemini gerçekleştirmek için yayımcının sitesini ziyaret etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9a52-108">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="e9a52-109">Abonelik faturalandırması, yalnızca kurulum tamamlandıktan sonra başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="e9a52-109">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9a52-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e9a52-110">Prerequisites</span></span>

- <span data-ttu-id="e9a52-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e9a52-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e9a52-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="e9a52-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e9a52-113">Ticari Market SaaS ürünleri için etkin aboneliğe sahip bir müşterinin bulunduğu tümleştirme korumalı alan iş ortağı hesabı.</span><span class="sxs-lookup"><span data-stu-id="e9a52-113">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="e9a52-114">Iş ortağı merkezi .NET SDK kullanan iş ortakları için, bu özelliğe erişmek için SDK sürüm 1.14.0 veya üstünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9a52-114">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="e9a52-115">C\#</span><span class="sxs-lookup"><span data-stu-id="e9a52-115">C\#</span></span>

<span data-ttu-id="e9a52-116">Ticari Market SaaS ürünleri için bir aboneliği etkinleştirmek üzere aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="e9a52-116">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="e9a52-117">Kullanılabilir abonelik işlemlerine bir arabirim oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9a52-117">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="e9a52-118">Müşteriyi tanımlamalısınız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9a52-118">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="e9a52-119">**Etkinleştirme** işlemini kullanarak aboneliği etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e9a52-119">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="e9a52-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e9a52-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e9a52-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e9a52-121">Request syntax</span></span>

| <span data-ttu-id="e9a52-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e9a52-122">Method</span></span>     | <span data-ttu-id="e9a52-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e9a52-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="e9a52-124">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="e9a52-124">**POST**</span></span> | <span data-ttu-id="e9a52-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/Activate http/1.1</span><span class="sxs-lookup"><span data-stu-id="e9a52-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e9a52-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="e9a52-126">URI parameter</span></span>

| <span data-ttu-id="e9a52-127">Ad</span><span class="sxs-lookup"><span data-stu-id="e9a52-127">Name</span></span>                   | <span data-ttu-id="e9a52-128">Tür</span><span class="sxs-lookup"><span data-stu-id="e9a52-128">Type</span></span>     | <span data-ttu-id="e9a52-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e9a52-129">Required</span></span> | <span data-ttu-id="e9a52-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e9a52-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e9a52-131">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="e9a52-131">**customer-tenant-id**</span></span> | <span data-ttu-id="e9a52-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="e9a52-132">**guid**</span></span> | <span data-ttu-id="e9a52-133">Y</span><span class="sxs-lookup"><span data-stu-id="e9a52-133">Y</span></span> | <span data-ttu-id="e9a52-134">Değer, bir müşteri belirtmenize olanak tanıyan, GUID biçimli bir müşteri kiracı tanımlayıcısıdır (**Müşteri Kiracı kimliği**).</span><span class="sxs-lookup"><span data-stu-id="e9a52-134">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="e9a52-135">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="e9a52-135">**subscription-id**</span></span> | <span data-ttu-id="e9a52-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="e9a52-136">**guid**</span></span> | <span data-ttu-id="e9a52-137">Y</span><span class="sxs-lookup"><span data-stu-id="e9a52-137">Y</span></span> | <span data-ttu-id="e9a52-138">Değer, bir abonelik belirtmenizi sağlayan GUID biçimli bir abonelik tanımlayıcısıdır (**abonelik kimliği**).</span><span class="sxs-lookup"><span data-stu-id="e9a52-138">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e9a52-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e9a52-139">Request headers</span></span>

<span data-ttu-id="e9a52-140">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e9a52-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e9a52-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e9a52-141">Request body</span></span>

<span data-ttu-id="e9a52-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="e9a52-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e9a52-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e9a52-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="e9a52-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e9a52-144">REST response</span></span>

<span data-ttu-id="e9a52-145">Bu yöntem, **abonelik kimliği** ve **durum** özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9a52-145">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e9a52-146">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e9a52-146">Response success and error codes</span></span>

<span data-ttu-id="e9a52-147">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e9a52-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e9a52-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9a52-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e9a52-149">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e9a52-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e9a52-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e9a52-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
