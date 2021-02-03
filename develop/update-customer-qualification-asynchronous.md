---
title: Müşterinin niteliklerini güncelleştirme
description: Bir müşterinin niteliklerini, profille ilişkili adres dahil, zaman uyumsuz filtreleme veya diting aracılığıyla güncelleştirmeyi öğrenin.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: e0390e8a9c2a277dcb9e18b026f12625400ae176
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770202"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="87be8-103">Müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="87be8-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="87be8-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="87be8-104">**Applies To**</span></span>

- <span data-ttu-id="87be8-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="87be8-105">Partner Center</span></span>

<span data-ttu-id="87be8-106">Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşterinin niteliklerini zaman uyumsuz olarak güncelleştirme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="87be8-106">Learn how to update a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="87be8-107">Bunu eşzamanlı olarak nasıl yapacağınızı öğrenmek için bkz. [zaman uyumlu doğrulama ile bir müşterinin nitelemesini güncelleştirme](update-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="87be8-107">To learn how to do this synchronously, see [Update a customer's qualification via synchronous validation](update-customer-qualification-synchronous.md).</span></span>

<span data-ttu-id="87be8-108">Bir iş ortağı, zaman uyumsuz olarak "eğitim" veya "Hükümentcommunıcloud" olarak bir müşterinin niteliklerini güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="87be8-108">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="87be8-109">Diğer değerler, "none" ve "kar olmayan" ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="87be8-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87be8-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="87be8-110">Prerequisites</span></span>

- <span data-ttu-id="87be8-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="87be8-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="87be8-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="87be8-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="87be8-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="87be8-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="87be8-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87be8-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="87be8-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="87be8-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="87be8-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="87be8-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="87be8-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="87be8-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="87be8-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="87be8-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="87be8-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="87be8-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="87be8-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="87be8-120">Request syntax</span></span>

| <span data-ttu-id="87be8-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="87be8-121">Method</span></span>  | <span data-ttu-id="87be8-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="87be8-122">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="87be8-123">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="87be8-123">**POST**</span></span> | <span data-ttu-id="87be8-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/nitelikler? Code = {validationcode} http/1.1</span><span class="sxs-lookup"><span data-stu-id="87be8-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="87be8-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="87be8-125">URI parameter</span></span>

<span data-ttu-id="87be8-126">Nitelemeyi güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="87be8-126">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="87be8-127">Ad</span><span class="sxs-lookup"><span data-stu-id="87be8-127">Name</span></span>                   | <span data-ttu-id="87be8-128">Tür</span><span class="sxs-lookup"><span data-stu-id="87be8-128">Type</span></span> | <span data-ttu-id="87be8-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="87be8-129">Required</span></span> | <span data-ttu-id="87be8-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87be8-130">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="87be8-131">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="87be8-131">**customer-tenant-id**</span></span> | <span data-ttu-id="87be8-132">GUID</span><span class="sxs-lookup"><span data-stu-id="87be8-132">GUID</span></span> | <span data-ttu-id="87be8-133">Yes</span><span class="sxs-lookup"><span data-stu-id="87be8-133">Yes</span></span>      | <span data-ttu-id="87be8-134">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="87be8-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="87be8-135">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="87be8-135">**validationCode**</span></span>     | <span data-ttu-id="87be8-136">int</span><span class="sxs-lookup"><span data-stu-id="87be8-136">int</span></span>  | <span data-ttu-id="87be8-137">No</span><span class="sxs-lookup"><span data-stu-id="87be8-137">No</span></span>       | <span data-ttu-id="87be8-138">Yalnızca kamu Community bulutu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="87be8-138">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="87be8-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="87be8-139">Request headers</span></span>

<span data-ttu-id="87be8-140">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="87be8-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="87be8-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="87be8-141">Request body</span></span>

<span data-ttu-id="87be8-142">[**Customernitelendirme**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) numaralandırmasından tamsayı değeri.</span><span class="sxs-lookup"><span data-stu-id="87be8-142">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="87be8-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="87be8-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="87be8-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="87be8-144">REST response</span></span>

<span data-ttu-id="87be8-145">Başarılı olursa, bu yöntem yanıt gövdesinde bir nitelikler nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="87be8-145">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="87be8-146">**Eğitim** nitelemesini içeren bir müşterinin (önceki bir niteliğe sahip **olmayan)** **gönderme** çağrısının bir örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="87be8-146">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="87be8-147">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="87be8-147">Response success and error codes</span></span>

<span data-ttu-id="87be8-148">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="87be8-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="87be8-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="87be8-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="87be8-150">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="87be8-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="87be8-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="87be8-151">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="87be8-152">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="87be8-152">Related articles</span></span>

- [<span data-ttu-id="87be8-153">Müşterinin niteliklerini al</span><span class="sxs-lookup"><span data-stu-id="87be8-153">Get a customer's qualifications</span></span>](get-a-customer-s-qualifications.md)
- [<span data-ttu-id="87be8-154">İş ortağının doğrulama kodlarını alma</span><span class="sxs-lookup"><span data-stu-id="87be8-154">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)