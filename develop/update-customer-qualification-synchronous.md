---
title: Müşterinin yeterliliğini güncelleştirme
description: Bir müşterinin niteliklerini, profille ilişkili adres da dahil, zaman uyumlu filtreleme veya dikele aracılığıyla güncelleştirme hakkında bilgi edinin.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c202d95beab771241a9665243be5f08ab6f82fd5
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711976"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="186f3-103">Zaman uyumlu doğrulama ile bir müşterinin nitelemesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="186f3-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="186f3-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="186f3-104">**Applies To**</span></span>

- <span data-ttu-id="186f3-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="186f3-105">Partner Center</span></span>

<span data-ttu-id="186f3-106">Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin niteliklerini zaman uyumlu olarak güncelleştirme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="186f3-106">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="186f3-107">Bunu zaman uyumsuz yapmayı öğrenmek için bkz. [bir müşterinin nitelemesini zaman uyumsuz doğrulama aracılığıyla güncelleştirme](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="186f3-107">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="186f3-108">Bir iş ortağı, bir müşterinin nitelemesini "eğitim" veya "kamu bulutu" olacak şekilde güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="186f3-108">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="186f3-109">Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="186f3-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="186f3-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="186f3-110">Prerequisites</span></span>

- <span data-ttu-id="186f3-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="186f3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="186f3-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="186f3-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="186f3-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="186f3-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="186f3-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="186f3-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="186f3-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="186f3-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="186f3-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="186f3-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="186f3-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="186f3-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="186f3-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="186f3-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="186f3-119">C\#</span><span class="sxs-lookup"><span data-stu-id="186f3-119">C\#</span></span>

<span data-ttu-id="186f3-120">Bir müşterinin nitelemesini "eğitim" olarak güncelleştirmek için mevcut bir [**müşterinin**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) **[Update/DotNet/api/Microsoft. Store. partnercenter. nitelik. ıcustomernitelik. Update)** öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="186f3-120">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="186f3-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="186f3-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="186f3-122">**Proje**: Partnersdk. Featuresamples **sınıfı**: CustomerQualificationOperations. cs</span><span class="sxs-lookup"><span data-stu-id="186f3-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="186f3-123">Bir müşterinin nitelemesini, mevcut bir müşteri üzerinde bir nitelik olmadan **Hükümentcommunitycloud** olarak güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="186f3-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification.</span></span>  <span data-ttu-id="186f3-124">Ayrıca iş ortağının, müşterinin [**Validationcode**](utility-resources.md#validationcode)'u içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="186f3-124">The partner is also are required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="186f3-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="186f3-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="186f3-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="186f3-126">Request syntax</span></span>

| <span data-ttu-id="186f3-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="186f3-127">Method</span></span>  | <span data-ttu-id="186f3-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="186f3-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="186f3-129">**PUT**</span><span class="sxs-lookup"><span data-stu-id="186f3-129">**PUT**</span></span> | <span data-ttu-id="186f3-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/nitelendirme? Code = {validationcode} http/1.1</span><span class="sxs-lookup"><span data-stu-id="186f3-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="186f3-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="186f3-131">URI parameter</span></span>

<span data-ttu-id="186f3-132">Nitelemeyi güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="186f3-132">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="186f3-133">Ad</span><span class="sxs-lookup"><span data-stu-id="186f3-133">Name</span></span>                   | <span data-ttu-id="186f3-134">Tür</span><span class="sxs-lookup"><span data-stu-id="186f3-134">Type</span></span> | <span data-ttu-id="186f3-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="186f3-135">Required</span></span> | <span data-ttu-id="186f3-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="186f3-136">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="186f3-137">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="186f3-137">**customer-tenant-id**</span></span> | <span data-ttu-id="186f3-138">GUID</span><span class="sxs-lookup"><span data-stu-id="186f3-138">GUID</span></span> | <span data-ttu-id="186f3-139">Yes</span><span class="sxs-lookup"><span data-stu-id="186f3-139">Yes</span></span>      | <span data-ttu-id="186f3-140">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="186f3-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="186f3-141">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="186f3-141">**validationCode**</span></span>     | <span data-ttu-id="186f3-142">int</span><span class="sxs-lookup"><span data-stu-id="186f3-142">int</span></span>  | <span data-ttu-id="186f3-143">No</span><span class="sxs-lookup"><span data-stu-id="186f3-143">No</span></span>       | <span data-ttu-id="186f3-144">Yalnızca kamu Community bulutu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="186f3-144">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="186f3-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="186f3-145">Request headers</span></span>

<span data-ttu-id="186f3-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="186f3-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="186f3-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="186f3-147">Request body</span></span>

<span data-ttu-id="186f3-148">[**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından tamsayı değeri.</span><span class="sxs-lookup"><span data-stu-id="186f3-148">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="186f3-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="186f3-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="186f3-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="186f3-150">REST response</span></span>

<span data-ttu-id="186f3-151">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="186f3-151">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="186f3-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="186f3-152">Response success and error codes</span></span>

<span data-ttu-id="186f3-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="186f3-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="186f3-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="186f3-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="186f3-155">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="186f3-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="186f3-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="186f3-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="186f3-157">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="186f3-157">Related articles</span></span>

- [<span data-ttu-id="186f3-158">Müşterinin nitelemesini alma</span><span class="sxs-lookup"><span data-stu-id="186f3-158">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="186f3-159">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="186f3-159">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)