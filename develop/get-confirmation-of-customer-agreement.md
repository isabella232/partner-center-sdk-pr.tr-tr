---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünün nasıl doğrulanacağı açıklanır.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3668a5e510effb533cade311f52513b9a81d40af
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760547"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="a2e27-103">Microsoft Müşteri Sözleşmesinin müşteri kabulünün onayını alma</span><span class="sxs-lookup"><span data-stu-id="a2e27-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="a2e27-104">**Uygulama hedefi**: Iş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a2e27-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="a2e27-105">**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a2e27-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a2e27-106">**Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="a2e27-107">Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin kabul edilmesine ilişkin onay (ler) i nasıl alabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a2e27-107">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2e27-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a2e27-108">Prerequisites</span></span>

- <span data-ttu-id="a2e27-109">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="a2e27-110">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a2e27-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="a2e27-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a2e27-111">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="a2e27-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a2e27-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a2e27-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e27-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a2e27-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e27-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a2e27-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e27-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a2e27-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="a2e27-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a2e27-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="a2e27-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="a2e27-118">.NET</span><span class="sxs-lookup"><span data-stu-id="a2e27-118">.NET</span></span>

<span data-ttu-id="a2e27-119">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="a2e27-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="a2e27-120">Belirtilen müşteri tanımlayıcısıyla **ıaggregatepartner. Customers** koleksiyonunu ve Call **byıd** metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2e27-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="a2e27-121">**Byagreementtype** metodunu çağırarak **anlaşmalar** özelliğini getirin ve sonuçları Microsoft Müşteri sözleşmesine filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="a2e27-121">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="a2e27-122">**Get** veya **GetAsync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="a2e27-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="a2e27-123">Tüm örnek, [konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [getcustomersözleşmeleri](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) sınıfında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a2e27-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a2e27-124">REST request</span></span>

<span data-ttu-id="a2e27-125">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="a2e27-125">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="a2e27-126">Müşterinin [anlaşmalar](./agreement-resources.md) koleksiyonunu almak IÇIN bir rest isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e27-126">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="a2e27-127">Sonuçların kapsamını yalnızca Microsoft Müşteri anlaşmasıyla sınırlamak için **agreementType** sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2e27-127">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a2e27-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a2e27-128">Request syntax</span></span>

<span data-ttu-id="a2e27-129">Aşağıdaki istek sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2e27-129">Use the following request syntax:</span></span>

| <span data-ttu-id="a2e27-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a2e27-130">Method</span></span> | <span data-ttu-id="a2e27-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a2e27-131">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a2e27-132">GET</span><span class="sxs-lookup"><span data-stu-id="a2e27-132">GET</span></span>    | <span data-ttu-id="a2e27-133">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri? agreementType = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a2e27-133">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a2e27-134">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a2e27-134">URI parameters</span></span>

<span data-ttu-id="a2e27-135">İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2e27-135">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="a2e27-136">Ad</span><span class="sxs-lookup"><span data-stu-id="a2e27-136">Name</span></span>             | <span data-ttu-id="a2e27-137">Tür</span><span class="sxs-lookup"><span data-stu-id="a2e27-137">Type</span></span> | <span data-ttu-id="a2e27-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a2e27-138">Required</span></span> | <span data-ttu-id="a2e27-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a2e27-139">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="a2e27-140">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="a2e27-140">customer-tenant-id</span></span> | <span data-ttu-id="a2e27-141">GUID</span><span class="sxs-lookup"><span data-stu-id="a2e27-141">GUID</span></span> | <span data-ttu-id="a2e27-142">Yes</span><span class="sxs-lookup"><span data-stu-id="a2e27-142">Yes</span></span> | <span data-ttu-id="a2e27-143">Değer, bir müşteriyi belirtmenizi sağlayan bir GUID biçimli **Customertenantıd** 'dir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-143">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="a2e27-144">anlaşma türü</span><span class="sxs-lookup"><span data-stu-id="a2e27-144">agreement-type</span></span> | <span data-ttu-id="a2e27-145">dize</span><span class="sxs-lookup"><span data-stu-id="a2e27-145">string</span></span> | <span data-ttu-id="a2e27-146">No</span><span class="sxs-lookup"><span data-stu-id="a2e27-146">No</span></span> | <span data-ttu-id="a2e27-147">Bu parametre tüm anlaşma meta verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a2e27-147">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="a2e27-148">Sorgu yanıtının belirli anlaşma türüne kapsamını atamak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2e27-148">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="a2e27-149">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a2e27-149">The supported values are:</span></span> <br/><br/> <span data-ttu-id="a2e27-150">**Microsoftcloudagreement** yalnızca *microsoftcloudagreement* türünün anlaşma meta verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-150">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="a2e27-151">**Microsoftcustomeragreement** yalnızca *microsoftcustomeragreement* türünde anlaşma meta verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-151">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="a2e27-152">**\**_ tüm anlaşma meta verilerini döndürür. (_ Kullanmayın\* \* \*\* kodunuzun beklenmeyen anlaşma türlerini işlemek için gerekli mantığı yoksa.) <br/> <br/> _* Note:\*\* URI parametresi belirtilmemişse, sorgu geri uyumluluk için varsayılan olarak **Microsoftcloudagreement** olur.</span><span class="sxs-lookup"><span data-stu-id="a2e27-152">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary logic to handle unexpected agreement types.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="a2e27-153">Microsoft, Sözleşme meta verilerini dilediğiniz zaman yeni anlaşma türleriyle ortaya çıkarabilir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-153">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="a2e27-154">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a2e27-154">Request headers</span></span>

<span data-ttu-id="a2e27-155">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a2e27-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a2e27-156">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a2e27-156">Request body</span></span>

<span data-ttu-id="a2e27-157">Yok.</span><span class="sxs-lookup"><span data-stu-id="a2e27-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a2e27-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a2e27-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="a2e27-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a2e27-159">REST response</span></span>

<span data-ttu-id="a2e27-160">Başarılı olursa, bu yöntem yanıt gövdesinde **anlaşma** kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a2e27-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a2e27-161">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a2e27-161">Response success and error codes</span></span>

<span data-ttu-id="a2e27-162">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a2e27-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="a2e27-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2e27-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a2e27-164">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a2e27-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a2e27-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a2e27-165">Response example</span></span>

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
