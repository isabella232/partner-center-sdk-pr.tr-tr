---
title: Dolaylı bir satıcının Microsoft Iş ortağı sözleşmesi imza durumunu doğrulama
description: AgreementStatus API 'sini kullanarak dolaylı bir satıcının Microsoft Iş ortağı sözleşmesinin imzalanıp imzalanmadığını doğrulayabilirsiniz.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 436f690991a2920465a5a13c73eb4c194956ae94
ms.sourcegitcommit: ca932ba511bf7464a634195d71891f989036ab74
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/29/2020
ms.locfileid: "97769934"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="3186c-103">Dolaylı bir satıcının Microsoft Iş ortağı sözleşmesi imza durumunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="3186c-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="3186c-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="3186c-104">**Applies to:**</span></span>

- <span data-ttu-id="3186c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3186c-105">Partner Center</span></span>
- <span data-ttu-id="3186c-106">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3186c-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3186c-107">Bir dolaylı satıcının, Microsoft İş Ortağı Ağı (MPN) KIMLIĞI (PGA/PLA) veya bulut çözümü sağlayıcısı (CSP) kiracı KIMLIĞI (Microsoft ID) kullanarak Microsoft Iş ortağı sözleşmesi 'Ni imzaladığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3186c-107">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="3186c-108">**AgreementStatus** API 'Sini kullanarak Microsoft Iş ortağı sözleşmesi imza durumunu denetlemek için bu tanımlayıcılardan birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3186c-108">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3186c-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3186c-109">Prerequisites</span></span>

- <span data-ttu-id="3186c-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3186c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3186c-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3186c-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3186c-112">MPN KIMLIĞI (PGA/PLA) veya dolaylı satıcıdan oluşan CSP kiracı KIMLIĞI (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="3186c-112">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="3186c-113">*Bu iki tanımlayıcıdan birini kullanmalısınız.*</span><span class="sxs-lookup"><span data-stu-id="3186c-113">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="3186c-114">C\#</span><span class="sxs-lookup"><span data-stu-id="3186c-114">C\#</span></span>

<span data-ttu-id="3186c-115">Dolaylı bir satıcının Microsoft Iş ortağı sözleşmesi imza durumunu almak için:</span><span class="sxs-lookup"><span data-stu-id="3186c-115">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="3186c-116">**AgreementSignatureStatus** özelliğini çağırmak Için **ıaggregatepartner. uyum** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3186c-116">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="3186c-117">[**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="3186c-117">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="3186c-118">Örnek: **[konsol test uygulaması](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="3186c-118">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="3186c-119">Proje: **Partnercentersdk. FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="3186c-119">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="3186c-120">Sınıf: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="3186c-120">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3186c-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3186c-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3186c-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3186c-122">Request syntax</span></span>

| <span data-ttu-id="3186c-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3186c-123">Method</span></span> | <span data-ttu-id="3186c-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3186c-124">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="3186c-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="3186c-125">**GET**</span></span> | <span data-ttu-id="3186c-126">*[{BaseUrl}](partner-center-rest-urls.md)*/v1/Compliance/{programname}/agreementstatus? mpnıd = {mpnıd} &tenantıd = {tenantıd}</span><span class="sxs-lookup"><span data-stu-id="3186c-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3186c-127">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="3186c-127">URI parameters</span></span>

<span data-ttu-id="3186c-128">İş ortağını tanımlamak için aşağıdaki iki sorgu parametresini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3186c-128">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="3186c-129">Bu iki sorgu parametrelerinden birini sağlamazsanız, **400 (hatalı istek)** hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3186c-129">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="3186c-130">Ad</span><span class="sxs-lookup"><span data-stu-id="3186c-130">Name</span></span> | <span data-ttu-id="3186c-131">Tür</span><span class="sxs-lookup"><span data-stu-id="3186c-131">Type</span></span> | <span data-ttu-id="3186c-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3186c-132">Required</span></span> | <span data-ttu-id="3186c-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3186c-133">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="3186c-134">**Mpnıd**</span><span class="sxs-lookup"><span data-stu-id="3186c-134">**MpnId**</span></span> | <span data-ttu-id="3186c-135">int</span><span class="sxs-lookup"><span data-stu-id="3186c-135">int</span></span> | <span data-ttu-id="3186c-136">No</span><span class="sxs-lookup"><span data-stu-id="3186c-136">No</span></span> | <span data-ttu-id="3186c-137">Dolaylı Bayi tanımlayan bir Microsoft İş Ortağı Ağı KIMLIĞI (PGA/PLA).</span><span class="sxs-lookup"><span data-stu-id="3186c-137">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="3186c-138">**Değerine**</span><span class="sxs-lookup"><span data-stu-id="3186c-138">**TenantId**</span></span> | <span data-ttu-id="3186c-139">GUID</span><span class="sxs-lookup"><span data-stu-id="3186c-139">GUID</span></span> | <span data-ttu-id="3186c-140">No</span><span class="sxs-lookup"><span data-stu-id="3186c-140">No</span></span> | <span data-ttu-id="3186c-141">Dolaylı satıcıdan oluşan CSP hesabını tanımlayan bir Microsoft KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="3186c-141">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3186c-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3186c-142">Request headers</span></span>

<span data-ttu-id="3186c-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI kalanı](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3186c-143">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="3186c-144">İstek örnekleri</span><span class="sxs-lookup"><span data-stu-id="3186c-144">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="3186c-145">MPN KIMLIĞI (PGA/PLA) kullanarak istek</span><span class="sxs-lookup"><span data-stu-id="3186c-145">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="3186c-146">Aşağıdaki örnek istek dolaylı satıcının Microsoft Iş ortağı sözleşmesi imza durumunu dolaylı Bayi Microsoft İş Ortağı Ağı KIMLIĞINI kullanarak alır.</span><span class="sxs-lookup"><span data-stu-id="3186c-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="3186c-147">CSP kiracı KIMLIĞI kullanarak istek</span><span class="sxs-lookup"><span data-stu-id="3186c-147">Request using CSP tenant ID</span></span>

<span data-ttu-id="3186c-148">Aşağıdaki örnek istek, dolaylı satıcının CSP kiracı KIMLIĞINI (Microsoft ID) kullanarak dolaylı satıcının Microsoft Iş ortağı sözleşmesi imza durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="3186c-148">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3186c-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3186c-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3186c-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3186c-150">Response success and error codes</span></span>

<span data-ttu-id="3186c-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3186c-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3186c-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3186c-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3186c-153">Tam liste için bkz. [Iş ortağı MERKEZI Rest hatası](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3186c-153">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="3186c-154">Yanıt örneği (başarılı)</span><span class="sxs-lookup"><span data-stu-id="3186c-154">Response example (success)</span></span>

<span data-ttu-id="3186c-155">Aşağıdaki örnek yanıt başarıyla dolaylı satıcının Microsoft Iş ortağı sözleşmesi 'Ni imzaladığı olup olmadığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3186c-155">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a><span data-ttu-id="3186c-156">Yanıt örnekleri (hata)</span><span class="sxs-lookup"><span data-stu-id="3186c-156">Response examples (failure)</span></span>

<span data-ttu-id="3186c-157">Dolaylı satıcının Microsoft Iş ortağı sözleşmesinin imzalama durumu döndürülemeyebilir, aşağıdaki örneklere benzer yanıtlar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3186c-157">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="3186c-158">GUID olmayan biçimli CSP kiracı KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="3186c-158">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="3186c-159">Aşağıdaki örnek yanıt, API 'ye geçirilen CSP kiracı KIMLIĞI bir GUID olmadığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-159">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="3186c-160">Sayısal olmayan MPN KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="3186c-160">Non-numeric MPN ID</span></span>

<span data-ttu-id="3186c-161">Aşağıdaki örnek yanıt, API 'ye geçirilen MPN KIMLIĞI (PGA/PLA) sayısal olmayan bir değer olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-161">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="3186c-162">MPN KIMLIĞI veya CSP kiracı KIMLIĞI yok</span><span class="sxs-lookup"><span data-stu-id="3186c-162">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="3186c-163">Aşağıdaki örnek yanıt, API 'ye bir MPN KIMLIĞI (PGA/PLA) veya CSP kiracı KIMLIĞI geçirmedikçe döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-163">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="3186c-164">İki KIMLIK türünden birini API 'ye geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3186c-164">You must pass one of the two ID types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="3186c-165">MPN KIMLIĞI ve CSP kiracı KIMLIĞI geçildi</span><span class="sxs-lookup"><span data-stu-id="3186c-165">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="3186c-166">Aşağıdaki örnek yanıt, hem MPN KIMLIĞI (PGA/PLA) hem de CSP kiracı KIMLIĞINI API 'ye geçirdiğinizde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-166">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="3186c-167">API 'ye iki tanımlayıcı türünden *yalnızca birini* geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3186c-167">You must pass *only one* of the two identifier types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="3186c-168">CSP dolaylı Bayi MPN kimliği (PGA/PLA) geçersiz ya da Iş ortağı üyeliği merkezinden Iş Ortağı Merkezi 'ne geçirilmedi</span><span class="sxs-lookup"><span data-stu-id="3186c-168">CSP Indirect Reseller MPN Id (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="3186c-169">Geçirilen dolaylı satıcı MPN KIMLIĞI (PGA/PLA) geçersiz olduğunda veya Iş ortağı üyeliği merkezinden Iş Ortağı Merkezi 'ne geçirilmediğinde aşağıdaki örnek yanıt döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-169">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="3186c-170">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="3186c-170">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="3186c-171">CSP dolaylı sağlayıcı bölgesi ve CSP dolaylı satıcı bölgesi eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="3186c-171">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="3186c-172">Dolaylı satıcı MPN KIMLIĞI (PGA/PLA) bölgesi dolaylı sağlayıcının bölgesiyle eşleşmediği zaman aşağıdaki örnek yanıt döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-172">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="3186c-173">CSP bölgeleri hakkında [daha fazla bilgi edinin](/partner-center/regional-authorization-overview) .</span><span class="sxs-lookup"><span data-stu-id="3186c-173">[Learn more](/partner-center/regional-authorization-overview) about CSP Regions.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="3186c-174">CSP dolaylı satıcı hesabı Iş Ortağı Merkezi 'nde var, ancak MPA imzasız</span><span class="sxs-lookup"><span data-stu-id="3186c-174">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="3186c-175">Aşağıdaki örnek yanıt, Iş ortağı merkezindeki CSP dolaylı satıcı hesabı MPA 'yı imzaladığı zaman döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-175">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="3186c-176">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="3186c-176">Learn More</span></span>](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="3186c-177">Belirtilen MPN KIMLIĞIYLE ilişkili CSP dolaylı satıcı hesabı yok</span><span class="sxs-lookup"><span data-stu-id="3186c-177">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="3186c-178">Iş Ortağı Merkezi, istekte geçirilen MPN KIMLIĞINI (PGA/PLA) tanıyabileceği halde, belirtilen MPN KIMLIĞI (PGA/PLA) ile ilişkili CSP kaydı yoksa, aşağıdaki örnek yanıt döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-178">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="3186c-179">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="3186c-179">Learn More</span></span>](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="3186c-180">Geçersiz kiracı KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="3186c-180">Invalid Tenant ID</span></span>

<span data-ttu-id="3186c-181">Iş Ortağı Merkezi, istekte geçirilen kiracı KIMLIĞIYLE ilişkili herhangi bir hesap bulamadığında aşağıdaki örnek yanıt döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-181">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="3186c-182">Verilen kiracı KIMLIĞINE sahip bir MPA bulunamadı</span><span class="sxs-lookup"><span data-stu-id="3186c-182">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="3186c-183">Aşağıdaki örnek yanıt, Iş Ortağı Merkezi belirtilen kiracı KIMLIĞINE sahip herhangi bir MPA imzasını bulamadığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3186c-183">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [],
    "source": "PartnerFD"
}
```
