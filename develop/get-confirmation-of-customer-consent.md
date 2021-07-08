---
title: Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, müşterinin müşteri tarafından kabulü onaylarının nasıl Microsoft Bulut Anlaşması.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: 1b1a8cbacb667e579bcd218a29c3f553afce26c2
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549272"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="03b4f-103">Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma</span><span class="sxs-lookup"><span data-stu-id="03b4f-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="03b4f-104">**Için geçerlidir:** İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="03b4f-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="03b4f-105">**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="03b4f-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="03b4f-106">Sözleşme **kaynağı** şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03b4f-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="03b4f-107">Prerequisites</span></span>

- <span data-ttu-id="03b4f-108">İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.9 veya daha yenisi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="03b4f-109">İş Ortağı Merkezi Java SDK'sı kullanıyorsanız sürüm 1.8 veya daha yeni bir sürüm gereklidir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="03b4f-110">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="03b4f-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="03b4f-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="03b4f-111">This scenario only supports app + user authentication.</span></span>

- <span data-ttu-id="03b4f-112">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="03b4f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="03b4f-113">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="03b4f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="03b4f-114">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="03b4f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="03b4f-115">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="03b4f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="03b4f-116">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="03b4f-117">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="03b4f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="03b4f-118">.NET (sürüm 1.4 veya daha yenisi)</span><span class="sxs-lookup"><span data-stu-id="03b4f-118">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="03b4f-119">Daha önce sağlanan müşteri kabulü onaylarını almak için:</span><span class="sxs-lookup"><span data-stu-id="03b4f-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="03b4f-120">**IAggregatePartner.Customers koleksiyonunu** kullanın ve belirtilen müşteri tanımlayıcısıyla **ById** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="03b4f-121">**Agreements özelliğini getirme** ve **ByAgreementType** yöntemini Microsoft Bulut Anlaşması sonuçları filtrele.</span><span class="sxs-lookup"><span data-stu-id="03b4f-121">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="03b4f-122">**Get veya** **GetAsync yöntemini** çağırma.</span><span class="sxs-lookup"><span data-stu-id="03b4f-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="03b4f-123">Eksiksiz bir örnek, konsol test uygulaması [projesinden GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="03b4f-124">.NET (sürüm 1.9 - 1.13)</span><span class="sxs-lookup"><span data-stu-id="03b4f-124">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="03b4f-125">Daha önce sağlanan müşteri kabulü onaylarını almak için:</span><span class="sxs-lookup"><span data-stu-id="03b4f-125">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="03b4f-126">**IAggregatePartner.Customers** koleksiyonunu kullanın ve belirtilen müşterinin tanımlayıcısıyla **ById** yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="03b4f-126">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="03b4f-127">Ardından **Agreements özelliğini ve** ardından **Get** veya **GetAsync yöntemlerini** çağırarak.</span><span class="sxs-lookup"><span data-stu-id="03b4f-127">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="03b4f-128">Java</span><span class="sxs-lookup"><span data-stu-id="03b4f-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="03b4f-129">Daha önce sağlanan müşteri kabulü onaylarını almak için:</span><span class="sxs-lookup"><span data-stu-id="03b4f-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="03b4f-130">**IAggregatePartner.getCustomers** işlevini kullanın ve belirtilen müşterinin tanımlayıcısıyla **byId** işlevini arayın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-130">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="03b4f-131">Ardından **getAgreements işlevini** ve ardından get işlevini **çağırarak.**</span><span class="sxs-lookup"><span data-stu-id="03b4f-131">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="03b4f-132">Eksiksiz bir örnek, konsol test uygulaması [projesinden GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) [sınıfında](https://github.com/Microsoft/Partner-Center-Java-Samples) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-132">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="03b4f-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03b4f-133">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="03b4f-134">Daha önce sağlanan müşteri kabulü onaylarını almak için:</span><span class="sxs-lookup"><span data-stu-id="03b4f-134">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="03b4f-135">[**Get-PartnerCustomerAgreement komutunu**](/powershell/module/partnercenter/get-partnercustomeragreement) kullanın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-135">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="03b4f-136">REST isteği</span><span class="sxs-lookup"><span data-stu-id="03b4f-136">REST request</span></span>

<span data-ttu-id="03b4f-137">Daha önce sağlanan müşteri kabulü onaylarını almak için aşağıdaki yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-137">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="03b4f-138">İlgili sertifikasyon **bilgileriyle** yeni bir Sözleşme kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03b4f-138">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="03b4f-139">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="03b4f-139">Request syntax</span></span>

| <span data-ttu-id="03b4f-140">Yöntem</span><span class="sxs-lookup"><span data-stu-id="03b4f-140">Method</span></span> | <span data-ttu-id="03b4f-141">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="03b4f-141">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="03b4f-142">GET</span><span class="sxs-lookup"><span data-stu-id="03b4f-142">GET</span></span>    | <span data-ttu-id="03b4f-143">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="03b4f-143">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="03b4f-144">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="03b4f-144">URI parameter</span></span>

<span data-ttu-id="03b4f-145">Onaylamakta olduğunu müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-145">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="03b4f-146">Ad</span><span class="sxs-lookup"><span data-stu-id="03b4f-146">Name</span></span>             | <span data-ttu-id="03b4f-147">Tür</span><span class="sxs-lookup"><span data-stu-id="03b4f-147">Type</span></span> | <span data-ttu-id="03b4f-148">Gerekli</span><span class="sxs-lookup"><span data-stu-id="03b4f-148">Required</span></span> | <span data-ttu-id="03b4f-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="03b4f-149">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="03b4f-150">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="03b4f-150">CustomerTenantId</span></span> | <span data-ttu-id="03b4f-151">GUID</span><span class="sxs-lookup"><span data-stu-id="03b4f-151">GUID</span></span> | <span data-ttu-id="03b4f-152">Y</span><span class="sxs-lookup"><span data-stu-id="03b4f-152">Y</span></span>        | <span data-ttu-id="03b4f-153">Değer, müşteri belirtmenize olanak sağlayan GUID biçiminde bir **CustomerTenantId** değeridir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-153">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="03b4f-154">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="03b4f-154">Request headers</span></span>

<span data-ttu-id="03b4f-155">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="03b4f-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="03b4f-156">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="03b4f-156">Request body</span></span>

<span data-ttu-id="03b4f-157">Yok.</span><span class="sxs-lookup"><span data-stu-id="03b4f-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="03b4f-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="03b4f-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="03b4f-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="03b4f-159">REST response</span></span>

<span data-ttu-id="03b4f-160">Başarılı olursa, bu yöntem yanıt **gövdesinde bir Anlaşma** kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="03b4f-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="03b4f-161">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="03b4f-161">Response success and error codes</span></span>

<span data-ttu-id="03b4f-162">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="03b4f-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="03b4f-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="03b4f-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="03b4f-164">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="03b4f-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="03b4f-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="03b4f-165">Response example</span></span>

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
