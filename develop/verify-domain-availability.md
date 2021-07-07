---
title: Etki alanı kullanılabilirliğini doğrulama
description: Bir etki alanının kullanılabilir olup olmadığını belirleme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530285"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="e1e5b-103">Etki alanı kullanılabilirliğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="e1e5b-103">Verify domain availability</span></span>

<span data-ttu-id="e1e5b-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e1e5b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e1e5b-105">Bir etki alanının kullanılabilir olup olmadığını belirleme.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-105">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1e5b-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e1e5b-106">Prerequisites</span></span>

- <span data-ttu-id="e1e5b-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e1e5b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e1e5b-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e1e5b-109">Bir etki alanı `contoso.onmicrosoft.com` (örneğin).</span><span class="sxs-lookup"><span data-stu-id="e1e5b-109">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="e1e5b-110">C\#</span><span class="sxs-lookup"><span data-stu-id="e1e5b-110">C\#</span></span>

<span data-ttu-id="e1e5b-111">Bir etki alanının kullanılabilir olup olduğunu doğrulamak için önce [**IAggregatePartner.Domains'i**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) çağırarak etki alanı işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-111">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="e1e5b-112">Ardından, kontrol [**etmek için etki alanıyla ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-112">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="e1e5b-113">Bu yöntem, belirli bir etki alanı için kullanılabilir işlemler için bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-113">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="e1e5b-114">Son olarak, etki [**alanının zaten**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) var olup olduğunu görmek için Exists yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-114">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="e1e5b-115">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1e5b-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e1e5b-116">**Project:** İş Ortağı Merkezi SDK'sı Örnekleri **Sınıfı:** CheckDomainAvailability.cs</span><span class="sxs-lookup"><span data-stu-id="e1e5b-116">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e1e5b-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e1e5b-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e1e5b-118">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="e1e5b-118">Request syntax</span></span>

| <span data-ttu-id="e1e5b-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e1e5b-119">Method</span></span>   | <span data-ttu-id="e1e5b-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e1e5b-120">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="e1e5b-121">**Kafa**</span><span class="sxs-lookup"><span data-stu-id="e1e5b-121">**HEAD**</span></span> | <span data-ttu-id="e1e5b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e1e5b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e1e5b-123">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="e1e5b-123">URI parameter</span></span>

<span data-ttu-id="e1e5b-124">Etki alanı kullanılabilirliğini doğrulamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-124">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="e1e5b-125">Ad</span><span class="sxs-lookup"><span data-stu-id="e1e5b-125">Name</span></span>       | <span data-ttu-id="e1e5b-126">Tür</span><span class="sxs-lookup"><span data-stu-id="e1e5b-126">Type</span></span>       | <span data-ttu-id="e1e5b-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e1e5b-127">Required</span></span> | <span data-ttu-id="e1e5b-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e1e5b-128">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="e1e5b-129">**Etki alanı**</span><span class="sxs-lookup"><span data-stu-id="e1e5b-129">**domain**</span></span> | <span data-ttu-id="e1e5b-130">**string**</span><span class="sxs-lookup"><span data-stu-id="e1e5b-130">**string**</span></span> | <span data-ttu-id="e1e5b-131">Y</span><span class="sxs-lookup"><span data-stu-id="e1e5b-131">Y</span></span>        | <span data-ttu-id="e1e5b-132">Kontrol etmek için etki alanını tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-132">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e1e5b-133">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e1e5b-133">Request headers</span></span>

<span data-ttu-id="e1e5b-134">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e1e5b-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e1e5b-135">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e1e5b-135">Request body</span></span>

<span data-ttu-id="e1e5b-136">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="e1e5b-136">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e1e5b-137">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e1e5b-137">Request example</span></span>

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e1e5b-138">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e1e5b-138">REST response</span></span>

<span data-ttu-id="e1e5b-139">Etki alanı mevcutsa kullanılamaz ve 200 Tamam yanıt durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-139">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="e1e5b-140">Etki alanı bulunamasa kullanılabilir ve 404 Bulunamadı yanıt durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-140">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e1e5b-141">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e1e5b-141">Response success and error codes</span></span>

<span data-ttu-id="e1e5b-142">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e1e5b-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1e5b-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e1e5b-144">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e1e5b-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="e1e5b-145">Etki alanı zaten kullanımda olduğunda için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e1e5b-145">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="e1e5b-146">Etki alanının kullanılabilir olduğu zaman için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e1e5b-146">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
