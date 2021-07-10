---
title: Müşterinin niteliklerini güncelleştirme
description: Profille ilişkili adres de dahil olmak üzere müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572106"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="414db-103">Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="414db-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="414db-104">Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="414db-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="414db-105">bir iş ortağı müşterinin niteliklerini zaman uyumsuz olarak "Eğitim" veya "GovernmentCocloud" olacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="414db-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="414db-106">"Hiçbiri" ve "Kar Amacı Gütmeyen" gibi diğer değerler ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="414db-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="414db-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="414db-107">Prerequisites</span></span>

- <span data-ttu-id="414db-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="414db-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="414db-109">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="414db-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="414db-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="414db-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="414db-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="414db-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="414db-112">İş Ortağı Merkezi menüsünden **CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="414db-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="414db-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="414db-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="414db-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="414db-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="414db-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="414db-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="414db-116">C\#</span><span class="sxs-lookup"><span data-stu-id="414db-116">C\#</span></span>

<span data-ttu-id="414db-117">Müşterinin "Eğitim" niteliğini oluşturmak için önce nitelik türünü temsil eden bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="414db-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="414db-118">Ardından, [**müşteri tanımlayıcısıyla IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="414db-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="414db-119">Ardından Bir [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**Nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="414db-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="414db-120">Son olarak, `CreateQualifications()` giriş `CreateQualificationsAsync()` parametresi olarak nite türü nesnesiyle veya çağrısında bulundurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="414db-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="414db-121">**Örnek:** [Konsol Örnek Uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="414db-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="414db-122">**Project:** SdkSamples **Sınıfı:** CreateCustomerQualification.cs</span><span class="sxs-lookup"><span data-stu-id="414db-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="414db-123">Bir müşterinin yeterliliği olmayan mevcut bir müşteride **KamuCocloud** niteliğini güncelleştirmek için iş ortağının müşterinin ValidationCode kodunu da [**içermesi gerekir.**](utility-resources.md#validationcode)</span><span class="sxs-lookup"><span data-stu-id="414db-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="414db-124">İlk olarak, nitelik türünü temsil eden bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="414db-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="414db-125">Ardından, [**müşteri tanımlayıcısıyla IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="414db-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="414db-126">Ardından Bir [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) arabirimi almak için [**Nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="414db-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="414db-127">Son olarak, `CreateQualifications()` nitelik `CreateQualificationsAsync()` türü nesnesiyle veya çağrısı ve giriş parametreleri olarak doğrulama kodu.</span><span class="sxs-lookup"><span data-stu-id="414db-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="414db-128">**Örnek:** [Konsol Örnek Uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="414db-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="414db-129">**Project:** SdkSamples **Sınıfı:** CreateCustomerQualificationWithGCC.cs</span><span class="sxs-lookup"><span data-stu-id="414db-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="414db-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="414db-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="414db-131">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="414db-131">Request syntax</span></span>

| <span data-ttu-id="414db-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="414db-132">Method</span></span>  | <span data-ttu-id="414db-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="414db-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="414db-134">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="414db-134">**POST**</span></span> | <span data-ttu-id="414db-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="414db-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="414db-136">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="414db-136">URI parameter</span></span>

<span data-ttu-id="414db-137">Niteliği güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="414db-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="414db-138">Ad</span><span class="sxs-lookup"><span data-stu-id="414db-138">Name</span></span>                   | <span data-ttu-id="414db-139">Tür</span><span class="sxs-lookup"><span data-stu-id="414db-139">Type</span></span> | <span data-ttu-id="414db-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="414db-140">Required</span></span> | <span data-ttu-id="414db-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="414db-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="414db-142">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="414db-142">**customer-tenant-id**</span></span> | <span data-ttu-id="414db-143">GUID</span><span class="sxs-lookup"><span data-stu-id="414db-143">GUID</span></span> | <span data-ttu-id="414db-144">Yes</span><span class="sxs-lookup"><span data-stu-id="414db-144">Yes</span></span>      | <span data-ttu-id="414db-145">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="414db-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="414db-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="414db-146">**validationCode**</span></span>     | <span data-ttu-id="414db-147">int</span><span class="sxs-lookup"><span data-stu-id="414db-147">int</span></span>  | <span data-ttu-id="414db-148">No</span><span class="sxs-lookup"><span data-stu-id="414db-148">No</span></span>       | <span data-ttu-id="414db-149">Yalnızca Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="414db-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="414db-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="414db-150">Request headers</span></span>

<span data-ttu-id="414db-151">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="414db-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="414db-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="414db-152">Request body</span></span>

<span data-ttu-id="414db-153">Bu tablo, istek gövdesinin nitelik nesnesini açıklar.</span><span class="sxs-lookup"><span data-stu-id="414db-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="414db-154">Özellik</span><span class="sxs-lookup"><span data-stu-id="414db-154">Property</span></span> | <span data-ttu-id="414db-155">Tür</span><span class="sxs-lookup"><span data-stu-id="414db-155">Type</span></span> | <span data-ttu-id="414db-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="414db-156">Required</span></span> | <span data-ttu-id="414db-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="414db-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="414db-158">Eleme</span><span class="sxs-lookup"><span data-stu-id="414db-158">Qualification</span></span> | <span data-ttu-id="414db-159">string</span><span class="sxs-lookup"><span data-stu-id="414db-159">string</span></span> | <span data-ttu-id="414db-160">Yes</span><span class="sxs-lookup"><span data-stu-id="414db-160">Yes</span></span> | <span data-ttu-id="414db-161">[**CustomerQualification enum değerinden dize**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) değeri.</span><span class="sxs-lookup"><span data-stu-id="414db-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="414db-162">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="414db-162">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="414db-163">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="414db-163">REST response</span></span>

<span data-ttu-id="414db-164">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelik nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="414db-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="414db-165">Aşağıda, Eğitim niteliğine sahip bir müşteriyle ilgili **POST** çağrısının bir örneği (daha önce **Yok** niteliğine sahip) **verilmiştir.**</span><span class="sxs-lookup"><span data-stu-id="414db-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="414db-166">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="414db-166">Response success and error codes</span></span>

<span data-ttu-id="414db-167">Her yanıt, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="414db-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="414db-168">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="414db-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="414db-169">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="414db-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="414db-170">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="414db-170">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="414db-171">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="414db-171">Related articles</span></span>

- [<span data-ttu-id="414db-172">Müşterinin niteliklerini al</span><span class="sxs-lookup"><span data-stu-id="414db-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="414db-173">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="414db-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
