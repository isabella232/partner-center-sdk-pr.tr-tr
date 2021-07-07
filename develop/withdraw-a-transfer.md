---
title: Bir aktarımı geri alma
description: Bir müşteri için oluşturulan aboneliklerin aktarımını geri alma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3c15cf09b4e466e178c7afb5f9d324fe1199418e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445213"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="7b50d-103">Bir aktarımı geri alma</span><span class="sxs-lookup"><span data-stu-id="7b50d-103">Withdraw a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b50d-104">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7b50d-104">Prerequisites</span></span>

- <span data-ttu-id="7b50d-105">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7b50d-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7b50d-106">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7b50d-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7b50d-107">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7b50d-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7b50d-108">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b50d-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7b50d-109">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7b50d-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7b50d-110">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7b50d-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7b50d-111">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="7b50d-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7b50d-112">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="7b50d-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7b50d-113">Mevcut bir aktarım için bir aktarım tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b50d-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7b50d-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7b50d-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b50d-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7b50d-115">Request syntax</span></span>

| <span data-ttu-id="7b50d-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7b50d-116">Method</span></span>    | <span data-ttu-id="7b50d-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7b50d-117">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b50d-118">**SILMELI**</span><span class="sxs-lookup"><span data-stu-id="7b50d-118">**DELETE**</span></span>| <span data-ttu-id="7b50d-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7b50d-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="7b50d-120">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="7b50d-120">URI parameter</span></span>

<span data-ttu-id="7b50d-121">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b50d-121">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="7b50d-122">Ad</span><span class="sxs-lookup"><span data-stu-id="7b50d-122">Name</span></span>            | <span data-ttu-id="7b50d-123">Tür</span><span class="sxs-lookup"><span data-stu-id="7b50d-123">Type</span></span>     | <span data-ttu-id="7b50d-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7b50d-124">Required</span></span> | <span data-ttu-id="7b50d-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7b50d-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="7b50d-126">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="7b50d-126">**customer-id**</span></span> | <span data-ttu-id="7b50d-127">string</span><span class="sxs-lookup"><span data-stu-id="7b50d-127">string</span></span>   | <span data-ttu-id="7b50d-128">Yes</span><span class="sxs-lookup"><span data-stu-id="7b50d-128">Yes</span></span>      | <span data-ttu-id="7b50d-129">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="7b50d-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="7b50d-130">**Aktarım kimliği**</span><span class="sxs-lookup"><span data-stu-id="7b50d-130">**transfer-id**</span></span> | <span data-ttu-id="7b50d-131">string</span><span class="sxs-lookup"><span data-stu-id="7b50d-131">string</span></span>   | <span data-ttu-id="7b50d-132">Yes</span><span class="sxs-lookup"><span data-stu-id="7b50d-132">Yes</span></span>      | <span data-ttu-id="7b50d-133">Aktarımı tanımlayan bir GUID biçimli aktarım kimliği.</span><span class="sxs-lookup"><span data-stu-id="7b50d-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="7b50d-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7b50d-134">Request headers</span></span>

<span data-ttu-id="7b50d-135">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7b50d-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="7b50d-136">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7b50d-136">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="7b50d-137">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7b50d-137">REST response</span></span>

<span data-ttu-id="7b50d-138">Başarılı olursa, bu yöntem Içerik döndürmez (204).</span><span class="sxs-lookup"><span data-stu-id="7b50d-138">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b50d-139">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7b50d-139">Response success and error codes</span></span>

<span data-ttu-id="7b50d-140">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7b50d-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b50d-141">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b50d-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b50d-142">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7b50d-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b50d-143">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7b50d-143">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
