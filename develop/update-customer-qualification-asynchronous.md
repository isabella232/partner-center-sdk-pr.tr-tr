---
title: Müşterinin niteliklerini güncelleştirme
description: Profille ilişkili adres da dahil olmak üzere müşterinin niteliklerini zaman uyumsuz olarak güncelleştirir.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030615"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="18695-103">Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="18695-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="18695-104">Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="18695-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="18695-105">Bir iş ortağı, zaman uyumsuz olarak "eğitim" veya "Hükümentcommunıcloud" olarak bir müşterinin niteliklerini güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="18695-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="18695-106">Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="18695-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18695-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="18695-107">Prerequisites</span></span>

- <span data-ttu-id="18695-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="18695-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="18695-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="18695-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="18695-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="18695-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="18695-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18695-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="18695-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="18695-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="18695-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="18695-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="18695-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="18695-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="18695-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="18695-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="18695-116">C\#</span><span class="sxs-lookup"><span data-stu-id="18695-116">C\#</span></span>

<span data-ttu-id="18695-117">"Eğitim" için bir müşterinin nitelemesini oluşturmak için, önce nitelik türünü temsil eden bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="18695-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="18695-118">Ardından, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="18695-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="18695-119">Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="18695-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="18695-120">Son olarak, `CreateQualifications()` `CreateQualificationsAsync()` bir giriş parametresi olarak nitelendirme türü nesnesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="18695-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="18695-121">**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="18695-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="18695-122">**Proje**: Sdksamples **sınıfı**: createcustomernitelik. cs</span><span class="sxs-lookup"><span data-stu-id="18695-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="18695-123">Bir müşterinin nitelemesini, mevcut bir müşteri üzerinde bir nitelik olmadan **Hükümentcommunitycloud** olarak güncelleştirmek için, ortağın ayrıca müşterinin [**validationcode**](utility-resources.md#validationcode)'u içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="18695-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="18695-124">İlk olarak, nitelik türünü temsil eden bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="18695-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="18695-125">Ardından, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="18695-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="18695-126">Ardından, bir [**ıcustomernitelik**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="18695-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="18695-127">Son olarak, `CreateQualifications()` ya da `CreateQualificationsAsync()` nitelik türü nesnesini ve doğrulama kodunu giriş parametreleri olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="18695-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="18695-128">**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="18695-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="18695-129">**Proje**: Sdksamples **sınıfı**: CreateCustomerQualificationWithGCC. cs</span><span class="sxs-lookup"><span data-stu-id="18695-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="18695-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="18695-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="18695-131">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="18695-131">Request syntax</span></span>

| <span data-ttu-id="18695-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="18695-132">Method</span></span>  | <span data-ttu-id="18695-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="18695-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="18695-134">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="18695-134">**POST**</span></span> | <span data-ttu-id="18695-135">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/nitelikler? Code = {validationcode} http/1.1</span><span class="sxs-lookup"><span data-stu-id="18695-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="18695-136">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="18695-136">URI parameter</span></span>

<span data-ttu-id="18695-137">Nitelemeyi güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="18695-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="18695-138">Ad</span><span class="sxs-lookup"><span data-stu-id="18695-138">Name</span></span>                   | <span data-ttu-id="18695-139">Tür</span><span class="sxs-lookup"><span data-stu-id="18695-139">Type</span></span> | <span data-ttu-id="18695-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="18695-140">Required</span></span> | <span data-ttu-id="18695-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="18695-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="18695-142">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="18695-142">**customer-tenant-id**</span></span> | <span data-ttu-id="18695-143">GUID</span><span class="sxs-lookup"><span data-stu-id="18695-143">GUID</span></span> | <span data-ttu-id="18695-144">Yes</span><span class="sxs-lookup"><span data-stu-id="18695-144">Yes</span></span>      | <span data-ttu-id="18695-145">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="18695-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="18695-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="18695-146">**validationCode**</span></span>     | <span data-ttu-id="18695-147">int</span><span class="sxs-lookup"><span data-stu-id="18695-147">int</span></span>  | <span data-ttu-id="18695-148">No</span><span class="sxs-lookup"><span data-stu-id="18695-148">No</span></span>       | <span data-ttu-id="18695-149">Yalnızca kamu Community bulutu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="18695-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="18695-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="18695-150">Request headers</span></span>

<span data-ttu-id="18695-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="18695-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="18695-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="18695-152">Request body</span></span>

<span data-ttu-id="18695-153">Bu tablo, istek gövdesinde nitelik nesnesini açıklar.</span><span class="sxs-lookup"><span data-stu-id="18695-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="18695-154">Özellik</span><span class="sxs-lookup"><span data-stu-id="18695-154">Property</span></span> | <span data-ttu-id="18695-155">Tür</span><span class="sxs-lookup"><span data-stu-id="18695-155">Type</span></span> | <span data-ttu-id="18695-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="18695-156">Required</span></span> | <span data-ttu-id="18695-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="18695-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="18695-158">Eleme</span><span class="sxs-lookup"><span data-stu-id="18695-158">Qualification</span></span> | <span data-ttu-id="18695-159">string</span><span class="sxs-lookup"><span data-stu-id="18695-159">string</span></span> | <span data-ttu-id="18695-160">Yes</span><span class="sxs-lookup"><span data-stu-id="18695-160">Yes</span></span> | <span data-ttu-id="18695-161">[**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından dize değeri.</span><span class="sxs-lookup"><span data-stu-id="18695-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="18695-162">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="18695-162">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a><span data-ttu-id="18695-163">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="18695-163">REST response</span></span>

<span data-ttu-id="18695-164">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelikler nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="18695-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="18695-165">**Eğitim** nitelemesini içeren bir müşterinin (önceki bir niteliğe sahip **olmayan)** **gönderme** çağrısının bir örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="18695-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="18695-166">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="18695-166">Response success and error codes</span></span>

<span data-ttu-id="18695-167">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="18695-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="18695-168">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="18695-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="18695-169">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="18695-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="18695-170">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="18695-170">Response example</span></span>

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a><span data-ttu-id="18695-171">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="18695-171">Related articles</span></span>

- [<span data-ttu-id="18695-172">Müşterinin niteliklerini al</span><span class="sxs-lookup"><span data-stu-id="18695-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="18695-173">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="18695-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
