---
title: Microsoft Bulut Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, Microsoft Bulut sözleşmesi için anlaşma meta verilerinin nasıl alınacağı açıklanmaktadır.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 2588327e72a13de75eb9e02675edbd535491adc4
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760802"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="80655-103">Microsoft Bulut Sözleşmesi için anlaşma meta verilerini alma</span><span class="sxs-lookup"><span data-stu-id="80655-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="80655-104">**Uygulama hedefi**: Iş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="80655-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="80655-105">**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="80655-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="80655-106">**AgreementMetaData** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="80655-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80655-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="80655-107">Prerequisites</span></span>

- <span data-ttu-id="80655-108">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,9 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="80655-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="80655-109">Iş ortağı merkezi Java SDK 'sını kullanıyorsanız sürüm 1,8 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="80655-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="80655-110">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="80655-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="80655-111">Bu senaryo, uygulama + kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="80655-111">This scenario supports app + user authentication.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="80655-112">.NET (sürüm 1,14 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="80655-112">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="80655-113">Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="80655-113">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="80655-114">İlk olarak, **ıaggregatepartner. AgreementDetails** koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="80655-114">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="80655-115">Koleksiyonu Microsoft Bulut sözleşmeye filtrelemek için **Byagreementtype** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="80655-115">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="80655-116">Son olarak, **Get** veya **GetAsync** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80655-116">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="80655-117">[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [Getagreementdetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) sınıfında, bir bütün örnek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="80655-117">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="80655-118">.NET (sürüm 1,9-1,13)</span><span class="sxs-lookup"><span data-stu-id="80655-118">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="80655-119">Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="80655-119">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="80655-120">Önce **ıaggregatepartner. AgreementDetails** koleksiyonunu alın ve **Get** veya **GetAsync** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80655-120">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="80655-121">Ardından, koleksiyon içinde Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın:</span><span class="sxs-lookup"><span data-stu-id="80655-121">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="80655-122">Java</span><span class="sxs-lookup"><span data-stu-id="80655-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="80655-123">Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="80655-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="80655-124">Önce **ıaggregatepartner. getAgreementDetails** işlevini çağırın ve sonra **Get** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80655-124">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="80655-125">Ardından, koleksiyon içinde Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın:</span><span class="sxs-lookup"><span data-stu-id="80655-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

<span data-ttu-id="80655-126">[Konsol test uygulaması](https://github.com/Microsoft/Partner-Center-Java-Samples) projesinden [Getagreementdetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) sınıfında, bir bütün örnek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="80655-126">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="80655-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80655-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="80655-128">Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="80655-128">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="80655-129">[**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="80655-129">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="80655-130">Ardından, koleksiyon içinde Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın:</span><span class="sxs-lookup"><span data-stu-id="80655-130">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="80655-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="80655-131">REST request</span></span>

<span data-ttu-id="80655-132">Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için, önce **AgreementMetaData** koleksiyonunu almak üzere bir rest isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="80655-132">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="80655-133">Sonra koleksiyonda Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın.</span><span class="sxs-lookup"><span data-stu-id="80655-133">Then search for the item in the collection that corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80655-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="80655-134">Request syntax</span></span>

| <span data-ttu-id="80655-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="80655-135">Method</span></span> | <span data-ttu-id="80655-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="80655-136">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="80655-137">GET</span><span class="sxs-lookup"><span data-stu-id="80655-137">GET</span></span>    | <span data-ttu-id="80655-138">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/SÖZLEŞMELERI http/1.1</span><span class="sxs-lookup"><span data-stu-id="80655-138">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80655-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="80655-139">Request headers</span></span>

<span data-ttu-id="80655-140">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80655-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80655-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="80655-141">Request body</span></span>

<span data-ttu-id="80655-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="80655-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="80655-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="80655-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="80655-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="80655-144">REST response</span></span>

<span data-ttu-id="80655-145">Başarılı olursa, bu yöntem yanıt gövdesinde bir **AgreementMetaData** kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="80655-145">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80655-146">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="80655-146">Response success and error codes</span></span>

<span data-ttu-id="80655-147">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="80655-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80655-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="80655-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80655-149">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80655-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80655-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="80655-150">Response example</span></span>

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="80655-151">Microsoft Bulut sözleşmesine karşılık gelen yanıttaki kaynağı tanımlamak için, **agreementType** özelliği "MicrosoftCloudAgreement" değerine sahip olan kaynağı arayın.</span><span class="sxs-lookup"><span data-stu-id="80655-151">To identify the resource in the response that corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
