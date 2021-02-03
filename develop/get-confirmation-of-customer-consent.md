---
title: Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, Microsoft Bulut sözleşmesinin müşteri kabulünün nasıl doğrulanacağı açıklanır.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769857"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="1e277-103">Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma</span><span class="sxs-lookup"><span data-stu-id="1e277-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="1e277-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="1e277-104">**Applies To**</span></span>

- <span data-ttu-id="1e277-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e277-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="1e277-106">**Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="1e277-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="1e277-107">Şunları yapmak için geçerli değildir:</span><span class="sxs-lookup"><span data-stu-id="1e277-107">It isn't applicable to:</span></span>
>
> - <span data-ttu-id="1e277-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e277-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="1e277-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e277-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="1e277-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e277-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e277-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1e277-111">Prerequisites</span></span>

- <span data-ttu-id="1e277-112">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,9 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1e277-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="1e277-113">Iş ortağı merkezi Java SDK 'sını kullanıyorsanız sürüm 1,8 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1e277-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="1e277-114">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1e277-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="1e277-115">Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1e277-115">This scenario supports only supports app + user authentication.</span></span>

- <span data-ttu-id="1e277-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1e277-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1e277-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e277-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1e277-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1e277-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1e277-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1e277-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1e277-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="1e277-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1e277-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="1e277-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="1e277-122">.NET (sürüm 1,4 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="1e277-122">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="1e277-123">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="1e277-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="1e277-124">Belirtilen müşteri tanımlayıcısıyla **ıaggregatepartner. Customers** koleksiyonunu ve Call **byıd** metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e277-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="1e277-125">**Byagreementtype** metodunu çağırarak **anlaşmalar** özelliğini getirin ve sonuçları Microsoft bulut sözleşmeye filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="1e277-125">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="1e277-126">**Get** veya **GetAsync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="1e277-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="1e277-127">Tüm örnek, [konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [getcustomersözleşmeleri](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) sınıfında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="1e277-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="1e277-128">.NET (sürüm 1,9-1,13)</span><span class="sxs-lookup"><span data-stu-id="1e277-128">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="1e277-129">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="1e277-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="1e277-130">**Iaggregatepartner. Customers** koleksiyonunu kullanın ve **byıd** metodunu belirtilen müşterinin tanımlayıcısıyla çağırın.</span><span class="sxs-lookup"><span data-stu-id="1e277-130">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="1e277-131">Ardından, **Get** veya **GetAsync** yöntemlerini çağırarak **anlaşmalar** özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="1e277-131">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="1e277-132">Java</span><span class="sxs-lookup"><span data-stu-id="1e277-132">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="1e277-133">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="1e277-133">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="1e277-134">**Iaggregatepartner. getCustomers** işlevini kullanın ve belirtilen müşterinin tanımlayıcısına sahip **byıd** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1e277-134">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="1e277-135">Ardından, **Get** Işlevini çağırarak **getagreements** işlevini alın.</span><span class="sxs-lookup"><span data-stu-id="1e277-135">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="1e277-136">Tüm örnek, [konsol test uygulaması](https://github.com/Microsoft/Partner-Center-Java-Samples) projesinden [getcustomersözleşmeleri](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) sınıfında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="1e277-136">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="1e277-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e277-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="1e277-138">Daha önce sağlanmış olan müşteri kabulünün onayını almak için:</span><span class="sxs-lookup"><span data-stu-id="1e277-138">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="1e277-139">[**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e277-139">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="1e277-140">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1e277-140">REST request</span></span>

<span data-ttu-id="1e277-141">Daha önce sağlanmış olan müşteri kabulünün onayını almak için aşağıdaki yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="1e277-141">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="1e277-142">İlgili sertifika bilgileriyle yeni bir **anlaşma** kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e277-142">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1e277-143">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1e277-143">Request syntax</span></span>

| <span data-ttu-id="1e277-144">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1e277-144">Method</span></span> | <span data-ttu-id="1e277-145">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1e277-145">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1e277-146">GET</span><span class="sxs-lookup"><span data-stu-id="1e277-146">GET</span></span>    | <span data-ttu-id="1e277-147">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="1e277-147">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1e277-148">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1e277-148">URI parameter</span></span>

<span data-ttu-id="1e277-149">Onayladığınız müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e277-149">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="1e277-150">Ad</span><span class="sxs-lookup"><span data-stu-id="1e277-150">Name</span></span>             | <span data-ttu-id="1e277-151">Tür</span><span class="sxs-lookup"><span data-stu-id="1e277-151">Type</span></span> | <span data-ttu-id="1e277-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1e277-152">Required</span></span> | <span data-ttu-id="1e277-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e277-153">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="1e277-154">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="1e277-154">CustomerTenantId</span></span> | <span data-ttu-id="1e277-155">GUID</span><span class="sxs-lookup"><span data-stu-id="1e277-155">GUID</span></span> | <span data-ttu-id="1e277-156">Y</span><span class="sxs-lookup"><span data-stu-id="1e277-156">Y</span></span>        | <span data-ttu-id="1e277-157">Değer, bir müşteriyi belirtmenizi sağlayan bir GUID biçimli **Customertenantıd** 'dir.</span><span class="sxs-lookup"><span data-stu-id="1e277-157">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1e277-158">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1e277-158">Request headers</span></span>

<span data-ttu-id="1e277-159">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1e277-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1e277-160">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1e277-160">Request body</span></span>

<span data-ttu-id="1e277-161">Yok.</span><span class="sxs-lookup"><span data-stu-id="1e277-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1e277-162">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1e277-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="1e277-163">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1e277-163">REST response</span></span>

<span data-ttu-id="1e277-164">Başarılı olursa, bu yöntem yanıt gövdesinde **anlaşma** kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1e277-164">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1e277-165">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1e277-165">Response success and error codes</span></span>

<span data-ttu-id="1e277-166">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1e277-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1e277-167">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e277-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1e277-168">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1e277-168">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1e277-169">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1e277-169">Response example</span></span>

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
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
