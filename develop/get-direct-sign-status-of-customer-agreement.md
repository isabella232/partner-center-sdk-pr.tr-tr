---
title: Microsoft Müşteri Sözleşmesi için müşterinin doğrudan imzalama durumunu alın.
description: DirectSignedCustomerAgreementStatus kaynağını, müşterinin Microsoft Müşteri sözleşmesinin doğrudan imzalama (doğrudan kabul) durumunu almak için kullanabilirsiniz.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030581"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="5e704-103">Müşterinin doğrudan imzalanmasından (doğrudan kabulünün) Microsoft müşteri anlaşması 'nın durumunu alın</span><span class="sxs-lookup"><span data-stu-id="5e704-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="5e704-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="5e704-104">**Applies to:**</span></span>

- <span data-ttu-id="5e704-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5e704-105">Partner Center</span></span>

<span data-ttu-id="5e704-106">**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="5e704-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="5e704-107">Bu kaynak için *geçerli değildir* :</span><span class="sxs-lookup"><span data-stu-id="5e704-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="5e704-108">21Vianet tarafından çalıştırılan İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5e704-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5e704-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5e704-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5e704-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5e704-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5e704-111">Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin doğrudan kabulünün durumunu nasıl alabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5e704-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e704-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5e704-112">Prerequisites</span></span>

- <span data-ttu-id="5e704-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5e704-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5e704-114">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5e704-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5e704-115">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e704-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5e704-116">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e704-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5e704-117">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5e704-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5e704-118">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5e704-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5e704-119">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5e704-119">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5e704-120">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="5e704-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5e704-121">C\#</span><span class="sxs-lookup"><span data-stu-id="5e704-121">C\#</span></span>

<span data-ttu-id="5e704-122">Müşterinin Microsoft Müşteri sözleşmesinin doğrudan kabulünün durumunu almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5e704-122">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="5e704-123">Ardından [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) arabirimini almak için [**anlaşmalar**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e704-123">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="5e704-124">Son olarak, `GetDirectSignedCustomerAgreementStatus()` `GetDirectSignedCustomerAgreementStatusAsync()` durumu almak için veya çağırın.</span><span class="sxs-lookup"><span data-stu-id="5e704-124">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="5e704-125">**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="5e704-125">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="5e704-126">**Proje**: Sdksamples **sınıfı**: GetDirectSignedCustomerAgreementStatus. cs</span><span class="sxs-lookup"><span data-stu-id="5e704-126">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5e704-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5e704-127">REST request</span></span>

<span data-ttu-id="5e704-128">Müşterinin Microsoft Müşteri sözleşmesinin doğrudan kabulünün durumunu almak için, müşteri için [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) almak üzere bir rest isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e704-128">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5e704-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5e704-129">Request syntax</span></span>

<span data-ttu-id="5e704-130">Aşağıdaki istek sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="5e704-130">Use the following request syntax:</span></span>

| <span data-ttu-id="5e704-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5e704-131">Method</span></span> | <span data-ttu-id="5e704-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5e704-132">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5e704-133">GET</span><span class="sxs-lookup"><span data-stu-id="5e704-133">GET</span></span>    | <span data-ttu-id="5e704-134">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="5e704-134">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="5e704-135">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="5e704-135">URI parameters</span></span>

<span data-ttu-id="5e704-136">İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5e704-136">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="5e704-137">Ad</span><span class="sxs-lookup"><span data-stu-id="5e704-137">Name</span></span>             | <span data-ttu-id="5e704-138">Tür</span><span class="sxs-lookup"><span data-stu-id="5e704-138">Type</span></span> | <span data-ttu-id="5e704-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5e704-139">Required</span></span> | <span data-ttu-id="5e704-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e704-140">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="5e704-141">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="5e704-141">customer-tenant-id</span></span> | <span data-ttu-id="5e704-142">GUID</span><span class="sxs-lookup"><span data-stu-id="5e704-142">GUID</span></span> | <span data-ttu-id="5e704-143">Yes</span><span class="sxs-lookup"><span data-stu-id="5e704-143">Yes</span></span> | <span data-ttu-id="5e704-144">Değer, bir müşterinin kiracı KIMLIĞINI belirtmenize olanak tanıyan bir GUID biçimli **Customertenantıd** 'dir.</span><span class="sxs-lookup"><span data-stu-id="5e704-144">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5e704-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5e704-145">Request headers</span></span>

<span data-ttu-id="5e704-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5e704-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5e704-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5e704-147">Request body</span></span>

<span data-ttu-id="5e704-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="5e704-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5e704-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5e704-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="5e704-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5e704-150">REST response</span></span>

<span data-ttu-id="5e704-151">Başarılı olursa, bu yöntem yanıt gövdesinde bir [ **DirectSignedCustomerAgreementStatus** kaynağı](./customer-agreement-direct-sign-status-resource.md) döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e704-151">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="5e704-152">Kaynağın, müşterinin doğrudan imzalama (doğrudan kabul) durumunu gösteren bir **IsSigned** özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="5e704-152">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="5e704-153">**Doğru** değeri, sözleşmenin doğrudan müşteri tarafından imzalanmış (kabul edildi) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5e704-153">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="5e704-154">**False** değeri, sözleşmenin doğrudan müşteri tarafından *imzalanmadığını (* kabul edilmediğini) gösterir.</span><span class="sxs-lookup"><span data-stu-id="5e704-154">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5e704-155">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5e704-155">Response success and error codes</span></span>

<span data-ttu-id="5e704-156">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5e704-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="5e704-157">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e704-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5e704-158">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5e704-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5e704-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5e704-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
