---
title: Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, Microsoft Müşteri Sözleşmesi için anlaşma meta verilerinin nasıl alınacağı açıklanmaktadır.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769431"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="32738-103">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma</span><span class="sxs-lookup"><span data-stu-id="32738-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="32738-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="32738-104">**Applies to:**</span></span>

- <span data-ttu-id="32738-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="32738-105">Partner Center</span></span>

<span data-ttu-id="32738-106">Microsoft Müşteri Sözleşmesi için anlaşma meta verileri şu anda yalnızca *Microsoft genel bulutundaki* Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="32738-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="32738-107">Şunları yapmak için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="32738-107">It doesn't apply to:</span></span>

- <span data-ttu-id="32738-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="32738-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="32738-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="32738-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="32738-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="32738-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="32738-111">Aşağıdakileri yapabilmeniz için Microsoft Müşteri Sözleşmesi 'nin anlaşma meta verilerini almalısınız:</span><span class="sxs-lookup"><span data-stu-id="32738-111">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="32738-112">Müşterinin Microsoft Müşteri sözleşmesinin kabul edildiğini onaylama</span><span class="sxs-lookup"><span data-stu-id="32738-112">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="32738-113">Microsoft müşteri anlaşması şablonu için bir indirme bağlantısı alma</span><span class="sxs-lookup"><span data-stu-id="32738-113">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="32738-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="32738-114">Prerequisites</span></span>

- <span data-ttu-id="32738-115">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="32738-115">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="32738-116">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="32738-116">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="32738-117">Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="32738-117">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="32738-118">.NET (sürüm 1,14 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="32738-118">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="32738-119">Microsoft Müşteri Sözleşmesi sözleşmesi meta verilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="32738-119">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="32738-120">İlk olarak, **ıaggregatepartner. AgreementDetails** koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="32738-120">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="32738-121">Koleksiyonu Microsoft Müşteri anlaşmasıyla filtrelemek için **Byagreementtype** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="32738-121">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="32738-122">Son olarak, **Get** veya **GetAsync** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="32738-122">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="32738-123">[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [Getagreementdetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) sınıfında, bir bütün örnek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="32738-123">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="32738-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="32738-124">REST request</span></span>

<span data-ttu-id="32738-125">Microsoft Müşteri Sözleşmesi sözleşmesi meta verilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="32738-125">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="32738-126">[AgreementMetaData](./agreement-metadata-resources.md) koleksiyonunu almak IÇIN bir rest isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32738-126">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="32738-127">Sonucu yalnızca Microsoft Müşteri anlaşmasıyla sınırlamak için **agreementType** sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="32738-127">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="32738-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="32738-128">Request syntax</span></span>

| <span data-ttu-id="32738-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="32738-129">Method</span></span> | <span data-ttu-id="32738-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="32738-130">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="32738-131">GET</span><span class="sxs-lookup"><span data-stu-id="32738-131">GET</span></span>    | <span data-ttu-id="32738-132">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/sözleşmeleri? agreementType = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="32738-132">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="32738-133">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="32738-133">URI parameters</span></span>

| <span data-ttu-id="32738-134">Ad</span><span class="sxs-lookup"><span data-stu-id="32738-134">Name</span></span>                   | <span data-ttu-id="32738-135">Tür</span><span class="sxs-lookup"><span data-stu-id="32738-135">Type</span></span>     | <span data-ttu-id="32738-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="32738-136">Required</span></span> | <span data-ttu-id="32738-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="32738-137">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="32738-138">anlaşma türü</span><span class="sxs-lookup"><span data-stu-id="32738-138">agreement-type</span></span> | <span data-ttu-id="32738-139">dize</span><span class="sxs-lookup"><span data-stu-id="32738-139">string</span></span> | <span data-ttu-id="32738-140">No</span><span class="sxs-lookup"><span data-stu-id="32738-140">No</span></span> | <span data-ttu-id="32738-141">Sorgu yanıtının belirli anlaşma türüne kapsamını atamak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="32738-141">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="32738-142">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="32738-142">The supported values are:</span></span> <br/><br/><span data-ttu-id="32738-143">Yalnızca *microsoftcloudagreement* türünde Sözleşme meta verilerini Içeren **Microsoftcloufegreement**</span><span class="sxs-lookup"><span data-stu-id="32738-143">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="32738-144">Yalnızca *microsoftcustomeragreement* türünde Sözleşme meta verilerini Içeren **microsoftcustomeragreement** .</span><span class="sxs-lookup"><span data-stu-id="32738-144">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="32738-145">**\*** Bu, tüm anlaşma meta verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="32738-145">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="32738-146">(Microsoft, **\*** herhangi bir zamanda yeni anlaşma türleriyle anlaşma meta verileri getirebileceğinden, kodunuzun tanıdık anlaşma türlerini işlemek için gerekli çalışma zamanı mantığına sahip olmadığı yapmayın.)</span><span class="sxs-lookup"><span data-stu-id="32738-146">(Don't use **\*** unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)</span></span><br/><br/> <span data-ttu-id="32738-147">**Note:** URI parametresi belirtilmemişse, sorgu geri uyumluluk için varsayılan olarak **Microsoftcloudagreement** olur.</span><span class="sxs-lookup"><span data-stu-id="32738-147">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="32738-148">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="32738-148">Request headers</span></span>

<span data-ttu-id="32738-149">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="32738-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="32738-150">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="32738-150">Request body</span></span>

<span data-ttu-id="32738-151">Yok.</span><span class="sxs-lookup"><span data-stu-id="32738-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="32738-152">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="32738-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="32738-153">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="32738-153">REST response</span></span>

<span data-ttu-id="32738-154">Başarılı olursa, bu yöntem yanıt gövdesinde bir [ **AgreementMetaData** kaynakları](./agreement-metadata-resources.md) koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="32738-154">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="32738-155">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="32738-155">Response success and error codes</span></span>

<span data-ttu-id="32738-156">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="32738-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="32738-157">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="32738-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="32738-158">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="32738-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="32738-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="32738-159">Response example</span></span>

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
