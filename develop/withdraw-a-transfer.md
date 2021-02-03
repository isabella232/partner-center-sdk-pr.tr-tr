---
title: Bir aktarımı geri alma
description: Bir müşteri için oluşturulan aboneliklerin aktarımını geri alma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768704"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="10a0d-103">Bir aktarımı geri alma</span><span class="sxs-lookup"><span data-stu-id="10a0d-103">Withdraw a transfer</span></span>

<span data-ttu-id="10a0d-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="10a0d-104">**Applies to:**</span></span>

- <span data-ttu-id="10a0d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="10a0d-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10a0d-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="10a0d-106">Prerequisites</span></span>

- <span data-ttu-id="10a0d-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="10a0d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="10a0d-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="10a0d-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="10a0d-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="10a0d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="10a0d-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a0d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="10a0d-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="10a0d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="10a0d-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="10a0d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="10a0d-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="10a0d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="10a0d-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="10a0d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="10a0d-115">Mevcut bir aktarım için bir aktarım tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="10a0d-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="10a0d-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="10a0d-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="10a0d-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="10a0d-117">Request syntax</span></span>

| <span data-ttu-id="10a0d-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="10a0d-118">Method</span></span>    | <span data-ttu-id="10a0d-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="10a0d-119">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="10a0d-120">**SILMELI**</span><span class="sxs-lookup"><span data-stu-id="10a0d-120">**DELETE**</span></span>| <span data-ttu-id="10a0d-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="10a0d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="10a0d-122">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="10a0d-122">URI parameter</span></span>

<span data-ttu-id="10a0d-123">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="10a0d-123">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="10a0d-124">Ad</span><span class="sxs-lookup"><span data-stu-id="10a0d-124">Name</span></span>            | <span data-ttu-id="10a0d-125">Tür</span><span class="sxs-lookup"><span data-stu-id="10a0d-125">Type</span></span>     | <span data-ttu-id="10a0d-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="10a0d-126">Required</span></span> | <span data-ttu-id="10a0d-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10a0d-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="10a0d-128">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="10a0d-128">**customer-id**</span></span> | <span data-ttu-id="10a0d-129">string</span><span class="sxs-lookup"><span data-stu-id="10a0d-129">string</span></span>   | <span data-ttu-id="10a0d-130">Yes</span><span class="sxs-lookup"><span data-stu-id="10a0d-130">Yes</span></span>      | <span data-ttu-id="10a0d-131">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="10a0d-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="10a0d-132">**Aktarım kimliği**</span><span class="sxs-lookup"><span data-stu-id="10a0d-132">**transfer-id**</span></span> | <span data-ttu-id="10a0d-133">string</span><span class="sxs-lookup"><span data-stu-id="10a0d-133">string</span></span>   | <span data-ttu-id="10a0d-134">Yes</span><span class="sxs-lookup"><span data-stu-id="10a0d-134">Yes</span></span>      | <span data-ttu-id="10a0d-135">Aktarımı tanımlayan bir GUID biçimli aktarım kimliği.</span><span class="sxs-lookup"><span data-stu-id="10a0d-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="10a0d-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="10a0d-136">Request headers</span></span>

<span data-ttu-id="10a0d-137">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="10a0d-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="10a0d-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="10a0d-138">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="10a0d-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="10a0d-139">REST response</span></span>

<span data-ttu-id="10a0d-140">Başarılı olursa, bu yöntem Içerik döndürmez (204).</span><span class="sxs-lookup"><span data-stu-id="10a0d-140">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="10a0d-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="10a0d-141">Response success and error codes</span></span>

<span data-ttu-id="10a0d-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="10a0d-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="10a0d-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="10a0d-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="10a0d-144">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="10a0d-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="10a0d-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="10a0d-145">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
