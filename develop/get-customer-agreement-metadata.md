---
title: Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, veri kaynağı için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025742"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="a4c37-103">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma</span><span class="sxs-lookup"><span data-stu-id="a4c37-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="a4c37-104">**Için geçerlidir:** İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a4c37-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="a4c37-105">**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a4c37-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a4c37-106">İş yüklerini Microsoft Müşteri Sözleşmesi meta verileri şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde desteklene bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="a4c37-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="a4c37-107">Şunların için önce Microsoft Müşteri Sözleşmesi meta verilerini alasiniz:</span><span class="sxs-lookup"><span data-stu-id="a4c37-107">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="a4c37-108">Müşterinin Microsoft Müşteri Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="a4c37-108">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="a4c37-109">Microsoft Müşteri Sözleşmesi şablonu için indirme bağlantısı alma</span><span class="sxs-lookup"><span data-stu-id="a4c37-109">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="a4c37-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a4c37-110">Prerequisites</span></span>

- <span data-ttu-id="a4c37-111">İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.14 veya daha yenisi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a4c37-111">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="a4c37-112">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a4c37-112">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="a4c37-113">Bu senaryo yalnızca App+User kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a4c37-113">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="a4c37-114">.NET (sürüm 1.14 veya daha yenisi)</span><span class="sxs-lookup"><span data-stu-id="a4c37-114">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="a4c37-115">Aşağıdakiler için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi:</span><span class="sxs-lookup"><span data-stu-id="a4c37-115">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="a4c37-116">İlk olarak **IAggregatePartner.AgreementDetails koleksiyonunu** alın.</span><span class="sxs-lookup"><span data-stu-id="a4c37-116">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="a4c37-117">Koleksiyona filtre uygulama filtresi yapmak için **ByAgreementType** yöntemini Microsoft Müşteri Sözleşmesi.</span><span class="sxs-lookup"><span data-stu-id="a4c37-117">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="a4c37-118">Son olarak **Get veya** **GetAsync yöntemini** arayın.</span><span class="sxs-lookup"><span data-stu-id="a4c37-118">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="a4c37-119">Eksiksiz bir örnek, konsol test uygulaması [projesinden GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a4c37-119">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a4c37-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a4c37-120">REST request</span></span>

<span data-ttu-id="a4c37-121">Aşağıdakiler için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi:</span><span class="sxs-lookup"><span data-stu-id="a4c37-121">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="a4c37-122">[AgreementMetaData](./agreement-metadata-resources.md) koleksiyonunu almak için bir REST isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4c37-122">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="a4c37-123">AgreementType **sorgu** parametresini kullanarak sonucun kapsamını yalnızca Microsoft Müşteri Sözleşmesi.</span><span class="sxs-lookup"><span data-stu-id="a4c37-123">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a4c37-124">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="a4c37-124">Request syntax</span></span>

| <span data-ttu-id="a4c37-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a4c37-125">Method</span></span> | <span data-ttu-id="a4c37-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a4c37-126">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="a4c37-127">GET</span><span class="sxs-lookup"><span data-stu-id="a4c37-127">GET</span></span>    | <span data-ttu-id="a4c37-128">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a4c37-128">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a4c37-129">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a4c37-129">URI parameters</span></span>

| <span data-ttu-id="a4c37-130">Ad</span><span class="sxs-lookup"><span data-stu-id="a4c37-130">Name</span></span>                   | <span data-ttu-id="a4c37-131">Tür</span><span class="sxs-lookup"><span data-stu-id="a4c37-131">Type</span></span>     | <span data-ttu-id="a4c37-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a4c37-132">Required</span></span> | <span data-ttu-id="a4c37-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a4c37-133">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="a4c37-134">sözleşme türü</span><span class="sxs-lookup"><span data-stu-id="a4c37-134">agreement-type</span></span> | <span data-ttu-id="a4c37-135">dize</span><span class="sxs-lookup"><span data-stu-id="a4c37-135">string</span></span> | <span data-ttu-id="a4c37-136">No</span><span class="sxs-lookup"><span data-stu-id="a4c37-136">No</span></span> | <span data-ttu-id="a4c37-137">Sorgu yanıtını belirli sözleşme türüne göre kapsam olarak kullanmak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4c37-137">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="a4c37-138">Desteklenen değerler:</span><span class="sxs-lookup"><span data-stu-id="a4c37-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="a4c37-139">**Yalnızca MicrosoftCloudAgreement** türünde sözleşme meta verilerini içeren *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="a4c37-139">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="a4c37-140">**Yalnızca MicrosoftCustomerAgreement** türünde sözleşme meta verilerini içeren *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="a4c37-140">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="a4c37-141">**\**_ tüm sözleşme meta verilerini döndürür. (_ kullanma\* \* _ Microsoft herhangi bir zamanda yeni sözleşme türleriyle sözleşme meta verilerine sahip olabilir, çünkü kodunuzun yabancı anlaşma türlerini işlemek için gerekli çalışma zamanı mantığı *yoksa.) <br/> <br/> _* Not:*\* URI parametresi belirtilmezse, geriye dönük uyumluluk için sorgu **varsayılan olarak MicrosoftCloudAgreement** olur.</span><span class="sxs-lookup"><span data-stu-id="a4c37-141">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="a4c37-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a4c37-142">Request headers</span></span>

<span data-ttu-id="a4c37-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a4c37-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a4c37-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a4c37-144">Request body</span></span>

<span data-ttu-id="a4c37-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="a4c37-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a4c37-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a4c37-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="a4c37-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a4c37-147">REST response</span></span>

<span data-ttu-id="a4c37-148">Başarılı olursa, bu yöntem yanıt gövdesinde [ **AgreementMetaData** kaynaklarının](./agreement-metadata-resources.md) bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a4c37-148">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a4c37-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a4c37-149">Response success and error codes</span></span>

<span data-ttu-id="a4c37-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a4c37-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="a4c37-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4c37-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a4c37-152">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a4c37-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a4c37-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a4c37-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
