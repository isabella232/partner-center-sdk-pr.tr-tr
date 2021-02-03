---
title: Kimliğe göre aktarım ayrıntılarını al
description: Bir müşterinin aboneliklerinin bir aktarımının ayrıntılarını alma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c39e9483f1e51469981b0d6fa2541a6372ff2dac
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768909"
---
# <a name="get-transfer-details-by-id"></a><span data-ttu-id="42560-103">Kimliğe göre aktarım ayrıntılarını al</span><span class="sxs-lookup"><span data-stu-id="42560-103">Get transfer details by id</span></span>

<span data-ttu-id="42560-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="42560-104">**Applies to:**</span></span>

- <span data-ttu-id="42560-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="42560-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42560-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="42560-106">Prerequisites</span></span>

- <span data-ttu-id="42560-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="42560-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42560-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="42560-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="42560-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="42560-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="42560-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42560-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="42560-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="42560-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="42560-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="42560-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="42560-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="42560-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="42560-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="42560-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="42560-115">Mevcut bir aktarım için bir aktarım tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="42560-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="42560-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="42560-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42560-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="42560-117">Request syntax</span></span>

| <span data-ttu-id="42560-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="42560-118">Method</span></span>   | <span data-ttu-id="42560-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="42560-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42560-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="42560-120">**GET**</span></span> | <span data-ttu-id="42560-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="42560-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="42560-122">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="42560-122">URI parameter</span></span>

<span data-ttu-id="42560-123">Müşteriyi tanımlamak ve kabul edilecek aktarımı belirtmek için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="42560-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="42560-124">Ad</span><span class="sxs-lookup"><span data-stu-id="42560-124">Name</span></span>            | <span data-ttu-id="42560-125">Tür</span><span class="sxs-lookup"><span data-stu-id="42560-125">Type</span></span>     | <span data-ttu-id="42560-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="42560-126">Required</span></span> | <span data-ttu-id="42560-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="42560-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="42560-128">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="42560-128">**customer-id**</span></span> | <span data-ttu-id="42560-129">string</span><span class="sxs-lookup"><span data-stu-id="42560-129">string</span></span>   | <span data-ttu-id="42560-130">Yes</span><span class="sxs-lookup"><span data-stu-id="42560-130">Yes</span></span>      | <span data-ttu-id="42560-131">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="42560-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="42560-132">**Aktarım kimliği**</span><span class="sxs-lookup"><span data-stu-id="42560-132">**transfer-id**</span></span> | <span data-ttu-id="42560-133">string</span><span class="sxs-lookup"><span data-stu-id="42560-133">string</span></span>   | <span data-ttu-id="42560-134">Yes</span><span class="sxs-lookup"><span data-stu-id="42560-134">Yes</span></span>      | <span data-ttu-id="42560-135">Aktarımı tanımlayan bir GUID biçimli aktarım kimliği.</span><span class="sxs-lookup"><span data-stu-id="42560-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="42560-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="42560-136">Request headers</span></span>

<span data-ttu-id="42560-137">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="42560-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="42560-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="42560-138">Request example</span></span>

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a><span data-ttu-id="42560-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="42560-139">REST response</span></span>

<span data-ttu-id="42560-140">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transferentity](transfer-entity-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="42560-140">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42560-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="42560-141">Response success and error codes</span></span>

<span data-ttu-id="42560-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="42560-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42560-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="42560-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42560-144">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="42560-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42560-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="42560-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1501
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
X-Locale: en-US
Date: Fri, 27 Mar 2020 18:25:25 GMT

{
  "id": "46e8ed67-8adf-4f65-b3d8-d31318080556",
  "status": "Active",
  "createdTime": "2020-03-27T18:22:33.2875302Z",
  "lastModifiedTime": "2020-03-27T18:22:33Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "75B71186-73C3-45B4-A403-281C0D7EB032",
      "offerId": "F72752C8-3E37-4C9B-A1A0-69E8442068DC",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central Team Member",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 1,
      "subscriptionId": "1FB4CB0A-EB79-4300-9E87-7D486054888A",
      "offerId": "88F9EB8A-0636-45E8-A601-553E0A48AA9E",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central External Accountant",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 2,
      "subscriptionId": "08AB3010-B647-402E-8955-B6C0FB364D8F",
      "offerId": "4D8F3B90-29B3-4E7B-B37C-4A435DDEF1D9",
      "billingCycle": "annual",
      "friendlyName": "Common Area Phone",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}

```
