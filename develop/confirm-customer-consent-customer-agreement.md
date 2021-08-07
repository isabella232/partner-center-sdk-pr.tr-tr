---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünü onaylama
description: İş Ortağı Merkezi API'lerini kullanarak Microsoft Müşteri Sözleşmesi kabul İş Ortağı Merkezi öğrenin.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 374a9670f5d4c05209e5cec07afe766bcf57f255f9266138b7aaf0e85f90f0ed
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991931"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Api'leri kullanarak Microsoft Müşteri Sözleşmesi kabul İş Ortağı Merkezi onaylayın

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş Ortağı Merkezi şu anda yalnızca Microsoft genel bulutlarında Microsoft Müşteri Sözleşmesi onay onay desteklemektedir.

Bu makalede, müşterinin müşteri kabulünü onaylama veya yeniden onaylama işleminin nasıl Microsoft Müşteri Sözleşmesi.

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.14 veya daha yenisi gereklidir.

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md) *Bu senaryo yalnızca App+User kimlik doğrulamasını destekler.*

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Müşterinin müşteri tarafından kabul edilen tarih (**dateAgreed**) Microsoft Müşteri Sözleşmesi.

- Müşteri kuruluşundan, kullanıcıyla ilgili bilgileri kabul eden Microsoft Müşteri Sözleşmesi. Şunları içerir:
  - Ad
  - Soyadı
  - E-posta adresi
  - Telefon numarası (isteğe bağlı)
- Bir müşteri için aşağıdaki değerler değişirse, İş Ortağı Merkezi müşteri için başka bir sözleşmenin oluşturulmuş olmasına izin verir: Ad Soyadı E-posta adresi Telefon numarası Aksi takdirde iş ortakları, yinelenen bir müşteri oluşturulduktan dolayı aşağıdaki hata kodunu alır


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

## <a name="net"></a>.NET

Müşterinin kabulünü onaylamak veya yeniden onaylamak için Microsoft Müşteri Sözleşmesi:

1. Veri kaynağı için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi. Uygulamanın **templateId'lerini** Microsoft Müşteri Sözleşmesi. Daha fazla bilgi için [bkz. Microsoft Müşteri Sözleşmesi.](get-customer-agreement-metadata.md)

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Onayın **ayrıntılarını içeren** yeni bir Sözleşme nesnesi oluşturun.

3. **IAgreggatePartner.Customers** koleksiyonunu kullanın ve belirtilen **customer-tenant-id** ile **ById** yöntemini çağırın.

4. Agreements **özelliğini,** ardından **Create** veya **CreateAsync çağrısıyla kullanın.**

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

Eksiksiz bir örnek, konsol test uygulaması [projesinin CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.

## <a name="rest-request"></a>REST isteği

Müşterinin kabulünü onaylamak veya yeniden onaylamak için Microsoft Müşteri Sözleşmesi:

1. Veri kaynağı için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi. Uygulamanın **templateId'lerini** Microsoft Müşteri Sözleşmesi. Daha fazla bilgi için [bkz. Microsoft Müşteri Sözleşmesi.](get-customer-agreement-metadata.md)

2. Müşterinin bu [ **hesabı kabul**](agreement-resources.md) etmiş olduğunu onaylamak için yeni bir Sözleşme Microsoft Müşteri Sözleşmesi. Aşağıdaki REST isteği [söz dizimlerini kullanın.](#request-syntax)

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Onaylamakta olduğunu müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad               | Tür | Gerekli | Açıklama                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Yes | Değer, müşteri belirtmenize olanak sağlayan bir tanımlayıcı olan GUID biçimli **müşteri-kiracı** kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tabloda REST isteği gövdesinde gerekli özellikler açıkmektedir.

| Ad      | Tür   | Description                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Sözleşme | object | İş ortağı tarafından sağlanan ayrıntılar, müşterinin kabulünü onaylamak Microsoft Müşteri Sözleşmesi. |

#### <a name="agreement"></a>Sözleşme

Bu tabloda, bir Sözleşme kaynağı oluşturmak için gereken en düşük [ **alanlar açıklandı.**](agreement-resources.md)

| Özellik       | Tür   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [İletişim](./utility-resources.md#contact) | Adı, soyadı , e-posta ve **phoneNumber** (isteğe bağlı) dahil olmak Microsoft Müşteri Sözleşmesi müşteri kuruluşundan kullanıcı hakkında bilgiler   |
| dateAgreed     | UTC tarih saat biçiminde dize |Müşterinin sözleşmeyi kabul etme tarihi. |
| templateId     | string | Müşteri tarafından kabul edilen sözleşme türünün benzersiz tanımlayıcısı. Uygulama için **templateId'Microsoft Müşteri Sözleşmesi** için anlaşma meta verilerini Microsoft Müşteri Sözleşmesi. Ayrıntılar [için bkz. Microsoft Müşteri Sözleşmesi](./get-customer-agreement-metadata.md) meta verilerini al. |
| tür           | string | Müşteri tarafından kabul edilen sözleşme türü. Müşteri kabul ettiyse "MicrosoftCustomerAgreement" Microsoft Müşteri Sözleşmesi. |

#### <a name="request-example"></a>İstek örneği

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

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem bir Sözleşme [ **kaynağı** döndürür.](./agreement-resources.md)

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

#### <a name="response-example"></a>Yanıt örneği

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
