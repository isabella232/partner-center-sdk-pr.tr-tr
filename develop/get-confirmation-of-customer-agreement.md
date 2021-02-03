---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünün nasıl doğrulanacağı açıklanır.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769437"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="82cf3-103">Microsoft Müşteri Sözleşmesinin müşteri kabulünün onayını alma</span><span class="sxs-lookup"><span data-stu-id="82cf3-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="82cf3-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="82cf3-104">**Applies to:**</span></span>

- <span data-ttu-id="82cf3-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="82cf3-105">Partner Center</span></span>

<span data-ttu-id="82cf3-106">**Sözleşme** kaynağı şu anda yalnızca *Microsoft genel bulutundaki* iş ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-106">The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="82cf3-107">Bu kaynak için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="82cf3-107">This resource doesn't apply to:</span></span>

- <span data-ttu-id="82cf3-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="82cf3-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="82cf3-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="82cf3-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="82cf3-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="82cf3-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="82cf3-111">Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin kabul edilmesine ilişkin onay (ler) i nasıl alabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="82cf3-111">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82cf3-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="82cf3-112">Prerequisites</span></span>

- <span data-ttu-id="82cf3-113">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="82cf3-114">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="82cf3-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="82cf3-115">Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="82cf3-115">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="82cf3-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="82cf3-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="82cf3-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82cf3-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="82cf3-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="82cf3-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="82cf3-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="82cf3-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="82cf3-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="82cf3-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="82cf3-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="82cf3-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="82cf3-122">.NET</span><span class="sxs-lookup"><span data-stu-id="82cf3-122">.NET</span></span>

<span data-ttu-id="82cf3-123">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="82cf3-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="82cf3-124">Belirtilen müşteri tanımlayıcısıyla **ıaggregatepartner. Customers** koleksiyonunu ve Call **byıd** metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="82cf3-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="82cf3-125">**Byagreementtype** metodunu çağırarak **anlaşmalar** özelliğini getirin ve sonuçları Microsoft Müşteri sözleşmesine filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="82cf3-125">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="82cf3-126">**Get** veya **GetAsync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="82cf3-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="82cf3-127">Tüm örnek, [konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [getcustomersözleşmeleri](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) sınıfında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="82cf3-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="82cf3-128">REST request</span></span>

<span data-ttu-id="82cf3-129">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="82cf3-129">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="82cf3-130">Müşterinin [anlaşmalar](./agreement-resources.md) koleksiyonunu almak IÇIN bir rest isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82cf3-130">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="82cf3-131">Sonuçların kapsamını yalnızca Microsoft Müşteri anlaşmasıyla sınırlamak için **agreementType** sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="82cf3-131">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="82cf3-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="82cf3-132">Request syntax</span></span>

<span data-ttu-id="82cf3-133">Aşağıdaki istek sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="82cf3-133">Use the following request syntax:</span></span>

| <span data-ttu-id="82cf3-134">Yöntem</span><span class="sxs-lookup"><span data-stu-id="82cf3-134">Method</span></span> | <span data-ttu-id="82cf3-135">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="82cf3-135">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="82cf3-136">GET</span><span class="sxs-lookup"><span data-stu-id="82cf3-136">GET</span></span>    | <span data-ttu-id="82cf3-137">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri? agreementType = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="82cf3-137">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="82cf3-138">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="82cf3-138">URI parameters</span></span>

<span data-ttu-id="82cf3-139">İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82cf3-139">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="82cf3-140">Ad</span><span class="sxs-lookup"><span data-stu-id="82cf3-140">Name</span></span>             | <span data-ttu-id="82cf3-141">Tür</span><span class="sxs-lookup"><span data-stu-id="82cf3-141">Type</span></span> | <span data-ttu-id="82cf3-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="82cf3-142">Required</span></span> | <span data-ttu-id="82cf3-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82cf3-143">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="82cf3-144">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="82cf3-144">customer-tenant-id</span></span> | <span data-ttu-id="82cf3-145">GUID</span><span class="sxs-lookup"><span data-stu-id="82cf3-145">GUID</span></span> | <span data-ttu-id="82cf3-146">Yes</span><span class="sxs-lookup"><span data-stu-id="82cf3-146">Yes</span></span> | <span data-ttu-id="82cf3-147">Değer, bir müşteriyi belirtmenizi sağlayan bir GUID biçimli **Customertenantıd** 'dir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-147">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="82cf3-148">anlaşma türü</span><span class="sxs-lookup"><span data-stu-id="82cf3-148">agreement-type</span></span> | <span data-ttu-id="82cf3-149">dize</span><span class="sxs-lookup"><span data-stu-id="82cf3-149">string</span></span> | <span data-ttu-id="82cf3-150">No</span><span class="sxs-lookup"><span data-stu-id="82cf3-150">No</span></span> | <span data-ttu-id="82cf3-151">Bu parametre tüm anlaşma meta verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="82cf3-151">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="82cf3-152">Sorgu yanıtının belirli anlaşma türüne kapsamını atamak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="82cf3-152">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="82cf3-153">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="82cf3-153">The supported values are:</span></span> <br/><br/> <span data-ttu-id="82cf3-154">**Microsoftcloudagreement** yalnızca *microsoftcloudagreement* türünün anlaşma meta verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-154">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="82cf3-155">**Microsoftcustomeragreement** yalnızca *microsoftcustomeragreement* türünde anlaşma meta verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-155">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="82cf3-156">**\*** Bu, tüm anlaşma meta verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="82cf3-156">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="82cf3-157">( **\*** Kodunuz, beklenmeyen anlaşma türlerini işlemek için gerekli mantığa sahip değilse kullanmayın.)</span><span class="sxs-lookup"><span data-stu-id="82cf3-157">(Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</span></span><br/><br/> <span data-ttu-id="82cf3-158">**Note:** URI parametresi belirtilmemişse, sorgu geri uyumluluk için varsayılan olarak **Microsoftcloudagreement** olur.</span><span class="sxs-lookup"><span data-stu-id="82cf3-158">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="82cf3-159">Microsoft, Sözleşme meta verilerini dilediğiniz zaman yeni anlaşma türleriyle ortaya çıkarabilir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-159">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="82cf3-160">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="82cf3-160">Request headers</span></span>

<span data-ttu-id="82cf3-161">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="82cf3-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="82cf3-162">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="82cf3-162">Request body</span></span>

<span data-ttu-id="82cf3-163">Yok.</span><span class="sxs-lookup"><span data-stu-id="82cf3-163">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="82cf3-164">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="82cf3-164">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="82cf3-165">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="82cf3-165">REST response</span></span>

<span data-ttu-id="82cf3-166">Başarılı olursa, bu yöntem yanıt gövdesinde **anlaşma** kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="82cf3-166">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="82cf3-167">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="82cf3-167">Response success and error codes</span></span>

<span data-ttu-id="82cf3-168">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="82cf3-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="82cf3-169">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="82cf3-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="82cf3-170">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="82cf3-170">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="82cf3-171">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="82cf3-171">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
