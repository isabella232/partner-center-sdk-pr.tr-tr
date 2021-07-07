---
title: Müşterinin yeterliliğini güncelleştirme
description: Bir müşterinin niteliklerini, profille ilişkili adres da dahil, zaman uyumlu filtreleme veya dikele aracılığıyla güncelleştirme hakkında bilgi edinin.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446658"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="41eb3-103">Zaman uyumlu doğrulama ile bir müşterinin nitelemesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="41eb3-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="41eb3-104">Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin niteliklerini zaman uyumlu olarak güncelleştirme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="41eb3-104">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="41eb3-105">Bunu zaman uyumsuz yapmayı öğrenmek için bkz. [bir müşterinin nitelemesini zaman uyumsuz doğrulama aracılığıyla güncelleştirme](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="41eb3-105">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="41eb3-106">Bir iş ortağı, bir müşterinin nitelemesini "eğitim" veya "kamu bulutu" olacak şekilde güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="41eb3-106">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="41eb3-107">Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="41eb3-107">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41eb3-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="41eb3-108">Prerequisites</span></span>

- <span data-ttu-id="41eb3-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="41eb3-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="41eb3-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="41eb3-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="41eb3-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="41eb3-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="41eb3-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41eb3-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="41eb3-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="41eb3-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="41eb3-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="41eb3-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="41eb3-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="41eb3-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="41eb3-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="41eb3-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="41eb3-117">C\#</span><span class="sxs-lookup"><span data-stu-id="41eb3-117">C\#</span></span>

<span data-ttu-id="41eb3-118">Bir müşterinin nitelemesini "eğitim" olarak güncelleştirmek için mevcut bir [**müşterinin**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) **[Update/DotNet/api/Microsoft. Store. partnercenter. nitelik. ıcustomernitelik. Update)** öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="41eb3-118">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="41eb3-119">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="41eb3-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="41eb3-120">**Project**: partnersdk. featuresamples **sınıfı**: CustomerQualificationOperations. cs</span><span class="sxs-lookup"><span data-stu-id="41eb3-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="41eb3-121">Bir müşterinin nitelemesini, mevcut bir müşteri üzerinde bir nitelik olmadan **Hükümentcommunitycloud** olarak güncelleştirmek için, ortağın müşterinin [**validationcode**](utility-resources.md#validationcode)'u içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="41eb3-121">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="41eb3-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="41eb3-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="41eb3-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="41eb3-123">Request syntax</span></span>

| <span data-ttu-id="41eb3-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="41eb3-124">Method</span></span>  | <span data-ttu-id="41eb3-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="41eb3-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="41eb3-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="41eb3-126">**PUT**</span></span> | <span data-ttu-id="41eb3-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/nitelendirme? Code = {validationcode} http/1.1</span><span class="sxs-lookup"><span data-stu-id="41eb3-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="41eb3-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="41eb3-128">URI parameter</span></span>

<span data-ttu-id="41eb3-129">Nitelemeyi güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="41eb3-129">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="41eb3-130">Ad</span><span class="sxs-lookup"><span data-stu-id="41eb3-130">Name</span></span>                   | <span data-ttu-id="41eb3-131">Tür</span><span class="sxs-lookup"><span data-stu-id="41eb3-131">Type</span></span> | <span data-ttu-id="41eb3-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="41eb3-132">Required</span></span> | <span data-ttu-id="41eb3-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41eb3-133">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="41eb3-134">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="41eb3-134">**customer-tenant-id**</span></span> | <span data-ttu-id="41eb3-135">GUID</span><span class="sxs-lookup"><span data-stu-id="41eb3-135">GUID</span></span> | <span data-ttu-id="41eb3-136">Yes</span><span class="sxs-lookup"><span data-stu-id="41eb3-136">Yes</span></span>      | <span data-ttu-id="41eb3-137">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="41eb3-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="41eb3-138">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="41eb3-138">**validationCode**</span></span>     | <span data-ttu-id="41eb3-139">int</span><span class="sxs-lookup"><span data-stu-id="41eb3-139">int</span></span>  | <span data-ttu-id="41eb3-140">Hayır</span><span class="sxs-lookup"><span data-stu-id="41eb3-140">No</span></span>       | <span data-ttu-id="41eb3-141">Yalnızca Government Community Cloud için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="41eb3-141">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="41eb3-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="41eb3-142">Request headers</span></span>

<span data-ttu-id="41eb3-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="41eb3-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="41eb3-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="41eb3-144">Request body</span></span>

<span data-ttu-id="41eb3-145">[**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından tamsayı değeri.</span><span class="sxs-lookup"><span data-stu-id="41eb3-145">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="41eb3-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="41eb3-146">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="41eb3-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="41eb3-147">REST response</span></span>

<span data-ttu-id="41eb3-148">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [**nitelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) özelliğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="41eb3-148">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="41eb3-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="41eb3-149">Response success and error codes</span></span>

<span data-ttu-id="41eb3-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="41eb3-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="41eb3-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="41eb3-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="41eb3-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="41eb3-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="41eb3-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="41eb3-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="41eb3-154">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="41eb3-154">Related articles</span></span>

- [<span data-ttu-id="41eb3-155">Müşterinin nitelemesini alma</span><span class="sxs-lookup"><span data-stu-id="41eb3-155">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="41eb3-156">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="41eb3-156">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
