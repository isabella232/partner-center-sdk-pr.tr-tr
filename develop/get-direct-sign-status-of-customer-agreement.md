---
title: Microsoft Müşteri Sözleşmesi için müşterinin doğrudan imzalama durumunu alın.
description: DirectSignedCustomerAgreementStatus kaynağını, müşterinin Microsoft Müşteri sözleşmesinin doğrudan imzalama (doğrudan kabul) durumunu almak için kullanabilirsiniz.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768740"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="b0ce5-103">Müşterinin doğrudan imzalanmasından (doğrudan kabulünün) Microsoft müşteri anlaşması 'nın durumunu alın</span><span class="sxs-lookup"><span data-stu-id="b0ce5-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="b0ce5-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="b0ce5-104">**Applies to:**</span></span>

- <span data-ttu-id="b0ce5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b0ce5-105">Partner Center</span></span>

<span data-ttu-id="b0ce5-106">**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="b0ce5-107">Bu kaynak için *geçerli değildir* :</span><span class="sxs-lookup"><span data-stu-id="b0ce5-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="b0ce5-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b0ce5-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b0ce5-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b0ce5-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b0ce5-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b0ce5-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b0ce5-111">Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin doğrudan kabulünün durumunu nasıl alabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b0ce5-112">REST isteği</span><span class="sxs-lookup"><span data-stu-id="b0ce5-112">REST request</span></span>

<span data-ttu-id="b0ce5-113">Müşterinin Microsoft Müşteri sözleşmesinin doğrudan kabulünün durumunu almak için, müşteri için [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) almak üzere bir rest isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-113">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b0ce5-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b0ce5-114">Request syntax</span></span>

<span data-ttu-id="b0ce5-115">Aşağıdaki istek sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="b0ce5-115">Use the following request syntax:</span></span>

| <span data-ttu-id="b0ce5-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b0ce5-116">Method</span></span> | <span data-ttu-id="b0ce5-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="b0ce5-117">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b0ce5-118">GET</span><span class="sxs-lookup"><span data-stu-id="b0ce5-118">GET</span></span>    | <span data-ttu-id="b0ce5-119">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="b0ce5-119">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b0ce5-120">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0ce5-120">URI parameters</span></span>

<span data-ttu-id="b0ce5-121">İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0ce5-121">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="b0ce5-122">Ad</span><span class="sxs-lookup"><span data-stu-id="b0ce5-122">Name</span></span>             | <span data-ttu-id="b0ce5-123">Tür</span><span class="sxs-lookup"><span data-stu-id="b0ce5-123">Type</span></span> | <span data-ttu-id="b0ce5-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0ce5-124">Required</span></span> | <span data-ttu-id="b0ce5-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0ce5-125">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="b0ce5-126">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="b0ce5-126">customer-tenant-id</span></span> | <span data-ttu-id="b0ce5-127">GUID</span><span class="sxs-lookup"><span data-stu-id="b0ce5-127">GUID</span></span> | <span data-ttu-id="b0ce5-128">Yes</span><span class="sxs-lookup"><span data-stu-id="b0ce5-128">Yes</span></span> | <span data-ttu-id="b0ce5-129">Değer, bir müşterinin kiracı KIMLIĞINI belirtmenize olanak tanıyan bir GUID biçimli **Customertenantıd** 'dir.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-129">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b0ce5-130">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="b0ce5-130">Request headers</span></span>

<span data-ttu-id="b0ce5-131">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b0ce5-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b0ce5-132">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b0ce5-132">Request body</span></span>

<span data-ttu-id="b0ce5-133">Yok.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b0ce5-134">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="b0ce5-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="b0ce5-135">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="b0ce5-135">REST response</span></span>

<span data-ttu-id="b0ce5-136">Başarılı olursa, bu yöntem yanıt gövdesinde bir [ **DirectSignedCustomerAgreementStatus** kaynağı](./customer-agreement-direct-sign-status-resource.md) döndürür.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-136">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="b0ce5-137">Kaynağın, müşterinin doğrudan imzalama (doğrudan kabul) durumunu gösteren bir **IsSigned** özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-137">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="b0ce5-138">**Doğru** değeri, sözleşmenin doğrudan müşteri tarafından imzalanmış (kabul edildi) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-138">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="b0ce5-139">**False** değeri, sözleşmenin doğrudan müşteri tarafından *imzalanmadığını (* kabul edilmediğini) gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-139">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b0ce5-140">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="b0ce5-140">Response success and error codes</span></span>

<span data-ttu-id="b0ce5-141">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="b0ce5-142">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0ce5-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b0ce5-143">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b0ce5-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b0ce5-144">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="b0ce5-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
