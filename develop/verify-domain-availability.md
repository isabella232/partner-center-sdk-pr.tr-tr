---
title: Etki alanı kullanılabilirliğini doğrulama
description: Bir etki alanının kullanıma hazır olup olmadığını belirleme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769605"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="ddcaa-103">Etki alanı kullanılabilirliğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="ddcaa-103">Verify domain availability</span></span>

<span data-ttu-id="ddcaa-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="ddcaa-104">**Applies To**</span></span>

- <span data-ttu-id="ddcaa-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-105">Partner Center</span></span>
- <span data-ttu-id="ddcaa-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ddcaa-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ddcaa-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ddcaa-109">Bir etki alanının kullanıma hazır olup olmadığını belirleme.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-109">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddcaa-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ddcaa-110">Prerequisites</span></span>

- <span data-ttu-id="ddcaa-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ddcaa-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ddcaa-113">Bir etki alanı (örneğin `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="ddcaa-113">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="ddcaa-114">C\#</span><span class="sxs-lookup"><span data-stu-id="ddcaa-114">C\#</span></span>

<span data-ttu-id="ddcaa-115">Bir etki alanının kullanılabilir olup olmadığını doğrulamak için, önce etki alanı işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) ' ı çağırın.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-115">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="ddcaa-116">Ardından, denetlenecek etki alanı ile [**bydomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-116">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="ddcaa-117">Bu yöntem, belirli bir etki alanı için kullanılabilir işlemlere bir arabirim alır.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-117">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="ddcaa-118">Son olarak, etki alanının zaten mevcut olup olmadığını görmek için [**EXISTS**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-118">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="ddcaa-119">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ddcaa-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ddcaa-120">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CheckDomainAvailability.cs</span><span class="sxs-lookup"><span data-stu-id="ddcaa-120">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ddcaa-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="ddcaa-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ddcaa-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-122">Request syntax</span></span>

| <span data-ttu-id="ddcaa-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="ddcaa-123">Method</span></span>   | <span data-ttu-id="ddcaa-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="ddcaa-124">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="ddcaa-125">**BAŞLı**</span><span class="sxs-lookup"><span data-stu-id="ddcaa-125">**HEAD**</span></span> | <span data-ttu-id="ddcaa-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Domains/{Domain} http/1.1</span><span class="sxs-lookup"><span data-stu-id="ddcaa-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ddcaa-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-127">URI parameter</span></span>

<span data-ttu-id="ddcaa-128">Etki alanı kullanılabilirliğini doğrulamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-128">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="ddcaa-129">Ad</span><span class="sxs-lookup"><span data-stu-id="ddcaa-129">Name</span></span>       | <span data-ttu-id="ddcaa-130">Tür</span><span class="sxs-lookup"><span data-stu-id="ddcaa-130">Type</span></span>       | <span data-ttu-id="ddcaa-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ddcaa-131">Required</span></span> | <span data-ttu-id="ddcaa-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ddcaa-132">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="ddcaa-133">**alanını**</span><span class="sxs-lookup"><span data-stu-id="ddcaa-133">**domain**</span></span> | <span data-ttu-id="ddcaa-134">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="ddcaa-134">**string**</span></span> | <span data-ttu-id="ddcaa-135">Y</span><span class="sxs-lookup"><span data-stu-id="ddcaa-135">Y</span></span>        | <span data-ttu-id="ddcaa-136">Denetlenecek etki alanını tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-136">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ddcaa-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="ddcaa-137">Request headers</span></span>

<span data-ttu-id="ddcaa-138">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ddcaa-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ddcaa-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="ddcaa-139">Request body</span></span>

<span data-ttu-id="ddcaa-140">Yok</span><span class="sxs-lookup"><span data-stu-id="ddcaa-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="ddcaa-141">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="ddcaa-141">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ddcaa-142">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="ddcaa-142">REST response</span></span>

<span data-ttu-id="ddcaa-143">Etki alanı varsa, kullanım için kullanılamaz ve 200 Tamam yanıt durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-143">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="ddcaa-144">Etki alanı bulunmazsa, kullanılabilir ve 404 yanıt durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-144">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ddcaa-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ddcaa-145">Response success and error codes</span></span>

<span data-ttu-id="ddcaa-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ddcaa-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ddcaa-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ddcaa-148">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ddcaa-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="ddcaa-149">Etki alanı zaten kullanımda olduğunda yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="ddcaa-149">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="ddcaa-150">Etki alanı kullanılabilir olduğunda yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="ddcaa-150">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
