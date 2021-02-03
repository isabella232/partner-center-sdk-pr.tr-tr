---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünü onaylama
description: Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri Sözleşmesi 'nin müşteri kabulünü onaylama hakkında bilgi edinin.
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 239ca43c70fb8aa7f0d06e564e6c0726b235ffbe
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770073"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="14892-103">Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama</span><span class="sxs-lookup"><span data-stu-id="14892-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="14892-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="14892-104">**Applies to:**</span></span>

- <span data-ttu-id="14892-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="14892-105">Partner Center</span></span>

<span data-ttu-id="14892-106">İş ortağı merkezi şu anda Microsoft Müşteri sözleşmesinin yalnızca *Microsoft genel bulutundaki* müşteri kabulünün onayını desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="14892-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="14892-107">Bu işlevsellik şu anda için geçerli değildir:</span><span class="sxs-lookup"><span data-stu-id="14892-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="14892-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="14892-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="14892-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="14892-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="14892-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="14892-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="14892-111">Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama veya yeniden onaylama işlemlerinin nasıl yapılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="14892-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14892-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="14892-112">Prerequisites</span></span>

- <span data-ttu-id="14892-113">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="14892-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="14892-114">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="14892-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="14892-115">*Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.*</span><span class="sxs-lookup"><span data-stu-id="14892-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="14892-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14892-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="14892-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14892-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="14892-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="14892-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="14892-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="14892-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="14892-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="14892-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="14892-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="14892-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="14892-122">Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde Tarih (**kabul edildi**).</span><span class="sxs-lookup"><span data-stu-id="14892-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="14892-123">Müşteri kuruluşundan, Microsoft Müşteri anlaşmasını kabul eden kullanıcı hakkında bilgiler.</span><span class="sxs-lookup"><span data-stu-id="14892-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-124">Şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="14892-124">This includes:</span></span>
  - <span data-ttu-id="14892-125">Ad</span><span class="sxs-lookup"><span data-stu-id="14892-125">First name</span></span>
  - <span data-ttu-id="14892-126">Soyadı</span><span class="sxs-lookup"><span data-stu-id="14892-126">Last name</span></span>
  - <span data-ttu-id="14892-127">E-posta adresi</span><span class="sxs-lookup"><span data-stu-id="14892-127">Email address</span></span>
  - <span data-ttu-id="14892-128">Telefon numarası (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="14892-128">Phone number (optional)</span></span>

## <a name="net"></a><span data-ttu-id="14892-129">.NET</span><span class="sxs-lookup"><span data-stu-id="14892-129">.NET</span></span>

<span data-ttu-id="14892-130">Microsoft Müşteri sözleşmesinin müşteri tarafından kabul edildiğini onaylamak veya yeniden doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="14892-130">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="14892-131">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın.</span><span class="sxs-lookup"><span data-stu-id="14892-131">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-132">Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="14892-132">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-133">Daha ayrıntılı bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="14892-133">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="14892-134">Onayın ayrıntılarını içeren yeni bir **anlaşma** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14892-134">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="14892-135">**Iagreggatepartner. Customers** koleksiyonunu kullanın ve belirtilen **Müşteri Kiracı kimliği** ile **byıd** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="14892-135">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="14892-136">, Ardından **Create** veya **createasync** çağrısı yaparak **anlaşmalar** özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="14892-136">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="14892-137">[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [createcustomeragreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) sınıfında bir bütün örnek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="14892-137">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="14892-138">REST isteği</span><span class="sxs-lookup"><span data-stu-id="14892-138">REST request</span></span>

<span data-ttu-id="14892-139">Microsoft Müşteri sözleşmesinin müşteri tarafından kabul edildiğini onaylamak veya yeniden doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="14892-139">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="14892-140">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın.</span><span class="sxs-lookup"><span data-stu-id="14892-140">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-141">Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="14892-141">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-142">Daha ayrıntılı bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="14892-142">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="14892-143">Müşterinin Microsoft Müşteri anlaşmasını kabul ettiğini onaylamak için yeni bir [ **anlaşma** kaynağı](agreement-resources.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14892-143">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-144">Aşağıdaki [rest istek sözdizimini](#request-syntax)kullanın.</span><span class="sxs-lookup"><span data-stu-id="14892-144">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14892-145">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="14892-145">Request syntax</span></span>

| <span data-ttu-id="14892-146">Yöntem</span><span class="sxs-lookup"><span data-stu-id="14892-146">Method</span></span> | <span data-ttu-id="14892-147">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="14892-147">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14892-148">POST</span><span class="sxs-lookup"><span data-stu-id="14892-148">POST</span></span>   | <span data-ttu-id="14892-149">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="14892-149">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="14892-150">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="14892-150">URI parameter</span></span>

<span data-ttu-id="14892-151">Onayladığınız müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="14892-151">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="14892-152">Ad</span><span class="sxs-lookup"><span data-stu-id="14892-152">Name</span></span>               | <span data-ttu-id="14892-153">Tür</span><span class="sxs-lookup"><span data-stu-id="14892-153">Type</span></span> | <span data-ttu-id="14892-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="14892-154">Required</span></span> | <span data-ttu-id="14892-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="14892-155">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="14892-156">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="14892-156">customer-tenant-id</span></span> | <span data-ttu-id="14892-157">GUID</span><span class="sxs-lookup"><span data-stu-id="14892-157">GUID</span></span> | <span data-ttu-id="14892-158">Yes</span><span class="sxs-lookup"><span data-stu-id="14892-158">Yes</span></span> | <span data-ttu-id="14892-159">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="14892-159">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="14892-160">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="14892-160">Request headers</span></span>

<span data-ttu-id="14892-161">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="14892-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14892-162">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="14892-162">Request body</span></span>

<span data-ttu-id="14892-163">Bu tabloda, REST istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="14892-163">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="14892-164">Ad</span><span class="sxs-lookup"><span data-stu-id="14892-164">Name</span></span>      | <span data-ttu-id="14892-165">Tür</span><span class="sxs-lookup"><span data-stu-id="14892-165">Type</span></span>   | <span data-ttu-id="14892-166">Description</span><span class="sxs-lookup"><span data-stu-id="14892-166">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="14892-167">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="14892-167">Agreement</span></span> | <span data-ttu-id="14892-168">object</span><span class="sxs-lookup"><span data-stu-id="14892-168">object</span></span> | <span data-ttu-id="14892-169">Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak için iş ortağı tarafından sunulan ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="14892-169">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="14892-170">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="14892-170">Agreement</span></span>

<span data-ttu-id="14892-171">Bu tablo, bir [ **anlaşma** kaynağı](agreement-resources.md)oluşturmak için gereken en düşük alanları açıklar.</span><span class="sxs-lookup"><span data-stu-id="14892-171">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="14892-172">Özellik</span><span class="sxs-lookup"><span data-stu-id="14892-172">Property</span></span>       | <span data-ttu-id="14892-173">Tür</span><span class="sxs-lookup"><span data-stu-id="14892-173">Type</span></span>   | <span data-ttu-id="14892-174">Description</span><span class="sxs-lookup"><span data-stu-id="14892-174">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="14892-175">primaryContact</span><span class="sxs-lookup"><span data-stu-id="14892-175">primaryContact</span></span> | [<span data-ttu-id="14892-176">İletişim</span><span class="sxs-lookup"><span data-stu-id="14892-176">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="14892-177">Microsoft Müşteri sözleşmesini kabul eden müşteri kuruluşundan Kullanıcı hakkında bilgiler:  **FirstName**, **LastName**, **email** ve **PhoneNumber** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="14892-177">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="14892-178">Kabul edilen tarih</span><span class="sxs-lookup"><span data-stu-id="14892-178">dateAgreed</span></span>     | <span data-ttu-id="14892-179">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="14892-179">string in UTC date time format</span></span> |<span data-ttu-id="14892-180">Müşterinin sözleşmeyi kabul ettiği tarih.</span><span class="sxs-lookup"><span data-stu-id="14892-180">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="14892-181">TemplateId</span><span class="sxs-lookup"><span data-stu-id="14892-181">templateId</span></span>     | <span data-ttu-id="14892-182">string</span><span class="sxs-lookup"><span data-stu-id="14892-182">string</span></span> | <span data-ttu-id="14892-183">Müşteri tarafından kabul edilen sözleşme türünün benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="14892-183">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="14892-184">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alarak Microsoft Müşteri Sözleşmesi için **TemplateId** 'yi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14892-184">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="14892-185">Ayrıntılar için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="14892-185">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="14892-186">tür</span><span class="sxs-lookup"><span data-stu-id="14892-186">type</span></span>           | <span data-ttu-id="14892-187">string</span><span class="sxs-lookup"><span data-stu-id="14892-187">string</span></span> | <span data-ttu-id="14892-188">Müşteri tarafından kabul edilen anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="14892-188">Agreement type accepted by the customer.</span></span> <span data-ttu-id="14892-189">Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde "MicrosoftCustomerAgreement" kullanın.</span><span class="sxs-lookup"><span data-stu-id="14892-189">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="14892-190">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="14892-190">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="14892-191">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="14892-191">REST response</span></span>

<span data-ttu-id="14892-192">Başarılı olursa, bu yöntem bir [ **anlaşma** kaynağı](./agreement-resources.md)döndürür.</span><span class="sxs-lookup"><span data-stu-id="14892-192">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14892-193">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="14892-193">Response success and error codes</span></span>

<span data-ttu-id="14892-194">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="14892-194">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="14892-195">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="14892-195">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14892-196">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="14892-196">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="14892-197">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="14892-197">Response example</span></span>

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
