---
title: ortağın Government Community Cloud doğrulama kodlarını al
description: iş ortağının Government Community Cloud doğrulama kodlarını alma.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 04bccf587628337004a5825b534048945f791839
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873879"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="dece5-103">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="dece5-103">Get a partner's validation codes</span></span>

<span data-ttu-id="dece5-104">bu makalede bir iş ortağının Government Community Cloud doğrulama kodları koleksiyonunu nasıl alacağınız açıklanır.</span><span class="sxs-lookup"><span data-stu-id="dece5-104">This article describes how to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="dece5-105">Kamu topluluk bulutu 'nda bir müşteri oluşturmak için bir doğrulama kodu gerekir.</span><span class="sxs-lookup"><span data-stu-id="dece5-105">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="dece5-106">kuruluşunuzun veya müşterinin kuruluşunun CSP için Office 365 Kamu GCC onaylanmasından ilgileniyorsanız, bkz. [csp iş ortağı ve müşteri uygunluk ölçütlerine yönelik Office 365 Kamu GCC](/partner-center/csp-gcc-validate).</span><span class="sxs-lookup"><span data-stu-id="dece5-106">If you are interested in having your organization or your customer's organization approved for Office 365 Government GCC for CSP, see [Office 365 Government GCC for CSP Partner and Customer eligibility criteria](/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dece5-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="dece5-107">Prerequisites</span></span>

- <span data-ttu-id="dece5-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="dece5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dece5-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="dece5-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dece5-110">Form doldurulduktan sonra doğrulama onaylandı [](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span><span class="sxs-lookup"><span data-stu-id="dece5-110">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="dece5-111">Nitelikleri olmayan bir müşteri.</span><span class="sxs-lookup"><span data-stu-id="dece5-111">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="dece5-112">C\#</span><span class="sxs-lookup"><span data-stu-id="dece5-112">C\#</span></span>

<span data-ttu-id="dece5-113">Bir iş ortağının doğrulama kodlarının tümünün listesini almak için **Getvalidationcodes**' ı çağırın.</span><span class="sxs-lookup"><span data-stu-id="dece5-113">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="dece5-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="dece5-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dece5-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="dece5-115">Request syntax</span></span>

| <span data-ttu-id="dece5-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="dece5-116">Method</span></span>  | <span data-ttu-id="dece5-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="dece5-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dece5-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="dece5-118">**GET**</span></span> | <span data-ttu-id="dece5-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/All/doğrulamaları http/1.1</span><span class="sxs-lookup"><span data-stu-id="dece5-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dece5-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="dece5-120">Request headers</span></span>

<span data-ttu-id="dece5-121">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dece5-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dece5-122">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="dece5-122">Request body</span></span>

<span data-ttu-id="dece5-123">Yok.</span><span class="sxs-lookup"><span data-stu-id="dece5-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dece5-124">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="dece5-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="dece5-125">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="dece5-125">REST response</span></span>

<span data-ttu-id="dece5-126">Başarılı olursa, bu yöntem yanıt gövdesinde [**Validationcode**](utility-resources.md#validationcode) kaynaklarının bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="dece5-126">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dece5-127">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="dece5-127">Response success and error codes</span></span>

<span data-ttu-id="dece5-128">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="dece5-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dece5-129">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dece5-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dece5-130">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dece5-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dece5-131">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="dece5-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
