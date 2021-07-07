---
title: Bir aktarımı reddetme
description: Bir müşteri için aboneliklerin aktarımını reddetme.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d09905979a89c9b2092462512c485524cd681d5f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445383"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="735a3-103">Bir aktarımı reddetme</span><span class="sxs-lookup"><span data-stu-id="735a3-103">Reject a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="735a3-104">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="735a3-104">Prerequisites</span></span>

- <span data-ttu-id="735a3-105">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="735a3-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="735a3-106">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="735a3-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="735a3-107">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="735a3-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="735a3-108">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="735a3-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="735a3-109">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="735a3-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="735a3-110">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="735a3-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="735a3-111">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="735a3-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="735a3-112">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="735a3-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="735a3-113">Mevcut bir aktarım için bir aktarım tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="735a3-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="735a3-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="735a3-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="735a3-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="735a3-115">Request syntax</span></span>

| <span data-ttu-id="735a3-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="735a3-116">Method</span></span>   | <span data-ttu-id="735a3-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="735a3-117">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="735a3-118">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="735a3-118">**PATCH**</span></span> | <span data-ttu-id="735a3-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="735a3-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="735a3-120">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="735a3-120">URI parameter</span></span>

<span data-ttu-id="735a3-121">Müşteriyi tanımlamak ve kabul edilecek aktarımı belirtmek için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="735a3-121">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="735a3-122">Ad</span><span class="sxs-lookup"><span data-stu-id="735a3-122">Name</span></span>            | <span data-ttu-id="735a3-123">Tür</span><span class="sxs-lookup"><span data-stu-id="735a3-123">Type</span></span>     | <span data-ttu-id="735a3-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="735a3-124">Required</span></span> | <span data-ttu-id="735a3-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="735a3-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="735a3-126">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="735a3-126">**customer-id**</span></span> | <span data-ttu-id="735a3-127">string</span><span class="sxs-lookup"><span data-stu-id="735a3-127">string</span></span>   | <span data-ttu-id="735a3-128">Yes</span><span class="sxs-lookup"><span data-stu-id="735a3-128">Yes</span></span>      | <span data-ttu-id="735a3-129">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="735a3-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="735a3-130">**Aktarım kimliği**</span><span class="sxs-lookup"><span data-stu-id="735a3-130">**transfer-id**</span></span> | <span data-ttu-id="735a3-131">string</span><span class="sxs-lookup"><span data-stu-id="735a3-131">string</span></span>   | <span data-ttu-id="735a3-132">Yes</span><span class="sxs-lookup"><span data-stu-id="735a3-132">Yes</span></span>      | <span data-ttu-id="735a3-133">Aktarımı tanımlayan bir GUID biçimli aktarım kimliği.</span><span class="sxs-lookup"><span data-stu-id="735a3-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="735a3-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="735a3-134">Request headers</span></span>

<span data-ttu-id="735a3-135">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="735a3-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="735a3-136">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="735a3-136">Request body</span></span>

<span data-ttu-id="735a3-137">Bu tablo, istek gövdesinde [Transferentity](transfer-entity-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="735a3-137">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="735a3-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="735a3-138">Property</span></span>              | <span data-ttu-id="735a3-139">Tür</span><span class="sxs-lookup"><span data-stu-id="735a3-139">Type</span></span>          | <span data-ttu-id="735a3-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="735a3-140">Required</span></span>  | <span data-ttu-id="735a3-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="735a3-141">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="735a3-142">kimlik</span><span class="sxs-lookup"><span data-stu-id="735a3-142">id</span></span>                    | <span data-ttu-id="735a3-143">dize</span><span class="sxs-lookup"><span data-stu-id="735a3-143">string</span></span>        | <span data-ttu-id="735a3-144">No</span><span class="sxs-lookup"><span data-stu-id="735a3-144">No</span></span>    | <span data-ttu-id="735a3-145">TransferEntity başarıyla oluşturulduktan sonra sağlanan bir transferEntity tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="735a3-145">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="735a3-146">durum</span><span class="sxs-lookup"><span data-stu-id="735a3-146">status</span></span>                | <span data-ttu-id="735a3-147">dize</span><span class="sxs-lookup"><span data-stu-id="735a3-147">string</span></span>        | <span data-ttu-id="735a3-148">No</span><span class="sxs-lookup"><span data-stu-id="735a3-148">No</span></span>    | <span data-ttu-id="735a3-149">TransferEntity durumu.</span><span class="sxs-lookup"><span data-stu-id="735a3-149">The status of the transferEntity.</span></span> <span data-ttu-id="735a3-150">Bir aktarımı reddetmek için, değer "Reddet" olarak ayarlanır</span><span class="sxs-lookup"><span data-stu-id="735a3-150">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="735a3-151">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="735a3-151">Request example</span></span>

```http
PATCH /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
Connection: keep-alive
Content-Length: 63

{"id":"ac4a9d22-ba07-444e-890f-cfe084eed498","status":"reject"}

```

## <a name="rest-response"></a><span data-ttu-id="735a3-152">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="735a3-152">REST response</span></span>

<span data-ttu-id="735a3-153">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transferentity](transfer-entity-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="735a3-153">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="735a3-154">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="735a3-154">Response success and error codes</span></span>

<span data-ttu-id="735a3-155">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="735a3-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="735a3-156">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="735a3-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="735a3-157">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="735a3-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="735a3-158">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="735a3-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1069
Content-Type: application/json; charset=utf-8
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
X-Locale: en-US
Date: Fri, 27 Mar 2020 17:50:33 GMT

{
  "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
  "status": "Reject",
  "createdTime": "2020-03-25T22:05:25.1057725Z",
  "lastModifiedTime": "2020-03-27T17:50:32Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
      "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
      "billingCycle": "monthly",
      "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
      "quantity": 20,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
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
