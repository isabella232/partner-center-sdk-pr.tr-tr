---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünü onaylama
description: Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri Sözleşmesi 'nin müşteri kabulünü onaylama hakkında bilgi edinin.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006070"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="fc9f2-103">Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama</span><span class="sxs-lookup"><span data-stu-id="fc9f2-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="fc9f2-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="fc9f2-104">**Applies to:**</span></span>

- <span data-ttu-id="fc9f2-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-105">Partner Center</span></span>

<span data-ttu-id="fc9f2-106">İş ortağı merkezi şu anda Microsoft Müşteri sözleşmesinin yalnızca *Microsoft genel bulutundaki* müşteri kabulünün onayını desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="fc9f2-107">Bu işlevsellik şu anda için geçerli değildir:</span><span class="sxs-lookup"><span data-stu-id="fc9f2-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="fc9f2-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fc9f2-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fc9f2-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fc9f2-111">Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama veya yeniden onaylama işlemlerinin nasıl yapılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc9f2-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fc9f2-112">Prerequisites</span></span>

- <span data-ttu-id="fc9f2-113">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="fc9f2-114">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="fc9f2-115">*Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.*</span><span class="sxs-lookup"><span data-stu-id="fc9f2-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="fc9f2-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc9f2-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fc9f2-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fc9f2-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fc9f2-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fc9f2-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fc9f2-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="fc9f2-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fc9f2-122">Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde Tarih (**kabul edildi**).</span><span class="sxs-lookup"><span data-stu-id="fc9f2-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="fc9f2-123">Müşteri kuruluşundan, Microsoft Müşteri anlaşmasını kabul eden kullanıcı hakkında bilgiler.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-124">Şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="fc9f2-124">This includes:</span></span>
  - <span data-ttu-id="fc9f2-125">Ad</span><span class="sxs-lookup"><span data-stu-id="fc9f2-125">First name</span></span>
  - <span data-ttu-id="fc9f2-126">Soyadı</span><span class="sxs-lookup"><span data-stu-id="fc9f2-126">Last name</span></span>
  - <span data-ttu-id="fc9f2-127">E-posta adresi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-127">Email address</span></span>
  - <span data-ttu-id="fc9f2-128">Telefon numarası (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fc9f2-128">Phone number (optional)</span></span>
- <span data-ttu-id="fc9f2-129">Bir müşteri için aşağıdaki değerler değişiyorsa, Iş ortağı merkezi bu müşteri için başka bir sözleşmenin oluşturulmasını sağlayacaktır: ad soyadı e-posta adresi telefon numarası Aksi takdirde iş ortakları, oluşturulan yinelenen bir müşteri nedeniyle aşağıdaki hata kodunu alır</span><span class="sxs-lookup"><span data-stu-id="fc9f2-129">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a><span data-ttu-id="fc9f2-130">.NET</span><span class="sxs-lookup"><span data-stu-id="fc9f2-130">.NET</span></span>

<span data-ttu-id="fc9f2-131">Microsoft Müşteri sözleşmesinin müşteri tarafından kabul edildiğini onaylamak veya yeniden doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="fc9f2-131">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="fc9f2-132">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-132">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-133">Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-133">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-134">Daha ayrıntılı bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="fc9f2-134">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="fc9f2-135">Onayın ayrıntılarını içeren yeni bir **anlaşma** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-135">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="fc9f2-136">**Iagreggatepartner. Customers** koleksiyonunu kullanın ve belirtilen **Müşteri Kiracı kimliği** ile **byıd** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-136">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="fc9f2-137">, Ardından **Create** veya **createasync** çağrısı yaparak **anlaşmalar** özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-137">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

<span data-ttu-id="fc9f2-138">[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [createcustomeragreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) sınıfında bir bütün örnek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-138">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc9f2-139">REST isteği</span><span class="sxs-lookup"><span data-stu-id="fc9f2-139">REST request</span></span>

<span data-ttu-id="fc9f2-140">Microsoft Müşteri sözleşmesinin müşteri tarafından kabul edildiğini onaylamak veya yeniden doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="fc9f2-140">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="fc9f2-141">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-141">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-142">Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-142">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-143">Daha ayrıntılı bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="fc9f2-143">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="fc9f2-144">Müşterinin Microsoft Müşteri anlaşmasını kabul ettiğini onaylamak için yeni bir [ **anlaşma** kaynağı](agreement-resources.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-144">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-145">Aşağıdaki [rest istek sözdizimini](#request-syntax)kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-145">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc9f2-146">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-146">Request syntax</span></span>

| <span data-ttu-id="fc9f2-147">Yöntem</span><span class="sxs-lookup"><span data-stu-id="fc9f2-147">Method</span></span> | <span data-ttu-id="fc9f2-148">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="fc9f2-148">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc9f2-149">POST</span><span class="sxs-lookup"><span data-stu-id="fc9f2-149">POST</span></span>   | <span data-ttu-id="fc9f2-150">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="fc9f2-150">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="fc9f2-151">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-151">URI parameter</span></span>

<span data-ttu-id="fc9f2-152">Onayladığınız müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-152">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="fc9f2-153">Ad</span><span class="sxs-lookup"><span data-stu-id="fc9f2-153">Name</span></span>               | <span data-ttu-id="fc9f2-154">Tür</span><span class="sxs-lookup"><span data-stu-id="fc9f2-154">Type</span></span> | <span data-ttu-id="fc9f2-155">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fc9f2-155">Required</span></span> | <span data-ttu-id="fc9f2-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fc9f2-156">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc9f2-157">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="fc9f2-157">customer-tenant-id</span></span> | <span data-ttu-id="fc9f2-158">GUID</span><span class="sxs-lookup"><span data-stu-id="fc9f2-158">GUID</span></span> | <span data-ttu-id="fc9f2-159">Yes</span><span class="sxs-lookup"><span data-stu-id="fc9f2-159">Yes</span></span> | <span data-ttu-id="fc9f2-160">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-160">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fc9f2-161">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="fc9f2-161">Request headers</span></span>

<span data-ttu-id="fc9f2-162">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc9f2-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc9f2-163">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="fc9f2-163">Request body</span></span>

<span data-ttu-id="fc9f2-164">Bu tabloda, REST istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-164">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="fc9f2-165">Ad</span><span class="sxs-lookup"><span data-stu-id="fc9f2-165">Name</span></span>      | <span data-ttu-id="fc9f2-166">Tür</span><span class="sxs-lookup"><span data-stu-id="fc9f2-166">Type</span></span>   | <span data-ttu-id="fc9f2-167">Description</span><span class="sxs-lookup"><span data-stu-id="fc9f2-167">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc9f2-168">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="fc9f2-168">Agreement</span></span> | <span data-ttu-id="fc9f2-169">object</span><span class="sxs-lookup"><span data-stu-id="fc9f2-169">object</span></span> | <span data-ttu-id="fc9f2-170">Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak için iş ortağı tarafından sunulan ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-170">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="fc9f2-171">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="fc9f2-171">Agreement</span></span>

<span data-ttu-id="fc9f2-172">Bu tablo, bir [ **anlaşma** kaynağı](agreement-resources.md)oluşturmak için gereken en düşük alanları açıklar.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-172">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="fc9f2-173">Özellik</span><span class="sxs-lookup"><span data-stu-id="fc9f2-173">Property</span></span>       | <span data-ttu-id="fc9f2-174">Tür</span><span class="sxs-lookup"><span data-stu-id="fc9f2-174">Type</span></span>   | <span data-ttu-id="fc9f2-175">Description</span><span class="sxs-lookup"><span data-stu-id="fc9f2-175">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="fc9f2-176">primaryContact</span><span class="sxs-lookup"><span data-stu-id="fc9f2-176">primaryContact</span></span> | [<span data-ttu-id="fc9f2-177">İletişim</span><span class="sxs-lookup"><span data-stu-id="fc9f2-177">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="fc9f2-178">Microsoft Müşteri sözleşmesini kabul eden müşteri kuruluşundan Kullanıcı hakkında bilgiler:  **FirstName**, **LastName**, **email** ve **PhoneNumber** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fc9f2-178">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="fc9f2-179">Kabul edilen tarih</span><span class="sxs-lookup"><span data-stu-id="fc9f2-179">dateAgreed</span></span>     | <span data-ttu-id="fc9f2-180">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="fc9f2-180">string in UTC date time format</span></span> |<span data-ttu-id="fc9f2-181">Müşterinin sözleşmeyi kabul ettiği tarih.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-181">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="fc9f2-182">TemplateId</span><span class="sxs-lookup"><span data-stu-id="fc9f2-182">templateId</span></span>     | <span data-ttu-id="fc9f2-183">string</span><span class="sxs-lookup"><span data-stu-id="fc9f2-183">string</span></span> | <span data-ttu-id="fc9f2-184">Müşteri tarafından kabul edilen sözleşme türünün benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-184">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="fc9f2-185">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alarak Microsoft Müşteri Sözleşmesi için **TemplateId** 'yi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-185">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="fc9f2-186">Ayrıntılar için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="fc9f2-186">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="fc9f2-187">tür</span><span class="sxs-lookup"><span data-stu-id="fc9f2-187">type</span></span>           | <span data-ttu-id="fc9f2-188">string</span><span class="sxs-lookup"><span data-stu-id="fc9f2-188">string</span></span> | <span data-ttu-id="fc9f2-189">Müşteri tarafından kabul edilen anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-189">Agreement type accepted by the customer.</span></span> <span data-ttu-id="fc9f2-190">Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde "MicrosoftCustomerAgreement" kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-190">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="fc9f2-191">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="fc9f2-191">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a><span data-ttu-id="fc9f2-192">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="fc9f2-192">REST response</span></span>

<span data-ttu-id="fc9f2-193">Başarılı olursa, bu yöntem bir [ **anlaşma** kaynağı](./agreement-resources.md)döndürür.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-193">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc9f2-194">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="fc9f2-194">Response success and error codes</span></span>

<span data-ttu-id="fc9f2-195">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-195">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="fc9f2-196">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc9f2-196">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc9f2-197">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc9f2-197">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="fc9f2-198">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="fc9f2-198">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
