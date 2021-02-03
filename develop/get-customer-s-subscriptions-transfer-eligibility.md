---
title: Müşterinin abonelik aktarım uygunluğunu alma
description: Aktarım için uygun/ineligibile bir müşterinin aboneliklerinin bir koleksiyonunu alma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 43086a32fa0dbbdecf65aac167c687f26fc4c2c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768741"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="a0e8a-103">Müşterinin abonelik aktarım uygunluğunu alma</span><span class="sxs-lookup"><span data-stu-id="a0e8a-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="a0e8a-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="a0e8a-104">**Applies To**</span></span>

- <span data-ttu-id="a0e8a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a0e8a-105">Partner Center</span></span>

<span data-ttu-id="a0e8a-106">Aktarım için uygun/uygun olmayan bir müşterinin aboneliklerinin bir koleksiyonunu alma.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-106">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0e8a-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a0e8a-107">Prerequisites</span></span>

- <span data-ttu-id="a0e8a-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a0e8a-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a0e8a-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a0e8a-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a0e8a-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a0e8a-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a0e8a-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a0e8a-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a0e8a-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="a0e8a-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="a0e8a-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a0e8a-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a0e8a-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a0e8a-117">Request syntax</span></span>

| <span data-ttu-id="a0e8a-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a0e8a-118">Method</span></span>  | <span data-ttu-id="a0e8a-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a0e8a-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0e8a-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="a0e8a-120">**GET**</span></span> | <span data-ttu-id="a0e8a-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/transferseligibility? transfertype = {aktarım-türü} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a0e8a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a0e8a-122">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="a0e8a-122">URI parameter</span></span>

<span data-ttu-id="a0e8a-123">Bu tablo, tüm abonelikleri almak için gerekli sorgu parametresini listeler.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-123">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="a0e8a-124">Ad</span><span class="sxs-lookup"><span data-stu-id="a0e8a-124">Name</span></span>               | <span data-ttu-id="a0e8a-125">Tür</span><span class="sxs-lookup"><span data-stu-id="a0e8a-125">Type</span></span>   | <span data-ttu-id="a0e8a-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a0e8a-126">Required</span></span> | <span data-ttu-id="a0e8a-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a0e8a-127">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="a0e8a-128">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="a0e8a-128">customer-tenant-id</span></span> | <span data-ttu-id="a0e8a-129">string</span><span class="sxs-lookup"><span data-stu-id="a0e8a-129">string</span></span> | <span data-ttu-id="a0e8a-130">Yes</span><span class="sxs-lookup"><span data-stu-id="a0e8a-130">Yes</span></span>      | <span data-ttu-id="a0e8a-131">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-131">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="a0e8a-132">Aktarım türü</span><span class="sxs-lookup"><span data-stu-id="a0e8a-132">transfer-type</span></span>      | <span data-ttu-id="a0e8a-133">string</span><span class="sxs-lookup"><span data-stu-id="a0e8a-133">string</span></span> | <span data-ttu-id="a0e8a-134">Yes</span><span class="sxs-lookup"><span data-stu-id="a0e8a-134">Yes</span></span>      | <span data-ttu-id="a0e8a-135">Hedeflenen aktarım türü.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-135">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="a0e8a-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a0e8a-136">Request headers</span></span>

<span data-ttu-id="a0e8a-137">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a0e8a-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a0e8a-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a0e8a-138">Request body</span></span>

<span data-ttu-id="a0e8a-139">Yok.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a0e8a-140">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a0e8a-140">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a0e8a-141">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a0e8a-141">REST response</span></span>

<span data-ttu-id="a0e8a-142">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Transferuygunluk](transfer-eligibility-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-142">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a0e8a-143">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a0e8a-143">Response success and error codes</span></span>

<span data-ttu-id="a0e8a-144">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a0e8a-145">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a0e8a-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a0e8a-146">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a0e8a-146">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a0e8a-147">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a0e8a-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
Date: Tue, 24 Mar 2020 23:43:25 GMT

[
  {
    "id": "548FA265-5F40-4765-9A6B-47826F72A4BF",
    "isEligible": false,
    "reason": "Subscription: 548FA265-5F40-4765-9A6B-47826F72A4BF is in state: Deleted"
  },
  {
    "id": "E2A3AEB3-70A7-42E3-930C-7519EEDDC45A",
    "isEligible": false,
    "reason": "Subscription: E2A3AEB3-70A7-42E3-930C-7519EEDDC45A is in state: Suspended"
  },
  {
    "id": "4B600A9A-DF56-4564-A75A-6CC6D2D0C9F9",
    "isEligible": false,
    "reason": "subscription is already part of another transfer request id : 31a06eac-c527-458a-a6b4-0de197a45996"
  },
  {
    "id": "D3350F46-AA29-4F6F-95A0-E3011988915C",
    "isEligible": true
  }
  {
    "id": "E82B2F4A-736A-4E2B-955C-C1A4C56C0171",
    "isEligible": true
  }
]
```
