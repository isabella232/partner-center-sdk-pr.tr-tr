---
title: Bir aktarımı reddetme
description: Bir müşteri için aboneliklerin aktarımını reddetme.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e4a182ff92a21cf72ca1c2da9de7e211b433725f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768980"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="cb354-103">Bir aktarımı reddetme</span><span class="sxs-lookup"><span data-stu-id="cb354-103">Reject a transfer</span></span>

<span data-ttu-id="cb354-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="cb354-104">**Applies to:**</span></span>

- <span data-ttu-id="cb354-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="cb354-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb354-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cb354-106">Prerequisites</span></span>

- <span data-ttu-id="cb354-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cb354-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cb354-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="cb354-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cb354-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb354-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cb354-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb354-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cb354-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="cb354-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cb354-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="cb354-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cb354-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="cb354-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cb354-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="cb354-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cb354-115">Mevcut bir aktarım için bir aktarım tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cb354-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="cb354-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="cb354-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cb354-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb354-117">Request syntax</span></span>

| <span data-ttu-id="cb354-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="cb354-118">Method</span></span>   | <span data-ttu-id="cb354-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="cb354-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb354-120">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="cb354-120">**PATCH**</span></span> | <span data-ttu-id="cb354-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cb354-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="cb354-122">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="cb354-122">URI parameter</span></span>

<span data-ttu-id="cb354-123">Müşteriyi tanımlamak ve kabul edilecek aktarımı belirtmek için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb354-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="cb354-124">Ad</span><span class="sxs-lookup"><span data-stu-id="cb354-124">Name</span></span>            | <span data-ttu-id="cb354-125">Tür</span><span class="sxs-lookup"><span data-stu-id="cb354-125">Type</span></span>     | <span data-ttu-id="cb354-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cb354-126">Required</span></span> | <span data-ttu-id="cb354-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb354-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="cb354-128">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="cb354-128">**customer-id**</span></span> | <span data-ttu-id="cb354-129">string</span><span class="sxs-lookup"><span data-stu-id="cb354-129">string</span></span>   | <span data-ttu-id="cb354-130">Yes</span><span class="sxs-lookup"><span data-stu-id="cb354-130">Yes</span></span>      | <span data-ttu-id="cb354-131">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="cb354-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="cb354-132">**Aktarım kimliği**</span><span class="sxs-lookup"><span data-stu-id="cb354-132">**transfer-id**</span></span> | <span data-ttu-id="cb354-133">string</span><span class="sxs-lookup"><span data-stu-id="cb354-133">string</span></span>   | <span data-ttu-id="cb354-134">Yes</span><span class="sxs-lookup"><span data-stu-id="cb354-134">Yes</span></span>      | <span data-ttu-id="cb354-135">Aktarımı tanımlayan bir GUID biçimli aktarım kimliği.</span><span class="sxs-lookup"><span data-stu-id="cb354-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="cb354-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="cb354-136">Request headers</span></span>

<span data-ttu-id="cb354-137">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cb354-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cb354-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="cb354-138">Request body</span></span>

<span data-ttu-id="cb354-139">Bu tablo, istek gövdesinde [Transferentity](transfer-entity-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="cb354-139">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="cb354-140">Özellik</span><span class="sxs-lookup"><span data-stu-id="cb354-140">Property</span></span>              | <span data-ttu-id="cb354-141">Tür</span><span class="sxs-lookup"><span data-stu-id="cb354-141">Type</span></span>          | <span data-ttu-id="cb354-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cb354-142">Required</span></span>  | <span data-ttu-id="cb354-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb354-143">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb354-144">kimlik</span><span class="sxs-lookup"><span data-stu-id="cb354-144">id</span></span>                    | <span data-ttu-id="cb354-145">dize</span><span class="sxs-lookup"><span data-stu-id="cb354-145">string</span></span>        | <span data-ttu-id="cb354-146">No</span><span class="sxs-lookup"><span data-stu-id="cb354-146">No</span></span>    | <span data-ttu-id="cb354-147">TransferEntity başarıyla oluşturulduktan sonra sağlanan bir transferEntity tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cb354-147">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="cb354-148">durum</span><span class="sxs-lookup"><span data-stu-id="cb354-148">status</span></span>                | <span data-ttu-id="cb354-149">dize</span><span class="sxs-lookup"><span data-stu-id="cb354-149">string</span></span>        | <span data-ttu-id="cb354-150">No</span><span class="sxs-lookup"><span data-stu-id="cb354-150">No</span></span>    | <span data-ttu-id="cb354-151">TransferEntity durumu.</span><span class="sxs-lookup"><span data-stu-id="cb354-151">The status of the transferEntity.</span></span> <span data-ttu-id="cb354-152">Bir aktarımı reddetmek için, değer "Reddet" olarak ayarlanır</span><span class="sxs-lookup"><span data-stu-id="cb354-152">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="cb354-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="cb354-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cb354-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="cb354-154">REST response</span></span>

<span data-ttu-id="cb354-155">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transferentity](transfer-entity-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="cb354-155">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cb354-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="cb354-156">Response success and error codes</span></span>

<span data-ttu-id="cb354-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="cb354-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cb354-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb354-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cb354-159">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cb354-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cb354-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="cb354-160">Response example</span></span>

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
