---
title: Oturum açma için müşterinin doğrudan imzalama durumunu Microsoft Müşteri Sözleşmesi.
description: DirectSignedCustomerAgreementStatus kaynağını kullanarak müşterinin doğrudan imzalama (doğrudan kabul) durumunu Microsoft Müşteri Sözleşmesi.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549187"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="2e7db-103">Müşterinin doğrudan imzalama (doğrudan kabul) durumunu Microsoft Müşteri Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="2e7db-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="2e7db-104">**Için geçerlidir:** İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2e7db-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="2e7db-105">**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2e7db-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2e7db-106">**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel İş Ortağı Merkezi kaynak tarafından de desteklene bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="2e7db-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="2e7db-107">Bu makalede, bir müşterinin doğrudan kabul durumunu nasıl ala bir Microsoft Müşteri Sözleşmesi.</span><span class="sxs-lookup"><span data-stu-id="2e7db-107">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e7db-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2e7db-108">Prerequisites</span></span>

- <span data-ttu-id="2e7db-109">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2e7db-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e7db-110">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="2e7db-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2e7db-111">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e7db-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e7db-112">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2e7db-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e7db-113">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="2e7db-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e7db-114">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="2e7db-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e7db-115">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="2e7db-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e7db-116">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2e7db-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2e7db-117">C\#</span><span class="sxs-lookup"><span data-stu-id="2e7db-117">C\#</span></span>

<span data-ttu-id="2e7db-118">Müşterinin doğrudan Microsoft Müşteri Sözleşmesi kabul durumunu almak için müşteri tanımlayıcısıyla [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="2e7db-118">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="2e7db-119">Ardından [**Agreements özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) kullanarak [**ICustomerAgreementCollection arabirimini**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) alın.</span><span class="sxs-lookup"><span data-stu-id="2e7db-119">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="2e7db-120">Son olarak, durumu `GetDirectSignedCustomerAgreementStatus()` almak `GetDirectSignedCustomerAgreementStatusAsync()` için veya çağrısı.</span><span class="sxs-lookup"><span data-stu-id="2e7db-120">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="2e7db-121">**Örnek:** [Konsol Örnek Uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="2e7db-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="2e7db-122">**Project:** SdkSamples **Sınıfı**: GetDirectSignedCustomerAgreementStatus.cs</span><span class="sxs-lookup"><span data-stu-id="2e7db-122">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e7db-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2e7db-123">REST request</span></span>

<span data-ttu-id="2e7db-124">Müşterinin doğrudan kabul durumunu almak için Microsoft Müşteri Sözleşmesi için [DirectSignedCustomerAgreementStatus'u](./customer-agreement-direct-sign-status-resource.md) almak için bir REST isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2e7db-124">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e7db-125">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="2e7db-125">Request syntax</span></span>

<span data-ttu-id="2e7db-126">Aşağıdaki istek söz dizimlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="2e7db-126">Use the following request syntax:</span></span>

| <span data-ttu-id="2e7db-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2e7db-127">Method</span></span> | <span data-ttu-id="2e7db-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2e7db-128">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e7db-129">GET</span><span class="sxs-lookup"><span data-stu-id="2e7db-129">GET</span></span>    | <span data-ttu-id="2e7db-130">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2e7db-130">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="2e7db-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="2e7db-131">URI parameters</span></span>

<span data-ttu-id="2e7db-132">İsteğiniz ile aşağıdaki URI parametrelerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2e7db-132">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="2e7db-133">Ad</span><span class="sxs-lookup"><span data-stu-id="2e7db-133">Name</span></span>             | <span data-ttu-id="2e7db-134">Tür</span><span class="sxs-lookup"><span data-stu-id="2e7db-134">Type</span></span> | <span data-ttu-id="2e7db-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2e7db-135">Required</span></span> | <span data-ttu-id="2e7db-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e7db-136">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e7db-137">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="2e7db-137">customer-tenant-id</span></span> | <span data-ttu-id="2e7db-138">GUID</span><span class="sxs-lookup"><span data-stu-id="2e7db-138">GUID</span></span> | <span data-ttu-id="2e7db-139">Yes</span><span class="sxs-lookup"><span data-stu-id="2e7db-139">Yes</span></span> | <span data-ttu-id="2e7db-140">Değer, bir müşterinin kiracı kimliğini belirtmenize olanak sağlayan GUID biçimli bir **CustomerTenantId** değeridir.</span><span class="sxs-lookup"><span data-stu-id="2e7db-140">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2e7db-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2e7db-141">Request headers</span></span>

<span data-ttu-id="2e7db-142">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2e7db-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e7db-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2e7db-143">Request body</span></span>

<span data-ttu-id="2e7db-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="2e7db-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2e7db-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2e7db-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="2e7db-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2e7db-146">REST response</span></span>

<span data-ttu-id="2e7db-147">Başarılı olursa, bu yöntem yanıt [ **gövdesinde bir DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="2e7db-147">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="2e7db-148">Kaynağın, müşterinin doğrudan imzalama (doğrudan kabul) durumunu belirten bir **isSigned** özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="2e7db-148">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="2e7db-149">true **değeri,** sözleşmenin doğrudan müşteri tarafından imzalandı (kabul edildi) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e7db-149">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="2e7db-150">false **değeri,** sözleşmenin doğrudan müşteri *tarafından* imzalanmaz (kabul edilir) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e7db-150">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e7db-151">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2e7db-151">Response success and error codes</span></span>

<span data-ttu-id="2e7db-152">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="2e7db-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="2e7db-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e7db-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e7db-154">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2e7db-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e7db-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2e7db-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
