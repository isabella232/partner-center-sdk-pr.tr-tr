---
title: Ortağın kamu Community bulut doğrulama kodlarını alın
description: Ortağın kamu Community bulut doğrulama kodlarını alma.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: d84a3d3c69d835e42565c4e6f1edb06ab338340a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769286"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="430a8-103">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="430a8-103">Get a partner's validation codes</span></span>

<span data-ttu-id="430a8-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="430a8-104">**Applies To**</span></span>

- <span data-ttu-id="430a8-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="430a8-105">Partner Center</span></span>

<span data-ttu-id="430a8-106">Ortağın kamu Community bulut doğrulama kodlarının bir koleksiyonunu alma.</span><span class="sxs-lookup"><span data-stu-id="430a8-106">How to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="430a8-107">Kamu topluluk bulutu 'nda bir müşteri oluşturmak için bir doğrulama kodu gerekir.</span><span class="sxs-lookup"><span data-stu-id="430a8-107">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="430a8-108">Kuruluşunuzun veya müşterilerinin kuruluşunuzun Office 365 Kamu GCC 'yi CSP için onayladığı konusunda ilgileniyorsanız, lütfen bkz. [CSP Iş ortağı ve müşteri uygunluk ölçütleri/iş merkezi/CSP-GCC-Validate için Office 365 Kamu GCC.</span><span class="sxs-lookup"><span data-stu-id="430a8-108">If you are interested in having your organization or your customers organization approved for Office 365 Government GCC for CSP, please see [Office 365 Government GCC for CSP Partner and Customer Eligibility Criteria/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="430a8-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="430a8-109">Prerequisites</span></span>

- <span data-ttu-id="430a8-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="430a8-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="430a8-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="430a8-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="430a8-112">Form doldurulduktan sonra doğrulama onaylandı [](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span><span class="sxs-lookup"><span data-stu-id="430a8-112">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="430a8-113">Nitelikleri olmayan bir müşteri.</span><span class="sxs-lookup"><span data-stu-id="430a8-113">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="430a8-114">C\#</span><span class="sxs-lookup"><span data-stu-id="430a8-114">C\#</span></span>

<span data-ttu-id="430a8-115">Bir iş ortağının doğrulama kodlarının tümünün listesini almak için **Getvalidationcodes**' ı çağırın.</span><span class="sxs-lookup"><span data-stu-id="430a8-115">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="430a8-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="430a8-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="430a8-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="430a8-117">Request syntax</span></span>

| <span data-ttu-id="430a8-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="430a8-118">Method</span></span>  | <span data-ttu-id="430a8-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="430a8-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="430a8-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="430a8-120">**GET**</span></span> | <span data-ttu-id="430a8-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/All/doğrulamaları http/1.1</span><span class="sxs-lookup"><span data-stu-id="430a8-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="430a8-122">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="430a8-122">Request headers</span></span>

<span data-ttu-id="430a8-123">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="430a8-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="430a8-124">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="430a8-124">Request body</span></span>

<span data-ttu-id="430a8-125">Yok.</span><span class="sxs-lookup"><span data-stu-id="430a8-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="430a8-126">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="430a8-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="430a8-127">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="430a8-127">REST response</span></span>

<span data-ttu-id="430a8-128">Başarılı olursa, bu yöntem yanıt gövdesinde [**Validationcode**](utility-resources.md#validationcode) kaynaklarının bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="430a8-128">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="430a8-129">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="430a8-129">Response success and error codes</span></span>

<span data-ttu-id="430a8-130">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="430a8-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="430a8-131">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="430a8-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="430a8-132">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="430a8-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="430a8-133">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="430a8-133">Response example</span></span>

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
