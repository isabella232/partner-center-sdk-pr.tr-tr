---
title: Aboneliklerin aktarımını kabul etme
description: Bir müşterinin aboneliklerinin aktarımını kabul etmek için Iş Ortağı Merkezi REST API nasıl kullanacağınızı öğrenin. REST isteği sözdizimi, üst bilgiler ve REST yanıtları içerir.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd9a6788b3dd022470e516ba928a6cd873970e53
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769964"
---
# <a name="accept-a-transfer-of-subscriptions-for-a-customer-using-partner-center-rest-apis"></a><span data-ttu-id="1486c-104">Iş Ortağı Merkezi REST API 'Lerini kullanarak bir müşterinin aboneliklerinin aktarımını kabul etme</span><span class="sxs-lookup"><span data-stu-id="1486c-104">Accept a transfer of subscriptions for a customer using Partner Center REST APIs</span></span>

<span data-ttu-id="1486c-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="1486c-105">**Applies to:**</span></span>

- <span data-ttu-id="1486c-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1486c-106">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1486c-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1486c-107">Prerequisites</span></span>

- <span data-ttu-id="1486c-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1486c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1486c-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1486c-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1486c-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1486c-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1486c-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1486c-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1486c-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1486c-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1486c-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1486c-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1486c-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="1486c-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1486c-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="1486c-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1486c-116">Mevcut bir aktarım için bir aktarım tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1486c-116">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1486c-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1486c-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1486c-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1486c-118">Request syntax</span></span>

| <span data-ttu-id="1486c-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1486c-119">Method</span></span>   | <span data-ttu-id="1486c-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1486c-120">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1486c-121">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="1486c-121">**POST**</span></span> | <span data-ttu-id="1486c-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Transfers/{transfer-id}/Accept http/1.1</span><span class="sxs-lookup"><span data-stu-id="1486c-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id}/accept HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="1486c-123">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1486c-123">URI parameter</span></span>

<span data-ttu-id="1486c-124">Müşteriyi tanımlamak ve kabul edilecek aktarımı belirtmek için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1486c-124">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="1486c-125">Ad</span><span class="sxs-lookup"><span data-stu-id="1486c-125">Name</span></span>            | <span data-ttu-id="1486c-126">Tür</span><span class="sxs-lookup"><span data-stu-id="1486c-126">Type</span></span>     | <span data-ttu-id="1486c-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1486c-127">Required</span></span> | <span data-ttu-id="1486c-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1486c-128">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="1486c-129">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="1486c-129">**customer-id**</span></span> | <span data-ttu-id="1486c-130">string</span><span class="sxs-lookup"><span data-stu-id="1486c-130">string</span></span>   | <span data-ttu-id="1486c-131">Yes</span><span class="sxs-lookup"><span data-stu-id="1486c-131">Yes</span></span>      | <span data-ttu-id="1486c-132">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="1486c-132">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="1486c-133">**Aktarım kimliği**</span><span class="sxs-lookup"><span data-stu-id="1486c-133">**transfer-id**</span></span> | <span data-ttu-id="1486c-134">string</span><span class="sxs-lookup"><span data-stu-id="1486c-134">string</span></span>   | <span data-ttu-id="1486c-135">Yes</span><span class="sxs-lookup"><span data-stu-id="1486c-135">Yes</span></span>      | <span data-ttu-id="1486c-136">Aktarımı tanımlayan bir GUID biçimli aktarım kimliği.</span><span class="sxs-lookup"><span data-stu-id="1486c-136">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="1486c-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1486c-137">Request headers</span></span>

<span data-ttu-id="1486c-138">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1486c-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="1486c-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1486c-139">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/aa2bddb6-9cc8-4949-80fe-a37d5e0a13ba/accept HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0

```

## <a name="rest-response"></a><span data-ttu-id="1486c-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1486c-140">REST response</span></span>

<span data-ttu-id="1486c-141">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transfersubmitresult](transfer-entity-resources.md#transfersubmitresult) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1486c-141">If successful, this method returns the populated [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1486c-142">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1486c-142">Response success and error codes</span></span>

<span data-ttu-id="1486c-143">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1486c-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1486c-144">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1486c-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1486c-145">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1486c-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1486c-146">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1486c-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3389
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Date: Wed, 25 Mar 2020 19:13:06 GMT

{
  "orders": [
    {
      "id": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "alternateId": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "5344C201-3099-44E5-B333-C3EB0401EDE0",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Customer Engagement Plan (36 mo)",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:23.183+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6IjIxYjkyMzkzLWZmY2UtNGJjNy04N2M1LTYyY2ZhODk3ZDhmOSIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    },
    {
      "id": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "alternateId": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "1A90EE13-2CB4-4785-BB0F-542813F00A37",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Business Central Essential",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:34.59+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6Ijc0MTRiOGVhLWMxNjctNGNjNC1iYzhlLWI0M2VmYzE3N2E0NiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    }
  ],
  "transferErrors": [
    {
      "transferGroupId": "1",
      "lineItems": [
        {
          "id": 1,
          "subscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "entitlementId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "offerId": "A4179D30-CC09-49F0-977E-DC2CB70B874F",
          "friendlyName": "Project Online Essentials",
          "quantity": 1,
          "transferGroupId": "1",
          "addonItems": [ ],
          "partnerIdOnRecord": "5139005",
          "billingCycle": "annual",
          "sourceSubscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A"
        }
      ],
      "code": 900103,
      "description": "Subscription SyncState must be SyncComplete for the Subscription to be a source in a Subscription Ownership Transfer. Subscription: 637ff8f6-d842-4573-8da8-89765356cd1a, current state: None",
      "attributes": {
        "objectType": "TransferError"
      }
    }
  ],
  "attributes": {
    "objectType": "TransferSubmitResult"
  }
}
```
