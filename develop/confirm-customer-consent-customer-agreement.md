---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünü onaylama
description: Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri Sözleşmesi 'nin müşteri kabulünü onaylama hakkında bilgi edinin.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974021"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="434bd-103">Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama</span><span class="sxs-lookup"><span data-stu-id="434bd-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="434bd-104">**Uygulama hedefi**: Iş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="434bd-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="434bd-105">**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="434bd-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="434bd-106">İş ortağı merkezi şu anda Microsoft Müşteri sözleşmesinin yalnızca Microsoft genel bulutundaki müşteri kabulünün onayını desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="434bd-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the Microsoft public cloud.</span></span>

<span data-ttu-id="434bd-107">Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama veya yeniden onaylama işlemlerinin nasıl yapılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="434bd-107">This article describes how to confirm or reconfirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="434bd-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="434bd-108">Prerequisites</span></span>

- <span data-ttu-id="434bd-109">Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="434bd-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="434bd-110">[Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="434bd-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="434bd-111">*Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.*</span><span class="sxs-lookup"><span data-stu-id="434bd-111">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="434bd-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="434bd-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="434bd-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="434bd-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="434bd-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="434bd-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="434bd-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="434bd-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="434bd-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="434bd-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="434bd-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="434bd-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="434bd-118">Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde Tarih (**kabul edildi**).</span><span class="sxs-lookup"><span data-stu-id="434bd-118">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="434bd-119">Müşteri kuruluşundan, Microsoft Müşteri anlaşmasını kabul eden kullanıcı hakkında bilgiler.</span><span class="sxs-lookup"><span data-stu-id="434bd-119">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-120">Şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="434bd-120">This includes:</span></span>
  - <span data-ttu-id="434bd-121">Ad</span><span class="sxs-lookup"><span data-stu-id="434bd-121">First name</span></span>
  - <span data-ttu-id="434bd-122">Soyadı</span><span class="sxs-lookup"><span data-stu-id="434bd-122">Last name</span></span>
  - <span data-ttu-id="434bd-123">E-posta adresi</span><span class="sxs-lookup"><span data-stu-id="434bd-123">Email address</span></span>
  - <span data-ttu-id="434bd-124">Telefon numarası (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="434bd-124">Phone number (optional)</span></span>
- <span data-ttu-id="434bd-125">bir müşteri için aşağıdaki değerler değişiyorsa, iş ortağı merkezi bu müşteri için başka bir sözleşmenin oluşturulmasını sağlayacaktır: ad adı soyadı e-posta adresi Telefon numarası aksi takdirde iş ortakları, oluşturulan yinelenen bir müşteri nedeniyle aşağıdaki hata kodunu alır</span><span class="sxs-lookup"><span data-stu-id="434bd-125">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


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

## <a name="net"></a><span data-ttu-id="434bd-126">.NET</span><span class="sxs-lookup"><span data-stu-id="434bd-126">.NET</span></span>

<span data-ttu-id="434bd-127">Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak veya yeniden doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="434bd-127">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="434bd-128">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın.</span><span class="sxs-lookup"><span data-stu-id="434bd-128">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-129">Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="434bd-129">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-130">Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="434bd-130">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="434bd-131">Onayın ayrıntılarını içeren yeni bir **anlaşma** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="434bd-131">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="434bd-132">**Iagreggatepartner. Customers** koleksiyonunu kullanın ve belirtilen **Müşteri Kiracı kimliği** ile **byıd** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="434bd-132">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="434bd-133">, Ardından **Create** veya **createasync** çağrısı yaparak **anlaşmalar** özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="434bd-133">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="434bd-134">[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [createcustomeragreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) sınıfında bir bütün örnek bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="434bd-134">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="434bd-135">REST isteği</span><span class="sxs-lookup"><span data-stu-id="434bd-135">REST request</span></span>

<span data-ttu-id="434bd-136">Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak veya yeniden doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="434bd-136">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="434bd-137">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın.</span><span class="sxs-lookup"><span data-stu-id="434bd-137">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-138">Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="434bd-138">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-139">Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="434bd-139">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="434bd-140">Müşterinin Microsoft Müşteri anlaşmasını kabul ettiğini onaylamak için yeni bir [ **anlaşma** kaynağı](agreement-resources.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="434bd-140">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-141">Aşağıdaki [rest istek sözdizimini](#request-syntax)kullanın.</span><span class="sxs-lookup"><span data-stu-id="434bd-141">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="434bd-142">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="434bd-142">Request syntax</span></span>

| <span data-ttu-id="434bd-143">Yöntem</span><span class="sxs-lookup"><span data-stu-id="434bd-143">Method</span></span> | <span data-ttu-id="434bd-144">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="434bd-144">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="434bd-145">POST</span><span class="sxs-lookup"><span data-stu-id="434bd-145">POST</span></span>   | <span data-ttu-id="434bd-146">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="434bd-146">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="434bd-147">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="434bd-147">URI parameter</span></span>

<span data-ttu-id="434bd-148">Onayladığınız müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="434bd-148">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="434bd-149">Ad</span><span class="sxs-lookup"><span data-stu-id="434bd-149">Name</span></span>               | <span data-ttu-id="434bd-150">Tür</span><span class="sxs-lookup"><span data-stu-id="434bd-150">Type</span></span> | <span data-ttu-id="434bd-151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="434bd-151">Required</span></span> | <span data-ttu-id="434bd-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="434bd-152">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="434bd-153">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="434bd-153">customer-tenant-id</span></span> | <span data-ttu-id="434bd-154">GUID</span><span class="sxs-lookup"><span data-stu-id="434bd-154">GUID</span></span> | <span data-ttu-id="434bd-155">Yes</span><span class="sxs-lookup"><span data-stu-id="434bd-155">Yes</span></span> | <span data-ttu-id="434bd-156">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="434bd-156">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="434bd-157">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="434bd-157">Request headers</span></span>

<span data-ttu-id="434bd-158">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="434bd-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="434bd-159">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="434bd-159">Request body</span></span>

<span data-ttu-id="434bd-160">Bu tabloda, REST istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="434bd-160">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="434bd-161">Ad</span><span class="sxs-lookup"><span data-stu-id="434bd-161">Name</span></span>      | <span data-ttu-id="434bd-162">Tür</span><span class="sxs-lookup"><span data-stu-id="434bd-162">Type</span></span>   | <span data-ttu-id="434bd-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="434bd-163">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="434bd-164">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="434bd-164">Agreement</span></span> | <span data-ttu-id="434bd-165">object</span><span class="sxs-lookup"><span data-stu-id="434bd-165">object</span></span> | <span data-ttu-id="434bd-166">Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak için iş ortağı tarafından sunulan ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="434bd-166">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="434bd-167">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="434bd-167">Agreement</span></span>

<span data-ttu-id="434bd-168">Bu tablo, bir [ **anlaşma** kaynağı](agreement-resources.md)oluşturmak için gereken en düşük alanları açıklar.</span><span class="sxs-lookup"><span data-stu-id="434bd-168">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="434bd-169">Özellik</span><span class="sxs-lookup"><span data-stu-id="434bd-169">Property</span></span>       | <span data-ttu-id="434bd-170">Tür</span><span class="sxs-lookup"><span data-stu-id="434bd-170">Type</span></span>   | <span data-ttu-id="434bd-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="434bd-171">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="434bd-172">primaryContact</span><span class="sxs-lookup"><span data-stu-id="434bd-172">primaryContact</span></span> | [<span data-ttu-id="434bd-173">İletişim</span><span class="sxs-lookup"><span data-stu-id="434bd-173">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="434bd-174">Microsoft Müşteri sözleşmesini kabul eden müşteri kuruluşundan Kullanıcı hakkındaki bilgiler:  **FirstName**, **LastName**, **email** ve **PhoneNumber** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="434bd-174">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="434bd-175">Kabul edilen tarih</span><span class="sxs-lookup"><span data-stu-id="434bd-175">dateAgreed</span></span>     | <span data-ttu-id="434bd-176">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="434bd-176">string in UTC date time format</span></span> |<span data-ttu-id="434bd-177">Müşterinin sözleşmeyi kabul ettiği tarih.</span><span class="sxs-lookup"><span data-stu-id="434bd-177">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="434bd-178">TemplateId</span><span class="sxs-lookup"><span data-stu-id="434bd-178">templateId</span></span>     | <span data-ttu-id="434bd-179">string</span><span class="sxs-lookup"><span data-stu-id="434bd-179">string</span></span> | <span data-ttu-id="434bd-180">Müşteri tarafından kabul edilen sözleşme türünün benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="434bd-180">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="434bd-181">Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alarak Microsoft Müşteri Sözleşmesi için **TemplateId** 'yi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="434bd-181">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="434bd-182">Ayrıntılar için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="434bd-182">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="434bd-183">tür</span><span class="sxs-lookup"><span data-stu-id="434bd-183">type</span></span>           | <span data-ttu-id="434bd-184">string</span><span class="sxs-lookup"><span data-stu-id="434bd-184">string</span></span> | <span data-ttu-id="434bd-185">Müşteri tarafından kabul edilen anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="434bd-185">Agreement type accepted by the customer.</span></span> <span data-ttu-id="434bd-186">Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde "MicrosoftCustomerAgreement" kullanın.</span><span class="sxs-lookup"><span data-stu-id="434bd-186">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="434bd-187">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="434bd-187">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="434bd-188">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="434bd-188">REST response</span></span>

<span data-ttu-id="434bd-189">Başarılı olursa, bu yöntem bir [ **anlaşma** kaynağı](./agreement-resources.md)döndürür.</span><span class="sxs-lookup"><span data-stu-id="434bd-189">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="434bd-190">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="434bd-190">Response success and error codes</span></span>

<span data-ttu-id="434bd-191">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="434bd-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="434bd-192">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="434bd-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="434bd-193">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="434bd-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="434bd-194">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="434bd-194">Response example</span></span>

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
